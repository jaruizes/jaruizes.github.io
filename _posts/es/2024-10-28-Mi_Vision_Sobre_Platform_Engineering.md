---
layout: post
title: "Plataformas, DevEx y otras muchas cosas que entender"
date: 2024-10-28 01:30
image: "/images/pe/intro/pe_intro.jpg"
description: "En este post doy un resumen de la charla de Platform Engineering en la CommitConf 2024."
tags: [Culture, Platform Engineering, DevEx]
lang: es
ref: platform-engineering
typora-root-url: ../..
---

Durante 2024 el placer de dar una charla en la **CommitConf** titulada **"Plataformas, DevEx y otras muchas cosas que entender"**. Si te perdiste la sesión o quieres repasar los puntos clave sobre por qué el *Platform Engineering* está en boca de todos (y cómo evitar que sea un fracaso estrepitoso), aquí te traigo un resumen ejecutivo.

📺 **Vídeo de la charla:** [Ver en YouTube](https://www.youtube.com/watch?v=SAeFqfqy0JM)  
📊 **Slides:** [Descargar PDF](https://jaruiz.io/downloads/commit2024/Plataformas_DevEx_y_otras_muchas_cosas_que_entender.pdf)



## Las plataformas no son algo nuevo

Como digo en la charla, los que llevamos ya un tiempo en la industria hemos vivido ya este tipo de iniciativas aunque no siempre las hemos
conocido con este nombre. Si miramos una fuente importante, como es el radar de ThoughtWorks, podemos ver que en 2017 ya se incluía este
concepto en su [radar](https://www.thoughtworks.com/content/dam/thoughtworks/documents/radar/2017/03/tr_technology_radar_vol_16_en.pdf).

Si echamos la vista un poco más atrás, podemos ver que ya se hacía referencia a este concepto:
![platform_eng_referenes](/images/platform/platform_eng_referenes.jpg)



## El problema: la explosión de la carga cognitiva 🧠💥

Hoy en día, un desarrollador se tiene que manejar dentro de un ecosistema "cloud native". Básicamente, se le pide que sepa de Kubernetes, 
Terraform, seguridad, observabilidad, escalabilidad, microservicios, mensajería basada en eventos, FinOps,...,etc. Al final, en su día a día tiene que
manejar un número elevado de conceptos, herramientas y tecnologías. 

No es lo mismo tener que resolver un problema con un número muy limitado de piezas que con un número elevado de piezas. A medida que aumenta el número de piezas, aumenta la complejidad para resolverlo:

![platform_eng_referenes](/images/platform/complex_ecosystem.jpg)

Por lo tanto, si lo trasladamos al ecosistema de desarrollo, a mayor número de piezas a manejar dentro de ese ecosistema, mayor es la complejidad de desarrollo y por tanto, mayor es la carga cognitiva que se tiene que gestionar.

![platform_eng_referenes](/images/platform/cognitive_load.jpg)



Por otro lado, la filosofía *"You build it, you run it"* es potente, pero sin el soporte adecuado, se convierte en un punto de conflicto y un medio de 
señalar únicamente a un punto concreto, el equipo de desarrollo, dejándolo en muchas ocasiones, totalmente solo, buscándose la vida. **¿El resultado?** Equipos quemados, fricciones constantes y un *time-to-market* que no mejora a pesar de estar en la nube.



![platform_eng_referenes](/images/platform/sociedad_codigo.jpg)



En este punto, es donde nace el concepto de **Platform Engineering**.



## ¿Qué es (realmente) una Plataforma? 🛠️

En la charla insisto en que no tenemos que confundir el concepto ya que "plataforma" suele referirse a "plataforma de contenedore", "plataforma de infraestructura", "plataforma de API", "plataforma de datos",...,etc. **Esto no es lo que entendemos como plataforma en el contexto de Platform Enginering.**

La definición que me gusta es la que dio "Evan Bottcher" (ThoughtWorks) en su artículo sobre [Plataformas](https://martinfowler.com/articles/talk-about-platforms.html):

![platform_eng_referenes](/images/platform/platform_definition.jpg)



Una plataforma, en el contexto de Platform Engineering, es un conjunto de:

- **APIs de autoservicio (portales, CLIs,...).**
- **Conocimiento y soporte** (la parte social que siempre olvidamos).
- **Golden Paths:** Caminos pavimentados que permiten a los equipos ser autónomos sin tener que reinventar la rueda en cada despliegue.

![platform_eng_referenes](/images/platform/platform_components.jpg)

La plataforma la gestiona el **equipo de plataforma** que tiene como objetivo aplicar prácticas de ingeniería para diseñar,
construir y proporcionar a la plataforma las capacidades más adecuadas en cada momento y contexto.

Hay que tener en cuenta que los clientes de esta plataforma y de este equipo de plataforma son los desarrolladores, aunque el equipo de plataforma 
tiene que tener muy claro el contexto en el que opera y los objetivos que persigue. Por un lado, los desarrolladores tendrán una lista infinita de
peticiones pero por otro lado, también habrá una lista de restricciones (coste, tiempo, equipo, etc) y condicionantes (infraestructura, licencias, etc).

Por lo tanto, el objetivo del equipo de plataforma y, por tanto, de la plataforma es ofrecer servicios que permitan a los desarrolladores hacer su 
trabajo de forma más fácil. Trabajar de forma más fácil suele tener asociado ser más eficiente y óptimo. Es un win-win (empleado-empresa)

> **Clave:** El objetivo no es "ir más rápido", sino "hacerlo más fácil". La velocidad es una consecuencia de la facilidad.



## ¿Cómo construir una plataforma? Thinnest Viable Platform (TVP) 📏

A la hora de construir una plataforma, como pasa en la construcción de cualquier producto, podemos optar por seleccionar los clientes potenciales,
escuchar sus necesidades y, a partir de eso, construir la plataforma, iterando y evolucionando según el feedback y necesidades en cada momento.

**Uno de los mayores errores que suele comenter es no escuchar al cliente** (los desarrolladores) porque se entiende que están claras las necesidades 
y encerrar a un equipo de plataforma durante meses para construir algo que luego los desarrolladores no necesita, no funciona como esperan 
y, acabarán odiando. Por ejemplo, podemos encontrar algunos casos como este:

![platform_error_implementation](/images/platform/platform_error_implementation.jpg)

En estos casos, **solemos encontrar que la plataforma se concibe como un fin, no como un medio para facilitar el desarrollo y producción de software a los equipos destinados a ello**.

Un enfoque que podemos adoptar es el del concepto de **TVP (Thinnest Viable Platform)**: construir solo lo justo y necesario en cada momento. Este termino proviene de Team Topologies y se definiía así:



> We're not aiming to build a massive platform. We're aiming to build what we in the book call a thinnest viable platform TVP. This TVP could be just a wiki page if that's all you need for your platform - it says we use this cloud provider and we only use these services from a cloud provider and here's the way we use them. That might just be a wiki page - that might be your platform.
>
> (Matthew Skelton, Team Topologies)



**Realmente, el principio es básico: entiende las necesidades reales de tus clientes en cada momento.**

Parece algo de sentido común pero, sorprendentemente, no se suele tener en cuenta en la práctica. Si tus equipos solo necesitan una Wiki bien estructurada hoy, no les obligues a usar un portal complejo. Itera, pide feedback y evoluciona la plataforma como un producto real. 



## Plataforma como producto

El enfoque TVP no deja de ser un enfoque lógico de desarrollo de producto, aunque se trate de un producto interno.  Cuando desarrollamos un producto, tenemos que realizar estos pasos de forma continua:

- Descubrir y entender las necesidades reales de los clos clientes
- Incorporar/evolucionar capacidades del producto orientadas a resolver esas necesidades
- Poner en manos del cliente, usar
- Pedir feedback, sacar conclusiones, tomar decisiones y volver al primer punto



En todo este proceso hay un rol clave: **Product Manager**. En mi opinion, este rol debe tener estar características o capacidades:

- Componente técnico, capaz de entender las necesidades de los equipos de desarrollo (los clientes)
- Componente social, capaz de entender las necesidades del resto de stakeholders pero también capaz de evangelizar en la colaboracion y en el uso de la plataforma
- Componente de estrategia, capaz de poner en conjunto todas las necesidades, generar y mantener un roadmap y estrategia de producto



## Características de una plataforma exitosa

Ya sabemos qué es una plataforma y cómo podemos crearla pero, llegados a este punto y como pasa con cualquier producto, tenemos que saber si la plataforma está siendo un éxito o no. 

Al ser una producto orientado a mejorar o facilitar el desarrollo de software parece claro que si, una vez que hemos puesto el producto a disposicion del usuario, el usuario no sufre una curva de aprendizaje grande y, desde los primeros momentos se nota que el software se desarrolla mejor y se logra una mayor productividad (cuando algo es más fácil se consigue más productividad que cuando es muy complejo), entonces estamos haciendo un buen producto. 

En cambio, si la curva de aprendizaje es grande, puede que estamos añadendo más complejidad (y carga cognitiva) al proceso de desarrollo en vez de reducirla:



![platform_ok](/images/platform/platform_ok.jpg)



Para conseguir que sea un éxito hay unos puntos clave a considerar:

- la plataforma debe ser **sencilla**: se trata de eliminar complejidad, no de añadirla. Tiene mucho que ver tambien con el concepto de TVP: no buscamos cantidad sino calidad.
- la plataforma tiene que ser **usable**: muy relacionado con la sencillez pero tambien con el entendimiento y conocimiento de los clientes, de cómo trabajan y desarrollan (por esto, el PM tiene que tener ese componente técnico)
- la plataforma tiene que ser **transparente**: tenemos que evitar que sea una caja negra. Es un producto por y para desarrolladores, tiene que estar abierto e incluso podemos hacer que los equipos de desarrollo ayuden a evolucionar la plataforma mediante pull request y mecanismos similares.
- la plataforma debe ser **estándar**: muy relacionado tambien con la sencillez, la usabilidad y la transparencia. No buscamos reinventar la rueda, no buscamos crear nuevos frameworks mediante capas de abstracción sobre los existentes. No queremos eso. Queremos que sea lo más estándar posible porque eso nos va a permitir más facilidad para evolucionarla. Por ejemplo, si es "propietaria", vamos a depender del conocimiento de las personas que están en la plataforma y la curva de aprendizaje para nuevas personas va a ser grande. Además, si hemos construido muchas capas encima de un core estándar, si ese core cambia, podemos tenemos bastantes problemas para evolucionar.
-  la plataforma debe estar **documentada**: sí, esto está muy relacionado con el punto anterior y con la transparencia. Cuanto más documentada está (ojo, no cantidad sino calidad), más sencillo y más corta será la curva de aprendizaje, tanto la del usuario como la de las personas que mantienen la plataforma.



Hay un último punto que es clave: la **ACEPTACIÓN**. La plataforma tiene que ser aceptada, no impuesta. Esto quiere decir que el usuario tiene que querer usarla sin que nadie le obligue, que no quiere decir otra cosa que el producto le gusta y le ayuda en su día a día. 

Cuando algo es impuesto y los usuarios van a tener que usarlo sí o sí, pasan varias cosas:

- los puntos anteriores (sencilla, usable, transparente, estándar, documentada) dejan de tener prácticamente sentido porque aunque no se cumplan, el usuario está obligado a usarlo. Por lo tanto, el ingeniero de plataforma no se siente obligado (vaya contradicción) a crear un buen producto.
- los usuarios se resignarán a usarla pero, por detrás, seguramente empiecen a crear sus propias herramientas o formas de simplificar su trabajo, por lo que la plataforma, se quedará únicamente como "un mal necesario" que no aporta ningun valor.

Sam Newman lo explica muy bien:

> Making the platform optional is very challenging for some people. It cost so much, we need to justify the cost. So people have to use it! Otherwise we wasted time and money. 
>
> And as Matthew and Manuel point out, when something becomes mandatory, interesting thing happens. 
>
> When you make people use the platform, you stop caring about making it easy to use, because they don’t have a choice. You aren't incentivised to improve the user experience to attract people to the platform, as they have to be there anyway. 
>
> (Sam Newman)



## El Stack Tecnológico 🏗️

Aunque el Platform Engineering no va de herramientas, en la charla analizamos un flujo moderno que puedes empezar a probar hoy mismo:

1.  **Backstage:** El portal que unifica el catálogo y ofrece *Software Templates*.
2.  **Crossplane:** Para gestionar infraestructura Cloud de forma declarativa (Kubernetes como plano de control).
3.  **ArgoCD:** El motor de GitOps que mantiene todo sincronizado.

No voy a entrar en detalle en este post porque creo que en las slides está bien explicado.



## Conclusiones para llevarse a casa 🏠

1.  **La plataforma es el medio, no el fin.** Si la plataforma se vuelve más compleja que el problema que intenta resolver, has fallado.
2.  **La adopción debe ser opcional.** Si tu plataforma es buena, los equipos querrán usarla. Si les obligas, buscarán formas de saltársela (*Shadow Ops*).
3.  **Enfoque de abajo a arriba.** Escucha a los devs antes que a los PowerPoints de management.

