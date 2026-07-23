## 1. Análisis de los documentos revisados

### 1.1 Problemas identificados

Al revisar la propuesta base, se identificaron los siguientes problemas:

- Gestión fragmentada de equipos, usuarios, cursos y recursos digitales.
- Pérdida de tiempo por instalaciones y configuraciones manuales.
- Diferencias entre los entornos de trabajo de los laboratorios y las computadoras personales.
- Falta de procesos claros para asignar horarios y reservar laboratorios.
- Responsabilidades poco definidas entre profesores, alumnos, encargados y autoridades.
- Ausencia de una política detallada para versionar, actualizar y retirar imágenes Docker.
- Falta de control sobre el software instalado y sus respectivas licencias.
- Escasa trazabilidad de solicitudes, cambios, aprobaciones e incidencias.

### 1.2 Comentarios a favor

- Se considera adecuada la utilización de imágenes Docker porque permite que estudiantes y profesores trabajen con las mismas versiones de herramientas, librerías y dependencias.
- La centralización de las imágenes facilita su reutilización en diferentes cursos y evita que cada estudiante tenga que configurar manualmente su entorno de trabajo.
- La propuesta mejora la portabilidad, ya que los estudiantes podrían replicar en sus computadoras personales el mismo entorno utilizado dentro del laboratorio.
- La aplicación de una matriz RACI conlleva la incorporación de procesos definidos para reservas, asignación de recursos y responsabilidades, ayudando a reducir las confusiones operativas entre los estudiantes y docentes.
- El modelo organizacional propuesto favorece una formación más cercana al entorno profesional, al integrar trabajo colaborativo por squads, mentoría docente y prácticas de seguridad, automatización y gestión de infraestructura.    

- El registro de solicitudes, aprobaciones y versiones permitiría identificar quién creó o modificó una imagen y para qué curso fue utilizada.
- También es favorable establecer roles diferenciados para profesores, estudiantes y encargados, porque reduce la posibilidad de realizar cambios no autorizados.

### 1.3 Comentarios en contra

Durante la revisión del Core y la Plataforma (Gestión de Usuarios y Accesos), se identificaron ciertos inconvenientes operativos, destacando los siguientes:
### Riesgo de punto único de fallo:
Si la capa central (como el sistema de autenticación Keycloak o la base de datos PostgreSQL) sufre una caída, todo el laboratorio queda inoperativo, impidiendo el acceso a los recursos y a los proyectos.  
### Curva de integración compleja:
Conectar herramientas de nivel empresarial de forma unificada exige un alto nivel técnico, lo que puede retrasar el desarrollo inicial si los equipos de alumnos no cuentan con la experiencia necesaria en arquitecturas complejas.  

En cuanto a la infraestructura de Hardware y Operaciones del laboratorio, se detectaron las siguientes complicaciones técnicas:
### Sobrecarga de mantenimiento físico y de red:
El modelo requiere instalar agentes en cada computadora física para reportar su estado y depende de una infraestructura de red local impecable; cualquier falla en los equipos de red de la universidad haría colapsar la conexión.  
### Altos costos de infraestructura:
Mantener servidores dedicados, sistemas de almacenamiento y recursos virtualizados (como Proxmox o Kubernetes) genera gastos económicos recurrentes y ocultos que la institución deberá sostener a largo plazo.  

Se observo alguno problemas de en la parte de manejo docker los cuales son:
### Inconsistencias de software: 
El clásico problema de "funciona en mi máquina" generado por tener entornos no estandarizados con diferentes versiones de herramientas y librerías.
### Pérdida de tiempo académico: 
La cantidad de horas que estudiantes y administradores desperdician realizando instalaciones y configuraciones manuales en lugar de programar.
### Dificultad de portabilidad: 
La incapacidad de los estudiantes para replicar de forma fácil y exacta el mismo entorno del laboratorio en sus computadoras personales.
### Riesgo de actualizaciones:
Una actualización durante el semestre podría generar incompatibilidades en los proyectos.

