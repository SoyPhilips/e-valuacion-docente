# 📊 Diagramas del Sistema e-VALuacion

## 📖 Introducción

Este documento presenta los diagramas técnicos del sistema e-VALuacion, incluyendo arquitectura del sistema, diagramas de flujo, diagramas de secuencia y representaciones visuales de la base de datos. Estos diagramas proporcionan una comprensión visual completa del diseño y funcionamiento del sistema.

## 🏗️ Arquitectura del Sistema

### Diagrama de Arquitectura General

```
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE PRESENTACIÓN                     │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐ │
│  │   HTML5     │  │    CSS3     │  │    JavaScript       │ │
│  │ (Estructura)│  │  (Estilos)  │  │ (Interactividad)    │ │
│  └─────────────┘  └─────────────┘  └─────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              Componentes de UI                          │ │
│  │  • Login/Logout    • Dashboard    • Formularios        │ │
│  │  • Reportes        • Administración • Navegación       │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE LÓGICA DE NEGOCIO               │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                JavaScript (Node.js)                     │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐ │ │
│  │  │ Controlador │  │ Controlador │  │   Controlador   │ │ │
│  │  │    Auth     │  │ Evaluación  │  │    Reportes     │ │ │
│  │  └─────────────┘  └─────────────┘  └─────────────────┘ │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐ │ │
│  │  │  Servicio   │  │  Servicio   │  │    Servicio     │ │ │
│  │  │  Usuarios   │  │ Evaluación  │  │   Analytics     │ │ │
│  │  └─────────────┘  └─────────────┘  └─────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE DATOS                           │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    SQLite Database                      │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐ │ │
│  │  │   Usuarios  │  │ Evaluaciones│  │    Respuestas   │ │ │
│  │  └─────────────┘  └─────────────┘  └─────────────────┘ │ │
│  │                                                         │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐ │ │
│  │  │  Materias   │  │ Formularios │  │    Preguntas    │ │ │
│  │  └─────────────┘  └─────────────┘  └─────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Patrón de Arquitectura: MVC (Model-View-Controller)

#### **Vista (View) - Capa de Presentación**
- **HTML5**: Estructura semántica y accesible
- **CSS3**: Diseño responsive y moderno
- **JavaScript**: Interactividad del lado cliente

#### **Controlador (Controller) - Lógica de Negocio**
- **Controladores REST**: Manejo de peticiones HTTP
- **Middleware de Autenticación**: Validación de sesiones
- **Validadores**: Verificación de datos de entrada

#### **Modelo (Model) - Capa de Datos**
- **ORM/Query Builder**: Abstracción de base de datos
- **Entidades**: Representación de objetos de negocio
- **Repositorios**: Patrones de acceso a datos

## 🔄 Diagrama de Flujo Principal

### Flujo de Evaluación Docente

```
                    ┌─────────────────┐
                    │   INICIO        │
                    └─────────┬───────┘
                              │
                    ┌─────────▼───────┐
                    │ Usuario ingresa │
                    │ credenciales    │
                    └─────────┬───────┘
                              │
                    ┌─────────▼───────┐
                    │ ¿Credenciales   │
                    │ válidas?        │
                    └─────┬───────┬───┘
                          │ NO    │ SÍ
                ┌─────────▼───┐   │
                │ Mostrar     │   │
                │ error       │   │
                └─────────────┘   │
                                  │
                        ┌─────────▼───────┐
                        │ Cargar dashboard│
                        │ según rol       │
                        └─────────┬───────┘
                                  │
                        ┌─────────▼───────┐
                        │ ¿Es estudiante? │
                        └─────┬───────┬───┘
                              │ NO    │ SÍ
                    ┌─────────▼───┐   │
                    │ Dashboard   │   │
                    │ Admin/      │   │
                    │ Docente     │   │
                    └─────────────┘   │
                                      │
                            ┌─────────▼───────┐
                            │ Mostrar lista   │
                            │ de evaluaciones │
                            │ pendientes      │
                            └─────────┬───────┘
                                      │
                            ┌─────────▼───────┐
                            │ Estudiante      │
                            │ selecciona      │
                            │ docente         │
                            └─────────┬───────┘
                                      │
                            ┌─────────▼───────┐
                            │ Cargar          │
                            │ formulario de   │
                            │ evaluación      │
                            └─────────┬───────┘
                                      │
                            ┌─────────▼───────┐
                            │ Estudiante      │
                            │ completa        │
                            │ formulario      │
                            └─────────┬───────┘
                                      │
                            ┌─────────▼───────┐
                            │ ¿Formulario     │
                            │ completo?       │
                            └─────┬───────┬───┘
                                  │ NO    │ SÍ
                        ┌─────────▼───┐   │
                        │ Mostrar     │   │
                        │ campos      │   │
                        │ faltantes   │   │
                        └─────────────┘   │
                                          │
                                ┌─────────▼───────┐
                                │ Guardar         │
                                │ evaluación en   │
                                │ base de datos   │
                                └─────────┬───────┘
                                          │
                                ┌─────────▼───────┐
                                │ Mostrar         │
                                │ confirmación    │
                                │ de envío        │
                                └─────────┬───────┘
                                          │
                                ┌─────────▼───────┐
                                │   FIN           │
                                └─────────────────┘
