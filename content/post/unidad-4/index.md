+++
date = '2025-05-18T13:17:00-06:00'
draft = false
title = 'Unidad 4: Computación paralela'
author = "David S."
image = "cover.jpg"
weight = 4

[menu]
  [menu.main]
  identifier = "unidad4"
  name = "Unidad 4"
  weight = -97

    [menu.main.params]
    icon = "number-4"
+++
# 1. Aspectos básicos de la computación paralela
El procesamiento paralelo consiste en la ejecución concurrente de múltiples instrucciones o flujos de datos con el objetivo de acelerar la resolución de problemas computacionales. A diferencia del modelo secuencial tradicional (donde las operaciones se realizan una tras otra), el paralelismo permite que varias tareas avancen al mismo tiempo, siempre y cuando no existan dependencias críticas entre ellas.

Este enfoque es especialmente útil en aplicaciones que manejan grandes volúmenes de datos, como simulaciones científicas, aprendizaje automático, renderizado gráfico y procesamiento de señales. Sin embargo, no todas las tareas pueden paralelizarse fácilmente, ya que algunas tienen dependencias secuenciales inherentes que limitan la concurrencia.

El paralelismo puede implementarse en diferentes niveles, desde instrucciones individuales hasta sistemas distribuidos:

1. Paralelismo a Nivel de Instrucción (ILP - Instruction-Level Parallelism)
Los procesadores modernos utilizan técnicas como pipelining, ejecución fuera de orden (out-of-order execution) y superscalaridad para ejecutar múltiples instrucciones en paralelo dentro de un mismo núcleo. Esto se logra detectando instrucciones independientes que no requieren esperar a que otras finalicen. Por ejemplo, en una arquitectura superscalar, si un programa tiene una suma y una multiplicación que no dependen una de la otra, la CPU puede ejecutarlas simultáneamente en unidades aritméticas distintas. Sin embargo, si una instrucción necesita el resultado de la otra, el paralelismo se ve limitado.

2. Paralelismo a Nivel de Hilo (TLP - Thread-Level Parallelism)
Cuando un solo núcleo no es suficiente, los sistemas modernos utilizan multihilo simultáneo (SMT), como la tecnología Hyper-Threading de Intel, que permite ejecutar múltiples hilos de ejecución en un mismo núcleo físico, compartiendo recursos pero mejorando la utilización del procesador. Además, los procesadores multinúcleo (como los actuales CPUs con 4, 8, 16 o más núcleos) permiten ejecutar hilos verdaderamente en paralelo, asignando diferentes tareas a cada núcleo. Esto es esencial en sistemas operativos modernos y aplicaciones optimizadas para concurrencia.

3. Paralelismo a Nivel de Datos (DLP - Data-Level Parallelism)
Algunas operaciones, como el procesamiento de matrices o imágenes, aplican la misma operación a múltiples elementos de datos. Aquí, las arquitecturas SIMD (Single Instruction, Multiple Data) son clave, ya que permiten ejecutar una sola instrucción sobre múltiples datos al mismo tiempo. Las extensiones de instrucciones SIMD (como SSE, AVX en x86 o NEON en ARM) son ampliamente utilizadas en aplicaciones multimedia, inteligencia artificial y procesamiento científico.

4. Paralelismo a Nivel de Tarea (Task Parallelism)
En este modelo, diferentes tareas independientes se ejecutan en paralelo. Por ejemplo, un servidor web puede manejar múltiples solicitudes de usuarios simultáneamente asignando cada una a un hilo o proceso distinto. Esto es común en sistemas distribuidos y computación en la nube.

5. Paralelismo a Gran Escala: GPU y Computación Distribuida
Las Unidades de Procesamiento Gráfico (GPU) son un caso especial de procesamiento paralelo masivo, diseñadas originalmente para renderizar gráficos pero ahora utilizadas en computación de alto rendimiento (HPC) y aprendizaje profundo. A diferencia de los CPUs, que tienen unos pocos núcleos optimizados para tareas generales, las GPU tienen miles de núcleos pequeños especializados en operaciones paralelizables. Por otro lado, la computación distribuida (como los clusters y sistemas como Apache Hadoop o Spark) permite dividir problemas enormes en subproblemas que se resuelven en múltiples máquinas conectadas en red.




# 2. Tipos de computación paralela
La computación paralela ha revolucionado la forma en que procesamos información, permitiendo resolver problemas complejos de manera eficiente mediante la distribución de tareas en múltiples unidades de procesamiento. Sin embargo, no todas las formas de paralelismo son iguales, y su implementación depende en gran medida de la arquitectura del sistema, la organización de la memoria y las características del problema a resolver.

