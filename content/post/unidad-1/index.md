+++
date = '2025-05-18T00:50:53-06:00'
draft = false
title = 'Unidad 1: Arquitecturas de computo'
author = "David S."
image = "cover.jpg"
weight = 1

[menu]
  [menu.main]
  identifier = "unidad1"
  name = "Unidad 1"
  weight = -100

    [menu.main.params]
    icon = "number-1"
+++
# 1. Arquitecturas de computo
La arquitectura de computadoras es una disciplina fundamental en la ingeniería en sistemas computacionales, ya que estudia cómo se estructura, organiza y coordina el hardware y, en cierto grado, cómo el software interactúa con él a bajo nivel. Uno de los pilares para entender la evolución de las computadoras modernas radica en los distintos modelos de arquitectura que se han desarrollado a lo largo del tiempo, cada uno adaptado a necesidades específicas de eficiencia, paralelismo, complejidad o costo. Entre los modelos más relevantes se encuentran el modelo clásico, el modelo segmentado y el modelo de multiprocesamiento.

## 1.1 Arquitectura clásica
El modelo clásico, también conocido como arquitectura secuencial o arquitectura de von Neumann, es el paradigma tradicional sobre el que se basan la mayoría de las computadoras desde mediados del siglo XX. Este modelo establece una organización en la que una sola unidad de procesamiento (la CPU) ejecuta instrucciones de forma secuencial, accediendo a una memoria común donde se almacenan tanto las instrucciones como los datos. Esta característica de tener una única memoria para ambos propósitos se conoce como el “cuello de botella de von Neumann”, ya que limita el rendimiento del sistema al forzar que las operaciones de lectura/escritura y de instrucciones compartan el mismo bus.

En la arquitectura clásica, el ciclo de ejecución consta de las siguientes fases fundamentales: búsqueda de la instrucción en memoria (fetch), decodificación de la instrucción (decode), ejecución de la operación (execute) y almacenamiento del resultado (writeback). Esta secuencia, conocida como ciclo de instrucción, se repite indefinidamente mientras el procesador esté activo. Un aspecto importante es que este modelo asume que cada instrucción debe completarse antes de iniciar la siguiente, lo que implica una ejecución estrictamente secuencial sin superposición de etapas.

A nivel estructural, el modelo clásico contiene unidades bien definidas: la unidad aritmético-lógica (ALU), que realiza operaciones matemáticas y lógicas; la unidad de control, que interpreta las instrucciones y coordina la ejecución; y los registros internos, que permiten un acceso rápido a datos intermedios sin tener que acudir a la memoria principal.

Este modelo es ideal para describir computadoras simples o para propósitos educativos, pero sufre de importantes limitaciones cuando se trata de mejorar el rendimiento o implementar paralelismo. Por esta razón, se desarrollaron modelos más complejos, como el segmentado.

## 1.2 Arquitectura segmentada (pipeline)
La arquitectura segmentada es una evolución directa del modelo clásico, diseñada con el objetivo de mejorar el rendimiento sin necesidad de aumentar la frecuencia del reloj o duplicar recursos. Inspirada en las líneas de ensamblaje de la industria manufacturera, esta técnica divide el ciclo de instrucción en varias etapas que pueden operar simultáneamente sobre distintas instrucciones.

Por ejemplo, mientras una instrucción está siendo ejecutada (etapa de ejecución), otra puede estar siendo decodificada y una tercera puede estar en proceso de ser leída desde memoria. Esta superposición de tareas se conoce como "pipeline" o segmentación de instrucciones, y permite que una nueva instrucción entre en el sistema en cada ciclo de reloj, lo que teóricamente aumenta el rendimiento hasta un factor igual al número de etapas del pipeline.

Sin embargo, esta segmentación también introduce nuevos retos. Uno de los principales es el manejo de las dependencias entre instrucciones, ya que dos instrucciones sucesivas podrían requerir el mismo dato o resultado. A estos conflictos se les conoce como “hazards” (riesgos) y se clasifican en tres tipos principales: data hazards, control hazards y structural hazards. Para solucionarlos, los procesadores modernos incorporan técnicas como el forwarding, stalling (interrupciones intencionales del pipeline), o incluso la ejecución especulativa.

