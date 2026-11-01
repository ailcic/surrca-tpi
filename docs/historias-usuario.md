# Historias de usuario del MVP

Formato: «Como [usuario], quiero [funcionalidad], para [beneficio]», con criterios de aceptación
y prioridad.

En este repositorio el software todavía no está construido. En el tablero, **Listo significa que
la historia está especificada y documentada, no que esté implementada**.

## H1. Alta del perfil

**Como** investigador/a de una MUPN, **quiero** crear mi perfil con mi correo institucional,
**para** acreditar mi pertenencia a la universidad y reunir mi producción en un solo lugar.

- **Prioridad:** alta.
- **Criterios de aceptación:**
  - El sistema acepta solo correos con el dominio de la universidad; si no, informa el rechazo.
  - El perfil nace como borrador, con `perfil_visible` en falso.
  - La filiación principal la determina la autoridad (Secretaría de Gestión de Personal), y el
    investigador o investigadora no puede modificarla.
  - Se pueden declarar filiaciones secundarias, actuales o pasadas, con fechas o vigencia.

## H2. Decisión de visibilidad

**Como** investigador/a de una MUPN, **quiero** decidir si mi perfil se muestra en el portal
público, **para** controlar qué hago visible y cuándo.

- **Prioridad:** alta.
- **Criterios de aceptación:**
  - Solo el propio investigador o investigadora puede cambiar `perfil_visible`.
  - Si no autoriza, el perfil se conserva como privado y no aparece en el portal.
  - Cada publicación actualiza el conteo de adopción de la meta M4.

## H3. Corrección de filiaciones

**Como** referente institucional de datos, **quiero** revisar y corregir las filiaciones que no
coinciden con las de Personal, **para** que el portal no muestre datos erróneos.

- **Prioridad:** media.
- **Criterios de aceptación:**
  - El sistema deriva al referente cada filiación principal que no coincide con la de Personal.
  - El referente también puede registrar una filiación secundaria en nombre del investigador o
    investigadora.
  - La corrección queda registrada con fecha y responsable.
  - Una filiación corregida permite continuar el alta sin que el perfil se publique solo.
