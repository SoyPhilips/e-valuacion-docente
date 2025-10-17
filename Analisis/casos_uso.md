# 🎭 Casos de Uso - Sistema e-VALuacion

## 📖 Introducción

Este documento presenta los casos de uso del sistema e-VALuacion, describiendo las interacciones entre los diferentes actores y el sistema para lograr objetivos específicos. Los casos de uso están organizados por módulos funcionales y priorizados según su importancia para el funcionamiento del sistema.

## 👥 Actores del Sistema

### 🎓 Estudiante
- **Descripción**: Usuario que realiza evaluaciones de desempeño docente
- **Responsabilidades**: Completar formularios de evaluación, consultar historial de evaluaciones
- **Características**: Acceso limitado, solo puede evaluar docentes de materias en las que está inscrito

### 👨‍🏫 Docente
- **Descripción**: Usuario que recibe evaluaciones y consulta sus resultados
- **Responsabilidades**: Consultar reportes de evaluación, revisar retroalimentación
- **Características**: Acceso a sus propios datos de evaluación, no puede modificar evaluaciones

### 👨‍💼 Administrador
- **Descripción**: Usuario con privilegios completos para gestionar el sistema
- **Responsabilidades**: Gestionar usuarios, configurar evaluaciones, generar reportes globales
- **Características**: Acceso completo al sistema, puede realizar todas las operaciones

## 🔐 Módulo de Autenticación y Gestión de Usuarios

### CU-001: Iniciar Sesión

**Actor Principal**: Estudiante, Docente, Administrador  
**Precondiciones**: El usuario debe tener credenciales válidas registradas en el sistema  
**Postcondiciones**: El usuario accede al sistema con los permisos correspondientes a su rol

#### Flujo Principal:
1. El usuario accede a la página de login
2. El sistema muestra el formulario de autenticación
3. El usuario ingresa su nombre de usuario y contraseña
4. El sistema valida las credenciales
5. El sistema redirige al usuario al dashboard correspondiente a su rol
6. El sistema registra el inicio de sesión en los logs de auditoría

#### Flujos Alternativos:
**FA-001.1: Credenciales Inválidas**
- 4a. El sistema detecta credenciales incorrectas
- 4b. El sistema muestra mensaje de error
- 4c. El sistema incrementa contador de intentos fallidos
- 4d. Regresa al paso 3

**FA-001.2: Cuenta Bloqueada**
- 4a. El sistema detecta que la cuenta está bloqueada
- 4b. El sistema muestra mensaje informativo sobre el bloqueo
- 4c. El sistema sugiere contactar al administrador

#### Requerimientos Especiales:
- Encriptación de contraseñas
- Bloqueo automático después de 5 intentos fallidos
- Sesión con timeout de 30 minutos de inactividad

---

### CU-002: Cerrar Sesión

**Actor Principal**: Estudiante, Docente, Administrador  
**Precondiciones**: El usuario debe tener una sesión activa  
**Postcondiciones**: La sesión del usuario se cierra y se redirige al login

#### Flujo Principal:
1. El usuario selecciona la opción "Cerrar Sesión"
2. El sistema muestra confirmación de cierre de sesión
3. El usuario confirma la acción
4. El sistema invalida la sesión actual
5. El sistema redirige a la página de login
6. El sistema registra el cierre de sesión en los logs

---

### CU-003: Recuperar Contraseña

**Actor Principal**: Estudiante, Docente, Administrador  
**Precondiciones**: El usuario debe tener un email registrado en el sistema  
**Postcondiciones**: El usuario recibe instrucciones para restablecer su contraseña

#### Flujo Principal:
1. El usuario selecciona "¿Olvidaste tu contraseña?" en el login
2. El sistema muestra formulario de recuperación
3. El usuario ingresa su email registrado
4. El sistema valida que el email existe en la base de datos
5. El sistema genera un token temporal de recuperación
6. El sistema envía email con enlace de recuperación
7. El usuario accede al enlace y establece nueva contraseña

