# 📅 Cronograma del Proyecto e-VALuacion

## 📖 Introducción

Este documento presenta el cronograma detallado para el desarrollo del sistema e-VALuacion, incluyendo todas las fases del proyecto, actividades específicas, recursos asignados, dependencias y entregables. El cronograma está diseñado para un desarrollo ágil y colaborativo entre Felipe Ramos y Carlos García.

## 🎯 Información General del Proyecto

| **Campo** | **Detalle** |
|-----------|-------------|
| **Nombre del Proyecto** | Sistema e-VALuacion |
| **Duración Total** | 8 semanas (56 días) |
| **Fecha de Inicio** | 15 de Noviembre 2024 |
| **Fecha de Finalización** | 10 de Enero 2025 |
| **Equipo de Desarrollo** | Felipe Ramos, Carlos García |
| **Metodología** | Desarrollo Ágil con Sprints de 2 semanas |

## 📊 Resumen Ejecutivo del Cronograma

### Distribución de Tiempo por Fase

```
┌─────────────────────────────────────────────────────────────┐
│                    DISTRIBUCIÓN DE FASES                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 📋 Fase 1: Análisis y Diseño        ████████░░░░ 20%       │
│ 🏗️ Fase 2: Desarrollo Backend       ██████████░░ 25%       │
│ 🎨 Fase 3: Desarrollo Frontend      ██████████░░ 25%       │
│ 🔗 Fase 4: Integración y Testing    ████████░░░░ 20%       │
│ 🚀 Fase 5: Despliegue y Documentación ████░░░░░░░ 10%      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Hitos Principales

| **Hito** | **Fecha** | **Entregable** |
|----------|-----------|----------------|
| 🎯 H1 | 22/Nov/2024 | Documentación y Diseño Completo |
| 🎯 H2 | 06/Dic/2024 | Backend Funcional |
| 🎯 H3 | 20/Dic/2024 | Frontend Completo |
| 🎯 H4 | 03/Ene/2025 | Sistema Integrado y Probado |
| 🎯 H5 | 10/Ene/2025 | Despliegue Final y Documentación |

## 📋 FASE 1: Análisis y Diseño (Semanas 1-2)

### **Semana 1: 15-22 Noviembre 2024**

#### **Sprint 1.1: Documentación y Análisis**

| **Día** | **Actividad** | **Responsable** | **Duración** | **Entregable** |
|---------|---------------|-----------------|--------------|----------------|
| **Lun 18** | Análisis de requerimientos detallado | Felipe & Carlos | 4h | Documento de requerimientos |
| **Mar 19** | Diseño de arquitectura del sistema | Felipe | 6h | Diagramas de arquitectura |
| **Mié 20** | Modelado de base de datos | Carlos | 6h | Modelo ER y scripts SQL |
| **Jue 21** | Diseño de interfaces (Wireframes) | Felipe | 5h | Mockups y wireframes |
| **Vie 22** | Revisión y validación de diseños | Felipe & Carlos | 3h | Documentación aprobada |

#### **Entregables Semana 1:**
- ✅ Documento de requerimientos funcionales y no funcionales
- ✅ Diagramas de arquitectura del sistema
- ✅ Modelo de base de datos completo
- ✅ Wireframes de todas las interfaces
- ✅ Plan de desarrollo detallado

### **Semana 2: 25 Noviembre - 2 Diciembre 2024**

#### **Sprint 1.2: Preparación del Entorno**

| **Día** | **Actividad** | **Responsable** | **Duración** | **Entregable** |
|---------|---------------|-----------------|--------------|----------------|
| **Lun 25** | Configuración del repositorio Git | Carlos | 2h | Repositorio configurado |
| **Mar 26** | Estructura de carpetas del proyecto | Felipe | 3h | Estructura base |
| **Mié 27** | Configuración del entorno de desarrollo | Felipe & Carlos | 4h | Entorno listo |
| **Jue 28** | Creación de la base de datos inicial | Carlos | 5h | BD con estructura básica |
| **Vie 29** | Prototipo de autenticación | Felipe | 6h | Login básico funcional |

#### **Entregables Semana 2:**
- ✅ Repositorio Git configurado con ramas de desarrollo
- ✅ Estructura de proyecto organizada
- ✅ Base de datos SQLite con tablas principales
- ✅ Sistema de autenticación básico
- ✅ Documentación técnica inicial

## 🏗️ FASE 2: Desarrollo Backend (Semanas 3-4)

### **Semana 3: 2-9 Diciembre 2024**

#### **Sprint 2.1: Core Backend**

| **Día** | **Actividad** | **Responsable** | **Duración** | **Entregable** |
|---------|---------------|-----------------|--------------|----------------|
| **Lun 2** | API de gestión de usuarios | Carlos | 6h | CRUD usuarios completo |
| **Mar 3** | API de gestión de materias y programas | Carlos | 5h | CRUD materias/programas |
| **Mié 4** | Sistema de roles y permisos | Felipe | 6h | Middleware de autorización |
| **Jue 5** | API de formularios de evaluación | Felipe | 6h | CRUD formularios |
| **Vie 6** | Validaciones y middleware de seguridad | Felipe & Carlos | 4h | Validaciones implementadas |

#### **Entregables Semana 3:**
- ✅ APIs REST para gestión de usuarios
- ✅ Sistema de roles y permisos funcional
- ✅ APIs para materias y programas académicos
- ✅ Sistema de formularios dinámicos
- ✅ Middleware de seguridad y validaciones

### **Semana 4: 9-16 Diciembre 2024**

#### **Sprint 2.2: Lógica de Evaluaciones**

| **Día** | **Actividad** | **Responsable** | **Duración** | **Entregable** |
|---------|---------------|-----------------|--------------|----------------|
| **Lun 9** | API de evaluaciones (crear, listar) | Carlos | 6h | API evaluaciones básica |
| **Mar 10** | Sistema de respuestas y calificaciones | Felipe | 6h | Procesamiento respuestas |
| **Mié 11** | Generación de reportes automáticos | Carlos | 5h | Motor de reportes |
| **Jue 12** | Sistema de notificaciones | Felipe | 4h | Notificaciones básicas |
| **Vie 13** | Testing y depuración del backend | Felipe & Carlos | 6h | Backend estable |

#### **Entregables Semana 4:**
- ✅ Sistema completo de evaluaciones
- ✅ Procesamiento y almacenamiento de respuestas
- ✅ Generador automático de reportes
- ✅ Sistema de notificaciones
- ✅ Backend completamente funcional y probado

## 🎨 FASE 3: Desarrollo Frontend (Semanas 5-6)

### **Semana 5: 16-23 Diciembre 2024**

#### **Sprint 3.1: Interfaces Principales**

| **Día** | **Actividad** | **Responsable** | **Duración** | **Entregable** |
|---------|---------------|-----------------|--------------|----------------|
| **Lun 16** | Estructura HTML base y navegación | Felipe | 5h | Layout principal |
| **Mar 17** | Estilos CSS y diseño responsive | Carlos | 6h | CSS framework propio |
| **Mié 18** | Página de login y autenticación | Felipe | 5h | Login funcional |
| **Jue 19** | Dashboard para estudiantes | Carlos | 6h | Dashboard estudiante |
| **Vie 20** | Dashboard para docentes | Felipe | 6h | Dashboard docente |

#### **Entregables Semana 5:**
- ✅ Estructura HTML semántica y accesible
- ✅ Sistema de estilos CSS responsive
- ✅ Interfaz de autenticación completa
- ✅ Dashboards diferenciados por rol
- ✅ Navegación intuitiva y funcional

### **Semana 6: 23-30 Diciembre 2024**

#### **Sprint 3.2: Funcionalidades Avanzadas**

| **Día** | **Actividad** | **Responsable** | **Duración** | **Entregable** |
|---------|---------------|-----------------|--------------|----------------|
| **Lun 23** | Formularios de evaluación dinámicos | Carlos | 6h | Formularios interactivos |
| **Mar 24** | Sistema de reportes y gráficos | Felipe | 5h | Visualización de datos |
| **Mié 25** | **🎄 DESCANSO NAVIDAD** | - | - | - |
| **Jue 26** | Panel de administración | Carlos | 6h | Admin panel completo |
| **Vie 27** | Optimización y pulimiento UI/UX | Felipe & Carlos | 5h | Interfaz optimizada |

#### **Entregables Semana 6:**
- ✅ Formularios de evaluación completamente funcionales
- ✅ Sistema de reportes con gráficos interactivos
- ✅ Panel de administración completo
- ✅ Interfaz optimizada y pulida
- ✅ Frontend completamente funcional

## 🔗 FASE 4: Integración y Testing (Semanas 7-8)

### **Semana 7: 30 Diciembre - 6 Enero 2025**

#### **Sprint 4.1: Integración y Pruebas**

| **Día** | **Actividad** | **Responsable** | **Duración** | **Entregable** |
|---------|---------------|-----------------|--------------|----------------|
| **Lun 30** | Integración Frontend-Backend | Felipe & Carlos | 6h | Sistema integrado |
| **Mar 31** | **🎊 DESCANSO AÑO NUEVO** | - | - | - |
| **Mié 1** | Testing de funcionalidades principales | Carlos | 6h | Casos de prueba |
| **Jue 2** | Corrección de bugs y optimizaciones | Felipe | 6h | Sistema estable |
| **Vie 3** | Testing de seguridad y rendimiento | Felipe & Carlos | 5h | Pruebas de seguridad |

#### **Entregables Semana 7:**
- ✅ Sistema completamente integrado
- ✅ Batería de pruebas ejecutadas
- ✅ Bugs principales corregidos
- ✅ Optimizaciones de rendimiento
- ✅ Validaciones de seguridad completadas

### **Semana 8: 6-10 Enero 2025**

#### **Sprint 4.2: Finalización y Despliegue**

| **Día** | **Actividad** | **Responsable** | **Duración** | **Entregable** |
|---------|---------------|-----------------|--------------|----------------|
| **Lun 6** | Preparación para despliegue | Carlos | 4h | Scripts de despliegue |
| **Mar 7** | Despliegue en GitHub Pages | Felipe | 3h | Sistema desplegado |
| **Mié 8** | Documentación final del usuario | Felipe & Carlos | 5h | Manual de usuario |
| **Jue 9** | Testing final y ajustes | Felipe & Carlos | 4h | Sistema final |
| **Vie 10** | Presentación y entrega final | Felipe & Carlos | 3h | Proyecto entregado |

#### **Entregables Semana 8:**
- ✅ Sistema desplegado y accesible
- ✅ Documentación completa del usuario
- ✅ Manual de instalación y configuración
- ✅ Presentación del proyecto
- ✅ Entrega final completada

## 📊 Matriz de Responsabilidades (RACI)

| **Actividad** | **Felipe Ramos** | **Carlos García** |
|---------------|------------------|-------------------|
| **Análisis de Requerimientos** | R, A | R, A |
| **Diseño de Arquitectura** | R, A | C, I |
| **Modelado de Base de Datos** | C, I | R, A |
| **Desarrollo Backend** | R, A | R, A |
| **Desarrollo Frontend** | R, A | R, A |
| **Testing y QA** | R, A | R, A |
| **Documentación** | R, A | R, A |
| **Despliegue** | C, I | R, A |

**Leyenda RACI:**
- **R** (Responsible): Responsable de ejecutar
- **A** (Accountable): Responsable final/aprobador
- **C** (Consulted): Consultado
- **I** (Informed): Informado

## 🛠️ Recursos y Herramientas

### **Herramientas de Desarrollo**

| **Categoría** | **Herramienta** | **Propósito** |
|---------------|-----------------|---------------|
| **Control de Versiones** | Git + GitHub | Gestión de código fuente |
| **Editor de Código** | VS Code | Desarrollo |
| **Base de Datos** | SQLite | Almacenamiento de datos |
| **Testing** | Jest / Manual Testing | Pruebas de funcionalidad |
| **Documentación** | Markdown | Documentación técnica |
| **Despliegue** | GitHub Pages | Hosting del proyecto |

### **Tecnologías del Stack**

| **Capa** | **Tecnología** | **Versión** |
|----------|----------------|-------------|
| **Frontend** | HTML5 | Estándar |
| **Estilos** | CSS3 | Estándar |
| **Interactividad** | JavaScript (ES6+) | Moderno |
| **Base de Datos** | SQLite | 3.x |
| **Control de Versiones** | Git | 2.x |

## ⚠️ Gestión de Riesgos

### **Riesgos Identificados y Mitigación**

| **Riesgo** | **Probabilidad** | **Impacto** | **Mitigación** |
|------------|------------------|-------------|----------------|
| **Retrasos por complejidad técnica** | Media | Alto | Buffer de tiempo en cada sprint |
| **Problemas de integración** | Baja | Alto | Testing continuo durante desarrollo |
| **Disponibilidad del equipo** | Media | Medio | Comunicación diaria y flexibilidad |
| **Cambios en requerimientos** | Baja | Medio | Documentación clara y aprobada |
| **Problemas de despliegue** | Baja | Alto | Pruebas de despliegue tempranas |

### **Plan de Contingencia**

```
┌─────────────────────────────────────────────────────────────┐
│                    PLAN DE CONTINGENCIA                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 🚨 Si hay retraso de 1-2 días:                            │
│    • Redistribuir tareas entre el equipo                   │
│    • Trabajar horas adicionales si es necesario            │
│                                                             │
│ 🚨 Si hay retraso de 3-5 días:                            │
│    • Reducir alcance de funcionalidades no críticas        │
│    • Priorizar MVP (Minimum Viable Product)                │
│                                                             │
│ 🚨 Si hay retraso mayor a 1 semana:                       │
│    • Reevaluar cronograma completo                         │
│    • Solicitar extensión de plazo si es posible            │
│    • Entregar versión reducida pero funcional              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## 📈 Métricas de Seguimiento