El paralelismo puede categorizarse según cómo se dividen las tareas y cómo interactúan los procesadores. Una de las clasificaciones más influyentes es la taxonomía de Flynn, que distingue entre cuatro modelos fundamentales que veremos a continuación.

## 2.1 Clasificación
### 1. SISD (Single Instruction, Single Data)
Este modelo representa la computación tradicional secuencial, donde un único flujo de instrucciones opera sobre un único flujo de datos. Las arquitecturas clásicas de von Neumann entran en esta categoría, con un solo procesador ejecutando instrucciones una tras otra. Aunque no es paralelo, es importante entenderlo como punto de partida para comparar con sistemas más avanzados.

### 2. SIMD (Single Instruction, Multiple Data)
En este esquema, una misma instrucción se aplica simultáneamente a múltiples datos. Es especialmente útil en operaciones vectoriales y matriciales, como procesamiento de imágenes o simulaciones numéricas. Las extensiones de instrucciones SSE, AVX (en CPUs x86) y los shaders en GPU son ejemplos de este enfoque.

### 3. MISD (Multiple Instruction, Single Data)
Este modelo es menos común y consiste en múltiples procesadores aplicando diferentes instrucciones sobre el mismo dato. Un caso teórico podría ser un sistema de tolerancia a fallos donde varias unidades verifican un cálculo, pero en la práctica, las implementaciones puras de MISD son raras.

### 4. MIMD (Multiple Instruction, Multiple Data)
Aquí, múltiples procesadores ejecutan diferentes instrucciones sobre distintos datos de manera independiente. Es el modelo más flexible y se utiliza en sistemas multinúcleo, clusters y computación distribuida. Puede ser de dos tipos:
- Memoria Compartida (Multiprocesadores): Todos los núcleos acceden a un mismo espacio de direcciones (ej. CPUs multinúcleo con UMA/NUMA).
- Memoria Distribuida (Multicomputadoras): Cada nodo tiene su propia memoria y se comunican mediante mensajes (ej. sistemas MPI, clusters).


## 2.2 Arquitectura de Computadoras secuenciales
Las primeras computadoras seguían un modelo estrictamente secuencial (SISD), donde cada instrucción debía completarse antes de iniciar la siguiente. Sin embargo, con el surgimiento del pipelining, se introdujo un primer nivel de paralelismo implícito, solapando etapas de ejecución (fetch, decode, execute, write-back) para mejorar el rendimiento.

A pesar de estas optimizaciones, el límite físico en la frecuencia de reloj (ley de Dennard) llevó a la adopción de arquitecturas explícitamente paralelas, como:
- Procesadores Superscalares: Capaces de ejecutar múltiples instrucciones por ciclo gracias a múltiples unidades funcionales.
- Multiprocesadores Simétricos (SMP): Varios CPUs compartiendo memoria en un mismo sistema.
- Arquitecturas Heterogéneas: Combinación de CPUs generales con aceleradores paralelos como GPU o TPUs.


## 2.3  Organización de direcciones de memoria
La manera en que los procesadores acceden a la memoria es crucial para el rendimiento en entornos paralelos. Existen dos enfoques principales:

### 1. Memoria Compartida (Shared Memory)
Todos los procesadores acceden a un mismo espacio de direcciones físico. Esto simplifica la programación pero requiere mecanismos de sincronización (semáforos, mutex) para evitar condiciones de carrera. Puede ser:

- UMA (Uniform Memory Access): Todos los núcleos tienen la misma latencia de acceso (ej. sistemas SMP básicos).

- NUMA (Non-Uniform Memory Access): La latencia varía según la proximidad del núcleo a la memoria (ej. servidores multi-socket).

### 2. Memoria Distribuida (Distributed Memory)
Cada nodo tiene su propia memoria local y se comunica con otros mediante paso de mensajes (MPI, RPC). Elimina la necesidad de sincronización global pero aumenta la complejidad en la gestión de datos distribuidos.

Un híbrido común es memoria compartida distribuida (DSM), donde el hardware simula un espacio de direcciones único sobre memoria físicamente distribuida.



# 3. Sistemas de memoria compartida
Los sistemas de memoria compartida representan uno de los paradigmas más importantes en computación paralela, donde múltiples procesadores acceden a un espacio de direcciones común. Sin embargo, el verdadero desafío en estas arquitecturas radica en cómo conectar eficientemente los procesadores con la memoria y entre sí. Aquí es donde las redes de interconexión dinámicas juegan un papel fundamental, determinando el rendimiento, la escalabilidad y la coherencia del sistema.