---

## 📝 Módulo de Evaluaciones

### CU-004: Realizar Evaluación Docente

**Actor Principal**: Estudiante  
**Precondiciones**: El estudiante debe estar inscrito en la materia del docente a evaluar  
**Postcondiciones**: La evaluación se registra en el sistema y se actualiza el estado

#### Flujo Principal:
1. El estudiante accede al módulo de evaluaciones
2. El sistema muestra lista de docentes disponibles para evaluar
3. El estudiante selecciona un docente específico
4. El sistema muestra el formulario de evaluación correspondiente
5. El estudiante completa todas las secciones del formulario
6. El estudiante revisa sus respuestas
7. El estudiante confirma y envía la evaluación
8. El sistema valida la completitud del formulario
9. El sistema guarda la evaluación en la base de datos
10. El sistema muestra confirmación de envío exitoso

#### Flujos Alternativos:
**FA-004.1: Evaluación Incompleta**
- 8a. El sistema detecta campos obligatorios vacíos
- 8b. El sistema resalta los campos faltantes
- 8c. El sistema muestra mensaje de error
- 8d. Regresa al paso 5

**FA-004.2: Evaluación Ya Realizada**
- 3a. El sistema detecta que ya existe una evaluación para este docente
- 3b. El sistema muestra mensaje informativo
- 3c. El sistema ofrece opción de ver evaluación anterior

---

### CU-005: Consultar Evaluaciones Pendientes

**Actor Principal**: Estudiante  
**Precondiciones**: El estudiante debe tener sesión activa  
**Postcondiciones**: Se muestra la lista de evaluaciones pendientes

#### Flujo Principal:
1. El estudiante accede al dashboard principal
2. El sistema consulta evaluaciones pendientes para el estudiante
3. El sistema muestra lista de docentes pendientes de evaluar
4. El sistema indica fechas límite para cada evaluación
5. El estudiante puede seleccionar una evaluación para completar

---

### CU-006: Crear Formulario de Evaluación

**Actor Principal**: Administrador  
**Precondiciones**: El administrador debe tener permisos de configuración  
**Postcondiciones**: Se crea un nuevo formulario de evaluación disponible para uso

#### Flujo Principal:
1. El administrador accede al módulo de gestión de formularios
2. El sistema muestra opciones de creación de formularios
3. El administrador selecciona "Crear Nuevo Formulario"
4. El sistema muestra el editor de formularios
5. El administrador define título y descripción del formulario
6. El administrador añade preguntas de diferentes tipos
7. El administrador configura escalas de calificación
8. El administrador establece criterios de validación
9. El administrador guarda el formulario
10. El sistema valida la estructura del formulario
11. El sistema activa el formulario para uso

#### Tipos de Preguntas Soportadas:
- **Escala Likert**: 1-5, 1-10 puntos
- **Opción Múltiple**: Selección única o múltiple
- **Texto Libre**: Comentarios y sugerencias
- **Calificación Numérica**: Valores específicos

---

## 📊 Módulo de Reportes y Analytics

### CU-007: Generar Reporte Individual de Docente

**Actor Principal**: Docente, Administrador  
**Precondiciones**: Deben existir evaluaciones completadas para el docente  
**Postcondiciones**: Se genera y muestra el reporte de desempeño individual

#### Flujo Principal:
1. El actor accede al módulo de reportes
2. El sistema muestra opciones de generación de reportes
3. El actor selecciona "Reporte Individual"
4. El sistema solicita parámetros del reporte (período, materia, etc.)
5. El actor especifica los filtros deseados
6. El sistema procesa las evaluaciones según los criterios
7. El sistema calcula métricas y estadísticas
8. El sistema genera visualizaciones (gráficos, tablas)
9. El sistema presenta el reporte completo
10. El actor puede exportar el reporte en PDF o Excel