```

## 📱 Diagrama de Componentes de UI

### Estructura de Componentes

```
┌─────────────────────────────────────────────────────────────┐
│                        APP PRINCIPAL                        │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    HEADER                               │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐ │ │
│  │  │    Logo     │  │ Navegación  │  │ Usuario/Logout  │ │ │
│  │  └─────────────┘  └─────────────┘  └─────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   SIDEBAR                               │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │ • Dashboard                                         │ │ │
│  │  │ • Evaluaciones                                      │ │ │
│  │  │ • Reportes                                          │ │ │
│  │  │ • Administración                                    │ │ │
│  │  │ • Configuración                                     │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                 CONTENIDO PRINCIPAL                     │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │ │
│  │  │              COMPONENTE DINÁMICO                    │ │ │
│  │  │                                                     │ │ │
│  │  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │ │ │
│  │  │  │  Dashboard  │  │ Formulario  │  │   Reporte   │ │ │ │
│  │  │  │ Component   │  │ Evaluación  │  │ Component   │ │ │ │
│  │  │  └─────────────┘  └─────────────┘  └─────────────┘ │ │ │
│  │  └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    FOOTER                               │ │
│  │  Copyright © 2024 - Felipe Ramos & Carlos García       │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 🔐 Diagrama de Secuencia - Autenticación

```
Estudiante    Frontend    Backend    Base de Datos
    │             │          │            │
    │─────────────▶│          │            │
    │ Ingresa      │          │            │
    │ credenciales │          │            │
    │             │──────────▶│            │
    │             │ POST      │            │
    │             │ /login    │            │
    │             │          │────────────▶│
    │             │          │ SELECT     │
    │             │          │ usuario    │
    │             │          │◀────────────│
    │             │          │ datos      │
    │             │          │ usuario    │
    │             │          │            │
    │             │          │ [validar   │
    │             │          │ password]  │
    │             │          │            │
    │             │◀──────────│            │
    │             │ JWT token │            │
    │             │ + datos   │            │
    │◀─────────────│          │            │
    │ Redirigir a  │          │            │
    │ dashboard    │          │            │
```

## 📊 Diagrama de Secuencia - Realizar Evaluación