Además, las instrucciones condicionales o las interrupciones pueden romper el flujo lineal del pipeline, generando ineficiencias si no se manejan correctamente. Por ello, muchos procesadores modernos integran predicción de saltos (branch prediction) y ejecución fuera de orden (out-of-order execution) como mejoras del modelo segmentado.

El pipeline es una técnica clave en microprocesadores modernos, y la mayoría de las arquitecturas actuales (incluyendo RISC y CISC) lo emplean, incluso combinándolo con otras formas de paralelismo como la ejecución múltiple de instrucciones (superescalaridad).

## 1.3 Arquitectura de multiprocesamiento
Con el crecimiento exponencial de la demanda de cómputo y la aparición de tareas que requieren procesamiento intensivo (como inteligencia artificial, simulaciones físicas o minería de datos), surgió la necesidad de ir más allá del paralelismo interno a un solo procesador. La arquitectura de multiprocesamiento responde a esta necesidad al integrar múltiples unidades de procesamiento que pueden operar en paralelo, compartiendo o no una memoria común.

Existen varios tipos de sistemas multiprocesador. Uno de los más comunes es el modelo SMP (Symmetric Multiprocessing), en el cual todos los procesadores tienen acceso equitativo a la memoria compartida y ejecutan tareas bajo un sistema operativo común. Este modelo se caracteriza por su balance y facilidad de programación, pero puede presentar cuellos de botella cuando muchos procesadores acceden simultáneamente al bus de memoria.

Otra variante es el modelo MPP (Massively Parallel Processing), en donde se emplean cientos o miles de procesadores con memorias locales, conectados mediante redes de interconexión de alta velocidad. Estos sistemas son ideales para tareas distribuidas a gran escala, como el cómputo científico o los centros de datos en la nube.

Además, existe el modelo NUMA (Non-Uniform Memory Access), en el cual cada procesador accede más rápido a su propia memoria local que a la memoria de otros procesadores. Este diseño mejora la escalabilidad, aunque introduce complejidad en la administración de la coherencia de memoria y en la asignación de tareas por parte del sistema operativo.

En la actualidad, incluso los computadores personales y los dispositivos móviles utilizan alguna forma de multiprocesamiento, generalmente en forma de núcleos múltiples (multi-core) dentro de un mismo chip. Cada núcleo puede ejecutar hilos de manera independiente, y en conjunto pueden aumentar el rendimiento y permitir una multitarea más eficiente.

Una consideración importante en este modelo es la concurrencia: no basta con tener múltiples procesadores si el software no está diseñado para ejecutarse en paralelo. Esto ha dado origen a paradigmas de programación concurrente y paralela, que forman parte esencial de la formación en arquitectura y sistemas operativos modernos.

# 2. Análisis de componentes en la arquitectura de computadoras
El análisis de componentes es una etapa fundamental para entender cómo está estructurado internamente un sistema de cómputo. Esta área de estudio descompone el sistema en módulos funcionales que interactúan entre sí para ejecutar programas, procesar datos y coordinar dispositivos periféricos. Los principales elementos que se analizan en esta sección son la arquitectura de la máquina, la CPU como núcleo del procesamiento, la unidad aritmético-lógica encargada de realizar cálculos, y los registros como forma de almacenamiento interno de alta velocidad.

## 2.1 Arquitecturas
Cuando se habla de "arquitecturas" en el contexto del análisis de componentes, se hace referencia a las diferentes formas en que puede organizarse y estructurarse una computadora a nivel lógico y funcional. Este concepto engloba no sólo el diseño del procesador, sino también la forma en que se conectan los subsistemas como la memoria, el sistema de entrada/salida, y los buses de datos y control.

Las dos arquitecturas más influyentes en el diseño de computadoras son:

- Arquitectura de von Neumann: en esta, las instrucciones y los datos residen en una única memoria, y comparten un mismo bus para ser transferidos hacia la CPU. Esto genera un problema conocido como el cuello de botella de von Neumann, ya que sólo puede transmitirse un dato o una instrucción por vez.

- Arquitectura Harvard: separa físicamente la memoria de instrucciones y la de datos, permitiendo un acceso más eficiente y simultáneo a ambas. Es común en microcontroladores y sistemas embebidos.

