

# **El Ciclo de Compilación y Ejecución de Aplicaciones Java desde la Línea de Comandos**

## **SECCIÓN I: Introducción y Fundamentos**

# **1: El Ciclo de Vida del Desarrollo Java** 

El desarrollo de software en Java se distingue fundamentalmente por su aproximación a la compilación, que se aparta del modelo de traducción directa a código máquina nativo. Este sistema fue diseñado para cumplir con el paradigma "Write Once, Run Anywhere" (Escribe una vez, ejecuta en cualquier lugar), lo que requiere una etapa intermedia crítica: la generación de *Bytecode*.1

Este informe técnico detalla el flujo de trabajo manual y fundamental para compilar y ejecutar código Java utilizando las herramientas del kit de desarrollo (JDK) directamente desde la terminal del sistema operativo, enfocándose en la operación de los comandos esenciales: javac y java. Comprender esta interacción es vital, ya que es la base arquitectónica sobre la que operan todos los entornos de desarrollo integrado (IDEs) modernos, proporcionando una comprensión profunda de cómo el código fuente se convierte en un programa ejecutable.2

La clave de la portabilidad de Java reside en el desacoplamiento del código fuente respecto al hardware subyacente. El código se traduce primero a un formato intermedio, el *Bytecode*, el cual es interpretado y optimizado por la Máquina Virtual de Java (JVM).3 Este diseño permite que el mismo archivo compilado (

.class) se ejecute sin modificaciones en Windows, Linux o macOS, siempre que exista una implementación compatible de la JVM.

# **2: Componentes Clave del Ecosistema Java**

Para llevar a cabo el proceso de compilación y ejecución, es indispensable distinguir entre los tres componentes principales del ecosistema Java, todos provistos por Oracle o implementaciones Open Source (como OpenJDK).

El **JDK (Java Development Kit)** es el paquete completo para desarrolladores. Es el único componente que incluye el compilador (javac) y otras herramientas de depuración y desarrollo esenciales. Para poder compilar programas, el desarrollador debe tener instalado el JDK.5

El **JRE (Java Runtime Environment)** es el entorno de ejecución. Este paquete está diseñado únicamente para ejecutar aplicaciones Java ya compiladas. Si bien incluye la Máquina Virtual de Java (JVM) y las bibliotecas estándar necesarias para que un programa funcione, carece del compilador javac. Por lo tanto, el JRE es suficiente para los usuarios finales, pero insuficiente para este ejercicio de compilación manual.5

La **JVM (Java Virtual Machine)** es la capa de abstracción de *software* que reside en el sistema operativo y es responsable de cargar, verificar y ejecutar el *Bytecode* generado por el compilador.6 La JVM es la tecnología que garantiza la portabilidad de Java, ya que actúa como el intérprete universal del

*Bytecode* en cualquier plataforma.

# **3: Configuración del Entorno: PATH y Consola**

Antes de comenzar la compilación, se asume una condición necesaria para la operación fluida de los comandos de Java: la configuración de la variable de entorno PATH.

Para que los comandos javac y java puedan ser invocados desde cualquier directorio en la terminal (ya sea CMD en Windows o Terminal en Linux/macOS), la ruta del sistema debe incluir el directorio bin de la instalación del JDK. Si la variable PATH no está configurada correctamente, el sistema operativo responderá con un error indicando que el comando no fue encontrado.7

Todos los pasos prácticos que se presentarán a continuación presuponen que el usuario se encuentra posicionado en el directorio de trabajo donde reside el archivo fuente .java. Esto simplifica la sintaxis, ya que la herramienta javac buscará el archivo en el directorio actual.

## **SECCIÓN II: Paso 1 – Creación del Código Fuente**

# **4: Definición del Programa Java Mínimo Funcional**

El primer paso consiste en crear el código fuente. La regla fundamental en Java para un archivo que contiene la clase principal es que el nombre del archivo fuente debe coincidir exactamente con el nombre de la clase pública que contiene el método de inicio (main), incluyendo la capitalización. Por lo tanto, si la clase se nombra ConsolaDemo, el archivo debe ser ConsolaDemo.java.9

Se emplea un ejemplo mínimo funcional, a menudo referido como "Hola Mundo", para enfocar la demostración en el proceso de compilación/ejecución y no en la complejidad de la lógica interna.10

Java