```
Estudiante    Frontend    Backend    Base de Datos
    │             │          │            │
    │─────────────▶│          │            │
    │ Selecciona   │          │            │
    │ docente      │          │            │
    │             │──────────▶│            │
    │             │ GET       │            │
    │             │ /formulario│           │
    │             │          │────────────▶│
    │             │          │ SELECT     │
    │             │          │ formulario │
    │             │          │◀────────────│
    │             │          │ preguntas  │
    │             │◀──────────│            │
    │             │ HTML      │            │
    │             │ formulario│            │
    │◀─────────────│          │            │
    │ Mostrar      │          │            │
    │ formulario   │          │            │
    │             │          │            │
    │─────────────▶│          │            │
    │ Completa y   │          │            │
    │ envía        │          │            │
    │             │──────────▶│            │
    │             │ POST      │            │
    │             │ /evaluacion│           │
    │             │          │ [validar   │
    │             │          │ datos]     │
    │             │          │            │
    │             │          │────────────▶│
    │             │          │ INSERT     │
    │             │          │ evaluacion │
    │             │          │◀────────────│
    │             │          │ ID         │
    │             │          │            │
    │             │          │────────────▶│
    │             │          │ INSERT     │
    │             │          │ respuestas │
    │             │          │◀────────────│
    │             │          │ OK         │
    │             │◀──────────│            │
    │             │ Confirmación│          │
    │◀─────────────│          │            │
    │ Evaluación   │          │            │
    │ guardada     │          │            │
```

## 🗄️ Diagrama Entidad-Relación (ERD)

```
┌─────────────────┐         ┌─────────────────┐
│    USUARIOS     │         │    PROGRAMAS    │
├─────────────────┤         ├─────────────────┤
│ • id (PK)       │    ┌────│ • id (PK)       │
│ • codigo        │    │    │ • codigo        │
│ • nombres       │    │    │ • nombre        │
│ • apellidos     │    │    │ • descripcion   │
│ • email         │    │    │ • facultad      │
│ • password_hash │    │    │ • estado        │
│ • tipo_usuario  │    │    └─────────────────┘
│ • programa_id(FK)│────┘              │
│ • estado        │                   │
│ • fecha_creacion│                   │
└─────────────────┘                   │
         │                            │
         │                            │
         │                            │
┌─────────────────┐                   │
│    MATERIAS     │                   │
├─────────────────┤                   │
│ • id (PK)       │                   │
│ • codigo        │                   │
│ • nombre        │                   │
│ • descripcion   │                   │
│ • creditos      │                   │
│ • programa_id(FK)│───────────────────┘
│ • docente_id(FK)│───────┐
│ • semestre      │       │
│ • estado        │       │
└─────────────────┘       │
         │                │
         │                │
         │                │
┌─────────────────┐       │
│  EVALUACIONES   │       │
├─────────────────┤       │
│ • id (PK)       │       │
│ • estudiante_id │───────┼─────────┐
│   (FK)          │       │         │
│ • docente_id(FK)│───────┘         │
│ • materia_id(FK)│─────────────────┘
│ • formulario_id │─────────────────┐
│   (FK)          │                 │
│ • periodo_id(FK)│─────────────┐   │
│ • estado        │             │   │
│ • fecha_inicio  │             │   │
│ • fecha_completa│             │   │
└─────────────────┘             │   │
         │                      │   │
         │                      │   │
         │                      │   │
┌─────────────────┐             │   │
│   RESPUESTAS    │             │   │
├─────────────────┤             │   │
│ • id (PK)       │             │   │
│ • evaluacion_id │─────────────┘   │
│   (FK)          │                 │
│ • pregunta_id   │─────────────┐   │
│   (FK)          │             │   │
│ • valor_numerico│             │   │
│ • valor_texto   │             │   │
│ • fecha_respuesta│            │   │
└─────────────────┘             │   │
                                │   │
┌─────────────────┐             │   │
│   PREGUNTAS     │             │   │
├─────────────────┤             │   │
│ • id (PK)       │─────────────┘   │
│ • formulario_id │─────────────────┘
│   (FK)          │
│ • texto_pregunta│
│ • tipo_pregunta │
│ • opciones_resp │
│ • escala_min    │
│ • escala_max    │
│ • es_obligatoria│
│ • orden_pregunta│
│ • ponderacion   │
│ • categoria     │
└─────────────────┘
         │
         │
         │
┌─────────────────┐
│  FORMULARIOS    │
├─────────────────┤
│ • id (PK)       │
│ • nombre        │
│ • descripcion   │
│ • tipo_evaluacion│
│ • version       │
│ • estado        │
│ • fecha_creacion│
│ • creado_por(FK)│
└─────────────────┘

┌─────────────────┐
│PERIODOS_EVALUAC │
├─────────────────┤
│ • id (PK)       │
│ • nombre        │
│ • descripcion   │
│ • fecha_inicio  │
│ • fecha_fin     │
│ • formulario_id │
│   (FK)          │
│ • estado        │
│ • creado_por(FK)│
└─────────────────┘
```

