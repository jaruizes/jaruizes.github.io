---
layout: post
title:  "REST API: Error handling"
date:   2018-04-21 15:01:35 +0300
category : API
description: "One of the most important thing when you're designing an API is **how it's going to handle errors** and how will be the content and the status of the responses that it's going to send to its clients"
tags:   [API, Rest]
---
One of the most important thing when you're designing an API is **how it's going to handle errors** and how will be the content and the status of the responses that it's going to send to its clients 

Basically, there are two design strategies to face it but there isn't a standard way. This two different strategies are:

* **Handling errors as API part directly:** this strategy consists on defining and documenting every error and its HTTP status code associated. The definition of the error is a part of the endpoint as the same way as input/output params are.
* **Handling errors not included in the API definition:** there isn't a definition of the different errors associated to the endpoint, so the most of endpoints return the same status code independently of the result of the execution. For instance, this the strategy that Facebook uses.

If you have designed (and implemented) SOAP services you are familiarized with the decision of throwing a SOAP fault or not. More or less this is the same problem. The key is in the design phase. 

_In my opinion, the default strategy has to be including errors as part of the API but in some cases or in some projects we have to keep in mind the ecosystem around the API. So, there isn't a clear answer to the question._

### 4xx vs 5xx
If we are chosen the first one, **the next question will be what is the difference between a status code 4xx and a status code 5xx.** It seems obvious but it's something that appears in a lot of projects when the team is designing or implementing the API.

Basically, when something goes wrong because the client sent some wrong data, the status code should be 4xx. The error is recoverable from the client side. But when something goes wrong because there is a failure in the server side, the status code should be 5xx. In this case, the error is not recoverable from the client side.  

For instance, if the client sends some data that needs validation and the result of the validation is KO, the status code must be 4xx, but if there is an error with the database or the typical NullPointer, the staus code must be 5xx

It's the same that checked and unchecked exceptions or business exceptions and runtime exceptions.

Once this is clear, the next step usually is getting specific 4xx status codes for each case. There are several standard status codes:

* 400: Bad Request
* 401: Unauthorized – Invalid credentials
* 403: Forbidden (associated to resources)
* 404: The resource does not exist
* 405: Method Not Allowed
* 408: Request Time-out

Often, there are situations in which it's difficult to matching a status code with the predefined codes 4xx. In that case we can use a custom status code, for instance the status 418 (I'm a teapot). The important thing is being coherent through the different endpoints and set the same strategy for all of them. 

It's very important that our API is easy to consume. The client has to control these status codes in the same way. If the client has to implement a different strategy for error handling in each endpoint, the client will not use our API.

### Additional info
We can (or should) add some information to the response when we return a status 4xx or 5xx. In my opinion, besides the status code, an error code it essential. With this code, the client can associate a i18n message or doing different actions depending of this one. 

We can also add other fields like "message" or "developerMessage" to help to solve the error. An example of this could be the following:

```json
{
    "status": 404,
    "code": 40483,
    "message": "Oops! It's something wrong",
    "developerMessage": "bla bla bla",
    "moreInfo": "http://www.mycompany.com/errors/40483"
}
```

From the security point of view, we have to be cautious because we can reveal some security issues with these additional fields. We have to keep in mind that we don't include implementation details in these extra fields. 

This is all. I hope this post has been useful for you!

### References:

* Apigee: http://apigee.com/about/blog/technology/restful-api-design-what-about-errors
* IBM: https://www.ibm.com/support/knowledgecenter/SS964W/com.ibm.wbpm.bpc.doc/topics/rdev_restapis_statuscodes.html
* Google: https://developers.google.com/drive/v3/web/handle-errors
* Microsoft: https://msdn.microsoft.com/en-us/library/azure/dd179357.aspx
* Twitter: https://dev.twitter.com/overview/api/response-codes
* Restful Cookbok: http://restcookbook.com/HTTP%20Methods/400-vs-500/
* Github: https://developer.github.com/v3/