En la práctica moderna, muchas arquitecturas implementan una versión híbrida de ambos modelos, empleando una arquitectura Harvard internamente (en la caché, por ejemplo), pero presentando una arquitectura von Neumann al programador.

Además, desde un enfoque estructural, se distinguen también dos grandes filosofías:

- CISC (Complex Instruction Set Computer): estas arquitecturas poseen instrucciones complejas y especializadas que realizan múltiples operaciones a la vez, lo que facilita la escritura de programas en ensamblador, pero aumenta la complejidad del hardware.

- RISC (Reduced Instruction Set Computer): utilizan un conjunto reducido y uniforme de instrucciones, lo que permite mayor velocidad, simplicidad en la implementación, y eficiencia en el uso del pipeline. Arquitecturas como ARM y MIPS son ejemplos de RISC.

Comprender estas arquitecturas permite analizar cómo los distintos componentes internos interactúan de manera coordinada para procesar información, y es la base para entender el funcionamiento de la CPU.

## 2.2 Unidad Central de Procesamiento (CPU)
La Unidad Central de Procesamiento es el núcleo de cualquier sistema informático. Se encarga de interpretar y ejecutar las instrucciones que forman un programa. En términos funcionales, se puede considerar que la CPU es el "cerebro" del sistema, ya que realiza tanto las operaciones aritmético-lógicas como el control del flujo de ejecución.

Una CPU está compuesta internamente por varias subunidades, entre las que destacan:

- Unidad de control: interpreta las instrucciones y genera las señales necesarias para que cada componente interno y periférico realice su función. Esta unidad determina qué registros se usan, cuándo se accede a la memoria, y qué operación debe realizarse en la ALU.

- ALU (Unidad Aritmético-Lógica): se encarga de realizar las operaciones aritméticas básicas (suma, resta, etc.) y lógicas (AND, OR, NOT, comparaciones).

- Registros: son pequeñas memorias internas de muy alta velocidad que permiten almacenar datos temporales, instrucciones y direcciones. Son fundamentales para el rendimiento del procesador, ya que acceder a ellos es mucho más rápido que acceder a la memoria principal.

- Buses internos: interconectan todos los elementos de la CPU, permitiendo la transferencia de datos, instrucciones y señales de control. Generalmente, se distinguen tres buses: de datos, de direcciones y de control.

Una CPU moderna puede tener múltiples núcleos (multi-core), cada uno de los cuales puede ejecutar instrucciones en paralelo. Además, incorpora unidades adicionales como FPU (unidad de punto flotante), unidades vectoriales (SIMD), predictores de saltos, unidades de ejecución fuera de orden y cachés internas.

## 2.3 Unidad Aritmético-Lógica (ALU)
La Unidad Aritmético-Lógica es un componente fundamental dentro de la CPU. Se encarga de ejecutar todas las operaciones matemáticas básicas y operaciones lógicas requeridas por los programas. Estas operaciones son de bajo nivel, pero esenciales para cualquier tipo de cálculo que la computadora necesite realizar.

Entre las operaciones aritméticas más comunes se encuentran:

- Suma y resta
- Multiplicación y división (en muchos procesadores se derivan de la suma/resta)
- Incremento y decremento
- Operaciones con signo y sin signo
- Entre las operaciones lógicas están:
- AND, OR, XOR, NOT
- Desplazamientos lógicos y aritméticos (shift y rotate)
- Comparaciones: por igualdad, mayor/menor, etc.

La ALU no trabaja de manera independiente: necesita recibir señales de control que le indiquen qué operación realizar. Estas señales son generadas por la unidad de control, que decodifica las instrucciones provenientes del programa. Además, los operandos con los que trabaja la ALU suelen estar almacenados en registros o provenientes de memoria.

El resultado de una operación realizada por la ALU se guarda en un registro de destino, y ciertos flags o bits de estado pueden actualizarse según el resultado (por ejemplo, si el resultado es cero, si hubo acarreo, si fue negativo, etc.). Estos flags son esenciales para la ejecución de instrucciones condicionales.