// Archivo: ConsolaDemo.java  
public class ConsolaDemo {  
    /\*\*  
     \* Punto de entrada principal para la Máquina Virtual de Java (JVM).  
     \* Imprime un mensaje de bienvenida en la salida estándar (consola).  
     \*/  
    public static void main(String args) {  
        System.out.println("--- EJECUCIÓN EXITOSA DESDE CONSOLA \---");  
        System.out.println("Compilación y Ejecución Manual de Java");  
    }  
}

# **El Contrato del Método main**

El método main es el punto de entrada obligatorio que la JVM busca al iniciar la ejecución de una aplicación Java.9 Su sintaxis específica actúa como un contrato que garantiza que la JVM pueda invocarlo correctamente. La sintaxis tradicional y completa es

public static void main(String args).11

#### **Análisis Técnico de la Sintaxis**

La presencia de modificadores específicos es crucial:

* **public:** Indica que el método es accesible desde cualquier lugar. Esto es un requisito de la JVM, que necesita invocar el método de inicio sin restricciones de acceso.  
* **static:** Significa que el método pertenece a la clase y no a una instancia específica de la misma. La JVM puede invocar main() sin la necesidad de instanciar un objeto de la clase ConsolaDemo, lo cual simplifica el proceso de arranque.  
* **void:** Señala que el método no devuelve ningún valor al sistema operativo después de su ejecución.  
* **String args:** Es un arreglo que permite al programa recibir argumentos de cadena pasados por el usuario directamente desde la línea de comandos en el momento de la ejecución.12

Aunque las versiones modernas de Java (Java 21+) han introducido características para simplificar el código inicial, permitiendo la omisión de la clase explícita, public, static y args 13, la comprensión del proceso de compilación y ejecución desde la consola requiere el uso y la comprensión de esta estructura completa y tradicional por razones de compatibilidad y arquitectura subyacente.

## **SECCIÓN III: Paso 2 – Compilación a Bytecode (javac)**

# **6: Invocación del Compilador Estándar (javac)**

El comando javac (Java Compiler) es la herramienta responsable de la primera fase del proceso de ejecución de Java: la traducción del código fuente legible por humanos al *Bytecode*. El compilador opera sobre el archivo fuente (.java), que está escrito en caracteres Unicode.

El Bytecode es una representación intermedia de las instrucciones del programa, diseñada para ser entendida por la JVM.2

La sintaxis básica para la compilación requiere especificar el nombre completo del archivo fuente, *incluyendo su extensión* .java.7

Bash

\# Comando de compilación  
$ javac ConsolaDemo.java

Si la compilación tiene éxito, es decir, si el código no contiene errores sintácticos o de tipado, el comando javac no producirá ninguna salida en la consola. Simplemente, devolverá el *prompt* del sistema, indicando que el proceso ha finalizado correctamente.8

# 

# **7: La Generación del Bytecode (Archivo .class)**

El resultado tangible de la ejecución exitosa de javac es la generación de uno o más archivos con la extensión .class en el mismo directorio (a menos que se especifique otra ubicación).7 Para el ejemplo anterior, se genera

ConsolaDemo.class.

El archivo .class contiene el *Bytecode* de Java. Este *Bytecode* es el lenguaje de máquina de la JVM y es inherentemente independiente de la plataforma.3

#### **Naturaleza del Bytecode**

* **Universalidad:** Es un formato binario que puede ser transportado y ejecutado en cualquier sistema que tenga una JVM compatible. Esta independencia de la arquitectura es el corazón de la portabilidad de Java.  
* **Compacidad:** El *Bytecode* es una forma de datos compacta; cada instrucción suele estar representada por un solo *byte*.3  
* **Ilegibilidad:** Si se intenta abrir el archivo .class con un editor de texto estándar, el contenido aparecerá como código "inentendible" debido a su naturaleza compilada y optimizada para la máquina virtual.14

# **8: Opciones Avanzadas de Compilación y classpath**

En entornos de desarrollo más complejos o cuando se utiliza código modularizado, la sintaxis simple de javac se extiende para manejar dependencias y paquetes.

#### **Manejo de Paquetes con \-d**

Si el código fuente pertenece a un paquete (por ejemplo, package com.ejemplo;), el archivo compilado .class debe residir en una estructura de directorios que refleje ese nombre de paquete. La opción \-d especifica el directorio de destino para los archivos de clase. Si se utiliza ., indica que la estructura de directorios debe crearse a partir del directorio actual.15

*Sintaxis con paquetes:*

Bash

$ javac \-d. com/ejemplo/ConsolaDemo.java

Esto genera automáticamente la carpeta com/ejemplo/ y coloca ConsolaDemo.class dentro de ella.6