En un sistema de memoria compartida, todos los núcleos de procesamiento pueden acceder directamente a la misma memoria física, lo que simplifica la programación paralela al eliminar la necesidad de comunicación explícita entre procesos. No obstante, esta aparente simplicidad oculta una compleja infraestructura de hardware que debe resolver varios problemas críticos:
- Contención por acceso a memoria: Cuando múltiples procesadores intentan leer o escribir en una misma ubicación simultáneamente.
- Coherencia de caché: Mantener consistencia entre las copias locales de datos almacenadas en las cachés de cada procesador.
- Latencia de acceso: Minimizar el tiempo que tarda un procesador en obtener datos desde la memoria compartida.

Las redes de interconexión dinámicas son las encargadas de manejar estas complejidades, permitiendo que los componentes del sistema se comuniquen de manera flexible según las demandas de la carga de trabajo.

## 3.1 Redes de interconexión dinámicas o indirectas
A diferencia de las redes estáticas (como las mallas o toros en sistemas de memoria distribuida), las redes dinámicas permiten conexiones configurables entre procesadores y memoria. Estas se dividen principalmente en dos categorías, las cuales son las siguientes:

### 3.1.1 Redes de medio compartido
En este esquema, todos los dispositivos comparten un único canal de comunicación, lo que significa que solo un transmisor puede enviar datos en un momento dado. Un ejemplo clásico es el bus compartido, utilizado ampliamente en sistemas multiprocesador simétricos (SMP).

**Ventajas:**
- Simplicidad: La arquitectura es fácil de implementar y entender.
- Bajo costo: Requiere menos hardware que alternativas más complejas.

**Limitaciones:**
- Ancho de banda limitado: Al ser un recurso compartido, el bus se convierte rápidamente en un cuello de botella cuando muchos procesadores intentan acceder a memoria simultáneamente.
- Escalabilidad pobre: A medida que se añaden más procesadores, la contención en el bus degrada el rendimiento.

Para mitigar estos problemas, se emplean técnicas como el arbitraje de bus, que decide qué procesador obtiene acceso al bus cuando hay múltiples solicitudes. Los protocolos de coherencia como MESI (Modified, Exclusive, Shared, Invalid) para mantener consistencia en las cachés. Sin embargo, en sistemas con decenas o cientos de núcleos, el bus compartido resulta insuficiente, llevando al uso de redes conmutadas más sofisticadas.

### 3.1.2 Redes conmutadas
Estas redes superan las limitaciones del medio compartido mediante el uso de conmutadores (switches) que permiten múltiples comunicaciones simultáneas. Aquí, la conexión entre procesadores y memoria es dinámica, estableciéndose rutas dedicadas según sea necesario.

Algunos de sus tipos principales que podemos mencionar son:
- Redes Crossbar (Cruzadas)
Un crossbar es una matriz de conexiones que permite enlazar cualquier entrada con cualquier salida sin bloqueo. Si un procesador quiere comunicarse con un módulo de memoria, se establece una ruta exclusiva a través de la matriz.

**Ventajas:**
- Paralelismo máximo: Múltiples comunicaciones pueden ocurrir al mismo tiempo siempre que no compartan filas o columnas.
- Baja latencia: Una vez establecida la ruta, la comunicación es directa.

**Desventajas:**
- Complejidad hardware: El número de conmutadores crece cuadráticamente (O(N²)), haciéndolo prohibitivo para sistemas con cientos de nodos.

- Redes Multietapa (Multistage Interconnection Networks, MIN)
Estas redes usan múltiples capas de conmutadores simples (como los omega o delta networks) para conectar N procesadores con N módulos de memoria. A diferencia del crossbar, requieren menos hardware (O(N log N)), pero pueden presentar bloqueos si múltiples solicitudes compiten por los mismos conmutadores intermedios.

**Aplicaciones:**
- Sistemas NUMA (Non-Uniform Memory Access), donde la memoria está distribuida físicamente pero es accesible lógicamente por todos los procesadores.
- GPUs modernas, que usan redes complejas para conectar núcleos de procesamiento con bancos de memoria.

- Redes Conmutadas de Alta Velocidad (Como InfiniBand o Ethernet RDMA)
En sistemas a gran escala (como supercomputadoras), se emplean redes conmutadas de baja latencia para interconectar nodos con memoria compartida distribuida. Estas redes permiten acceso remoto directo a memoria (RDMA), reduciendo la sobrecarga del sistema operativo en la comunicación.

# 4. Sistemas de memoria distribuida: Multiprocesadores
En el ámbito de la computación de alto rendimiento, los sistemas de memoria distribuida representan un enfoque escalable para el procesamiento paralelo, donde cada procesador tiene su propia memoria local y la comunicación entre nodos se realiza mediante el paso explícito de mensajes. A diferencia de los sistemas de memoria compartida, estos esquemas eliminan los cuellos de botella asociados al acceso concurrente a una memoria centralizada, pero introducen desafíos en cuanto a la comunicación eficiente entre procesadores. Aquí, las redes de interconexión estáticas juegan un papel fundamental, definiendo cómo los nodos se conectan físicamente y cómo los datos fluyen a través del sistema.