#### Métricas Incluidas:
- **Promedio General**: Calificación promedio en todas las categorías
- **Distribución de Calificaciones**: Histograma de puntuaciones
- **Tendencias Temporales**: Evolución del desempeño en el tiempo
- **Comparativa**: Posición relativa respecto a otros docentes
- **Comentarios Destacados**: Retroalimentación cualitativa relevante

---

### CU-008: Consultar Dashboard de Indicadores

**Actor Principal**: Administrador  
**Precondiciones**: El administrador debe tener acceso al módulo de analytics  
**Postcondiciones**: Se muestra el dashboard con indicadores clave del sistema

#### Flujo Principal:
1. El administrador accede al dashboard de indicadores
2. El sistema carga datos actualizados de evaluaciones
3. El sistema calcula KPIs principales
4. El sistema genera visualizaciones interactivas
5. El sistema presenta métricas en tiempo real
6. El administrador puede filtrar por período, programa, etc.

#### Indicadores Clave:
- **Tasa de Participación**: % de evaluaciones completadas vs. asignadas
- **Promedio Institucional**: Calificación promedio de todos los docentes
- **Distribución por Programas**: Desempeño por área académica
- **Tendencias Temporales**: Evolución de indicadores en el tiempo
- **Top Performers**: Docentes con mejor desempeño

---

## 🛠️ Módulo de Administración

### CU-009: Gestionar Usuarios del Sistema

**Actor Principal**: Administrador  
**Precondiciones**: El administrador debe tener permisos de gestión de usuarios  
**Postcondiciones**: Los usuarios son creados, modificados o desactivados según corresponda

#### Flujo Principal:
1. El administrador accede al módulo de gestión de usuarios
2. El sistema muestra lista de usuarios existentes
3. El administrador selecciona la acción deseada (crear, editar, desactivar)
4. El sistema presenta el formulario correspondiente
5. El administrador completa la información requerida
6. El sistema valida los datos ingresados
7. El sistema ejecuta la operación solicitada
8. El sistema confirma la operación exitosa

#### Operaciones Disponibles:
- **Crear Usuario**: Registro de nuevos estudiantes, docentes o administradores
- **Editar Perfil**: Modificación de información personal y académica
- **Asignar Roles**: Cambio de permisos y responsabilidades
- **Desactivar Cuenta**: Suspensión temporal o permanente de acceso
- **Resetear Contraseña**: Generación de nueva contraseña temporal

---

### CU-010: Configurar Períodos de Evaluación

**Actor Principal**: Administrador  
**Precondiciones**: El administrador debe tener permisos de configuración del sistema  
**Postcondiciones**: Se establecen los períodos activos para evaluaciones

#### Flujo Principal:
1. El administrador accede a configuración de períodos
2. El sistema muestra períodos existentes y su estado
3. El administrador selecciona "Crear Nuevo Período"
4. El sistema presenta formulario de configuración
5. El administrador define fechas de inicio y fin
6. El administrador asigna docentes y materias al período
7. El administrador establece formularios a utilizar
8. El sistema valida que no existan conflictos de fechas
9. El sistema activa el período de evaluación
10. El sistema notifica a usuarios relevantes

---

## 🔍 Casos de Uso Extendidos

### CU-011: Monitorear Progreso de Evaluaciones

**Actor Principal**: Administrador  
**Precondiciones**: Debe existir un período de evaluación activo  
**Postcondiciones**: Se presenta el estado actual del proceso de evaluación

#### Flujo Principal:
1. El administrador accede al monitor de progreso
2. El sistema calcula estadísticas de participación
3. El sistema identifica evaluaciones pendientes
4. El sistema genera alertas por baja participación
5. El sistema presenta dashboard de seguimiento
6. El administrador puede enviar recordatorios automáticos

#### Métricas de Seguimiento:
- **Tasa de Completitud**: % de evaluaciones finalizadas
- **Participación por Programa**: Desglose por área académica
- **Evaluaciones Pendientes**: Lista de estudiantes sin evaluar
- **Tiempo Promedio**: Duración típica para completar evaluaciones

