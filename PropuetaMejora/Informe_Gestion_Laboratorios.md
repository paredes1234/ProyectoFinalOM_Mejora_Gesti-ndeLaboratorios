## 1. Análisis de los documentos revisados

Explicar qué aspectos de los documentos fueron considerados adecuados, cuáles presentan limitaciones y qué elementos necesitan ser ampliados.

### 1.1 Problemas identificados

Señalar los principales problemas relacionados con horarios, equipos, software, imágenes Docker, licencias y responsabilidades.

### 1.2 Comentarios a favor

Mencionar los puntos positivos de la propuesta revisada y explicar por qué podrían ser útiles.

### 1.3 Comentarios en contra

Indicar las debilidades, riesgos o aspectos poco claros encontrados en los documentos.

### 1.4 Observaciones

Agregar comentarios complementarios sobre información faltante, contradicciones o temas que requieren mayor detalle.

### 1.5 Propuestas de mejora

### Docker:

1. Congelamiento Semestral de Entornos ("Cápsulas de Tiempo")
El problema operativo: En el desarrollo de software, las herramientas y dependencias se actualizan con mucha frecuencia. Si la plataforma actualiza automáticamente una imagen de contenedor a mitad de un semestre, existe un alto riesgo de que el código que los alumnos han estado desarrollando deje de compilar o funcione de manera errática por incompatibilidades con la nueva versión.

La solución propuesta: Establecer una política de procesos de "congelamiento de versiones" al inicio de cada ciclo académico. Una vez   que el docente valida y aprueba la imagen oficial de su asignatura, esta se sella. Cualquier actualización técnica que el sistema       detecte se documentará y encolará para ser evaluada e implementada recién en el siguiente semestre. Las únicas excepciones serán        parches críticos de ciberseguridad.

El beneficio organizativo: Garantiza predictibilidad y estabilidad operativa. Estudiantes y docentes tienen la certeza de que el        entorno técnico será idéntico desde la primera clase hasta la entrega del proyecto final, eliminando horas improductivas de soporte     técnico por errores de configuración.


## 2. Conclusiones

Resumir los principales resultados del análisis

## 3. Recomendaciones

Proponer acciones prácticas para implementar y mejorar la gestión de los laboratorios.

