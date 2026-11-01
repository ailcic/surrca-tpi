# Diccionario de datos (versión preliminar)

Convención: **PK**, identificador único; **NN**, campo obligatorio; **UQ**, valor que no puede
repetirse; **FK →**, campo que referencia a otra entidad. Los nombres y los tamaños de los campos
son supuestos de diseño, para una Macro Universidad Pública
Nacional (MUPN) cualquiera.

## Entidad 1: Investigador

| Campo | Tipo | Restricciones | Descripción funcional |
|:-----------------------|:---------------|:-------------------|:------------------------------------------|
| id_investigador | Integer | PK | Identificador interno que asigna el sistema. No cambia aunque cambien los demás datos del investigador. |
| apellido | String(60) | NN | Apellido tal como figura en las publicaciones; se usa para ordenar y buscar en el portal. |
| nombre | String(60) | NN | Nombre o nombres del investigador. |
| email_institucional | String(100) | UQ | Correo con el dominio de la universidad. Acredita la pertenencia y sirve como usuario de acceso al perfil. Puede estar vacío en quien dirige un proyecto y no se registró, porque la ficha mínima no depende del registro. |
| id_unidad | Integer | NN, FK → Unidad académica | Unidad de filiación principal. La determina una autoridad (fuente: Secretaría de Gestión de Personal); el investigador no puede modificarla. |
| perfil_visible | Boolean | NN; por defecto, falso | Indica si el perfil se muestra en el portal público. Seguridad: solo lo modifica el propio investigador, porque la visibilidad es voluntaria. Es la base para medir la meta M4 de la Entrega N.º 2. |

## Entidad 2: Unidad académica

| Campo | Tipo | Restricciones | Descripción funcional |
|:-----------------------|:---------------|:-------------------|:------------------------------------------|
| id_unidad | Integer | PK | Identificador interno de la unidad. |
| nombre | String(120) | NN, UQ | Nombre oficial de la unidad (por ejemplo, «Facultad de Ciencias Exactas»). |
| tipo | String(20) | NN; datos aceptables: Facultad, Instituto, Centro | Clase de unidad. Una lista cerrada evita variantes de escritura y permite filtrar el portal. |
| id_unidad_superior | Integer | FK → Unidad académica | Unidad de la que depende (por ejemplo, un instituto de su facultad). Queda vacío en las facultades. Reproduce en los datos la estructura formal del organigrama general. |
| es_piloto | Boolean | NN; por defecto, falso | Marca las tres facultades piloto de la Entrega N.º 2 (tareas P3, I2 e I4); permite medir la adopción sobre ellas. |

## Entidad 3: Proyecto (subsidio)

| Campo | Tipo | Restricciones | Descripción funcional |
|:-----------------------|:---------------|:-------------------|:------------------------------------------|
| id_proyecto | Integer | PK | Identificador interno del proyecto. |
| codigo | String(20) | NN, UQ | Código que asigna la Secretaría de Ciencia y Técnica al aprobar el proyecto; es el que figura en las resoluciones y en los informes. |
| titulo | String(250) | NN | Título del proyecto. |
| id_director | Integer | NN, FK → Investigador | Investigador que dirige el proyecto; su perfil lo muestra entre sus antecedentes. |
| id_unidad | Integer | NN, FK → Unidad académica | Unidad académica sede del proyecto. |
| organismo_financiador | String(100) | NN | Entidad que otorga el subsidio (la propia universidad u otro organismo de ciencia). |
| monto_otorgado | Decimal(14,2) | ≥ 0 | Monto del subsidio, en pesos. Fuente y seguridad: lo carga y lo modifica solo la Secretaría Económico-Financiera. |
| fecha_inicio | Date | NN | Fecha de inicio de la ejecución. |
| fecha_fin | Date | NN; ≥ fecha_inicio | Fecha de finalización prevista. |
| vigente | Boolean | calculado | Fórmula: es verdadero si la fecha actual está entre fecha_inicio y fecha_fin. No se carga a mano. |

## Entidad 4: Filiación secundaria

Un investigador puede formar parte de otra institución en paralelo, o haberlo hecho. Por eso,
además de la filiación principal (id_unidad en Investigador), puede tener filiaciones secundarias.

| Campo | Tipo | Restricciones | Descripción funcional |
|:-----------------------|:---------------|:-------------------|:------------------------------------------|
| id_filiacion | Integer | PK | Identificador interno de la filiación. |
| id_investigador | Integer | NN, FK → Investigador | Investigador al que corresponde. |
| institucion | String(120) | NN | Institución declarada; puede ser ajena a la universidad. |
| fecha_inicio | Date | | Inicio de la filiación, si se conoce. |
| fecha_fin | Date | ≥ fecha_inicio | Fin de la filiación, si terminó. |
| vigente | Boolean | NN | Indica si sigue vigente. Se declara cuando no hay fechas; si fecha_fin ya pasó, es falso. |
| declarada_por | String(20) | NN; datos aceptables: Investigador, Referente | Quién la declaró. A diferencia de la principal, no la determina una autoridad. |

## Entidad 5: Producción precargada

Lo que se puede recuperar automáticamente del CV, de ORCID o de repositorios se precarga, y cada
persona decide qué se muestra.

| Campo | Tipo | Restricciones | Descripción funcional |
|:-----------------------|:---------------|:-------------------|:------------------------------------------|
| id_produccion | Integer | PK | Identificador interno del elemento. |
| id_investigador | Integer | NN, FK → Investigador | Investigador al que corresponde. |
| titulo | String(250) | NN | Título del elemento, tal como llega de la fuente. |
| origen | String(20) | NN; datos aceptables: CV, ORCID, Repositorio | Fuente de la que se recuperó. |
| circuito | String(20) | NN; datos aceptables: Institucional, Externo | Externo: otro organismo, o producción ajena a la docencia y la investigación, como una novela. |
| visible | Boolean | NN; por defecto, falso | Indica si se muestra en el portal. Seguridad: solo lo modifica el propio investigador. |

## Ficha mínima de un proyecto

Un proyecto avalado o subsidiado es visible aunque quien lo dirige no se registre. La ficha mínima no
agrega campos: muestra codigo, titulo, id_director, id_unidad, organismo_financiador, fecha_inicio y
fecha_fin de la entidad Proyecto. No muestra monto_otorgado.

## Relaciones entre las entidades

- Cada **Investigador** puede tener cero o más elementos de **Producción precargada** (id_investigador).

- Cada **Investigador** puede tener cero o más **Filiaciones secundarias** (id_investigador).

- Cada **Investigador** pertenece a una **Unidad académica** (id_unidad), y una unidad
  tiene muchos investigadores.
- Una **Unidad académica** puede depender de otra (id_unidad_superior): un instituto
  depende de su facultad.
- Cada **Proyecto** tiene un director (id_director, un Investigador) y una sede
  (id_unidad, una Unidad académica).
- **Pendiente para la versión siguiente:** los integrantes del proyecto, además del
  director, forman una relación de muchos a muchos, que requiere una tabla intermedia.