---

### CU-012: Exportar Datos del Sistema

**Actor Principal**: Administrador  
**Precondiciones**: Deben existir datos de evaluaciones en el sistema  
**Postcondiciones**: Los datos se exportan en el formato solicitado

#### Flujo Principal:
1. El administrador accede a herramientas de exportación
2. El sistema presenta opciones de exportación disponibles
3. El administrador selecciona tipo de datos a exportar
4. El administrador especifica formato de salida (CSV, Excel, JSON)
5. El administrador define filtros y criterios
6. El sistema procesa la solicitud de exportación
7. El sistema genera el archivo de exportación
8. El sistema proporciona enlace de descarga
9. El administrador descarga el archivo generado

---

## 📋 Matriz de Casos de Uso vs Requerimientos

| Caso de Uso | Requerimientos Relacionados | Prioridad | Complejidad |
|-------------|----------------------------|-----------|-------------|
| CU-001 | RF-001.1, RNF-002.1 | Crítica | Media |
| CU-002 | RF-001.1, RNF-002.2 | Crítica | Baja |
| CU-003 | RF-001.2, RNF-002.1 | Importante | Media |
| CU-004 | RF-002.1, RF-002.3 | Crítica | Alta |
| CU-005 | RF-002.3, RNF-003.1 | Importante | Baja |
| CU-006 | RF-002.1, RF-004.2 | Crítica | Alta |
| CU-007 | RF-003.1, RF-003.2 | Importante | Alta |
| CU-008 | RF-003.2, RF-004.1 | Importante | Media |
| CU-009 | RF-001.2, RF-004.1 | Crítica | Media |
| CU-010 | RF-004.1, RF-004.2 | Importante | Media |
| CU-011 | RF-003.2, RF-004.1 | Deseable | Media |
| CU-012 | RF-003.1, RF-004.1 | Deseable | Baja |

## 🎯 Escenarios de Prueba

### Escenario 1: Evaluación Completa de Docente
**Objetivo**: Verificar el flujo completo de evaluación desde login hasta confirmación
**Actores**: Estudiante
**Pasos**:
1. Login exitoso del estudiante
2. Navegación a evaluaciones pendientes
3. Selección de docente específico
4. Completado de formulario de evaluación
5. Envío y confirmación de evaluación

### Escenario 2: Generación de Reporte Administrativo
**Objetivo**: Validar la generación de reportes consolidados
**Actores**: Administrador
**Pasos**:
1. Login como administrador
2. Acceso al módulo de reportes
3. Configuración de parámetros de reporte
4. Generación de reporte consolidado
5. Exportación en formato PDF

### Escenario 3: Gestión de Usuario Nuevo
**Objetivo**: Probar el proceso de alta de nuevos usuarios
**Actores**: Administrador
**Pasos**:
1. Acceso al módulo de gestión de usuarios
2. Creación de nuevo perfil de estudiante
3. Asignación de materias y docentes
4. Activación de cuenta
5. Verificación de acceso del nuevo usuario

## ✅ Criterios de Aceptación Generales

### Funcionalidad
- Todos los casos de uso críticos deben funcionar sin errores
- Los flujos alternativos deben manejarse apropiadamente
- Las validaciones deben prevenir datos inconsistentes

### Usabilidad
- Navegación intuitiva entre casos de uso relacionados
- Mensajes de error claros y constructivos
- Tiempo de respuesta aceptable para todas las operaciones

### Seguridad
- Validación de permisos en cada caso de uso
- Protección contra accesos no autorizados
- Auditoría completa de todas las acciones críticas

---

*Este documento de casos de uso proporciona una guía completa para el desarrollo, testing y validación del sistema e-VALuacion, asegurando que todas las interacciones usuario-sistema estén claramente definidas y sean implementables.*