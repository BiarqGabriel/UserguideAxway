# Axway Mapping Services 3.6 DML — User Guide

> **Versión:** 3.6 UP2026-03  
> **Producto relacionado:** Axway B2Bi 2.6 UP2026-03  
> **Tipo:** On-Premises  
> **Última actualización:** Marzo 2026  
> **Documentación oficial:** [docs.axway.com](https://docs.axway.com/bundle/MappingServices_36_UsersGuide_DML_allOS_en_HTML5/page/Content/AxwayStartPage_DML_UG.htm)

---

## Tabla de Contenidos

1. [¿Qué es Axway Mapping Services?](#qué-es-axway-mapping-services)
2. [Lenguaje DML](#lenguaje-dml)
3. [Ciclo de Vida de un Mapping](#ciclo-de-vida-de-un-mapping)
4. [DML Mapping Projects](#dml-mapping-projects)
   - [Componentes del Proyecto](#componentes-del-proyecto)
   - [Estructura de Directorios](#estructura-de-directorios)
   - [Versiones DML](#versiones-dml)
5. [Business Documents](#business-documents)
   - [Tipos de Business Documents](#tipos-de-business-documents)
   - [Estructura y Cardinalidad](#estructura-y-cardinalidad)
   - [Validación y Codificación](#validación-y-codificación)
6. [Maps](#maps)
   - [Editor de Maps](#editor-de-maps)
   - [Tipos de Maps](#tipos-de-maps)
7. [Mapping Flows](#mapping-flows)
   - [Elementos de un Mapping Flow](#elementos-de-un-mapping-flow)
   - [Canales en Mapping Flows](#canales-en-mapping-flows)
8. [Extended Objects](#extended-objects)
   - [Custom Functions](#custom-functions)
   - [Tables](#tables)
   - [Variables](#variables)
   - [Global Runtime Objects](#global-runtime-objects)
9. [Simulación de Mappings](#simulación-de-mappings)
   - [Test Cases](#test-cases)
   - [Simulation Suite](#simulation-suite)
10. [Documentación de Objetos](#documentación-de-objetos)
11. [Despliegue de Mappings](#despliegue-de-mappings)
    - [Métodos de Despliegue](#métodos-de-despliegue)
    - [Object Dependency Browser](#object-dependency-browser)
12. [Control de Versiones](#control-de-versiones)
13. [Meta Data](#meta-data)
14. [Referencia del Lenguaje DML](#referencia-del-lenguaje-dml)
    - [Expresiones DML](#expresiones-dml)
    - [Sintaxis y Uso](#sintaxis-y-uso)
    - [Funciones DML](#funciones-dml)
15. [Preferencias DML](#preferencias-dml)
16. [Soporte y Recursos Adicionales](#soporte-y-recursos-adicionales)

---

## ¿Qué es Axway Mapping Services?

Axway Mapping Services es una **Rich Client Application (RCA)** construida sobre el framework **Eclipse**. Es una suite de desarrollo de mappings (mapeos) autónoma que permite:

- Diseñar, simular, documentar y versionar Mappings de datos empresariales.
- Desplegar Mappings en un servidor Axway de tiempo de ejecución (runtime).
- Transformar datos de cualquier formato de origen a cualquier formato de destino (**Any2Any**).

Un **Mapping**, en el contexto de la integración de aplicaciones empresariales (EAI), es una estructura para procesar los datos o metadatos asociados a los mensajes que transitan por la red.

### Características principales

| Característica | Descripción |
|---|---|
| Desarrollo offline | Permite desarrollo y simulación de DML Mappings sin conexión al servidor |
| Desarrollo gráfico | Interfaz gráfica para el desarrollo de Mappings |
| Estándares EDI y XML | Soporte para EDIFACT, X12, XSD, SAP, HL7, SWIFT y más |
| Database & Web Services | Capacidad de mapear hacia y desde bases de datos y servicios web |
| Any2Any Mapping | Transformación entre cualquier par de formatos |

### Lenguajes de Mapping soportados

Mapping Services proporciona dos lenguajes de mapping:

- **DML (Data Manipulation Language):** Lenguaje propietario de Axway, de muy alto nivel, orientado a la generación de valores a partir de datos de entrada.
- **Datamapper:** Lenguaje alternativo de mapping gráfico.

---

## Lenguaje DML

DML (Data Manipulation Language) es el **lenguaje de programación y mapping propietario de Axway** que instruye al motor de integración sobre cómo generar un valor a partir de datos de entrada.

### Características de DML

- **Lenguaje de muy alto nivel:** El negocio genera datos sin necesidad de entender los procesos técnicos subyacentes.
- **No es un lenguaje de programación completo:** No se preocupa de bits, bytes ni asignación de memoria.
- **Maneja todos los tipos de datos comunes** independientemente de su codificación técnica: números, fechas y textos.
- **Motor de mapeado:** El Motor de Maps (Map Engine) utiliza instrucciones DML para transformar Business Documents de entrada en Business Documents de salida.

### Usos del DML

| Contexto | Uso de DML |
|---|---|
| Business Document | **Validation Rule:** Expresión booleana para verificar el contenido de un Business Document recibido o enviado por un Canal |
| DML Block Map | **Decision Path:** Condiciones bajo las cuales el servidor de integración mapea y enruta un Business Document |
| Map | **Instrucciones de transformación:** Instrucciones que el servidor de integración usa para transformar y mapear un Business Document de entrada a uno de salida |

---

## Ciclo de Vida de un Mapping

El siguiente diagrama resume los pasos necesarios para crear, probar y desplegar un DML Mapping:

```
1. Crear DML Mapping Project
        ↓
2. Crear Business Documents (entrada y salida)
        ↓
3. Crear Maps (definir transformaciones)
        ↓
4. Crear Mapping Flows (orquestar el routing y mapping)
        ↓
5. Crear Test Cases (datos de prueba)
        ↓
6. Configurar y lanzar Simulaciones
        ↓
7. Documentar objetos DML Mapping
        ↓
8. Desplegar DML Mappings al servidor runtime
```

### Descripción de cada paso

1. **Crear DML Mapping Project:** El punto de entrada principal para cada Mapping Project es el archivo `project.ms`.
2. **Crear Business Documents:** Crear o importar Business Documents que contienen los datos de mensajes de entrada y salida. Estos son los objetos de entrada y salida de los Mapping Flows.
3. **Crear Maps:** Definir cómo los objetos de entrada se mapean a los objetos de salida.
4. **Crear Mapping Flows:** Basándose en los Business Documents y Maps creados, los Mapping Flows contienen instrucciones específicas sobre cómo enrutar, mapear y manejar los datos de entrada.
5. **Crear Test Cases:** Crear casos de prueba y datos de prueba para validar el Mapping.
6. **Configurar y lanzar Simulaciones:** Probar el DML Mapping Project con una simulación o una suite de simulación.
7. **Documentar objetos:** Crear documentación para el DML Mapping Project.
8. **Desplegar Mappings:** Finalmente, completar el DML Mapping Project y desplegar el Mapping en el servidor runtime.

---

## DML Mapping Projects

Un **DML Mapping Project** es un proyecto Eclipse estándar con una estructura de directorios predeterminada. Un Mapping Project combina todos los archivos necesarios para crear, diseñar y modificar uno o más Mappings.

- Un mismo Mapping Project puede contener **múltiples Mappings**.
- Todos los Mappings dentro del mismo proyecto pueden usar los mismos recursos (Tables, Custom Functions, etc.).
- Los recursos que deben reutilizarse en múltiples Mappings en el servidor runtime deben ubicarse en el **Global Runtime Objects**.

### Componentes del Proyecto

Un DML Mapping Project puede contener los siguientes componentes:

| Componente | Descripción |
|---|---|
| Business Documents | Descripciones de mensajes de origen y destino |
| Maps | Definen la transformación del documento fuente al documento destino |
| Mapping Flows | Describen cómo se orquesta un Mapping |
| Variables | Objetos que almacenan y pasan valores |
| Tables | Contienen datos para usar en el procesamiento de mensajes |
| Functions | Funciones personalizadas (Custom Functions) |
| Test data | Mensajes de prueba (EDI, XML, etc.) y la suite de simulación |
| Configurations | Configuraciones para la simulación |
| Documentation | Documentación del proyecto |

### Estructura de Directorios

La estructura de directorios es generada automáticamente al crear un nuevo Mapping Project:

```
<NombreProyecto>/
├── project.ms              ← Archivo principal del proyecto (entry point)
├── Business Documents/     ← Descripciones de mensajes fuente y destino
├── Documentation/          ← Documentaciones de Mapping
├── Extended Objects/       ← Custom Functions, Tables, Variables
│   ├── Functions/
│   ├── Tables/
│   └── Variables/
├── Mapping Flows/          ← Flujos de orquestación del Mapping
├── Maps/                   ← Especificaciones de transformación (.mdm)
└── Testdata/               ← Mensajes de prueba y suites de simulación
```

### Archivo de Proyecto (`project.ms`)

El archivo `project.ms` es el **punto de entrada principal** de cada Mapping Project:

- Define el **lenguaje de mapping** y la **versión** para todos los Mappings del proyecto.
- Puede contener **Meta Data** adicional sobre los Mappings.
- Proporciona operaciones de documentación, despliegue y versionado.

### Versiones DML

Un DML Mapping Project puede ser designado como **DML 1.5**, **2.0** o **2.1**.

> Todos los proyectos nuevos se crean como **DML 2.0 o superior**.

#### Diferencias entre DML 2.0 y DML 1.5

| Aspecto | DML 1.5 | DML 2.0 |
|---|---|---|
| Justificación (Justification) | Algunas configuraciones eran ignoradas | El atributo Justification tiene el efecto esperado |
| Variable Length Output Fields | Comportamiento inconsistente con decimales | Padding con ceros hasta coincidir con la definición del campo |
| `Pad reals with leading/trailing zero` | Dependía del valor de `CORE_DECIMAL_POINT_NOT_MANDATORY` | Funciona independientemente del entorno variable |
| Mínima longitud para Integer | No verificada | Verificada para campos variables |

#### Diferencias entre DML 2.1 y DML 2.0

| Aspecto | DML 2.0 | DML 2.1 |
|---|---|---|
| Precisión y escala para XML | No interpretada de forma consistente | Tomadas en cuenta; error si los valores no coinciden |
| Namespaces extra en XSD | Mantenidos | Eliminados en la generación |
| Short real numbers | Sin advertencia | Genera advertencia si `facet check` está habilitado junto con `accept document with error` |

#### Cambiar la versión DML

1. Hacer doble clic en el archivo de proyecto en el Project Explorer.
2. En la lista **Project Properties**, hacer clic en **Mapping Details**.
3. Seleccionar la versión en el menú desplegable **Version** (1.5 o 2.0).
4. Guardar los cambios.

La versión se muestra como etiqueta en el archivo `project.ms`, por ejemplo: `[DML-2.0]`.

#### Efectos de la versión en importación/exportación

- **Importar un proyecto anterior** establece la versión a 1.5.
- **Exportar un paquete de despliegue** mantiene la versión existente del proyecto (1.5 o 2.0).
- **Importar un paquete de despliegue previamente desplegado** establece la versión a 1.5 incluso si algunos objetos estaban en 2.0 (se emite una advertencia).

> **Nota:** Document Identifier no está soportado en B2Bi.

---

## Business Documents

Un **Business Document** describe la composición y estructura de los mensajes de entrada y salida para los Mappings. En Mapping Services, la estructura para contener datos de mensajes es un Business Document.

### Roles de los Business Documents

| Rol | Descripción |
|---|---|
| **Input** | El Map Engine extrae los datos del mensaje de entrada y los escribe en el nodo apropiado del Business Document de entrada |
| **Output** | El Map Engine usa instrucciones en los Maps para procesar los datos del BD de entrada y escribe los resultados en los nodos del BD de salida |
| **Output/Input** | En ciertos contextos, un BD puede servir como salida de un Map y como entrada del siguiente Map en el mismo Mapping Flow |

### Tipos de Business Documents

Mapping Services DML soporta los siguientes tipos de Business Documents:

| Tipo | Descripción |
|---|---|
| **HL7** | Estándar de mensajería para el sector sanitario (Health Level 7) |
| **Flat File** | Archivos de texto plano con formato fijo o delimitado |
| **COBOL** (Fixed/Variable) | Estructuras de datos COBOL de longitud fija o variable |
| **Tracked Objects** | Objetos para tracking en Axway Sentinel |
| **Cargo IMP** | Estándar para la industria del transporte aéreo de carga |
| **SCRIPT** | Formato para prescripciones electrónicas |
| **EDIFACT** | Estándar EDI de las Naciones Unidas (UN/EDIFACT) |
| **ANSI X12** | Estándar EDI norteamericano |
| **TRADACOMS** | Estándar EDI del sector retail británico |
| **IDoc** | Intermediate Document de SAP |
| **SWIFT FIN** (System/User) | Estándar de mensajería financiera interbancaria |
| **XML** | Documentos XML genéricos |
| **XSD** | XML Schema Definition |
| **JSON** | JavaScript Object Notation |
| **JDBC Database** | Documentos basados en consultas de base de datos via JDBC |
| **Generic** | Business Document genérico configurable |

### Estructura y Cardinalidad

La estructura de un Business Document define la jerarquía de nodos (grupos, segmentos, campos) y su cardinalidad (mínimo/máximo de ocurrencias).

### Validación y Codificación

- **Validation Rules:** Expresiones DML booleanas que el servidor de integración usa para verificar el contenido de un Business Document en recepción/envío.
- **Data Encoding:** Configuración de la codificación de caracteres del Business Document.
- **UML View:** Vista UML de la estructura del Business Document.
- **Business Document Libraries:** Repositorio de Business Documents reutilizables (incluyendo estándares como EDIFACT, X12, SAP).

---

## Maps

Los **Maps** son las **unidades centrales de procesamiento** de las aplicaciones de integración. Cada Map recibe información de uno o más Business Documents de entrada y genera información hacia un Business Document de salida.

Un Map es una **especificación de diseño**: especifica qué campos o registros de un mensaje fuente se copian (y si es necesario, se manipulan) al Business Document destino.

- Los Maps tienen la extensión de archivo `.mdm`.
- Un Map pertenece y está contenido en un Mapping Flow.

### Tipos de entrada/salida de un Map

| Tipo | Descripción |
|---|---|
| **Input Business Document** | Un Map puede tener un único BD de entrada o ninguno. Los datos del BD de entrada se mapean directamente o se transforman antes de escribirse al BD de salida. |
| **Output Business Document** | Cada Map está vinculado a un BD de salida. Los Maps son conjuntos de expresiones que generan valores para los nodos de este BD. |

### Editor de Maps

El editor de Maps proporciona una vista visual del mapeo entre el documento fuente y el destino, con posibilidad de:
- Crear mapeos directos entre campos (drag & drop).
- Ingresar expresiones DML para transformar valores.
- Visualizar estructuras de Business Documents de entrada y salida de forma simultánea.

### Tipos de Maps

| Tipo | Descripción |
|---|---|
| **DML Map** | Map estándar usando el lenguaje DML para transformaciones |
| **Auto-generated Map** | Mapeo generado automáticamente a partir de Business Documents |
| **Database Map** | Map orientado a consultar/escribir en bases de datos via JDBC |
| **Web Services Map** | Map para invocar o exponer servicios web (SOAP/WSDL) |
| **SAP Map** | Map específico para integración con SAP (IDocs, BAPIs, RFCs) |

---

## Mapping Flows

Los **Mapping Flows** son objetos de mapping que contienen instrucciones específicas sobre cómo enrutar, mapear o manejar unidades de datos de entrada.

### Elementos de un Mapping Flow

Un Mapping Flow típicamente contiene:

| Elemento | Descripción |
|---|---|
| **Input Object** | Objeto de entrada del flujo |
| **Output Objects** | Uno o más objetos de salida |
| **Block Container** | Contenedor para realizar el mapeo de contenido del mensaje o el routing |
| **Business Documents** | BDs para contener los datos de mensajes de entrada y salida |
| **Events** | Para detectar errores de contenido y de parsing |

### Formas de Crear un Mapping Flow

1. **Usando el wizard específico** de creación de Mapping Flows.
2. **Generando** un Mapping Flow desde un Business Document o Map.
3. **Generando** al crear un Mapping XML to EDIFACT.
4. **Importando** un Mapping Flow existente desde un paquete de despliegue.

### Canales en Mapping Flows

Los **canales** definen los modos de transporte y los parámetros de conexión para el envío/recepción de mensajes. Se pueden configurar canales de entrada y salida para utilizar durante la simulación.

### Propiedades de un Mapping Flow

- **Input/Output channels:** Canales de transporte configurados.
- **Concatenation and splitting:** Gestión de la concatenación y división de mensajes.
- Soporte para **Map Engine Validation Rules** para controlar el comportamiento de validación en el Motor de Maps.

---

## Extended Objects

El **DML Mapping Project** proporciona la carpeta **Extended Objects** para alojar tres tipos de objetos reutilizables:

### Custom Functions

Las Custom Functions permiten **extender el conjunto estándar de funciones DML** disponibles en Mapping Services.

- Se pueden añadir funciones personalizadas implementadas en Java.
- Ejemplo incluido: `com.axway.integrator.samples.customFunction.SAPUpdateIdocStatus` — Envía el estado de un IDoc a SAP.
- Una vez creadas, las Custom Functions están disponibles en el editor de Maps como cualquier otra función DML.

### Tables

Las **Tables** son objetos de Mapping Services que **contienen datos para usar en el procesamiento de mensajes**.

- Se pueden usar como tablas de traducción/lookup de valores.
- Soportan parámetros estáticos y dinámicos.
- Las funciones DML de acceso a Tables incluyen: `returnColumn`, `returnColumnInPeriod`, `isKeyPresent`, `isKeyPresentInPeriod`.

### Variables

Las **Variables** son objetos de Mapping Services que **almacenan y pasan valores** durante el procesamiento.

- Permiten mantener estados intermedios durante el procesamiento de un Mapping.
- Pueden ser usadas en expresiones DML dentro de Maps y Mapping Flows.
- Útiles para acumulación de valores, contadores y transferencia de datos entre Maps en un Mapping Flow.

### Global Runtime Objects

El **Global Runtime Objects** es un proyecto especial creado automáticamente que:

- Contiene recursos (Tables, Custom Functions, Variables) **compartidos entre múltiples Mapping Projects** en el servidor runtime.
- Es creado automáticamente por defecto al crear un Mapping Project.
- **Importante:** Modificar un Global Runtime Object puede afectar a cientos de Mappings en el servidor. Se debe definir un proceso preciso para su despliegue en equipo.

---

## Simulación de Mappings

Después de diseñar un DML Mapping, el siguiente paso es verificar que funciona correctamente. Mapping Services proporciona **funcionalidad de simulación** que permite probar Mappings antes del despliegue.

- Se pueden probar **mensajes individuales** o **conjuntos de mensajes**.
- Soporta **simulación estándar** y **suites de simulación** (para facilitar regresiones).

### Test Cases

Los **Test Cases** son casos de prueba que contienen:
- **Test data:** Archivos de mensajes de prueba (EDI, XML, flat files, etc.).
- **Configuración de simulación:** Definición de canales de entrada/salida, atributos, etc.

#### Crear un Test Case

1. En el Project Explorer, abrir el Mapping Project.
2. Crear mensajes de prueba representativos.
3. Configurar el Test Case con los parámetros de simulación.
4. Asociar el Test Case al Mapping Flow que se desea probar.

### Simulation Suite

La **Simulation Suite** facilita la ejecución de múltiples casos de prueba de forma automatizada, ideal para **pruebas de regresión**.

- Permite agrupar múltiples Test Cases.
- Se puede configurar para ejecutar en lote.
- Genera informes de resultados de simulación.

### Uso de Canales y Atributos en Simulación

- **Canales en simulación:** Se pueden configurar canales de entrada/salida simulados para probar el comportamiento con diferentes protocolos de transporte.
- **Atributos en simulación:** Se pueden definir atributos de mensaje para probar el comportamiento del Mapping bajo distintas condiciones.

---

## Documentación de Objetos

Mapping Services permite generar documentación automática para los objetos del DML Mapping Project.

- La documentación puede incluir información de todos los objetos del proyecto: Business Documents, Maps, Mapping Flows, etc.
- La **Meta Data** del proyecto puede ser incluida en la documentación generada.
- La documentación es generada directamente desde el Project Information editor.

---

## Despliegue de Mappings

El despliegue hace que los DML Mappings estén **disponibles en los servidores runtime**. El servidor runtime de Axway B2Bi está soportado.

### Proceso de Despliegue

Mapping Services proporciona un **export wizard** donde se puede:

1. Seleccionar el target (destino) de despliegue.
2. Definir opciones de despliegue.
3. Los Mappings son **empaquetados, transferidos y compilados** automáticamente.

El despliegue se puede ejecutar también en **modo background**, liberando la vista de edición para continuar trabajando.

### Métodos de Despliegue

| Método | Descripción |
|---|---|
| **Despliegue al file system** | Exporta el Mapping al sistema de ficheros local; el paquete de despliegue generado debe instalarse en el servidor runtime mediante línea de comandos |
| **Despliegue directo al runtime** | Despliega el paquete de despliegue directamente al servidor runtime desde Mapping Services sin intervención manual adicional |

### Tipos de Despliegue

| Tipo | Descripción |
|---|---|
| **Deploy Mappings** | Despliegue estándar de Mappings al runtime |
| **Deploy and Share Mapping Objects** | Despliegue y compartición de objetos entre proyectos |
| **Deploy XSD Business Documents to B2Bi** | Despliegue específico de BDs tipo XSD al servidor B2Bi |
| **Deploy Tracked Object Business Documents** | Despliegue de BDs de tipo Tracked Objects (para Sentinel) |

### Object Dependency Browser

Herramienta que proporciona **visibilidad sobre las dependencias entre recursos**. Antes de desplegar, se recomienda revisar las dependencias:

- Si los recursos tienen dependencias con otros recursos, **todos o ninguno** deben seleccionarse para el despliegue.
- Se accede desde el Project Information editor.

### Runtime Repository Browser

Permite **explorar el repositorio del servidor runtime** directamente desde Mapping Services, facilitando la gestión de los Mappings desplegados.

### Sentinel Repository Browser

Permite **explorar el repositorio de Axway Sentinel** para gestionar los Tracked Objects desplegados y su integración con el sistema de monitoreo.

### Consideraciones sobre Global Runtime Objects

- Los Global Runtime Objects son compartidos entre múltiples Mappings tras el despliegue.
- Es fundamental definir en equipo **un proceso claro** de cuándo y cómo desplegar Global Runtime Objects modificados.
- Un único Global Runtime Object puede afectar a **cientos de Mappings** en el servidor runtime.

---

## Control de Versiones

Para versionar el trabajo, Mapping Services proporciona **funcionalidad de versionado basada en SVN (Apache Subversion)**.

- Simplifica el enfoque SVN y proporciona **funcionalidad de trabajo en equipo**.
- Mantiene los Mappings siempre en un **estado válido**.
- Introduce el concepto de **recursos globales** para compartir objetos entre proyectos.

### Conceptos Clave de Versionado

| Concepto | Descripción |
|---|---|
| **SVN Integration** | Uso de SVN como sistema de control de versiones subyacente |
| **Shared Resources** | Recursos compartidos entre proyectos y equipos |
| **Global Runtime Projects** | Proyectos con gestión de versiones para recursos globales |
| **Shared Object Usage and Deployment** | Concepto para el uso compartido y despliegue de objetos entre equipos globales |

### Global Runtime Projects con Version Management

Especialmente importante para el trabajo en Mapping Projects en equipos distribuidos globalmente, es el concepto de **Shared object usage and deployment**, que describe mejores prácticas para la gestión y compartición de recursos en entornos multinacional.

---

## Meta Data

El concepto de **Meta Data** permite definir y almacenar **información adicional sobre el Mapping Project** dentro del propio proyecto.

### Ejemplos de Meta Data

- Descripción breve del formato fuente y destino.
- Nombre y datos de contacto del autor.
- Fecha de creación.
- Cualquier información definida por el usuario.

### Beneficios de Meta Data

- **Búsqueda y filtrado:** Facilita encontrar Mapping Projects en entornos con gran número de Mappings.
- **Repositorio central:** Funciona en workspace local o en SVN, enriqueciendo el repositorio con búsqueda y filtrado personalizable para todo el equipo.
- **Agrupación:** Permite filtrar y agrupar Mappings basándose en criterios específicos.
- **Documentación:** Se puede incluir en la documentación generada del proyecto.

### Niveles de Meta Data

Los Meta Data Configurations se pueden asignar en distintos niveles dentro del Project Information:

| Nivel | Descripción |
|---|---|
| **Project Details** | Meta Data para todo el Mapping Project |
| **Mapping Details** | Meta Data para todos los Mappings del proyecto |
| **Document Identifier** | Meta Data para Document Identifiers (solo DML Mapping Projects) |

### Meta Data Configurations

Las **Meta Data Configurations** definen genéricamente la estructura de los Meta Data usados en un Mapping:

- Se definen una vez y se asignan a proyectos.
- Se pueden **exportar** para compartir entre equipos.
- Se pueden **editar y gestionar** centralmente.
- Se integran con el **Version Management** del proyecto.

---

## Referencia del Lenguaje DML

### Expresiones DML

Una **expresión DML** es una instrucción individual para el Map Engine. Las expresiones DML se utilizan para:

| Contexto | Uso |
|---|---|
| Business Document | **Validation Rule:** Expresión booleana para validar el contenido de un BD |
| DML Block Map | **Decision Path:** Condiciones de enrutamiento |
| Map | **Instrucciones de transformación** del BD de entrada al BD de salida |

### Sintaxis y Uso

La referencia de sintaxis DML cubre los siguientes aspectos:

| Sección | Descripción |
|---|---|
| **Business Document Paths** | Sintaxis para referenciar nodos de un BD en expresiones DML (por ejemplo, `InputBDoc/Segmento/Campo`) |
| **Case Sensitivity** | DML es **case-insensitive** para nombres de funciones, pero **case-sensitive** para nombres de campos y objetos |
| **Comments** | Sintaxis para comentar código (`/* comentario */`) |
| **Constants** | Definición y uso de constantes literales (strings, números, fechas) |
| **Data Class** | Tipos de datos soportados: string, integer, real, date, datetime, binary |
| **Null and Absent** | Manejo especial de valores `null` (campo existe pero sin valor) y `absent` (campo no existe en el mensaje) |
| **Instructions** | Instrucciones de control de flujo y asignación |
| **Message Attributes** | Atributos del mensaje de transporte accesibles desde DML |
| **Operators** | Operadores aritméticos, de comparación y lógicos disponibles |
| **Reserved Words** | Palabras reservadas y caracteres especiales del lenguaje |
| **Usage Limits** | Limitaciones de uso (longitud máxima de expresiones, profundidad de anidamiento, etc.) |

### Tipos de Datos (Data Class)

| Tipo | Descripción |
|---|---|
| `String` (V) | Cadena de texto de longitud variable |
| `Integer` (I) | Número entero |
| `Real` (R) | Número real (decimal) |
| `Date` (D) | Valor de fecha |
| `DateTime` | Valor de fecha y hora |
| `Binary` (B) | Datos binarios |

### Funciones DML

Mapping Services incluye un catálogo extenso de funciones DML agrupadas por categorías:

#### Funciones de Fecha y Hora

| Función | Descripción |
|---|---|
| `addDays(date, n)` | Añade `n` días a una fecha |
| `addSeconds(datetime, n)` | Añade `n` segundos a un datetime |
| `getDate()` | Obtiene la fecha actual del sistema |
| `getDateAndTime()` | Obtiene fecha y hora actual |
| `getDay(date)` | Obtiene el día del mes |
| `getMonth(date)` | Obtiene el número del mes |
| `getYear(date)` | Obtiene el año |
| `getHours(datetime)` | Obtiene las horas |
| `getMinutes(datetime)` | Obtiene los minutos |
| `getSeconds(datetime)` | Obtiene los segundos |
| `getUTC()` | Obtiene la fecha/hora actual en UTC |
| `dayOfWeek(date)` | Obtiene el día de la semana (1=Lunes) |
| `dayOfYear(date)` | Obtiene el día del año (1-365) |
| `nbDays(date1, date2)` | Calcula el número de días entre dos fechas |
| `nbSeconds(dt1, dt2)` | Calcula el número de segundos entre dos datetimes |
| `makeDateAndTime(date, time)` | Combina una fecha y una hora en un datetime |

#### Funciones Matemáticas

| Función | Descripción |
|---|---|
| `abs(n)` | Valor absoluto |
| `ceil(n)` | Redondeo hacia arriba (techo) |
| `floor(n)` | Redondeo hacia abajo (suelo) |
| `round(n, decimals)` | Redondeo al número de decimales especificado |
| `integerPortion(n)` | Parte entera de un número real |
| `decimalPortion(n)` | Parte decimal de un número real |
| `exponent(base, exp)` | Potenciación |
| `remainder(n, divisor)` | Módulo/resto de la división |

#### Funciones de Cadenas y Binarios

| Función | Descripción |
|---|---|
| `length(str)` | Longitud de una cadena |
| `extract(str, start, length)` | Extrae una subcadena |
| `getSubString(str, start, end)` | Obtiene una subcadena |
| `getStringLeft(str, n)` | Obtiene los primeros `n` caracteres |
| `getStringRight(str, n)` | Obtiene los últimos `n` caracteres |
| `index(str, searchStr)` | Posición de una subcadena en otra |
| `countString(str, searchStr)` | Cuenta ocurrencias de una subcadena |
| `toLower(str)` | Convierte a minúsculas |
| `toUpper(str)` | Convierte a mayúsculas |
| `trimString(str)` | Elimina espacios al inicio y final |
| `trimStringLeft(str)` | Elimina espacios al inicio |
| `trimStringRight(str)` | Elimina espacios al final |
| `padStringLeft(str, length, char)` | Rellena con caracteres por la izquierda |
| `padStringRight(str, length, char)` | Rellena con caracteres por la derecha |
| `replaceString(str, old, new)` | Reemplaza primera ocurrencia |
| `replaceStringAll(str, old, new)` | Reemplaza todas las ocurrencias |
| `convertStringToEncoding(str, encoding)` | Convierte la codificación de una cadena |
| `byteSize(binary)` | Tamaño en bytes de un valor binario |

#### Funciones de Conversión

| Función | Descripción |
|---|---|
| `convertToD(value)` | Convierte al tipo Date |
| `convertToI(value)` | Convierte al tipo Integer |
| `convertToR(value)` | Convierte al tipo Real |
| `convertToV(value)` | Convierte al tipo String (Variable) |

#### Funciones de Formateo

| Función | Descripción |
|---|---|
| `formatString_dates(date, format)` | Formatea una fecha según un patrón de formato |
| `formatString_integers(int, format)` | Formatea un entero según un patrón |
| `formatString_real(real, format)` | Formatea un número real según un patrón |

#### Funciones Estadísticas

| Función | Descripción |
|---|---|
| `sum(field)` | Suma de valores de un campo iterado |
| `average(field)` | Promedio de valores de un campo iterado |
| `count(field)` | Cuenta de instancias de un campo |
| `max(field)` | Valor máximo de un campo iterado |
| `min(field)` | Valor mínimo de un campo iterado |

#### Funciones Misceláneas

| Función | Descripción |
|---|---|
| `generateUniqueId()` | Genera un identificador único (UUID) |
| `isNull(value)` | Verifica si el valor es null |
| `isAbsent(field)` | Verifica si el campo es absent (no existe en el mensaje) |
| `isNullOrAbsent(field)` | Combina verificación de null y absent |
| `replaceIfNull(value, default)` | Retorna `default` si `value` es null |
| `replaceIfAbsent(field, default)` | Retorna `default` si el campo es absent |
| `replaceIfNullOrAbsent(field, default)` | Retorna `default` si es null o absent |
| `isObjectAvailableOnServer(objectName)` | Verifica si un objeto está disponible en el servidor runtime |

#### Funciones de Acceso a Business Document

| Función | Descripción |
|---|---|
| `getClass(node)` | Obtiene la clase (tipo de dato) de un nodo del BD |
| `getName(node)` | Obtiene el nombre de un nodo del BD |
| `getSegment(node)` | Obtiene el segmento de un nodo |
| `getPositionInSegment(node)` | Obtiene la posición dentro del segmento |
| `indexChildInstance(node, n)` | Accede a la n-ésima instancia de un nodo hijo |
| `isFirstChildInstance(node)` | Verifica si es la primera instancia del nodo hijo |
| `isLastChildInstance(node)` | Verifica si es la última instancia del nodo hijo |

#### Funciones de Instancia de Business Document

| Función | Descripción |
|---|---|
| `setDocumentAttribute(doc, name, value)` | Establece un atributo de documento en el BD de entrada |
| `setDocumentAttributeToOutput(doc, name, value)` | Establece un atributo de documento en el BD de salida |

#### Funciones de Mensaje

| Función | Descripción |
|---|---|
| `getAttribute(name)` | Obtiene el valor de un atributo del mensaje |
| `setAttribute(name, value)` | Establece el valor de un atributo del mensaje |
| `getStringAttribute(name)` | Obtiene atributo de tipo string |
| `getIntegerAttribute(name)` | Obtiene atributo de tipo integer |
| `getRealAttribute(name)` | Obtiene atributo de tipo real |
| `getDateAttribute(name)` | Obtiene atributo de tipo date |
| `getInputInstance()` | Obtiene la instancia del mensaje de entrada |
| `getInputMessage()` | Obtiene el contenido completo del mensaje de entrada |
| `getMessagePriority()` | Obtiene la prioridad del mensaje |
| `setMessagePriority(value)` | Establece la prioridad del mensaje |

#### Funciones de Attachments (Adjuntos)

| Función | Descripción |
|---|---|
| `addAttachment(data, contentType, contentId)` | Añade un adjunto al mensaje |
| `countAttachments()` | Cuenta el número de adjuntos |
| `getAttachmentData(index)` | Obtiene los datos de un adjunto por índice |
| `getAttachmentContentId(index)` | Obtiene el Content-ID de un adjunto |
| `getAttachmentContentType(index)` | Obtiene el Content-Type de un adjunto |
| `selectAttachment(index)` | Selecciona un adjunto específico para procesamiento |
| `selectAllAttachments()` | Selecciona todos los adjuntos |
| `unselectAttachment(index)` | Deselecciona un adjunto |
| `unselectAllAttachments()` | Deselecciona todos los adjuntos |
| `selectAttachmentsForOutput(...)` | Selecciona adjuntos para el mensaje de salida |
| `selectAllAttachmentsForOutput()` | Selecciona todos los adjuntos para el mensaje de salida |
| `unselectAllAttachmentsForOutput()` | Deselecciona todos los adjuntos del mensaje de salida |
| `unselectAttachmentForOutput(index)` | Deselecciona un adjunto específico del mensaje de salida |

#### Funciones de Contexto

| Función | Descripción |
|---|---|
| `getContextAttribute(name)` | Obtiene el valor de un atributo de contexto |
| `setContextAttribute(name, value)` | Establece el valor de un atributo de contexto |
| `removeContextAttribute(name)` | Elimina un atributo de contexto |

#### Funciones JMS

| Función | Descripción |
|---|---|
| `getJMSStringProperty(name)` | Obtiene una propiedad JMS de tipo string |
| `getJMSIntegerProperty(name)` | Obtiene una propiedad JMS de tipo integer |
| `getJMSRealProperty(name)` | Obtiene una propiedad JMS de tipo real |
| `setJMSProperty(name, value)` | Establece una propiedad JMS |
| `setJMSDocumentProperty(name, value)` | Establece una propiedad JMS a nivel de documento |
| `removeJMSProperty(name)` | Elimina una propiedad JMS |
| `keepJMSChannelProperties()` | Mantiene las propiedades del canal JMS en el mensaje de salida |

#### Funciones de Sistema

| Función | Descripción |
|---|---|
| `getEnv(varName)` | Obtiene el valor de una variable de entorno del sistema operativo |
| `setEnv(varName, value)` | Establece el valor de una variable de entorno |
| `runProgram(command)` | Ejecuta un programa externo del sistema operativo |

#### Funciones de Tablas (Table Lookup)

| Función | Descripción |
|---|---|
| `returnColumn(table, key, column)` | Retorna el valor de la columna especificada dado un key |
| `returnColumnInPeriod(table, key, date, column)` | Retorna el valor de columna válido para una fecha (tablas con vigencia temporal) |
| `isKeyPresent(table, key)` | Verifica si existe un key en la tabla |
| `isKeyPresentInPeriod(table, key, date)` | Verifica si existe un key válido para una fecha dada |

#### Funciones de Tablas con Parámetros Dinámicos

Permite usar parámetros dinámicos (calculados en runtime) para acceder a tablas de lookup con múltiples claves.

#### Funciones de Trace Access (Trazabilidad)

| Función | Descripción |
|---|---|
| `addTrace(code, message, module)` | Añade una entrada de traza al log |
| `countTraces()` | Cuenta el número de trazas registradas |
| `getTraces()` | Obtiene todas las trazas registradas |
| `getLastTraceCode()` | Obtiene el código de la última traza |
| `getLastTraceMessage()` | Obtiene el mensaje de la última traza |
| `getLastTraceModule()` | Obtiene el módulo de la última traza |

#### Funciones de Truncado

| Función | Descripción |
|---|---|
| `truncate(value, length)` | Trunca un valor de texto o numérico a la longitud especificada |

#### Funciones EDI

| Función | Descripción |
|---|---|
| `generateNextIdInSequence(name)` | Genera el siguiente número de secuencia EDI (para control numbers) |

#### Funciones de Sentinel (Tracking)

| Función | Descripción |
|---|---|
| `getTrackedObjectId()` | Obtiene el ID del Tracked Object actual |
| `getTrackedObjectName()` | Obtiene el nombre del Tracked Object |
| `getTrackedObjectUserId()` | Obtiene el User ID del Tracked Object |
| `sendCycleLink(...)` | Envía un Cycle Link a Axway Sentinel |
| `setTrackedObjectAttribute(name, value)` | Establece un atributo de un Tracked Object |

#### Funciones de Message Logger

| Función | Descripción |
|---|---|
| `addMessageLoggerEvent(...)` | Añade un evento al Message Logger |
| `getMessageLoggerId()` | Obtiene el ID del Message Logger |

#### Funciones SWIFT

| Función | Descripción |
|---|---|
| `checkBICSubtypes(bic)` | Verifica subtipos de un código BIC |
| `isValidAmount(value)` | Valida que un valor sea un importe SWIFT válido |
| `isValidIBANCode(iban)` | Valida un código IBAN |
| `isValidBICCode(bic)` | Valida un código BIC |
| `isValidISINCode(isin)` | Valida un código ISIN |
| `updateBICTable(...)` | Actualiza la tabla BIC local |

#### Funciones de B2Bi User Attributes

| Función | Descripción |
|---|---|
| `getInboundUserAttribute(name)` | Obtiene un atributo de usuario B2Bi del mensaje entrante |
| `getOutboundUserAttribute(name)` | Obtiene un atributo de usuario B2Bi del mensaje saliente |

#### Variable Century (para Fechas)

| Función | Descripción |
|---|---|
| `configureCenturyVariable` | Configura la variable Century para el manejo de años de dos dígitos en fechas EDI (YYMMDD)  |

---

## Preferencias DML

La sección **Set DML Preferences** permite personalizar el comportamiento de Mapping Services. Incluye, entre otras:

- **Mapping language and version decoration:** Personalizar cómo se muestra la versión DML en el Project Explorer.
- Preferencias generales de visualización del editor.
- Configuraciones de comportamiento del Map Engine durante la simulación.

---

## Soporte y Recursos Adicionales

### Documentación Relacionada

- [Guía de Usuario DML - Referencia completa](https://docs.axway.com/bundle/MappingServices_36_UsersGuide_DML_allOS_en_HTML5/page/Content/AxwayStartPage_DML_UG.htm)
- [Plataformas Soportadas](https://docs.axway.com/bundle/Axway_Products_SupportedPlatforms_allOS_en_HTML5)
- [Accesibilidad y ACRs](https://docs.axway.com/bundle/AccessibilityVPATS_allOS_en_HTML5)
- [Documentación B2Bi 2.6](https://docs.axway.com/search?labelkey=prod-b2bi-26-UP2026-03&labelkey=ct-html)

### Soporte Global Axway

El equipo **Axway Global Support** proporciona soporte mundial 24x7 para clientes con acuerdos de soporte activos.

- **Email:** support@axway.com
- **Portal de soporte:** [https://support.axway.com](https://support.axway.com/)
- **Portal de documentación:** [https://docs.axway.com](https://docs.axway.com/)

### Tags de Producto

| Tag | Descripción |
|---|---|
| `prod-b2bi-26-UP2026-03` | B2Bi versión 2.6, Update Pack 2026-03 |
| `ct-user` | Documentación de usuario |
| `env-onprem` | Entorno On-Premises |
| `ct-getstarted` | Documentación de inicio rápido |

---

## Licencia y Propiedad Intelectual

© 2026 Axway, All Rights Reserved.

- [Términos de Uso](https://www.axway.com/en/terms-of-use)
- [Declaración de Privacidad](https://www.axway.com/en/privacy-statement)
- [Código de Ética](https://www.axway.com/en/code-of-ethics)
- [Programa de Cumplimiento de Privacidad - GDPR](https://www.axway.com/en/gdpr)