### **KPIs del Proyecto**

| **Métrica** | **Objetivo** | **Frecuencia** |
|-------------|--------------|----------------|
| **Porcentaje de Completitud** | 100% | Semanal |
| **Bugs Encontrados/Resueltos** | <5 bugs críticos | Diario |
| **Cobertura de Testing** | >80% | Por sprint |
| **Tiempo de Respuesta** | <2 segundos | Al final |
| **Satisfacción del Usuario** | >4/5 | Al entregar |

### **Dashboard de Progreso**

```
Semana 1: ████████████████████████████████████████ 100%
Semana 2: ████████████████████████████████████████ 100%
Semana 3: ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   0%
Semana 4: ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   0%
Semana 5: ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   0%
Semana 6: ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   0%
Semana 7: ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   0%
Semana 8: ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   0%

Progreso General: ████████░░░░░░░░░░░░░░░░░░░░░░░░░░ 25%
```

## 📋 Lista de Verificación (Checklist)

### **Entregables por Fase**

#### **Fase 1: Análisis y Diseño**
- [ ] Documento de requerimientos aprobado
- [ ] Diagramas de arquitectura completados
- [ ] Modelo de base de datos validado
- [ ] Wireframes de todas las interfaces
- [ ] Cronograma detallado aprobado

#### **Fase 2: Desarrollo Backend**
- [ ] APIs REST implementadas y probadas
- [ ] Sistema de autenticación funcional
- [ ] Base de datos con datos de prueba
- [ ] Validaciones y seguridad implementadas
- [ ] Documentación de APIs completada