## 🌐 Diagrama de Navegación del Sistema

```
                    ┌─────────────────┐
                    │   LOGIN PAGE    │
                    └─────────┬───────┘
                              │
                    ┌─────────▼───────┐
                    │ ROLE DETECTION  │
                    └─────┬───┬───┬───┘
                          │   │   │
            ┌─────────────┘   │   └─────────────┐
            │                 │                 │
    ┌───────▼───────┐ ┌───────▼───────┐ ┌───────▼───────┐
    │   ESTUDIANTE  │ │    DOCENTE    │ │ ADMINISTRADOR │
    │   DASHBOARD   │ │   DASHBOARD   │ │   DASHBOARD   │
    └───────┬───────┘ └───────┬───────┘ └───────┬───────┘
            │                 │                 │
    ┌───────▼───────┐ ┌───────▼───────┐ ┌───────▼───────┐
    │ EVALUACIONES  │ │   REPORTES    │ │ GESTIÓN       │
    │ PENDIENTES    │ │  PERSONALES   │ │ USUARIOS      │
    └───────┬───────┘ └───────────────┘ └───────┬───────┘
            │                                   │
    ┌───────▼───────┐                 ┌───────▼───────┐
    │  FORMULARIO   │                 │ CONFIGURACIÓN │
    │  EVALUACIÓN   │                 │ FORMULARIOS   │
    └───────┬───────┘                 └───────┬───────┘
            │                                 │
    ┌───────▼───────┐                 ┌───────▼───────┐
    │ CONFIRMACIÓN  │                 │   REPORTES    │
    │    ENVÍO      │                 │   GLOBALES    │
    └───────────────┘                 └───────────────┘
```

## 📱 Wireframes de Interfaces Principales

### Dashboard Estudiante