#### **Dependencias de Librerías con \-cp o \-classpath**

Si el programa que se está compilando utiliza clases externas que ya han sido compiladas (típicamente en archivos JAR o en otros directorios), el compilador necesita saber dónde buscar estos recursos. Esto se especifica mediante las opciones \-cp o \-classpath.16

*Sintaxis con classpath:*

Bash

$ javac \-cp ruta/a/librerias ConsolaDemo.java

Esta opción dirige a javac a buscar dependencias en las ubicaciones especificadas antes de resolver las referencias dentro del archivo fuente.17

## **SECCIÓN IV: Paso 3 – Ejecución en la JVM (java)**

# **9: Invocación del Ejecutor (java)**

Una vez que el Bytecode (.class) ha sido generado, el siguiente paso es ejecutarlo utilizando el comando java. Este comando inicia la Máquina Virtual de Java (JVM) y delega en ella la carga y ejecución del código.

La invocación del comando java es una de las principales fuentes de errores sintácticos para los principiantes debido a un requisito crucial: se debe proporcionar **solo el nombre de la clase principal** que contiene el método main, y **se debe omitir la extensión** .class.5

Bash

\# Comando de ejecución correcto  
$ java ConsolaDemo

#### **La Importancia de Omitir la Extensión**

La omisión de la extensión .class no es una mera convención, sino un requisito funcional. Al proporcionar solo el nombre de la clase (ConsolaDemo), se activa el **Cargador de Clases** (Class Loader) de la JVM para buscar y cargar dinámicamente el archivo de clase binario. Si un desarrollador intenta ejecutar con la extensión: $ java ConsolaDemo.class, la JVM asume que está buscando una clase literal llamada ConsolaDemo.class, resultando en una falla como ClassNotFoundException.6 Esto subraya que la ejecución en Java se basa en la referencia al objeto de clase y no en la llamada directa al archivo binario del sistema.

# 

# 

# **10: Demostración Completa del Ciclo de Consola**

La siguiente simulación en la terminal ilustra el flujo secuencial completo, desde la existencia inicial del código fuente hasta la ejecución exitosa del Bytecode:

Bash

\# 1\. Verificar archivos iniciales (Solo ConsolaDemo.java existe)  
$ ls   
ConsolaDemo.java

\# 2\. Compilar el código fuente, generando Bytecode  
$ javac ConsolaDemo.java 

\# 3\. Verificar archivos post-compilación (Ahora ConsolaDemo.class existe)  
$ ls   
ConsolaDemo.java   ConsolaDemo.class

\# 4\. Ejecutar el Bytecode usando solo el nombre de la clase  
$ java ConsolaDemo   
\--- EJECUCIÓN EXITOSA DESDE CONSOLA \---  
Compilación y Ejecución Manual de Java

Al ejecutar el comando java ConsolaDemo, la JVM carga el archivo ConsolaDemo.class y comienza a procesar las instrucciones contenidas en el método main, resultando en la salida de texto en la consola.5

# **11: Ejecución de Clases con Paquetes**

Si la clase principal forma parte de un paquete, la ejecución se vuelve más rigurosa, exigiendo el uso del Nombre de Clase Completamente Calificado (Fully Qualified Class Name \- FQCN).

Si la clase ConsolaDemo está definida dentro del paquete com.ejemplo, el archivo ConsolaDemo.class residirá en la estructura de directorios com/ejemplo/. Para que la JVM pueda localizar la clase, la ejecución debe hacerse desde el directorio raíz del paquete, utilizando el FQCN.6

#### **Sintaxis de Consola con Uso de Paquetes**

| Acción | Propósito | Comando de Consola (Ej. com.ejemplo.Demo) | Notas Técnicas |
| :---- | :---- | :---- | :---- |
| **Compilación** | Generar el .class en la estructura de directorios correcta. | javac \-d. com/ejemplo/Demo.java | \-d. crea automáticamente la estructura de directorios com/ejemplo/. 15 |
| **Ejecución** | Iniciar la clase usando el nombre completo. | java com.ejemplo.Demo | Se requiere el Nombre de Clase Completamente Calificado (FQCN). 6 |

Intentar ejecutar un programa dentro de un paquete sin especificar el nombre completo resultará en un fallo, ya que la JVM no podrá encontrar la clase en el classpath predeterminado.6 Este requisito refuerza la comprensión de que la ejecución Java se basa en la jerarquía de nombres definida por los paquetes.

## **SECCIÓN V: Análisis Arquitectónico Profundo**