Por último, respecto al Frontend y la Experiencia de Usuario (Portal Web), se evidenciaron los siguientes retos a considerar:
### Mantenimiento de desarrollo intensivo:
Sostener una aplicación web personalizada (Custom UI) que consuma múltiples APIs resulta sumamente difícil de administrar a lo largo del tiempo, especialmente ante la constante rotación semestral de los estudiantes que la programan.  
### Riesgo de desincronización de interfaz:
Si el portal web sufre problemas de latencia y no logra reflejar el estado físico de los equipos en tiempo real (por ejemplo, mostrando como "disponible" una computadora que acaba de dañarse), se generará frustración y desconfianza en los estudiantes.

### 1.4 Observaciones

Se identificaron los siguientes aspectos que requieren mayor detalle:
### Aplicación de parches críticos:
Aunque se propone congelar las versiones durante el semestre, debe definirse el procedimiento para aplicar actualizaciones urgentes de seguridad.

### 1.5 Propuestas de mejora

### Docker:

### a. Congelamiento Semestral de Entornos ("Cápsulas de Tiempo")
El problema operativo: En el desarrollo de software, las herramientas y dependencias se actualizan con mucha frecuencia. Si la plataforma actualiza automáticamente una imagen de contenedor a mitad de un semestre, existe un alto riesgo de que el código que los alumnos han estado desarrollando deje de compilar o funcione de manera errática por incompatibilidades con la nueva versión.

La solución propuesta: Establecer una política de procesos de "congelamiento de versiones" al inicio de cada ciclo académico. Una vez   que el docente valida y aprueba la imagen oficial de su asignatura, esta se sella. Cualquier actualización técnica que el sistema       detecte se documentará y encolará para ser evaluada e implementada recién en el siguiente semestre. Las únicas excepciones serán        parches críticos de ciberseguridad.

El beneficio organizativo: Garantiza predictibilidad y estabilidad operativa. Estudiantes y docentes tienen la certeza de que el        entorno técnico será idéntico desde la primera clase hasta la entrega del proyecto final, eliminando horas improductivas de soporte     técnico por errores de configuración.

### b. Pre-carga Automática de Datos Académicos (Data Seeding)
El problema operativo: La propuesta original resuelve excelentemente la entrega de software (ej. un motor de base de datos como PostgreSQL), pero no el contenido. Al iniciar una sesión de laboratorio, los usuarios pierden una porción significativa del tiempo de clase creando tablas e insertando datos ficticios manualmente para poder probar sus ejercicios.

La solución propuesta: Integrar un proceso de "Data Seeding" (sembrado de datos) durante la creación de las imágenes. El administrador del laboratorio, en coordinación con el docente, preparará contenedores que no solo tengan el software instalado, sino que incluyan bases de datos pre-pobladas con miles de registros estandarizados listos para usarse.

El beneficio organizativo: Optimización directa del tiempo efectivo de aprendizaje. El alumno descarga el contenedor y, al iniciarlo, cuenta inmediatamente con el ecosistema de datos necesario para programar, enfocando el esfuerzo en la resolución de problemas y no en la preparación del entorno.

### c. Sistema de reserva y asignación de laboratorios

El problema operativo: Actualmente no se establece un proceso suficientemente claro para reservar los laboratorios ni para resolver conflictos cuando dos cursos o proyectos solicitan el mismo horario. Esto puede ocasionar cruces de horarios, cambios de último momento y laboratorios reservados que finalmente no son utilizados.

La solución propuesta: Implementar un sistema centralizado de reservas en el cual los profesores y responsables de proyectos puedan solicitar un laboratorio indicando el curso, número de estudiantes, software requerido, fecha y horario.

El sistema deberá verificar automáticamente la disponibilidad y evitar reservas duplicadas. Cuando exista un conflicto, se aplicarán criterios de prioridad, como cursos obligatorios, cantidad de estudiantes, disponibilidad de otros laboratorios y fecha de presentación de la solicitud.

También se propone establecer un tiempo máximo para confirmar la reserva. Si el responsable no confirma o cancela con anticipación, el horario podrá ser liberado para otro curso o proyecto.

El beneficio organizativo: Esta mejora permitiría aprovechar mejor los laboratorios, reducir los cruces de horarios y mantener un registro de quién reservó cada espacio. Además, facilitaría la planificación académica y permitiría identificar horarios libres que podrían ser utilizados por estudiantes o proyectos.

### d. Proceso formal de gestión de incidentes