```
┌─────────────────────────────────────────────────────────────┐
│ [LOGO] e-VALuacion              [Usuario: Juan P.] [Logout] │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  📊 DASHBOARD - ESTUDIANTE                                  │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 📝 EVALUACIONES PENDIENTES                              │ │
│  │                                                         │ │
│  │ ┌─────────────────┐ ┌─────────────────┐ ┌─────────────┐ │ │
│  │ │ Prof. García    │ │ Prof. Martínez  │ │ Prof. López │ │ │
│  │ │ Matemáticas     │ │ Física          │ │ Química     │ │ │
│  │ │ Vence: 15/Nov   │ │ Vence: 18/Nov   │ │ Vence: 20/Nov│ │ │
│  │ │ [EVALUAR]       │ │ [EVALUAR]       │ │ [EVALUAR]   │ │ │
│  │ └─────────────────┘ └─────────────────┘ └─────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ ✅ EVALUACIONES COMPLETADAS                             │ │
│  │                                                         │ │
│  │ • Prof. Rodríguez - Programación (Completada 10/Nov)   │ │
│  │ • Prof. Sánchez - Base de Datos (Completada 08/Nov)    │ │
│  │ • Prof. Torres - Redes (Completada 05/Nov)             │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Formulario de Evaluación

```
┌─────────────────────────────────────────────────────────────┐
│ [LOGO] e-VALuacion              [Usuario: Juan P.] [Logout] │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  📝 EVALUACIÓN DOCENTE - Prof. García (Matemáticas)        │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 1. METODOLOGÍA DE ENSEÑANZA                             │ │
│  │                                                         │ │
│  │ ¿Cómo califica la claridad en las explicaciones?       │ │
│  │ ○ 1 - Muy Malo  ○ 2 - Malo  ● 3 - Regular             │ │
│  │ ○ 4 - Bueno     ○ 5 - Excelente                        │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 2. PUNTUALIDAD Y ASISTENCIA                             │ │
│  │                                                         │ │
│  │ ¿El docente cumple con los horarios establecidos?      │ │
│  │ ○ 1 - Nunca     ○ 2 - Rara vez  ○ 3 - A veces         │ │
│  │ ● 4 - Casi siempre  ○ 5 - Siempre                      │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 3. COMENTARIOS ADICIONALES                              │ │
│  │                                                         │ │
│  │ ┌─────────────────────────────────────────────────────┐ │ │
│  │ │ El profesor explica muy bien los conceptos...       │ │ │
│  │ │                                                     │ │ │
│  │ └─────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  [GUARDAR BORRADOR]                        [ENVIAR EVALUACIÓN] │
└─────────────────────────────────────────────────────────────┘
```

### Dashboard Administrador

```
┌─────────────────────────────────────────────────────────────┐
│ [LOGO] e-VALuacion            [Admin: Carlos G.] [Logout]   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ⚙️ PANEL DE ADMINISTRACIÓN                                 │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 📊 MÉTRICAS GENERALES                                   │ │
│  │                                                         │ │
│  │ Total Usuarios: 1,247    Evaluaciones Completadas: 892 │ │
│  │ Docentes Activos: 45     Tasa Participación: 71.5%     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 🛠️ ACCIONES RÁPIDAS                                     │ │
│  │                                                         │ │
│  │ [CREAR USUARIO]  [NUEVO FORMULARIO]  [GENERAR REPORTE] │ │
│  │ [GESTIONAR PERÍODOS]  [CONFIGURACIÓN]  [RESPALDOS]     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ 📈 ACTIVIDAD RECIENTE                                   │ │
│  │                                                         │ │
│  │ • 15:30 - Nueva evaluación completada (Est. 12345)     │ │
│  │ • 14:45 - Usuario creado: Prof. Nuevo                  │ │
│  │ • 13:20 - Reporte generado: Período 2024-2             │ │
│  │ • 12:10 - Formulario actualizado: Evaluación Docente   │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 🔄 Diagrama de Estados - Evaluación

```
    ┌─────────────┐
    │   CREADA    │ ◄─── Estado inicial cuando se asigna
    └──────┬──────┘
           │ estudiante accede
           ▼
    ┌─────────────┐
    │  INICIADA   │ ◄─── Estudiante comenzó a llenar formulario
    └──────┬──────┘
           │ completa y envía
           ▼
    ┌─────────────┐
    │ COMPLETADA  │ ◄─── Evaluación finalizada exitosamente
    └─────────────┘
           │
           │ (opcional - solo admin)
           ▼
    ┌─────────────┐
    │  ARCHIVADA  │ ◄─── Movida a archivo histórico
    └─────────────┘

    Estados alternativos:
    
    INICIADA ──────► ┌─────────────┐
                     │ CANCELADA   │ ◄─── Admin cancela evaluación
                     └─────────────┘
    
    INICIADA ──────► ┌─────────────┐
                     │  EXPIRADA   │ ◄─── Tiempo límite vencido
                     └─────────────┘
```

## 📊 Diagrama de Flujo de Datos (DFD)

### Nivel 0 - Diagrama de Contexto