En un sistema de memoria distribuida, cada nodo de procesamiento consta de:
- Una o más CPUs con capacidad de ejecución independiente.
- Memoria local privada, accesible únicamente por el procesador asociado.
- Mecanismos de comunicación (como interfaces de red) para intercambiar datos con otros nodos.

Este modelo es la base de arquitecturas como los clusters y las supercomputadoras modernas, donde miles de nodos trabajan en conjunto para resolver problemas masivamente paralelos. La ausencia de memoria compartida global simplifica el diseño hardware (evitando problemas de coherencia) pero requiere algoritmos y protocolos de comunicación cuidadosamente diseñados, como el estándar MPI (Message Passing Interface).


## 4.1 Redes de interconexión estáticas
Las redes estáticas (también llamadas directas) definen una topología física fija entre los nodos, donde las conexiones son permanentes y no pueden reconfigurarse dinámicamente. Estas redes son comunes en sistemas donde la predictibilidad y la baja latencia son críticas, como en procesadores vectoriales o sistemas integrados de alto rendimiento.

### Características Clave
- Regularidad: La topología sigue un patrón geométrico predefinido (como una malla, toro o hipercubo).

- Escalabilidad Determinista: El número de conexiones por nodo (grado) y el diámetro de la red (máxima distancia entre dos nodos) crecen de manera predecible al añadir más procesadores.

- Localidad Explotable: Las aplicaciones pueden optimizarse para minimizar la comunicación entre nodos distantes, aprovechando vecindarios cercanos en la red.

# 5. Casos de estudio
La malla bidimensional ha sido una topología ampliamente adoptada en arquitecturas paralelas debido a su simplicidad y escalabilidad. En sistemas como el Intel Paragon, una de las primeras supercomputadoras comerciales basadas en esta estructura, los nodos se organizaban en una cuadrícula donde cada procesador se conectaba directamente con sus vecinos inmediatos en cuatro direcciones. Esta disposición permitía un diseño modular y eficiente para problemas con localidad espacial, como simulaciones de dinámica de fluidos o procesamiento de imágenes. Sin embargo, a medida que el número de nodos crecía, la distancia entre procesadores en esquinas opuestas de la malla aumentaba linealmente, generando latencias significativas en operaciones que requerían comunicación global.

Una evolución natural de la malla es el toro, que introduce conexiones adicionales entre los nodos ubicados en los bordes de la red, creando un patrón circular en cada dimensión. Este enfoque fue implementado exitosamente en el IBM Blue Gene/L, donde miles de nodos se interconectaban en una red tridimensional con enlaces toroidales. La principal ventaja de esta topología era la reducción del diámetro de la red, lo que permitía comunicaciones más rápidas entre nodos distantes en comparación con una malla tradicional. Además, la redundancia en las conexiones mejoraba la tolerancia a fallos, ya que los mensajes podían enrutarse a través de caminos alternativos si algún enlace fallaba. No obstante, la complejidad física del cableado y la necesidad de gestionar las conexiones circulares añadían desafíos en el diseño de estos sistemas.

Por otro lado, el hipercubo representó una solución radicalmente diferente, donde cada nodo se conectaba a otros siguiendo las dimensiones de un cubo multidimensional. Arquitecturas como la nCUBE aprovecharon esta topología para ofrecer un diámetro mínimo y un alto grado de paralelismo en operaciones globales. En un hipercubo de dimensión *d*, cualquier par de nodos estaba separado por a lo sumo *d* saltos, lo que lo hacía ideal para algoritmos que requerían comunicaciones intensivas entre todos los procesadores. Sin embargo, la escalabilidad de estos sistemas era discreta, limitada a potencias de dos, y el número de conexiones por nodo crecía logarítmicamente con el tamaño total de la red, incrementando tanto el coste como el consumo energético.

Finalmente, las topologías en árbol, incluyendo variantes como los fat trees, abordaron el problema de la agregación de datos en sistemas jerárquicos. En la supercomputadora Cray T3E, por ejemplo, se utilizó una estructura de árbol "gordo" donde los niveles superiores de la red tenían mayor ancho de banda para evitar congestiones. Esto era particularmente útil en aplicaciones donde los nodos hoja necesitaban enviar datos a un punto central, como en operaciones de reducción o broadcast. No obstante, la naturaleza jerárquica de estas redes introducía cuellos de botella potenciales en los nodos raíz, que podían saturarse bajo cargas de comunicación intensivas.