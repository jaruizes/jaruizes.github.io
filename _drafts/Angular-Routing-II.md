---
author: jaruizes
layout: post
title: "Angular - Router Hooks: Guards"
date: 2017-02-07 10:00
category : Angular
comments: false
tags:
 - Angular 2
 - Javascript
 - Routing
---

In this post we're going to see how we can protect some views or components. This is so easy in Angular 2. The use case is very simple: building a login and if the credentials (user and password) are right, navigating to a protected view. 

The code is uploaded in [github](https://github.com/jaruizes/angular2-routing/tree/router-hooks).

The first we need is a login service. We're going to build a easy one (login.service.ts):

```typescript
import {Injectable} from "@angular/core";

@Injectable()
export class LoginService {

  login(user:string, password: string):boolean {
    if ((user && user == 'admin') && (password && password == '1234')) {
      sessionStorage.setItem('userlogged', 'ok');
      return true;
    }
    return false;
  }

  closeSession():void {
    sessionStorage.removeItem('userlogged');
  }

  isUserLogged():boolean {
    let userlogged:string = sessionStorage.getItem('userlogged');
    return userlogged != null && userlogged == 'ok';
  }

}
```
We've declared just three methods:

- login(user, password): this method is used to perform a login in the system. If the user and password are OK, it sets a auth key in the session storage.
- closeSession(): removes the auth key stored in the session storage.
- isUserLogged(): get the auth key and checks if its value is 'true'


The second we need is building a login form. We are going to build a light one adding it to the _feature1.component.html::
```html
...

<div style="font-weight: bold; border: solid 1px black; width: 40%">
  <div style="padding: 0.4rem">
    <label>User:</label>
    <input type="text" #user>
  </div>
  <div style="padding: 0.4rem">
    <label>Password:</label>
    <input type="password" #password>
  </div>
  <br>
  <div style="padding: 0.4rem">
    <input type="button" value="Try!" (click)="goToSecretFeature(user.value, password.value)" />
  </div>
</div>
...

```

And we use the login service to check the credentials in _feature1.component.ts_:

```typescript
...
constructor(private _router: Router, private loginService:LoginService){}
...
goToSecretFeature(user, password) {
    if (this.loginService.login(user,password)) {
      this._router.navigate(['/feature4']);
    } else {
      window.alert('Try again!');
    }
}
...
```

#### Guards

Angular define some router hooks to do some action during the navigation. In this case we're going to show how to deny the access to some components in base on certain logic. We define a new path associated to a new component (_feature4.component.ts_) and we want to protect this path to a not allowed users. We modify _app.routing.ts_ to do this:

```typescript
const routes: Routes = [
  { path: '', component: HomeComponent, data: {appName: 'Angular Routing', appVersion: '1.0.0'}},
  { path: 'feature1', component: Feature1Component},
  { path: 'feature2', component: Feature2Component},
  { path: 'feature2/:param1', component: Feature2Component},
  { path: 'feature3', component: Feature3Component,
    children: [
      { path: 'feature31', component: Feature31Component},
      { path: 'feature32', component: Feature32Component},
      { path: 'feature33/:origin', component: Feature33Component}
    ]
  },
  { path: 'feature4', component: Feature4Component, canActivate: [HasPrivateAccessGuard], canDeactivate: [ConfirmExitPrivateZoneGuard]},
  { path: '**', component: PageNotFoundComponent}
];
```

If you check the path 'feature4' you'll see that we've added two properties: canActivate and canDeactivate.

Both of them are known as "_Guards_". In Angular, Guards are, in a high level, interfaces that define methods that every application has to implement as it wants but these methods have to return either Observable<boolean>, Promise<boolean> or boolean.

When a navigation action is going to be performed, Route checks if there is a Guard associated to the target path and it is so, it executes the method that implements the guard.

Let's talk about canActivate and canDeactivate.

#### CanActivate 

CanActivate is jan interface. Its [definition](https://angular.io/docs/ts/latest/api/router/index/CanActivate-interface.html){:target="_blank"} says:

> Indicates that a class can implement to be a guard deciding if a route can be activated.

This guard is "executed" before enter to a target path in order to check if is possible to activate the route or not. 

So, as interface, you have to create a class that implements this interface. This interface declares the _canActivate_ method and you have to implement the logic that you need in your application in order grant the access to the component. In our example this logic is so easy. Basically, call to the login service to check whether the user is logged or not (_has-private-access.guard.ts_):

```typescript
import {Injectable} from "@angular/core";
import {CanActivate} from "@angular/router";
import {LoginService} from "../services/login.service";

@Injectable()
export class HasPrivateAccessGuard implements CanActivate {

  constructor(private loginService:LoginService) {}

  canActivate() {
    return this.loginService.isUserLogged();
  }
}

```

We've created a class _HasPrivateAccessGuard_ that implements _CanActivate_ interface so, by this way, it has to implement a canActivate method. The implementation in our case is so simple: if the _loginService.isUserLogged()_ returns false, the navigation action to '/feature4' is not done. 

If we try to access directly to /feature4, nothing happens. If we add a _console.log()_ sentence in _HasPrivateAccessGuard_ we can asses that the guard is executed. The logic inside the guard could be so complex as you want:

```typescript
@Injectable()
export class HasPrivateAccessGuard implements CanActivate {
    ...
    canActivate() {
     console.log('This is the HasPrivateAccessGuard...');
     return this.loginService.isUserLogged();
    }
}
```

![Acces denied](/images/guards-canactivate/access_denied.png)

Now we are trying to get to "/feature4" using the login form. We have to enter the user (in our case is 'admin') and password (in our case is '1234') and click on the button:

![Login form](/images/guards-canactivate/login_form.png)

The Router calls to the guard (_HasPrivateAccessGuard_), the login service says that everything is ok and finally the navigation action is done, showing the view associated to "_/feature4_":

![Feature 4](/images/guards-canactivate/feature4.png)

#### CanDeactivate 

This is other interface and its definition says:

> Indicates that a class can implement to be a guard deciding if a route can be deactivated.

So, this guard is "executed" over the current path when a navigation action to a other path is required. 

Using this interface is a little bit trickier than _CanActivate_ because is declaring a generic type in its definition:

```typescript
export interface CanDeactivate<T> {
  canDeactivate(component: T, route: ActivatedRouteSnapshot, state: RouterStateSnapshot):
      Observable<boolean>|Promise<boolean>|boolean;
}
```

So you need to implement the method _canDeactivate_ but you need to define a type/interface to associate as type of CanDeactivate:

```typescript
import {Injectable} from "@angular/core";
import {CanDeactivate} from "@angular/router";
import {Observable} from "rxjs";
import {LoginService} from "../services/login.service";

export interface CanComponentDeactivate {
  canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean;
}

@Injectable()
export class ConfirmExitPrivateZoneGuard implements CanDeactivate<CanComponentDeactivate> {

  constructor(private loginService:LoginService) {}

  canDeactivate(component: CanComponentDeactivate) {
    if (component.canDeactivate && component.canDeactivate()) {
      this.loginService.closeSession();
      return true;
    }

    return false;
  }

}
```

This means that the component associated to the path must implement _CanComponentDeactivate_ because the Router is going to call to the _canDeactivate_ method of the guard with a param of type _CanComponentDeactivate_. 

In other words, if we associated a CanDeactivate guard to a path, the component linked to this path has to implement a method (or methods) defined in the Type associated to the CanDeactivate guard and the component is responsible to implement the logic to determine if the navigation can be done or not. 

In our example, we add the following logic to _Feature4Component_:

```typescript
import {Component} from '@angular/core';
import {CanComponentDeactivate} from "../guards/confirm-exit-private-zone.guard";
@Component({
  selector: 'feature4',
  templateUrl: './feature4.component.html'
})
export class Feature4Component implements CanComponentDeactivate {

  canDeactivate() {
    return window.confirm('Do you really want to exit?');
  }
}
```

If the user is in "_/feature4" and decide to navigate to other path, the _ConfirmExitPrivateZoneGuard_ is executed and finally the method _canDeactivate_ of Feature4Component is called, showing the confirm dialog to the user:

![CanDeactivate](/images/guards-canactivate/candeactivate.png)