```
                    ┌─────────────┐
                    │ ESTUDIANTES │
                    └──────┬──────┘
                           │ evaluaciones
                           ▼
    ┌─────────────┐  ┌─────────────────┐  ┌─────────────┐
    │   DOCENTES  │──│   SISTEMA       │──│ADMINISTRADOR│
    │             │  │  e-VALuacion    │  │             │
    └─────────────┘  └─────────────────┘  └─────────────┘
           ▲                 │                    │
           │ reportes        │ datos              │ configuración
           └─────────────────┘                    ▼
                                         ┌─────────────┐
                                         │BASE DE DATOS│
                                         └─────────────┘
```

### Nivel 1 - Procesos Principales

```
┌─────────────┐     ┌─────────────────┐     ┌─────────────┐
│Gestionar    │────▶│   D1: Usuarios  │◀────│Autenticar   │
│Usuarios     │     └─────────────────┘     │Usuario      │
└─────────────┘                             └─────────────┘
      │                                            │
      ▼                                            ▼
┌─────────────────┐                     ┌─────────────────┐
│   D2: Materias  │                     │D3: Evaluaciones │
└─────────────────┘                     └─────────────────┘
      │                                            │
      ▼                                            ▼
┌─────────────┐     ┌─────────────────┐     ┌─────────────┐
│Procesar     │────▶│ D4: Respuestas  │◀────│Realizar     │
│Evaluaciones │     └─────────────────┘     │Evaluación   │
└─────────────┘                             └─────────────┘
      │                                            │
      ▼                                            ▼
┌─────────────────┐                     ┌─────────────────┐
│  D5: Reportes   │                     │ D6: Formularios │
└─────────────────┘                     └─────────────────┘
```

## 🎨 Paleta de Colores y Estilos

### Colores Principales

```
┌─────────────────────────────────────────────────────────────┐
│ PALETA DE COLORES e-VALuacion                               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 🔵 Azul Primario:    #2563EB (rgb(37, 99, 235))           │
│ 🟦 Azul Secundario:  #3B82F6 (rgb(59, 130, 246))          │
│ 🟢 Verde Éxito:      #10B981 (rgb(16, 185, 129))          │
│ 🟡 Amarillo Alerta:  #F59E0B (rgb(245, 158, 11))          │
│ 🔴 Rojo Error:       #EF4444 (rgb(239, 68, 68))           │
│ ⚫ Gris Texto:       #374151 (rgb(55, 65, 81))             │
│ ⚪ Gris Claro:       #F9FAFB (rgb(249, 250, 251))          │
│ ⬜ Blanco:           #FFFFFF (rgb(255, 255, 255))          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Tipografía

```
┌─────────────────────────────────────────────────────────────┐
│ TIPOGRAFÍA                                                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ Fuente Principal: 'Inter', sans-serif                      │
│ Fuente Secundaria: 'Roboto', sans-serif                    │
│                                                             │
│ H1: 2.5rem (40px) - Bold                                   │
│ H2: 2rem (32px) - Semibold                                 │
│ H3: 1.5rem (24px) - Medium                                 │
│ Body: 1rem (16px) - Regular                                │
│ Small: 0.875rem (14px) - Regular                           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## 📱 Responsive Design Breakpoints

```
┌─────────────────────────────────────────────────────────────┐
│ BREAKPOINTS RESPONSIVE                                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 📱 Mobile:    320px - 768px                                │
│    • Navegación colapsada                                   │
│    • Formularios en una columna                             │
│    • Tablas con scroll horizontal                           │
│                                                             │
│ 📟 Tablet:    768px - 1024px                               │
│    • Sidebar colapsable                                     │
│    • Formularios en dos columnas                            │
│    • Grids adaptables                                       │
│                                                             │
│ 💻 Desktop:   1024px+                                       │
│    • Layout completo                                        │
│    • Sidebar fijo                                           │
│    • Múltiples columnas                                     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

*Estos diagramas proporcionan una guía visual completa para el desarrollo del sistema e-VALuacion, facilitando la comprensión de la arquitectura, flujos de trabajo y diseño de interfaces del proyecto.*