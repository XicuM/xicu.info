---
title: Mi proyecto final de grado
date: 2024-11-04T11:17:58+02:00
hideMeta: true
ShowBreadCrumbs: true
comments: true
showToc: true
tags: ["FPGA", "C++", "Simulink"]
github: https://github.com/XicuM/tfg
cover:
    image: /projects/tfg/control.jpg
---

## Motivación

A finales de 2021, comencé a buscar un tema interesante para mi proyecto final de grado. Quería trabajar en algo significativo pero accesible dadas las estrictas limitaciones de tiempo y conocimientos que tenía. Siempre he sido un estudiante ambicioso y en ese momento quería desafiarme a mí mismo.

Mi amigo [Shexing](https://www.linkedin.com/in/shexing/) se unió a un proyecto estudiantil que comenzó en septiembre de 2021. Fue seleccionado para formar parte de [BCN eMotorsport](https://bcnemotorsport.upc.edu), cuyo objectivo era construir un coche de carreras eléctrico y autónomo para competiciones de Formula Student, celebradas a nivel internacional en países como Austria, Alemania y España.

Shexing me ccntó sus experiencias con BCN eMotorsport y me convenció para conocer al equipo. Aunque nunca me ha interesado particularmente el motorsport, acepté visitar las oficinas. Allí hablé con [Jesús](https://www.linkedin.com/in/jes%C3%BAs-higueras-%C3%A1lvarez-a02267163/) y [Mikel](https://www.linkedin.com/in/mikel-aceldegui/), quienes me mostraron el espíritu start-up del equipo y me presentaron el desafío más ambicioso al cual se enfrentaban: diseñar un controlador de motor propio para el monoplaza.

En febrero de 2022, me uní al proyecto junto con [Albert](https://www.linkedin.com/in/albert-pla-verge-34755b1a9/), que también entraba como nuevo miembro del equipo. Dividimos el proyecto en dos partes principales:
- **Hardware**. Incluía tareas como la selección de los componentes y el diseño de la placa de potencia.
- **Control y Firmware**: Contituido por el diseño y la implementación del algoritmo de control en una FPGA, así como su comunicación con el resto del vehículo.

Como tenía experiencia en diseño digital y programación, asumí la parte de control, mientras que Albert se encargó del hardware. Pronto, el equipo nos apodó los "Inverter Bros" y avanzamos juntos de manera constante hacia nuestro objetivo.

## El proyecto

{{< figure src="/projects/tfg/cat14x.jpg" caption="El CAT14x, el monoplaza de BCN eMotorsport de 2022." >}}

El proyecto del controlador de motor propio tenía como objetivo reemplazar los inversores comerciales existentes, un par de Lenze Mobile DSU 60/60, con una solución más adaptada y eficiente, mejorando el rendimiento de nuestro coche de Formula Student, que contaba con tracción en las cuatro ruedas en la pista.

Los inversores Lenze son voluminosos, diseñados para vehículos mucho más grandes tales como buses, y su funcionamiento interno no permite adaptarlo a las necesidades del equipo. El nuevo inversor fue diseñado para aprovechar la tecnología de MOSFET de carburo de silicio (SiC), lo que permite una frecuencia de conmutación más alta en comparación con los IGBT utilizados en los inversores actuales. Además, se anticipó que la carcasa protectora del nuevo inversor reduciría significativamente el peso de este componente.

## Mi contribución

Mi papel en el proyecto consistió en implementar un algoritmo de control orientado al campo (FOC) en una placa de FPGA. El algoritmo fue adaptado para el motor síncrono de imanes permanentes (IPMSM) utilizado en el monoplaza de BCN eMotorsport.

Los principales objetivos del proyecto del TFG fueron:
- **Selección de Hardware**: Elegir una placa FPGA y un resolver o encoder.
- **Análisis del Algoritmo de Control**: Refinar el algoritmo inicial desarrollado por el equipo.
- **Implementación en FPGA**: Implementar el algoritmo de control en un módulo de sistema con FPGA.
- **Diseño de Software para Microcontrolador**: Desarrollar software en el microcontrolador para recibir comandos a través del bus CAN.
- **Validación del Algoritmo de Control**: Verificar el rendimiento del algoritmo de control implementado.

Si tienes curiosidad, puedes descargar la tesis completa [aquí](https://upcommons.upc.edu/bitstream/handle/2117/388310/Memoria_FMP.pdf?sequence=3&isAllowed=y) en catalán.

## El marco teórico

{{< figure src="/projects/tfg/inverter.svg" alt="Algoritmo de control" caption="Esquema de un inversor ideal." >}}

Los motores IPMSM se puede modelar como una inductancia y una resistencia en serie para cada fase. Hay dos tipos de conexiones en un motor trifásico: estrella y delta. En este caso, la conexión era una conexión en estrella: las tres ramas del motor se unen en un punto medio llamado punto neutro, simbolizado por una 'n'.

La topología de inversor elegida fue el inversor de dos niveles (TLI). Esta decisión se basó en factores como la experiencia del equipo, la configuración de la batería, el análisis de pérdidas y consideraciones de tamaño, peso y costo.

Para controlar el motor, se seleccionó un algoritmo de control orientado al campo (FOC). Este algoritmo se utiliza ampliamente en aplicaciones de vehículos eléctricos debido a su capacidad para proporcionar un alto par a bajas velocidades y una alta eficiencia a altas velocidades. Se utilizaron dos técnicas avanzadas para mejorar el rendimiento del algoritmo FOC:
- **Máximo Par por Amperio (MTPA)**, que proporciona al motor instrucciones óptimas en todo momento para maximizar el par mientras se minimiza el consumo de energía.
- **Debilitamiento de Campo (FW)**, una estrategia que ajusta inteligentemente el campo magnético para permitir que el motor gire más rápido.

{{< figure src="/projects/tfg/regions.png" caption="Las regiones operativas del controlador de motor, en el marco d-q." >}}

El FOC utiliza una serie de transformaciones inteligentes:

1. **Transformación de Clarke**. Esta transformación toma las corrientes trifásicas que vienen del motor (marco *a-b-c*) y las traduce a un sistema de coordenadas más simple (conocido como marco *α-β*). Es similar a coger un objeto 3D y aplanarlo en una superficie 2D, con lo que se simplifica la representación sin perder información esencial.

2. **Transformación de Park**: Esta otra transformación toma las corrientes simplificadas y alinea su marco de referencia con el campo magnético rotativo del motor (yendo del denominado marco *α-β* al marco rotativo *d-q*). Esta tranformación hace algo similar a girar el reloj al mismo tiempo que la manecilla de los segundos, lo que crea la ilusión de que la manecilla no se mueve. Una vez aplicada esta transformación, podemos desacoplar el control del flujo magnético y el par, facilitando el control del motor.

Finalmente, el FOC necesita de una técnica de modulación para convertir el voltaje de salida del conversor en un voltaje medido en las fases del inversor. Por esta razón, decidimos implementar la "Modulación por Ancho de Pulso de Vector Espacial" (SVPWM). Esta técnica es más eficiente que los métodos PWM tradicionales, como la modulación PWM sinusoidal, ya que permite transiciones más suaves entre niveles de voltaje, reduciendo la distorsión armónica y mejorando el rendimiento del motor.

{{< figure src="/projects/tfg/svpwm.png" caption="Ciclos de trabajo generados por SVPWM, con su característica forma de M." >}}

## Consideraciones de diseño e implementación

### ¿Por qué una FPGA?

Para la implementación, se decidió usar una FPGA en lugar de depender solo de un microprocesador. Las FPGAs son como Legos digitales, que nos permiten construir circuitos personalizados adaptados a nuestras necesidades exactas. Por eso se llama lógica programable, ya que crea circuitos lógicos con un programa.

En el contexto del control de motores, las FPGAs ofrecen varias ventajas clave:

- **Procesamiento en paralelo**: Las FPGAs pueden realizar múltiples operaciones simultáneamente. Esto es crucial para el control de motores, donde necesitamos procesar información y ajustar señales en tiempo real para mantener un rendimiento óptimo.

- **Tiempo determinista**: Las FPGAs aseguran que las señales se entreguen en el momento exacto. Esto es especialmente importante cuando se trabaja con MOSFETs de SiC, que pueden encenderse y apagarse increíblemente rápido, requiriendo un control preciso para maximizar la eficiencia y prevenir daños.

El SoC elegido fue el Zynq-7010 de Xilinx, que combina una FPGA con un potente microprocesador, dándonos lo mejor de ambos mundos. Este SoC se alojó inicialmente en una placa de desarrollo Diligent Cora Z7-10, que luego fue reemplazada por una placa MYIR Z-Turn para proporcionar más recursos lógicos, GPIOs y mejor documentación.

{{< figure src="/projects/tfg/test.png" caption="Pruebas con la Diligent Cora Z7-10" >}}

### Conjunto de Herramientas

El proyecto se desarrolló utilizando una combinación de herramientas:

- **Vitis Model Composer**, una extensión de Matlab/Simulink®, usado para implementar la lógica programable. Este entorno de bajo código proporciona un conjunto de bloques para describir e implementar la lógica programable, lo que ofreció un desarrollo y pruebas más rápidos en comparación con escribir código en un lenguaje de descripción de hardware como VHDL.
- **Vivado**, usado para la síntesis, implementación y depuración del diseño FPGA.
- **PetaLinux**, usado como sistema operativo para gestionar el microprocesador.
- **C++** como lenguaje utilizado para desarrollar la máquina de estados, la interfaz de usuario y la comunicación CAN con otros sistemas del vehículo.

### Optimización de la lógica programable

Una parte importante de la implementación de la lógica programable fue el proceso de toma de decisiones utilizado para optimizar el sistema de control del inversor, incluyendo la reducción del uso de recursos seleccionando los tipos de datos correctos (como es la aritmética de punto fijo), el uso de pipeline para un menor consumo de energía dinámica y ajustes de tiempo muerto en los "Gate Drivers" para prevenir problemas de cortocircuito en el inversor.

### Integración del software

En el lado del software, se implementó una máquina de estados para controlar el arranque y parada del motor, y se creó una interfaz de usuario para monitorear el estado del motor y establecer los puntos de consigna de velocidad y par. Se crearon clases personalizadas en C++ para representar registros y sensores, permitiendo crear una capa modular de abstracción de la comunicación entre la FPGA y el microprocesador.

{{< figure src="/projects/tfg/implementation.png" caption="Implementación final del algoritmo de control en Vitis Model Composer." >}}

## Conclusiones

El camino trazado cuando emprendes un proyecto de innovación suele ser bastante sinuoso, y este no fue una excepción. Por ejemplo, encontré bastantes problemas en la depuracón del algoritmo de control usando la plataforma Vivado Model Composer. Por suerte y gracias al trabajo duro, la simulación de la implementación del algoritmo FOC en la FPGA se completó con éxito.

Por otra parte, más que un aprendizaje técnico (que lo fue), este proyecto me enseñó lecciones valiosas sobre cómo trabajar en desarrollos grandes y complejos. Sabía que este era un proyecto ambicioso y tenía muchas ganas de trabajar en él. No obstante, no pude ejecutar todos los objetivos que me había propuesto, ya que en un inicio no era consciente de la complejidad y magnitud del proyecto. Con esto, aprendí que es importante estudiar el problema en profundidad antes de comenzar a trabajar en él, y a partir de allí, establecer metas realistas y aprender a ser flexible cuando las cosas no salen según lo planeado.

## Una mirada atrás

Reflexionando sobre mi tiempo en BCN eMotorsport y aunque no pude terminarlo como hubiera querido, me siento bastante orgulloso de lo que hice. Albert y yo seguimos el proyecto durante medio año más. Sin embargo, como *Team Leader* la temporada siguiente, decidí abandonar el proyecto puesto que ya no encajaba con la estrategia del equipo. Habría sido una gran mejora para los futuros coches del equipo, pero resultó no ser la mejor manera de gastar el escaso tiempo y personal del equipo. Después de mucha comunicación entre los miembros del equipo, nos dimos cuenta de que muchos otros proyectos podrían haber tenido el mismo impacto en las competiciones con menos esfuerzo.

Este segundo año en BCN eMotorsport me enseñó una lección crítica e importante: un buen ingeniero debe cuestionar los requerimientos y objetivos que le dan al empezar el proyecto para poder encontrar la mejor manera de utilizar el tiempo y recursos disponibles.