Problema operativo: No se detalla qué debe ocurrir ante fallas como caída de servicios, imágenes defectuosas, pérdida de acceso, problemas de red o equipos dañados durante una práctica.

Solución propuesta: Definir un proceso de incidentes con registro desde el portal, clasificación por prioridad, responsable asignado, tiempos objetivo de atención y comunicación al usuario. También se pueden documentar soluciones frecuentes en una base de conocimiento.

Beneficio organizativo: Permite responder de forma ordenada y medible ante problemas, disminuye el tiempo de interrupción de clases y evita repetir soluciones ya conocidas.

### e. Inventario de componentes y licencias por imagen

El problema operativo: Las imágenes Docker pueden incluir librerías, herramientas o dependencias con licencias desconocidas, incompatibles o no autorizadas. El escaneo de vulnerabilidades no garantiza por sí solo el cumplimiento de las licencias de software.

La solución propuesta: Generar automáticamente un inventario de componentes de cada imagen antes de publicarla. Este registro debe incluir nombre, versión, origen y licencia de cada dependencia. Si se detecta software sin licencia identificada o no permitido, la publicación deberá bloquearse hasta su revisión.

El beneficio organizativo: Permite conocer exactamente qué software contiene cada imagen, facilita las auditorías, reduce riesgos legales y mejora la trazabilidad de los entornos utilizados en cursos y proyectos.

### f. Depuración Basada en Evidencia

El problema operativo: Con el tiempo, el repositorio acumula imágenes Docker de cursos antiguos o tecnologías en desuso, aumentando el consumo de almacenamiento. Archivar solo por antigüedad es riesgoso: se puede eliminar una imagen que un curso aún necesita, o mantener años una que nadie usa hace semestres. Tampoco hay visibilidad clara de qué curso depende de qué imagen.

La solución propuesta: Implementar un sistema de ciclo de vida basado en el uso real y en un mapa de dependencias imagen-curso. Cada imagen se clasificará como Activa, En observación (sin uso en 2 semestres) o Candidata a archivado (sin uso en 3+ semestres). Antes de archivar, se notificará al Responsable de Imágenes y al docente asociado con un reporte de qué cursos la usaron. Las imágenes archivadas tendrán un periodo de gracia antes de eliminarse definitivamente.

El beneficio organizativo: El beneficio organizativo: El repositorio se limpia según evidencia real de uso, no por fechas arbitrarias, reduciendo el riesgo de afectar cursos activos y optimizando el almacenamiento institucional.

## 2. Conclusiones

Arquitectura Modular y Escalable: El diseño por capas y el uso del Modelo Spotify permiten que distintos equipos (squads) trabajen e integren mejoras de forma paralela sin romper la estabilidad del sistema general.  

Innovación en los Procesos: Más allá de las herramientas técnicas, el mayor valor del proyecto radica en optimizar la organización: recupera tiempo académico efectivo y elimina la fricción administrativa para estudiantes y docentes. 

Puente entre Academia e Industria: Al implementar flujos de trabajo de nivel empresarial (CI/CD, trazabilidad, contenedores), el laboratorio se convierte en un simulador que prepara directamente a los alumnos para el mercado laboral moderno.  

El Reto de la Integración Unificada: Dado que el grupo propone mejoras en diferentes áreas (hardware, software y procesos), el desafío final y la clave del éxito será mantener una gobernanza estricta para que todas las partes se comuniquen de forma segura, simple y sin conflictos.


En conclusión, la implementación de esta plataforma híbrida representa una solución integral que trasciende lo técnico para optimizar de raíz los procesos operativos del laboratorio. Gracias a su arquitectura modular y al modelo organizacional ágil, las diversas propuestas de mejora planteadas por nuestro equipo pueden integrarse de manera sinérgica en cada capa del sistema, desde la gestión física hasta el portal de usuario. En última instancia, este proyecto grupal no solo elimina la fricción administrativa y estandariza los entornos de desarrollo, sino que transforma el espacio académico en un ecosistema profesional moderno que conecta directamente la formación universitaria con los más altos estándares de la industria tecnológica

## 3. Recomendaciones

Proponer acciones prácticas para implementar y mejorar la gestión de los laboratorios.