## 2.4 Registros
Los registros son unidades de almacenamiento extremadamente rápidas que se encuentran dentro del procesador. A diferencia de la memoria principal, que tiene un acceso relativamente lento, los registros permiten almacenar temporalmente datos e instrucciones en proceso de ejecución con una latencia mínima.

Existen varios tipos de registros, según su propósito:

- Registros de propósito general: se utilizan para almacenar operandos temporales. Por ejemplo, en la arquitectura x86 se tienen registros como EAX, EBX, ECX, EDX.
- Registros de propósito específico:
  - Contador de programa (PC): guarda la dirección de la próxima instrucción a ejecutar.
  - Registro de instrucción (IR): contiene la instrucción actual que se está decodificando o ejecutando.
  - Registro de estado o flags: almacena indicadores de estado (cero, acarreo, signo, desbordamiento, etc.).
  - Puntero de pila (SP): guarda la dirección del tope de la pila.
  - Base y desplazamiento: usados para direccionamiento de memoria segmentado.
  - Registros de control: utilizados por el sistema operativo o por el hardware para coordinar operaciones internas del procesador, como la memoria virtual o los modos de ejecución.

La cantidad y tipo de registros varía según la arquitectura. Por ejemplo, las arquitecturas RISC tienden a tener muchos registros de propósito general para reducir la necesidad de acceder a la memoria. En cambio, las arquitecturas CISC tienen menos registros pero instrucciones más potentes que operan directamente sobre memoria.

El acceso rápido a registros permite que muchas instrucciones se ejecuten en tan solo un ciclo de reloj, por lo que su uso eficiente es clave para el rendimiento del sistema. Por eso, muchos compiladores optimizan el uso de registros en tiempo de compilación.

## 2.5 Buses
En la arquitectura de computadoras, un bus es un sistema de comunicación interno que permite la transferencia de datos entre los distintos componentes del sistema, como la CPU, la memoria y los dispositivos de entrada/salida. Aunque la palabra “bus” evoca la idea de un canal físico, en realidad representa una abstracción lógica y eléctrica del mecanismo de transporte de datos dentro del hardware del sistema.

El bus es fundamental para la operación coordinada de los distintos módulos de la computadora. Para comprender su funcionamiento, hay que tener presente que la CPU necesita constantemente comunicarse con otros elementos para leer instrucciones, mover datos, almacenar resultados y recibir o enviar señales externas. El bus actúa como el medio común a través del cual se realiza toda esta actividad.

El sistema de buses está compuesto por tres canales principales: el bus de direcciones, que lleva información sobre la ubicación de datos o instrucciones en memoria; el bus de datos, que transporta los valores binarios propiamente dichos; y el bus de control, que transmite señales que sincronizan y determinan el tipo de operación que se está ejecutando (lectura, escritura, interrupción, etc.).

En muchas arquitecturas, el diseño y el ancho de estos buses impactan directamente el rendimiento. Por ejemplo, un bus de datos de 64 bits permite transferir el doble de información en un solo ciclo que uno de 32 bits. Además, la velocidad del bus y su ancho de banda determinan cuánta información puede moverse entre los componentes del sistema por segundo. Por eso, en computadoras de alto rendimiento, se emplean tecnologías como buses dedicados, buses internos de alta velocidad, o incluso redes de interconexión en sistemas multinúcleo o multiprocesador.

## 2.6. Memoria
En el corazón de cualquier computadora está el sistema de memoria, que constituye el soporte físico y lógico donde se almacenan los datos y las instrucciones necesarias para que el sistema opere. El procesador, por rápido que sea, depende enteramente de su capacidad para acceder eficientemente a la memoria. Por lo tanto, el análisis de este componente es esencial para entender el rendimiento y la arquitectura de cualquier sistema computacional.

### 2.6.1 Fundamentos de la gestión de memoria
La gestión de memoria es la técnica mediante la cual el sistema operativo administra el espacio de memoria física y virtual disponible para los programas en ejecución. Dado que la memoria es un recurso limitado, debe asignarse, protegerse, y reciclarse de manera eficiente para evitar cuellos de botella, errores y vulnerabilidades.

