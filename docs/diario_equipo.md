# Diario del equipo — VideojuegosHub

**Asignatura:** Evolución y Gestión de la Configuración (EGC) — Curso 2026/2027  
**Responsable del seguimiento:** Javier Jiménez Galván (Project Manager)  
**Última actualización:** 26/11/2026

Este diario recoge cronológicamente los avances, acuerdos, incidencias y decisiones relevantes del proyecto. Las actas de reunión y las issues del repositorio complementan este registro y permiten consultar el detalle de cada actuación.

## 07/11/2026 — Organización inicial del equipo

Se celebró la primera reunión para organizar el proyecto, repartir la redacción de los apartados del acta fundacional y establecer una distribución inicial de roles y responsabilidades. De los cinco integrantes inicialmente previstos, uno no pudo continuar al no superar el examen e Israel no asistió a la reunión, por lo que quedó pendiente confirmar la composición definitiva del equipo.

**Referencia:** [Acta de reunión nº 01](reuniones/reunion-01.md).

## 09/11/2026 — Formalización del acta fundacional

Se firmó el acta fundacional inicial, en la que se recogieron los acuerdos de organización, comunicación, gestión de ramas, tareas, commits y CI/CD del equipo.

Durante la fase inicial del proyecto, el tutor aprobó la propuesta de VideojuegosHub: adaptar UVLHub al dominio de los videojuegos mediante datasets en formato CSV. No se dispone de la fecha exacta de dicha aprobación.

## 13/11/2026 — Reorganización del equipo y creación del repositorio

Ante la falta de confirmación de la participación de Israel, se decidió reorganizar el proyecto contando con tres integrantes y adaptar el acta fundacional y la distribución de responsabilidades.

Gonzalo Gómez Cabezas creó el fork de UVLHub y la rama `trunk`, estableciendo así la base del flujo de trabajo EGCFlow.

**Referencia:** [Acta de reunión nº 02](reuniones/reunion-02.md).

## 20/11/2026 — Selección de Work Items

Se confirmó la composición definitiva del equipo y se seleccionaron cinco Work Items: los dos comunes y tres individuales (dos de dificultad alta y uno de dificultad media).

| Issue | Work Item | Categoría |
| --- | --- | --- |
| [#2](https://github.com/GonzaloGomez29/VideojuegosHub/issues/2) | WI-newdataset | Común |
| [#3](https://github.com/GonzaloGomez29/VideojuegosHub/issues/3) | WI-fakenodo | Común |
| [#6](https://github.com/GonzaloGomez29/VideojuegosHub/issues/6) | Two-factor authentication (2FA) | High |
| [#7](https://github.com/GonzaloGomez29/VideojuegosHub/issues/7) | Active session management | High |
| [#8](https://github.com/GonzaloGomez29/VideojuegosHub/issues/8) | Embeddable badge (for GitHub/Websites) | Medium |

También se registraron en el repositorio las tareas complementarias de DevOps relativas a la adaptación de la integración continua ([#4](https://github.com/GonzaloGomez29/VideojuegosHub/issues/4)) y la automatización de las releases ([#5](https://github.com/GonzaloGomez29/VideojuegosHub/issues/5)).

**Referencia:** [Acta de reunión nº 03](reuniones/reunion-03.md).

## 23/11/2026 — Revisión del proyecto con el tutor

Durante la revisión del proyecto se identificaron dos aspectos a mejorar:

- Limpiar el repositorio de los commits previos al proyecto.
- Completar los campos de las issues, especialmente las asignaciones y el tipo.

Estas observaciones quedan registradas para su resolución y posterior seguimiento.

## 26/11/2026 — Documentación de las reuniones e integración en trunk

Javier Jiménez Galván redactó e incorporó las tres actas de las reuniones iniciales en `docs/reuniones/`, mediante la rama `docs/9-actas-reuniones`. Se sincronizó dicha rama con `trunk` para incorporar los últimos cambios de configuración de Pytest y posteriormente se integraron las actas en `trunk`. La rama de tarea se eliminó y el equipo dio por finalizada la tarea de documentación.


**Referencias:** [Issue #9](https://github.com/GonzaloGomez29/VideojuegosHub/issues/9).
## 26/11/2026 — Actualización del acta fundacional

Los tres integrantes aprobaron una modificación de los acuerdos internos para adaptar el procedimiento de trabajo al tamaño definitivo del equipo. Jiayi Zhang incorporó la versión actualizada del acta fundacional al repositorio.

Los cambios aprobados fueron los siguientes:

- Corregir las referencias a cuatro integrantes y cuatro roles, reflejando la composición real de tres personas.
- Eximir las tareas exclusivamente documentales de la revisión obligatoria por otro integrante, permitiendo que su autor las integre en `trunk`.
- Mantener la revisión por otro integrante para las tareas que afecten al código, la configuración o la automatización del proyecto.
- Mantener las restantes normas de EGCFlow y las comprobaciones de integración continua.

Se adaptaron los apartados 3, 5.3, 5.5, 5.6 y 6.3 del acta fundacional para que los acuerdos fueran coherentes entre sí.

**Referencia:** [Issue #11](https://github.com/GonzaloGomez29/VideojuegosHub/issues/11).

## Estado del proyecto a 26/11/2026

El equipo ha completado la fase inicial de organización y ha avanzado en la preparación del repositorio, la documentación y la configuración de CI/CD. Todavía no se ha iniciado la implementación de las funcionalidades correspondientes a los Work Items.

La asignación definitiva de los WIs permanece pendiente. Antes de concretar el reparto, se considera necesario descomponer los dos WIs comunes, `newdataset` y `fakenodo`, en subissues de menor alcance que permitan distribuir el trabajo entre los tres integrantes.

### Próximos pasos

- [ ] Descomponer WI-newdataset (#2) y WI-fakenodo (#3) en subissues.
- [ ] Asignar responsables y planificar el desarrollo de los Work Items.
- [ ] Completar y validar la configuración de CI/CD, incluida la revisión de la incidencia del validador de commits.
- [ ] Iniciar la implementación de las funcionalidades siguiendo EGCFlow.
