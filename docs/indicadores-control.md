# Indicadores de control

Los indicadores I1 a I4 son las metas M1 a M4 del plan del proyecto, con sus mismas cifras. Las
cifras de I5 a I7 son supuestos de diseño, y cada universidad que adopte el sistema debería
revisarlas con sus datos reales. I4 mide perfiles activos: la ficha mínima de un proyecto no cuenta,
porque se publica sin que intervenga la decisión de la persona.

| N.º | Indicador | Fórmula | Estándar | Fuente y frecuencia | Acción correctiva |
|:--|:------|:------|:----|:------|:--------|
| I1 | Tiempo de respuesta (M1) | Percentil 95 de las búsquedas, con 100 000 registros y 200 usuarios concurrentes | ≤ 2 s | Prueba de carga P2, y en cada versión | Revisar índices y consultas antes de ampliar la infraestructura |
| I2 | Escalabilidad (M2) | Degradación de I1 con 500 000 registros | ≤ 20 % | Prueba de carga P2, y en cada versión | Revisar la indexación y planificar la capacidad con la universidad |
| I3 | Plazo (M3) | Semana de cierre de la tarea I3 | Semana 25 | Cronograma, semanal | Reprogramar según la ruta crítica o acotar el alcance |
| I4 | Adopción (M4) | Investigadores con perfil activo ÷ investigadores de las 3 facultades piloto | ≥ 50 % a las 8 semanas | Conteo del sistema, semanal | Acompañar y revisar las razones de cada facultad; nunca publicar sin autorización lo que es voluntario |
| I5 | Filiaciones principales que no coinciden | Altas derivadas al referente ÷ altas totales | ≤ 10 % | Registro del proceso, mensual | Revisar con Personal el origen de las diferencias |
| I6 | Tiempo de corrección de la filiación principal | Días hábiles entre la derivación y la corrección | ≤ 5 días hábiles | Registro del proceso, mensual | Reasignar la carga o simplificar la revisión |
| I7 | Cambios revisados | Pull Requests fusionados con revisión ÷ Pull Requests fusionados | 100 % | Historial de GitHub, en cada versión | Revisar a posteriori y exigir la revisión antes de fusionar |