A nivel básico, cuando un programa se ejecuta, se le asigna un espacio de direcciones que contiene distintas regiones: código (instrucciones del programa), datos estáticos, pila (stack) y montón (heap). Estas regiones son administradas mediante esquemas como la segmentación (donde cada tipo de datos ocupa un segmento distinto) o la paginación (donde la memoria se divide en bloques de tamaño fijo llamados páginas).

El sistema operativo utiliza estructuras como tablas de páginas, listas de bloques libres y mecanismos de intercambio (swap) para gestionar qué parte de la memoria física está siendo utilizada por qué proceso, y qué porciones pueden guardarse temporalmente en disco para liberar RAM cuando sea necesario.

Además, la protección de memoria es clave: cada proceso debe estar aislado del resto para que no corrompa datos de otros. Esto se logra mediante técnicas de traducción de direcciones con la ayuda de una unidad de gestión de memoria (MMU) que convierte direcciones virtuales en direcciones físicas en tiempo real.

Este nivel de abstracción no solo mejora la seguridad, sino que permite aprovechar mejor los recursos físicos disponibles, ejecutando múltiples procesos como si cada uno tuviera su propia computadora.

### 2.6.2 Memoria principal
La memoria principal, también conocida como RAM (Random Access Memory), es el espacio de almacenamiento directamente accesible por la CPU para ejecutar instrucciones y manipular datos. Es una memoria volátil, lo que significa que su contenido se pierde al apagar el equipo.

Su función central es actuar como intermediaria entre el almacenamiento permanente (como un disco duro o SSD) y el procesador. Cuando un programa se abre, su contenido se carga desde el disco a la memoria RAM para que el CPU pueda acceder a él rápidamente. Por eso, la velocidad de la memoria y su cantidad disponible influyen directamente en el rendimiento del sistema.

Existen varios tipos de RAM, siendo la más común en la actualidad la DRAM (Dynamic RAM), que necesita ser refrescada constantemente para mantener los datos. También está la SRAM (Static RAM), más rápida y costosa, utilizada en cachés. La RAM opera con tiempos de acceso en el orden de nanosegundos, pero aún así es mucho más lenta que los registros de la CPU, lo que motivó la creación de mecanismos de cacheo.

La organización de la memoria RAM puede ser lineal o segmentada, y su acceso puede ser sincrónico (como en SDRAM) o asincrónico. La tecnología de canal dual, triple o cuádruple permite que varias memorias trabajen en paralelo, duplicando o cuadruplicando el ancho de banda disponible.

### 2.6.3 Memoria caché
La memoria caché es un tipo de memoria extremadamente rápida y costosa que se encuentra dentro o muy cerca del procesador. Su objetivo es minimizar la diferencia de velocidad entre la CPU y la RAM, evitando que el procesador se detenga mientras espera los datos de memoria principal.

Cuando la CPU necesita acceder a un dato o instrucción, primero consulta si ya está disponible en la caché. Si lo está, se produce un acierto (hit) y el acceso es inmediato. Si no lo está, se produce un fallo (miss) y debe recuperarse desde la RAM, lo cual implica mayor latencia.

Las cachés modernas están organizadas en niveles jerárquicos:

- Nivel 1 (L1): es la más rápida y más pequeña (típicamente de 32 KB a 128 KB), ubicada directamente dentro del núcleo del procesador. Se suele dividir en dos: una para instrucciones y otra para datos.
- Nivel 2 (L2): más grande y algo más lenta, pero aún dentro del chip del procesador. Su tamaño va de 256 KB a varios MB.
- Nivel 3 (L3): compartida entre varios núcleos en procesadores multinúcleo. Más grande (hasta decenas de MB), pero más lenta que L1 y L2.

El funcionamiento de la caché se basa en políticas de reemplazo (como LRU: Least Recently Used) y técnicas de mapeo (directo, asociativo, totalmente asociativo) para decidir qué datos conservar o descartar. Estas técnicas permiten optimizar qué porciones de memoria se mantienen cerca del procesador en función del patrón de acceso reciente.

Desde un punto de vista de diseño, la eficiencia de la caché es uno de los factores más críticos para el rendimiento de una CPU moderna. Por eso, la ingeniería de procesadores dedica gran esfuerzo a diseñar subsistemas de caché eficientes, con múltiples niveles, predicción de saltos, y prefetching inteligente.