# **12: La Arquitectura de Ejecución de Dos Etapas**

La portabilidad de Java es el resultado directo de su arquitectura de ejecución de dos etapas, lo que lo diferencia de lenguajes que compilan directamente a código nativo específico de la máquina.1

1. **Etapa de Compilación (javac):** En esta etapa, el compilador del JDK (javac) traduce el código fuente (.java) a *Bytecode* universal (.class). El principal objetivo es verificar la corrección sintáctica y de tipos de Java. El *Bytecode* generado es una representación de instrucciones que no está acoplada a ninguna arquitectura de *hardware* en particular.  
2. **Etapa de Ejecución (java/JVM):** La Máquina Virtual de Java toma este *Bytecode* intermedio y lo procesa. Es durante esta etapa que el código se traduce o compila (mediante el Compilador JIT) en código máquina nativo específico para el sistema operativo y el CPU en uso.

Esta dualidad de compilación implica una separación clara: los errores de javac son estrictamente problemas sintácticos, mientras que los errores de java son problemas de entorno, tiempo de ejecución, o lógica interna. Esta arquitectura desacopla la creación del código de su ejecución, permitiendo que las compañías desplieguen un único archivo Bytecode en servidores que operan bajo diferentes sistemas operativos (Windows, Linux, AIX, etc.) sin necesidad de recompilaciones nativas para cada entorno.

# **13: Etapas Críticas Dentro de la JVM**

Una vez que se invoca el comando java, la Máquina Virtual de Java inicia un proceso secuencial y metódico antes de que el código del método main comience a ejecutarse. Este proceso interno es fundamental para garantizar la seguridad y la eficiencia de la aplicación.1

Etapas Internas de Ejecución en la JVM

| Etapa | Componente | Función Clave | Beneficio Arquitectónico |
| :---- | :---- | :---- | :---- |
| **1\. Carga** | Cargador de Clases | Localiza y lee el Bytecode (.class) en la memoria.1 | Gestión de dependencias y modularidad, crucial para entornos grandes. |
| **2\. Verificación** | Verificador de Bytecode | Asegura la integridad y validez estructural del código.4 | Seguridad fundamental, previene manipulación de la pila y accesos ilegales. |
| **3\. Ejecución** | Intérprete/JIT | Traduce o compila dinámicamente el Bytecode a código máquina nativo.3 | Portabilidad inmediata y optimización de rendimiento a largo plazo. |

# **14: La Seguridad por Diseño: Bytecode Verifier**

La portabilidad, que permite ejecutar código intermedio en cualquier máquina, podría introducir riesgos de seguridad si ese código intermedio pudiera ser manipulado maliciosamente después de la compilación inicial. El **Verificador de Bytecode** (Bytecode Verifier) es el mecanismo de defensa crucial que transforma esta potencial vulnerabilidad en una ventaja de seguridad central de Java.4

Cuando el Cargador de Clases introduce un archivo .class en la memoria de la JVM, el Verificador lo inspecciona instrucción por instrucción antes de que cualquier código se ejecute. Su propósito es asegurar que el *Bytecode* está bien formado y no viola las estrictas reglas de la máquina virtual. El Verificador comprueba aspectos como la ausencia de desbordamientos de pila, la gestión válida de punteros y la prohibición de conversiones de tipos de datos que puedan comprometer el sistema.4

Este control de integridad se realiza independientemente de dónde provenga el código (local o remoto) y es la razón arquitectónica fundamental por la que las aplicaciones Java han mantenido históricamente una reputación de robustez y seguridad en entornos empresariales. La validación ocurre como un paso preventivo antes de que el código pueda interactuar con la CPU a través del JIT.4

# **15: Optimización Dinámica: El Compilador JIT**

La ejecución de Java comienza a menudo con el intérprete de la JVM traduciendo el *Bytecode* línea por línea, lo que es inherentemente más lento que la ejecución de código nativo. Sin embargo, para mejorar el rendimiento, la JVM emplea el Compilador Just-In-Time (JIT).

El JIT observa el comportamiento de la aplicación en tiempo de ejecución. Si un método o bloque de código se invoca repetidamente, se clasifica como "código caliente" (hot code). En ese momento, el JIT entra en acción. El JIT toma ese *Bytecode* de alto uso y lo compila directamente a código máquina nativo específico para el *hardware* de la máquina actual (por ejemplo, instrucciones x86 o ARM).3

