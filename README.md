# SURRCA: Sistema Unificado de Registro y Repositorio de Ciencia Abierta

Documentación técnica del proyecto SURRCA, desarrollada para el Trabajo Práctico Integrador de
Organización Empresarial de la Tecnicatura Universitaria en Programación a Distancia (UTN).

## Descripción del sistema

SURRCA es un sistema propuesto para una Macro Universidad Pública Nacional (MUPN). No se refiere a
una universidad en particular: hay varias universidades nacionales de este tamaño y cualquiera de
ellas podría usarlo. Su objetivo es mostrar la producción científica y académica de la universidad
con datos verificables. Su alcance inicial (MVP) tiene dos módulos: un portal público de
visibilización y perfiles de investigadores.

La visibilidad tiene dos capas. Una es obligatoria: la información mínima de un proyecto avalado o
subsidiado se muestra por la sola existencia del proyecto. La otra es voluntaria: cada persona decide
si muestra su perfil y qué muestra de lo que se precarga.

Este repositorio contiene documentación, no el código del sistema.

## Integrantes

- Andrés Alejandro Ilcic ([@ailcic](https://github.com/ailcic))

## Contenido

| Documento | Qué contiene |
|---|---|
| [Procesos BPMN](docs/bpmn/) | Alta y publicación de perfil, y publicación de la ficha mínima, como imagen y como modelo `.bpmn` editable |
| [Historias de usuario](docs/historias-usuario.md) | Las tres historias del tablero |
| [Indicadores de control](docs/indicadores-control.md) | Indicadores y estándares para la auditoría técnica |
| [Diccionario de datos](docs/diccionario-datos.md) | Investigador, Unidad académica, Proyecto, Filiación secundaria y Producción precargada |
| [Planificación y estructura](docs/planificacion/) | Matriz FODA, Gantt y organigramas |

## Tablero

[Backlog del MVP en GitHub Projects](https://github.com/users/ailcic/projects/1/views/2). En el tablero, **Listo** significa que la historia está especificada y documentada, no que esté implementada.

## Declaración de Uso de IA

A lo largo de este TPI se hizo una evaluación de las posibilidades de la herramienta Claude Code bajo
supervisión constante, usándose para revisar estilos y formatos, también para la generación de tablas
y diagramas desde descripciones de lenguaje natural. La exclusiva responsabilidad de los contenidos
continúa siendo del autor.

### Prompts utilizados y por qué

- **«Vamos a realizar la entrega 4 del TPI».** Pedido general, junto con la consigna y la
  devolución de la entrega anterior. Es un prompt amplio: dejó en el asistente buena parte de la
  organización del trabajo, por lo que se le pidió un plan para aprobar antes de ejecutarlo.
- **Decisiones planteadas como preguntas de opción múltiple.** El asistente redactó las opciones y
  el autor eligió, entre otras cosas, el proceso a modelar. Las opciones de un asistente limitan lo
  que se considera. Por eso la pregunta sobre el proceso se hizo sin una opción recomendada.
- **Borrador de las historias de usuario.** El autor pidió una propuesta para editar, porque las
  entregas anteriores no las habían definido.

### Correcciones humanas

- **Filiación.** El asistente modeló una sola filiación por investigador y dejó abierta quién la
  corregía. El autor distinguió una filiación principal, determinada por una autoridad, de las
  secundarias, que el investigador o el referente declaran con fechas o vigencia, porque una persona
  puede pertenecer a más de una institución. El cambio afectó al BPMN y al diccionario de datos.
- **«La MUPN» o «una MUPN».** El asistente trataba a la MUPN como una institución única. El autor lo
  corrigió, porque hay varias universidades nacionales de este tamaño y la propuesta sirve para
  cualquiera de ellas.
- **Historias de usuario.** El autor revisó las tres propuestas y conservó sus enunciados.

### Aportes de la revisión

Los comentarios de [@drAndric](https://github.com/drAndric) en los issues cambiaron el modelo:

- **Información mínima obligatoria ([#1](https://github.com/ailcic/surrca-tpi/issues/1)).** El borrador
  trataba toda la visibilidad como voluntaria. Se agregó un segundo proceso para la ficha mínima de
  los proyectos, que no depende del registro.
- **Precarga ([#2](https://github.com/ailcic/surrca-tpi/issues/2)).** La decisión era única, por todo el
  perfil. Ahora lo recuperado del CV, de ORCID o de repositorios se precarga, y cada persona elige qué
  se muestra.
- **Filiación ([#3](https://github.com/ailcic/surrca-tpi/issues/3)).** Confirmó la corrección del autor:
  al menos una filiación fijada por la autoridad de la universidad, y otras opcionales.

### Límites

Las cifras de los indicadores I5 a I7 son supuestos de diseño. Qué campos forman la ficha mínima y que
lo precargado arranque oculto son propuestas del asistente sobre esos comentarios. El modelo BPMN se validó
con un script contra las reglas del material de la cátedra, lo que comprueba su forma pero no que
describa bien el proceso.