## 7. Manejo de Entrada/Salida (E/S)
El manejo de entrada/salida (E/S) en una computadora abarca el conjunto de mecanismos que permiten que el procesador se comunique con los dispositivos periféricos, ya sean teclados, discos, pantallas, impresoras, tarjetas de red o cualquier otro componente externo. En un sentido amplio, cualquier operación que implique comunicación con el "mundo exterior" de la CPU entra dentro del dominio de la E/S.

A diferencia de la memoria principal, que está diseñada para acceso rápido y estructurado, los dispositivos de E/S suelen ser lentos, heterogéneos y no uniformes. Esta discrepancia de velocidad y comportamiento hace que la E/S requiera técnicas especializadas para evitar que el procesador quede inactivo esperando, desperdiciando tiempo de cómputo valioso. Por eso, la arquitectura moderna implementa múltiples métodos de control de E/S, cada uno con distintos niveles de intervención del procesador y autonomía del hardware.

### 7.1 Módulos de entrada/salida
Los módulos de E/S son circuitos o conjuntos de lógica que actúan como intermediarios entre la CPU y los dispositivos periféricos. Su rol es traducir las señales y comandos del sistema a un formato comprensible para el periférico, y viceversa. Este módulo se encarga de coordinar el acceso, generar señales de control, gestionar buffers de datos y, en muchos casos, realizar conversiones entre velocidades o formatos de datos.

Desde el punto de vista funcional, los módulos de E/S ofrecen al procesador un conjunto de registros para control (por ejemplo, activar el dispositivo), estado (por ejemplo, indicar si está ocupado), y datos (para leer o escribir información). El procesador puede acceder a estos registros como si fueran parte de su espacio de direcciones, ya sea mediante E/S mapeada en memoria o E/S mapeada en puertos.

En sistemas modernos, muchos módulos de E/S se integran dentro de controladores de dispositivos o controladoras (como las controladoras SATA, USB, o de red), que son componentes programables responsables de manejar toda la interacción con un tipo específico de dispositivo.

### 7.2 Entrada/salida programada
En el esquema más básico, conocido como E/S programada, el procesador es responsable directo de iniciar y completar todas las operaciones de E/S. Esto significa que la CPU emite instrucciones explícitas para acceder al módulo de E/S, consulta continuamente (polling) si el dispositivo está listo, y transfiere los datos palabra por palabra entre los registros del módulo de E/S y la memoria.

Este enfoque, aunque simple, tiene una gran desventaja: el procesador queda ocupado durante todo el proceso de transferencia, lo que genera una baja eficiencia general del sistema, especialmente cuando se trata de dispositivos lentos como discos o redes. Sin embargo, la E/S programada puede ser útil en sistemas embebidos o dispositivos simples donde la eficiencia energética o la simplicidad del hardware son prioritarios.

Por ejemplo, si el procesador quiere leer una tecla presionada, entra en un bucle de espera preguntando al teclado “¿hay una tecla disponible?”, y cuando finalmente la hay, lee su valor directamente. Este bucle de espera (busy-waiting) consume tiempo que podría emplearse en otras tareas.

### 7.3 Entrada/salida mediante interrupciones
Para mejorar el rendimiento, muchos sistemas emplean la entrada/salida con interrupciones. En este modelo, el procesador emite una orden al módulo de E/S y continúa ejecutando otras instrucciones sin esperar a que la operación de E/S se complete. Cuando el dispositivo ha terminado su tarea (por ejemplo, cuando ha recibido datos o ha finalizado una escritura), genera una interrupción, es decir, una señal al procesador que lo obliga a detener lo que está haciendo y atender la solicitud del dispositivo.

Esta interrupción provoca que el CPU ejecute una rutina especial llamada manejador de interrupciones (Interrupt Service Routine, ISR), la cual procesa la información relacionada con la E/S (por ejemplo, leer un byte del teclado, verificar el estado de una tarjeta de red, o mover datos a la memoria). Luego, el procesador puede reanudar la tarea que estaba ejecutando antes de ser interrumpido.

