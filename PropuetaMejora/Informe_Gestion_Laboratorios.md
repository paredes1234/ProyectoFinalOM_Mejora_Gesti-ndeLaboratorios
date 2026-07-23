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
- El registro de solicitudes, aprobaciones y versiones permitiría identificar quién creó o modificó una imagen y para qué curso fue utilizada.

### 1.3 Comentarios en contra

Se observo alguno problemas de en la parte de manejo docker los cuales son:
### Inconsistencias de software: 
El clásico problema de "funciona en mi máquina" generado por tener entornos no estandarizados con diferentes versiones de herramientas y librerías.
### Pérdida de tiempo académico: 
La cantidad de horas que estudiantes y administradores desperdician realizando instalaciones y configuraciones manuales en lugar de programar.
### Dificultad de portabilidad: 
La incapacidad de los estudiantes para replicar de forma fácil y exacta el mismo entorno del laboratorio en sus computadoras personales.
### Ausencia de trazabilidad: 
La falta de un registro claro y auditable sobre qué imágenes y software específico se utilizaron durante un curso o proyecto.
### Riesgo de actualizaciones:
Una actualización durante el semestre podría generar incompatibilidades en los proyectos.
### Falta de control de versiones:
No se establece una política para conservar o reemplazar versiones anteriores.

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


## 2. Conclusiones

Arquitectura Modular y Escalable: El diseño por capas y el uso del Modelo Spotify permiten que distintos equipos (squads) trabajen e integren mejoras de forma paralela sin romper la estabilidad del sistema general.  

Innovación en los Procesos: Más allá de las herramientas técnicas, el mayor valor del proyecto radica en optimizar la organización: recupera tiempo académico efectivo y elimina la fricción administrativa para estudiantes y docentes. 

Puente entre Academia e Industria: Al implementar flujos de trabajo de nivel empresarial (CI/CD, trazabilidad, contenedores), el laboratorio se convierte en un simulador que prepara directamente a los alumnos para el mercado laboral moderno.  

El Reto de la Integración Unificada: Dado que el grupo propone mejoras en diferentes áreas (hardware, software y procesos), el desafío final y la clave del éxito será mantener una gobernanza estricta para que todas las partes se comuniquen de forma segura, simple y sin conflictos.


En conclusión, la implementación de esta plataforma híbrida representa una solución integral que trasciende lo técnico para optimizar de raíz los procesos operativos del laboratorio. Gracias a su arquitectura modular y al modelo organizacional ágil, las diversas propuestas de mejora planteadas por nuestro equipo pueden integrarse de manera sinérgica en cada capa del sistema, desde la gestión física hasta el portal de usuario. En última instancia, este proyecto grupal no solo elimina la fricción administrativa y estandariza los entornos de desarrollo, sino que transforma el espacio académico en un ecosistema profesional moderno que conecta directamente la formación universitaria con los más altos estándares de la industria tecnológica

## 3. Recomendaciones

Proponer acciones prácticas para implementar y mejorar la gestión de los laboratorios.