El código compilado por el JIT se almacena en la memoria y se ejecuta directamente en llamadas futuras. Este proceso dinámico y selectivo asegura que, con el tiempo, las partes más críticas y usadas de una aplicación Java alcancen una velocidad de ejecución comparable a la de las aplicaciones compiladas nativamente.3 La compilación JIT es una forma de compensar el sobrecosto inicial de la interpretación y asegurar la eficiencia en programas de larga ejecución.

## **SECCIÓN VI: Conclusión y Solución de Problemas**

# 

# 

# **16: Resumen de Errores Comunes en Consola**

Trabajar directamente en la consola expone al desarrollador a errores de configuración y sintaxis que son gestionados automáticamente por los IDEs. Los dos errores más comunes ilustran la diferencia fundamental entre el entorno del compilador (javac) y el entorno de ejecución (java).

#### **Error 1: Fallo en la Invocación del Compilador**

Síntoma: El sistema responde con mensajes como javac: command not found o Error: file not found.  
Causa: La causa principal es la falta de configuración del directorio bin del JDK en la variable de entorno PATH, lo que impide que el sistema operativo localice el ejecutable del compilador. Alternativamente, puede ser que el nombre del archivo fuente, incluyendo la extensión, haya sido escrito incorrectamente.8

Solución: Verificar que la variable PATH apunte correctamente al JDK o asegurar que se usa la sintaxis correcta: javac MiClase.java.

#### **Error 2: ClassNotFoundException en Ejecución**

Síntoma: La JVM reporta que no puede encontrar la clase principal.  
Causa Principal: Este es el error más recurrente y generalmente se debe a una de las siguientes: (A) Intentar ejecutar incluyendo la extensión, por ejemplo, java MiClase.class. (B) Estar posicionado en un directorio incorrecto que no está en el classpath de la JVM. (C) No haber utilizado el Nombre de Clase Completamente Calificado (FQCN) si la clase pertenece a un paquete.6

Solución: La solución más inmediata es asegurarse de que la ejecución se realice sin la extensión: java MiClase. Para entornos con paquetes, se debe usar java com.paquete.MiClase.5

# **17: Comparativa de Comandos y Extensiones (Tabla de Referencia)**

Para evitar la confusión de los principiantes, la siguiente tabla sintetiza la entrada esperada por cada uno de los comandos clave, que operan en fases distintas del ciclo de vida del programa Java. La confusión entre si se debe usar el nombre del archivo fuente (.java) o el objeto de clase compilada (sin extensión) es la fuente principal de errores de sintaxis en la consola.

Tabla de Referencia Rápida para Comandos Java

| Comando | Función Principal | Entrada Requerida | Manejo de Extensión | Salida Generada/Acción |
| :---- | :---- | :---- | :---- | :---- |
| javac | Compilador (Crea Bytecode) | Nombre del archivo **fuente** | **Obligatorio** (.java) | Genera Bytecode (.class) |
| java | Ejecutor (Inicia la JVM) | Nombre de la **clase** principal | **Prohibida** (No usar .class) | Carga el Bytecode y ejecuta main() |

Este resumen muestra que javac requiere una referencia al archivo físico de texto fuente, mientras que java requiere una referencia al objeto lógico de clase cargable, lo que explica la diferencia en la sintaxis de la extensión.5

# **18: Resumen Arquitectónico del Proceso Java (Cierre)**

El ciclo de desarrollo y ejecución de Java se estructura en cuatro fases interdependientes:

1. **Fase 1: Escritura:** Creación del código fuente legible y estructurado (.java), respetando la convención de que el nombre del archivo coincide con el nombre de la clase principal.  
2. **Fase 2: Compilación (javac):** Transformación del código fuente en *Bytecode* universal e independiente de la plataforma (.class).  
3. **Fase 3: Carga y Verificación (java):** La JVM utiliza el Cargador de Clases para traer el Bytecode a la memoria. El Verificador de Bytecode garantiza la seguridad y la integridad del código, un paso de defensa crucial antes de cualquier ejecución nativa.  
4. **Fase 4: Ejecución y Optimización:** La JVM interpreta el Bytecode y, simultáneamente, el Compilador JIT identifica y compila dinámicamente el código más utilizado en instrucciones de máquina nativas específicas, garantizando un alto rendimiento a largo plazo.

La robustez y la portabilidad de Java no son accidentes sintácticos, sino consecuencias directas de la capa intermedia que proporciona la Máquina Virtual de Java. Esta arquitectura asegura una separación efectiva entre la plataforma de desarrollo y la plataforma de despliegue, combinando seguridad (verificador) y rendimiento dinámico (JIT).