Este modelo permite que el CPU aproveche mejor su tiempo, ya que no queda bloqueado esperando, sino que actúa solo cuando se requiere su atención. La clave para que esto funcione bien está en el diseño de prioridades de interrupciones y el tiempo de respuesta del sistema operativo para atenderlas.

### 7.4 Acceso directo a memoria (DMA)
El siguiente nivel de sofisticación es el uso de DMA (Direct Memory Access), que permite que ciertos módulos de E/S realicen transferencias directamente entre el dispositivo y la memoria principal, sin intervención activa del procesador. Esto es posible gracias a un componente llamado controlador DMA, que actúa como un “procesador secundario” especializado en mover datos.

Cuando se inicia una operación de DMA, el procesador simplemente le indica al controlador qué datos mover, desde dónde, hacia dónde y cuántos. Luego, el CPU puede seguir ejecutando otras tareas, mientras el controlador DMA se encarga de realizar la transferencia en segundo plano. Cuando finaliza, el controlador genera una interrupción al procesador para avisarle que la operación ha terminado.

Esta técnica es extremadamente eficiente para transferencias masivas de datos, como la lectura o escritura en disco, la reproducción de audio, o el procesamiento de video. En estos casos, la CPU se convierte en un coordinador más que en un ejecutor de operaciones de E/S, lo que libera su tiempo para tareas más críticas como el control del flujo de programas o el procesamiento lógico.

El uso de DMA requiere una coordinación precisa para evitar conflictos de acceso a memoria. Por ejemplo, cuando tanto la CPU como el controlador DMA intentan acceder simultáneamente a la memoria, se emplean técnicas como arbitraje del bus, acceso intercalado o bloqueo temporal.

### 7.5 Canales y procesadores de E/S
En sistemas de computación de alto rendimiento, como los mainframes o servidores de misión crítica, el volumen de operaciones de E/S es tan alto que incluso los controladores DMA pueden no ser suficientes. En este contexto, se introducen los canales de E/S y los procesadores de E/S, que son unidades de hardware completas y autónomas, dedicadas exclusivamente al manejo de dispositivos periféricos.

Un canal de E/S es esencialmente un procesador especializado que ejecuta instrucciones específicas de E/S, conocidas como programas de canal. Este canal puede gestionar múltiples dispositivos, realizar transferencias complejas y resolver interrupciones por sí mismo, sin cargar al procesador principal.

Los procesadores de E/S van aún más lejos: son CPUs independientes dentro del sistema, con su propio sistema de control y ejecución, que se encargan de todo el subsistema de entrada/salida. Este modelo permite un desacoplamiento casi completo entre el procesamiento de datos y el acceso a dispositivos, mejorando enormemente la escalabilidad del sistema.

Este enfoque es típico en arquitecturas como IBM Z (mainframes) o en supercomputadoras, donde el objetivo es maximizar la eficiencia del cómputo mientras se garantiza un flujo continuo de datos desde y hacia el almacenamiento masivo o la red.

## 8. Buses
En los sistemas computacionales modernos, los buses representan uno de los pilares fundamentales de la arquitectura del hardware. Constituyen el mecanismo principal mediante el cual los diferentes componentes del sistema —como el procesador, la memoria principal, los dispositivos de entrada/salida, entre otros— se comunican entre sí. Para comprender la importancia de los buses, es esencial explorar su tipología, estructura, jerarquía y su relación intrínseca con el sistema de interrupciones.

Un bus puede definirse como un conjunto de líneas de comunicación compartidas que transportan datos, direcciones y señales de control entre los distintos elementos de un sistema informático. La arquitectura del bus, por tanto, está diseñada para permitir la transferencia eficiente y coordinada de información en ambos sentidos, bajo un conjunto de reglas bien definidas. Desde un punto de vista funcional, un bus se compone típicamente de tres subconjuntos: el bus de datos, el bus de direcciones y el bus de control.

El bus de datos es el canal por el cual circula la información que será procesada o que ha sido procesada. Su ancho, es decir, el número de líneas físicas que lo componen, determina cuántos bits pueden transferirse simultáneamente. Por ejemplo, un bus de datos de 32 bits puede mover 4 bytes por ciclo de reloj, lo que influye directamente en el rendimiento del sistema. Por otro lado, el bus de direcciones se utiliza para identificar la ubicación de la fuente o el destino de los datos en la memoria o en dispositivos de entrada/salida. Es decir, permite al procesador seleccionar una dirección específica donde leer o escribir datos. Finalmente, el bus de control transporta las señales que gestionan el flujo de datos, como las órdenes de lectura o escritura, señales de reloj, y líneas de interrupción.

