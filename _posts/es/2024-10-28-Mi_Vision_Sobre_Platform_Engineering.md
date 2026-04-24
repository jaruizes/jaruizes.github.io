---
layout: post
title: "Plataformas, DevEx y otras muchas cosas que entender (antes del boom de la IA)"
date: 2024-10-28 01:30
image: "/images/pe/intro/pe_intro.jpg"
description: "En este post doy un resumen de la charla de Platform Engineering en la CommitConf 2024."
tags: [Culture, Platform Engineering, DevEx]
lang: es
ref: platform-engineering
typora-root-url: ../..
---

Durante 2024, antes del boom que estamos viviendo de la IA, tuve el placer de dar una charla en la **CommitConf** titulada **"Plataformas, DevEx y otras muchas cosas que entender"**. Si te perdiste la sesión o quieres repasar los puntos clave sobre por qué el *Platform Engineering* está en boca de todos (y cómo evitar que sea un fracaso estrepitoso), aquí te traigo un resumen "ejecutivo".

📺 **Vídeo de la charla:** [Ver en YouTube](https://www.youtube.com/watch?v=SAeFqfqy0JM)  
📊 **Slides:** [Descargar PDF](https://jaruiz.io/downloads/commit2024/Plataformas_DevEx_y_otras_muchas_cosas_que_entender.pdf)



## Platform Engineering no es algo nuevo

Como digo en la charla, si llevas ya un tiempo en la industria, cuando empiezas a leer artículos y a profundizar en esto, te habrás dado cuenta de que  este tipo de iniciativas ya las has vivido aunque, seguramente, no siempre las hayas conocido con este nombre. 

Por ejemplo, si miramos una fuente importante, como es el radar de ThoughtWorks, podemos ver que en 2017 ya se incluía este concepto en su [radar](https://www.thoughtworks.com/content/dam/thoughtworks/documents/radar/2017/03/tr_technology_radar_vol_16_en.pdf). Pero, si echamos la vista un poco más atrás, podemos ver que ya se hacía referencia a este concepto en 2015:
![platform_eng_referenes](/images/platform/platform_eng_referenes.jpg)

¿Por qué ahora se habla de Platform Engineering por todos lados?



## El problema: la explosión de la carga cognitiva 

Cuando empecé profesionalmente en esto de desarrollar software, una persona podía crear funcionalidades completas sin manejar a la vez muchas herramientas. No hace falta irse a Cobol...Por ejemplo, si has vivido tiempos de Fatwire o te ha tocado trabajar con Struts o con Spring MVC, por ejemplo,  una persona tocaba tanto la vista como el acceso a datos, incluyendo las consultas SQL (tan temidas hoy día). Si había un fallo, ibas al log y lo veías claramente. Si tenías que depurar, lanzabas el debug y hacías la depuración completa.

Actualmente, con la evolucion de las arquitecturas y la separacion de capas, por ejemplo, SPA, API Rest, etc...y la tendencia (por decirlo así) "Cloud Native", un desarrollador manejar un ecosistema de muchísimas más piezas. Básicamente, se le pide que sepa de Kubernetes, 
Terraform, seguridad, observabilidad, escalabilidad, microservicios, mensajería basada en eventos, FinOps,...,etc. Al final, en su día a día tiene que
manejar un número elevado de conceptos, herramientas y tecnologías, elevando mucho la complejidad de desarrollo. 

No es lo mismo tener que resolver un problema con un número muy limitado de piezas que con un número elevado de piezas

![platform_eng_referenes](/images/platform/complex_ecosystem.jpg)

Que haya tantas "piezas" no es objeto de este post pero viene de la mano de la evolucion tanto del negocio como de la tecnologia (¿fue antes el huevo o la gallina?). Las necesidades de los clientes han crecido exponencialmente: muchos más canales disponibles (móviles, web, machine-to-machine y APIs everywhere, IoT y wearables,...,etc), mucho más necesidad o tiempo de "estar conectados/ser informados" y mucho más volumen de información  manejada. Para solventar estas necesidades, el ecosistema de desarrollo de SW tiene que evolucionar en consecuencia.



Por lo tanto, como he comentado, a mayor número de piezas a manejar dentro del ecosistema, mayor es la complejidad que se experimenta y por tanto, mayor es la carga cognitiva (esfuerzo mental) que se tiene que gestionar o soportar para llevar a cabo una tarea (**aquí es donde la IA nos va a ayudar bastante**).

![platform_eng_referenes](/images/platform/cognitive_load.jpg)



Por otro lado, la famosa filosofía ***"You build it, you run it"*** que fue "acuñada" en 2016 por *Werner Vogels*, es potente, pero sin el soporte adecuado o en "malas manos", se convierte en un punto de conflicto y un medio de señalar únicamente a un punto concreto, el equipo de desarrollo. **¿El resultado?** Equipos quemados, fricciones constantes y un *time-to-market* que no mejora.



![platform_eng_referenes](/images/platform/sociedad_codigo.jpg)



En este punto, es donde nace el concepto de **Platform Engineering**. Para entender este concepto, lo primero es entender qué es una plataforma en el contexto de Platform Engineering



## ¿Qué es (realmente) una Plataforma en Platform Engineering? 

En la charla insisto en que tenemos que entender el concepto de "plataforma" dentro de Platform Engineering. Cuando se habla de plataforma, se puede entender "plataforma de contenedores", "plataforma de infraestructura", "plataforma de API", "plataforma de datos",...,etc. 

**Esto no es lo que entendemos como plataforma en el contexto de Platform Enginering.**



Para mí, una de las mejores definiciones de plataforma en este contexto es la que dio "Evan Bottcher" (ThoughtWorks) en su artículo sobre [Plataformas](https://martinfowler.com/articles/talk-about-platforms.html):



> A digital platform is a foundation of self-service APIs, tools, services, knowledge and support which are arranged as a compelling internal product. 
>
> Autonomous delivery teams can make use of the platform to deliver product features at a higher pace, with reduced coordination. 
>
> (Evan Bottcher)
>
>  https://martinfowler.com/articles/talk-about-platforms.html



Por lo tanto, una plataforma, en el contexto de Platform Engineering, es un conjunto de:

- **APIs de autoservicio (portales, CLIs,...).**
- **Conocimiento y soporte** (la parte social que siempre olvidamos).
- **Golden Paths:** Caminos pavimentados que permiten a los equipos ser autónomos sin tener que reinventar la rueda en cada despliegue.



![platform_eng_referenes](/images/platform/platform_components.jpg)



La plataforma la gestiona el **equipo de plataforma** que tiene como objetivo aplicar prácticas de ingeniería para diseñar, construir y proporcionar a la plataforma las capacidades más adecuadas en cada momento y contexto.

Hay que tener en cuenta que **los clientes de esta plataforma y de este equipo de plataforma son los desarrolladores**, aunque el equipo de plataforma **tiene que tener muy claro el contexto en el que opera** en el que hay una serie de stakeholders (los CxO, por ejemplo) que establerán restricciones, condicionantes o realizarán alguna peticion. Esto no deja de ser el contexto en el que se trabaja.

El equipo de plataforma se va a encontrar por un lado a los clientes directos, los desarrolladores, que tendrán una lista infinita de peticiones y, por otro lado, también habrá una lista de restricciones (coste, tiempo, equipo, etc) y condicionantes (infraestructura, licencias, etc) que vienen del resto de stakeholders.

Por lo tanto, **el objetivo del equipo de plataforma y, por tanto, de la plataforma es ofrecer servicios que permitan a los desarrolladores hacer su** 
**trabajo de forma más fácil dentro del contexto en el que se mueven esos equipos (la empresa)**. 

Trabajar de forma más fácil suele tener asociado ser más eficiente y óptimo. Es un win-win (empleado-empresa)



> **Clave:** No confudamos objetivos. El objetivo no es "ir más rápido", sino "hacerlo más fácil". La velocidad suele ser una consecuencia de la facilidad, no el objetivo en sí.



## ¿Cómo construir la plataforma? Thinnest Viable Platform (TVP)

A la hora de construir una plataforma, como pasa en la construcción de cualquier producto, hay dos caminos principalmente:

- creer que sabemos más que los clientes potenciales y ponernos "mano a la obra" a construir el producto que queremos nosotros

- optar por seleccionar los clientes potenciales, escuchar sus necesidades y, a partir de eso, construir la plataforma, iterando y evolucionando según el feedback y necesidades en cada momento.

  

El primer punto es **uno de los mayores errores que se suele comenter**. 

En muchas ocaciones, se entiende que están claras las necesidades, se monta un equipo de plataforma  y se dedica durante meses a construir "algo" que seguramente los desarrolladores no necesitan, no funciona como esperan, no llega cuando lo esperan y acabarán odiando. Podemos encontrar algunos casos como este si buscamos un poco:



![platform_error_implementation](/images/platform/platform_error_implementation.jpg)



En estos casos, **se suele repetir el patrón de que la plataforma se concibe como un fin y no como un medio para facilitar el desarrollo y producción de software**.

Para evitar esto, un enfoque que podemos adoptar es el del concepto de **TVP (Thinnest Viable Platform)**: **construir solo lo justo y necesario en cada momento**. 



Este termino proviene de Team Topologies y se definiía así:



> We're not aiming to build a massive platform. We're aiming to build what we in the book call a thinnest viable platform TVP. 
>
> This TVP could be just a wiki page if that's all you need for your platform - it says we use this cloud provider and we only use these services from a cloud provider and here's the way we use them. 
>
> That might just be a wiki page - that might be your platform.
>
> 
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

Al ser un producto orientado a mejorar o facilitar el desarrollo de software parece claro que, lo ideal sería que no se requiriese una curva de aprendizaje grande para empezar a notar la ganancia, es decir, el proceso de desarrollo de software mejora y, además, repercute en una mayor productividad (cuando algo es más fácil se consigue más productividad que cuando es muy complejo). Si esto pasa, entonces estamos haciendo un buen producto. 

En cambio, si la curva de aprendizaje es grande, puede que estamos añadendo más complejidad (y carga cognitiva) al proceso de desarrollo en vez de reducirla:





![platform_ok](/images/platform/platform_ok.jpg)



Para conseguir que sea un éxito hay unos puntos clave a considerar:

- la plataforma debe ser **sencilla**: se trata de eliminar complejidad, no de añadirla. Tiene mucho que ver tambien con el concepto de TVP: no buscamos cantidad sino calidad.
- la plataforma tiene que ser **usable**: muy relacionado con la sencillez pero tambien con el entendimiento y conocimiento de los clientes, de cómo trabajan y desarrollan (por esto, el PM tiene que tener ese componente técnico)
- la plataforma tiene que ser **transparente**: tenemos que evitar que sea una caja negra. Es un producto por y para desarrolladores, tiene que estar abierto e incluso podemos hacer que los equipos de desarrollo ayuden a evolucionar la plataforma mediante pull request y mecanismos similares.
- la plataforma debe ser **estándar**: muy relacionado tambien con la sencillez, la usabilidad y la transparencia. No buscamos reinventar la rueda, no buscamos crear nuevos frameworks mediante capas de abstracción sobre los existentes. No queremos eso. Queremos que sea lo más estándar posible porque eso nos va a permitir más facilidad para evolucionarla. Por ejemplo, si es "propietaria", vamos a depender del conocimiento de las personas que están en la plataforma y la curva de aprendizaje para nuevas personas va a ser grande. Además, si hemos construido muchas capas encima de un core estándar, si ese core cambia, podemos tenemos bastantes problemas para evolucionar.
-  la plataforma debe estar **documentada**: sí, esto está muy relacionado con el punto anterior y con la transparencia. Cuanto más documentada está (ojo, no cantidad sino calidad), más sencillo y más corta será la curva de aprendizaje, tanto la del usuario como la de las personas que mantienen la plataforma.



Hay un último punto que es clave: la **ACEPTACIÓN**: la plataforma tiene que ser aceptada, no impuesta. 

Esto quiere decir que el usuario tiene que querer usarla sin que nadie le obligue, que no quiere decir otra cosa que el producto le gusta y le ayuda en su día a día. Cuando algo es impuesto y los usuarios van a tener que usarlo sí o sí, pasan varias cosas:

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



## El Stack Tecnológico

Aunque el Platform Engineering no va de herramientas, en la charla analizamos un flujo moderno que puedes empezar a probar hoy mismo:

1.  **Backstage:** El portal que unifica el catálogo y ofrece *Software Templates*.
2.  **Crossplane:** Para gestionar infraestructura Cloud de forma declarativa (Kubernetes como plano de control).
3.  **ArgoCD:** El motor de GitOps que mantiene todo sincronizado.

No voy a entrar en detalle en este post porque creo que en las slides está bien explicado.



## Conclusiones

1.  **La plataforma es el medio, no el fin.** Si la plataforma se vuelve más compleja que el problema que intenta resolver, has fallado.
2.  **La plataforma debe ser tan grande o tan pequeña como tenga que ser en cada momento** (TVP)
3.  **La adopción debe ser opcional.** Si tu plataforma es buena, los equipos querrán usarla. Si les obligas, buscarán formas de saltársela (*Shadow Ops*).
4.  **Enfoque de abajo a arriba.** Escucha a los devs antes que a los PowerPoints de management.



Espero que os haya gustado el post. Volveré con un enfoque en la era IA!