#### **Fase 3: Desarrollo Frontend**
- [ ] Todas las interfaces implementadas
- [ ] Diseño responsive verificado
- [ ] Interactividad JavaScript funcional
- [ ] Integración con APIs probada
- [ ] Optimización de rendimiento realizada

#### **Fase 4: Integración y Testing**
- [ ] Sistema completamente integrado
- [ ] Todas las pruebas ejecutadas exitosamente
- [ ] Bugs críticos resueltos
- [ ] Documentación de usuario completada
- [ ] Sistema desplegado y accesible

## 📞 Comunicación y Reuniones

### **Calendario de Reuniones**

| **Tipo de Reunión** | **Frecuencia** | **Duración** | **Participantes** |
|---------------------|----------------|--------------|-------------------|
| **Daily Standup** | Diario | 15 min | Felipe & Carlos |
| **Sprint Planning** | Inicio de sprint | 1 hora | Felipe & Carlos |
| **Sprint Review** | Final de sprint | 1 hora | Felipe & Carlos |
| **Retrospectiva** | Final de sprint | 30 min | Felipe & Carlos |

### **Canales de Comunicación**

- **WhatsApp**: Comunicación diaria y urgente
- **GitHub Issues**: Seguimiento de tareas y bugs
- **GitHub Discussions**: Decisiones técnicas
- **Reuniones Presenciales**: Planificación y revisiones importantes

## 🎯 Criterios de Éxito

### **Criterios de Aceptación del Proyecto**

1. **Funcionalidad Completa**
   - ✅ Sistema de autenticación operativo
   - ✅ Evaluaciones funcionales para estudiantes
   - ✅ Reportes automáticos para docentes
   - ✅ Panel administrativo completo

2. **Calidad Técnica**
   - ✅ Código limpio y bien documentado
   - ✅ Base de datos normalizada y optimizada
   - ✅ Interfaz responsive y accesible
   - ✅ Seguridad implementada correctamente

3. **Entrega y Documentación**
   - ✅ Sistema desplegado y accesible
   - ✅ Documentación técnica completa
   - ✅ Manual de usuario disponible
   - ✅ Código fuente en repositorio Git

---

*Este cronograma será actualizado semanalmente para reflejar el progreso real del proyecto y cualquier ajuste necesario en las fechas o actividades planificadas.*