### 8.2 Tipos de buses
Existen varios tipos de buses clasificados según su función. Los buses internos (también llamados buses locales o del sistema) permiten la comunicación entre el CPU, la memoria principal y algunos dispositivos internos de alto rendimiento. Un ejemplo clásico es el bus del sistema en arquitecturas x86, que conecta la CPU con el chipset y la RAM. Los buses externos o de expansión, en cambio, están destinados a conectar dispositivos periféricos como discos duros, impresoras o tarjetas de video. Dentro de esta categoría encontramos estándares como PCI, PCIe, USB, entre otros. Algunos buses están dedicados exclusivamente a funciones específicas, como los buses de memoria, buses gráficos (como AGP en sistemas antiguos) o buses seriales como SATA.

### 8.2 Estructura de los buses
La estructura del bus se refiere a cómo se organizan físicamente y lógicamente sus líneas. Tradicionalmente, los buses han sido compartidos, es decir, todos los dispositivos conectados a él comparten las mismas líneas físicas. En este esquema, solo un dispositivo puede comunicarse en un instante determinado, lo que requiere de un mecanismo de arbitraje para decidir quién tiene el control del bus. El arbitraje puede ser centralizado, cuando una unidad (generalmente el chipset o un controlador de bus) decide a quién otorgar el control; o distribuido, cuando los dispositivos negocian entre sí de manera descentralizada. En arquitecturas modernas, el concepto de bus ha evolucionado hacia arquitecturas de interconexión más sofisticadas, como los crossbars, las redes en chip (NoC) o las interconexiones punto a punto como las que ofrece PCI Express, que eliminan los cuellos de botella de los buses compartidos tradicionales.
i
### 8.3 Jerarquía de los buses
Respecto a la jerarquía de buses, los sistemas computacionales actuales suelen organizar sus buses en varios niveles que reflejan la cercanía al procesador y el rendimiento necesario. En la parte superior se encuentran los buses de alto rendimiento, como el bus frontal (Front-Side Bus) o el bus de interconexión del procesador, que comunica directamente la CPU con la memoria principal o el controlador de memoria. Más abajo en la jerarquía encontramos buses de propósito general como PCI o PCIe, y finalmente, en los niveles más bajos, buses lentos como USB o I²C, empleados en comunicaciones con periféricos de baja velocidad o dispositivos embebidos. Esta jerarquía no solo responde a razones de velocidad, sino también de costo, consumo energético y modularidad del diseño.

### 8.4 Interrupciones
Un elemento crítico del funcionamiento de los buses y, por extensión, de todo el sistema, son las interrupciones. Las interrupciones constituyen un mecanismo mediante el cual un dispositivo puede señalar al procesador que requiere atención inmediata. Cuando se produce una interrupción, el procesador detiene temporalmente su ejecución normal y transfiere el control a una rutina especial llamada manejador de interrupciones (ISR, por sus siglas en inglés). Este mecanismo es esencial para implementar entrada/salida eficiente sin recurrir a técnicas ineficaces como la espera activa (busy waiting), y permite al sistema reaccionar rápidamente ante eventos asíncronos como la llegada de datos desde un puerto de red, la finalización de una operación de disco o la presión de una tecla por parte del usuario.

Las interrupciones pueden ser enmascarables o no enmascarables. Las primeras pueden ser temporalmente desactivadas por el procesador cuando necesita ejecutar código crítico sin ser interrumpido, mientras que las segundas, como las señales de fallo de hardware, no pueden ser ignoradas. El sistema también gestiona un esquema de prioridades para determinar qué interrupción debe ser atendida primero si se presentan varias simultáneamente. Este manejo eficiente requiere el uso de controladores de interrupciones programables (como el PIC en arquitecturas x86 o el APIC en versiones modernas), que permiten el direccionamiento adecuado de las señales de interrupción.