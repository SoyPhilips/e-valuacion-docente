# 🗄️ Modelos de Datos - Sistema e-VALuacion

## 📖 Introducción

Este documento presenta el diseño detallado de la base de datos del sistema e-VALuacion, incluyendo el modelo conceptual, lógico y físico. La base de datos está diseñada para ser eficiente, escalable y mantener la integridad de los datos de evaluación docente.

## 🎯 Objetivos del Diseño

### Objetivos Principales
- **Integridad de Datos**: Garantizar consistencia y validez de la información
- **Rendimiento Óptimo**: Consultas eficientes para reportes y analytics
- **Escalabilidad**: Soporte para crecimiento futuro de usuarios y datos
- **Seguridad**: Protección de información sensible y personal
- **Trazabilidad**: Auditoría completa de cambios y accesos

### Principios de Diseño
- **Normalización**: Eliminación de redundancia de datos
- **Flexibilidad**: Adaptabilidad a nuevos tipos de evaluación
- **Simplicidad**: Estructura clara y mantenible
- **Eficiencia**: Optimización para operaciones frecuentes

## 🏗️ Arquitectura de Base de Datos

### Tecnología Seleccionada: SQLite

#### Justificación de la Elección
- **Simplicidad de Despliegue**: No requiere servidor de base de datos separado
- **Portabilidad**: Base de datos en archivo único, fácil de respaldar
- **Rendimiento**: Excelente para aplicaciones de tamaño medio
- **Compatibilidad**: Soporte nativo en JavaScript/Node.js
- **Desarrollo Local**: Ideal para prototipado y desarrollo inicial

#### Limitaciones Consideradas
- **Concurrencia**: Limitada para escrituras simultáneas masivas
- **Escalabilidad**: Apropiada hasta ~100GB de datos
- **Funcionalidades**: Menos características avanzadas que PostgreSQL/MySQL

### Estrategia de Migración Futura
Para escalabilidad futura, el diseño permite migración a:
- **PostgreSQL**: Para mayor concurrencia y funcionalidades avanzadas
- **MySQL**: Para compatibilidad con hosting compartido
- **MongoDB**: Para datos no estructurados y analytics avanzados

## 📊 Modelo Conceptual

### Entidades Principales

#### 👤 Usuario
- Representa a todos los actores del sistema
- Incluye estudiantes, docentes y administradores
- Contiene información personal y de autenticación

#### 🎓 Programa Académico
- Representa carreras o programas de estudio
- Agrupa materias relacionadas
- Facilita reportes por área académica

#### 📚 Materia
- Representa asignaturas específicas
- Asociada a programas académicos
- Impartida por docentes específicos

#### 📝 Formulario de Evaluación
- Plantilla para diferentes tipos de evaluación
- Configurable por administradores
- Reutilizable para múltiples períodos

#### ❓ Pregunta
- Elementos individuales de los formularios
- Diferentes tipos (escala, múltiple, texto)
- Configuración de validación y ponderación

#### 📋 Evaluación
- Instancia específica de evaluación completada
- Vincula estudiante, docente, materia y período
- Contiene todas las respuestas del formulario

#### 💬 Respuesta
- Respuesta individual a una pregunta específica
- Almacena valor numérico o textual
- Incluye metadatos de auditoría

#### 📅 Período de Evaluación
- Define ventanas temporales para evaluaciones
- Controla disponibilidad de formularios
- Facilita organización por semestres/trimestres

## 🔗 Modelo Lógico

### Diagrama Entidad-Relación

```
[Usuario] ||--o{ [Evaluacion] : realiza/recibe
[Usuario] ||--o{ [Materia] : imparte
[Usuario] }o--|| [Programa] : pertenece_a

[Materia] ||--o{ [Evaluacion] : es_evaluada_en
[Materia] }o--|| [Programa] : pertenece_a

[Formulario] ||--o{ [Pregunta] : contiene
[Formulario] ||--o{ [Evaluacion] : utiliza

[Evaluacion] ||--o{ [Respuesta] : contiene
[Pregunta] ||--o{ [Respuesta] : responde_a

[Periodo] ||--o{ [Evaluacion] : ocurre_en
```

### Relaciones Principales

#### Usuario - Evaluación (1:N)
- Un usuario puede realizar múltiples evaluaciones (como estudiante)
- Un usuario puede recibir múltiples evaluaciones (como docente)
- Relación polimórfica manejada por campos de tipo

#### Formulario - Pregunta (1:N)
- Un formulario contiene múltiples preguntas
- Las preguntas pueden reutilizarse en diferentes formularios
- Orden de preguntas controlado por campo secuencial

#### Evaluación - Respuesta (1:N)
- Una evaluación contiene múltiples respuestas
- Cada respuesta corresponde a una pregunta específica
- Integridad referencial estricta

## 🗃️ Modelo Físico - Estructura de Tablas

### Tabla: usuarios

```sql
CREATE TABLE usuarios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    codigo_estudiante VARCHAR(20) UNIQUE,
    nombres VARCHAR(100) NOT NULL,
    apellidos VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    tipo_usuario ENUM('estudiante', 'docente', 'administrador') NOT NULL,
    programa_id INTEGER,
    estado ENUM('activo', 'inactivo', 'suspendido') DEFAULT 'activo',
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    fecha_ultimo_acceso DATETIME,
    intentos_fallidos INTEGER DEFAULT 0,
    bloqueado_hasta DATETIME NULL,
    
    FOREIGN KEY (programa_id) REFERENCES programas(id),
    INDEX idx_email (email),
    INDEX idx_codigo (codigo_estudiante),
    INDEX idx_tipo (tipo_usuario)
);
```

### Tabla: programas

```sql
CREATE TABLE programas (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    codigo VARCHAR(10) UNIQUE NOT NULL,
    nombre VARCHAR(200) NOT NULL,
    descripcion TEXT,
    facultad VARCHAR(100),
    estado ENUM('activo', 'inactivo') DEFAULT 'activo',
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    INDEX idx_codigo (codigo),
    INDEX idx_estado (estado)
);
```

### Tabla: materias

```sql
CREATE TABLE materias (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    codigo VARCHAR(15) UNIQUE NOT NULL,
    nombre VARCHAR(200) NOT NULL,
    descripcion TEXT,
    creditos INTEGER,
    programa_id INTEGER NOT NULL,
    docente_id INTEGER,
    semestre INTEGER,
    estado ENUM('activo', 'inactivo') DEFAULT 'activo',
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    FOREIGN KEY (programa_id) REFERENCES programas(id),
    FOREIGN KEY (docente_id) REFERENCES usuarios(id),
    INDEX idx_codigo (codigo),
    INDEX idx_programa (programa_id),
    INDEX idx_docente (docente_id)
);
```

### Tabla: formularios

```sql
CREATE TABLE formularios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre VARCHAR(200) NOT NULL,
    descripcion TEXT,
    tipo_evaluacion ENUM('examen', 'tarea', 'proyecto', 'docente') NOT NULL,
    version VARCHAR(10) DEFAULT '1.0',
    estado ENUM('borrador', 'activo', 'archivado') DEFAULT 'borrador',
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    fecha_activacion DATETIME,
    creado_por INTEGER,
    
    FOREIGN KEY (creado_por) REFERENCES usuarios(id),
    INDEX idx_tipo (tipo_evaluacion),
    INDEX idx_estado (estado)
);
```

### Tabla: preguntas

```sql
CREATE TABLE preguntas (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    formulario_id INTEGER NOT NULL,
    texto_pregunta TEXT NOT NULL,
    tipo_pregunta ENUM('escala_likert', 'opcion_multiple', 'texto_libre', 'numerica') NOT NULL,
    opciones_respuesta JSON, -- Para preguntas de opción múltiple
    escala_minima INTEGER DEFAULT 1,
    escala_maxima INTEGER DEFAULT 5,
    es_obligatoria BOOLEAN DEFAULT TRUE,
    orden_pregunta INTEGER NOT NULL,
    ponderacion DECIMAL(3,2) DEFAULT 1.00,
    categoria VARCHAR(50), -- Ej: "metodologia", "puntualidad", "comunicacion"
    
    FOREIGN KEY (formulario_id) REFERENCES formularios(id) ON DELETE CASCADE,
    INDEX idx_formulario (formulario_id),
    INDEX idx_orden (formulario_id, orden_pregunta),
    INDEX idx_categoria (categoria)
);
```

### Tabla: periodos_evaluacion

```sql
CREATE TABLE periodos_evaluacion (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre VARCHAR(100) NOT NULL,
    descripcion TEXT,
    fecha_inicio DATE NOT NULL,
    fecha_fin DATE NOT NULL,
    formulario_id INTEGER NOT NULL,
    estado ENUM('programado', 'activo', 'finalizado', 'cancelado') DEFAULT 'programado',
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    creado_por INTEGER,
    
    FOREIGN KEY (formulario_id) REFERENCES formularios(id),
    FOREIGN KEY (creado_por) REFERENCES usuarios(id),
    INDEX idx_fechas (fecha_inicio, fecha_fin),
    INDEX idx_estado (estado)
);
```

### Tabla: evaluaciones

```sql
CREATE TABLE evaluaciones (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    estudiante_id INTEGER NOT NULL,
    docente_id INTEGER NOT NULL,
    materia_id INTEGER NOT NULL,
    formulario_id INTEGER NOT NULL,
    periodo_id INTEGER NOT NULL,
    estado ENUM('iniciada', 'completada', 'cancelada') DEFAULT 'iniciada',
    fecha_inicio DATETIME DEFAULT CURRENT_TIMESTAMP,
    fecha_completada DATETIME,
    tiempo_total_minutos INTEGER,
    ip_address VARCHAR(45),
    user_agent TEXT,
    
    FOREIGN KEY (estudiante_id) REFERENCES usuarios(id),
    FOREIGN KEY (docente_id) REFERENCES usuarios(id),
    FOREIGN KEY (materia_id) REFERENCES materias(id),
    FOREIGN KEY (formulario_id) REFERENCES formularios(id),
    FOREIGN KEY (periodo_id) REFERENCES periodos_evaluacion(id),
    
    UNIQUE KEY unique_evaluacion (estudiante_id, docente_id, materia_id, periodo_id),
    INDEX idx_estudiante (estudiante_id),
    INDEX idx_docente (docente_id),
    INDEX idx_materia (materia_id),
    INDEX idx_periodo (periodo_id),
    INDEX idx_estado (estado)
);
```

### Tabla: respuestas

```sql
CREATE TABLE respuestas (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    evaluacion_id INTEGER NOT NULL,
    pregunta_id INTEGER NOT NULL,
    valor_numerico DECIMAL(5,2),
    valor_texto TEXT,
    fecha_respuesta DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    FOREIGN KEY (evaluacion_id) REFERENCES evaluaciones(id) ON DELETE CASCADE,
    FOREIGN KEY (pregunta_id) REFERENCES preguntas(id),
    
    UNIQUE KEY unique_respuesta (evaluacion_id, pregunta_id),
    INDEX idx_evaluacion (evaluacion_id),
    INDEX idx_pregunta (pregunta_id)
);
```

### Tabla: logs_auditoria

```sql
CREATE TABLE logs_auditoria (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    usuario_id INTEGER,
    accion VARCHAR(50) NOT NULL,
    tabla_afectada VARCHAR(50),
    registro_id INTEGER,
    datos_anteriores JSON,
    datos_nuevos JSON,
    ip_address VARCHAR(45),
    user_agent TEXT,
    fecha_accion DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id),
    INDEX idx_usuario (usuario_id),
    INDEX idx_fecha (fecha_accion),
    INDEX idx_accion (accion),
    INDEX idx_tabla (tabla_afectada)
);
```

## 📈 Vistas y Consultas Optimizadas

### Vista: resumen_evaluaciones_docente

```sql
CREATE VIEW resumen_evaluaciones_docente AS
SELECT 
    d.id as docente_id,
    d.nombres || ' ' || d.apellidos as nombre_docente,
    m.nombre as materia,
    p.nombre as programa,
    COUNT(e.id) as total_evaluaciones,
    AVG(r.valor_numerico) as promedio_general,
    MIN(r.valor_numerico) as calificacion_minima,
    MAX(r.valor_numerico) as calificacion_maxima,
    pe.nombre as periodo
FROM usuarios d
JOIN materias m ON d.id = m.docente_id
JOIN programas p ON m.programa_id = p.id
JOIN evaluaciones e ON d.id = e.docente_id AND m.id = e.materia_id
JOIN respuestas r ON e.id = r.evaluacion_id
JOIN periodos_evaluacion pe ON e.periodo_id = pe.id
WHERE d.tipo_usuario = 'docente' 
  AND e.estado = 'completada'
  AND r.valor_numerico IS NOT NULL
GROUP BY d.id, m.id, pe.id;
```

### Vista: estadisticas_participacion

```sql
CREATE VIEW estadisticas_participacion AS
SELECT 
    pe.id as periodo_id,
    pe.nombre as periodo,
    p.nombre as programa,
    COUNT(DISTINCT u.id) as estudiantes_inscritos,
    COUNT(DISTINCT e.estudiante_id) as estudiantes_participantes,
    ROUND(
        (COUNT(DISTINCT e.estudiante_id) * 100.0 / COUNT(DISTINCT u.id)), 2
    ) as porcentaje_participacion
FROM periodos_evaluacion pe
CROSS JOIN programas p
LEFT JOIN usuarios u ON u.programa_id = p.id AND u.tipo_usuario = 'estudiante'
LEFT JOIN evaluaciones e ON e.estudiante_id = u.id 
    AND e.periodo_id = pe.id 
    AND e.estado = 'completada'
GROUP BY pe.id, p.id;
```

## 🔧 Índices y Optimización

### Índices Principales

```sql
-- Índices para mejorar rendimiento de consultas frecuentes
CREATE INDEX idx_evaluaciones_docente_periodo ON evaluaciones(docente_id, periodo_id);
CREATE INDEX idx_respuestas_valor ON respuestas(valor_numerico) WHERE valor_numerico IS NOT NULL;
CREATE INDEX idx_usuarios_activos ON usuarios(estado) WHERE estado = 'activo';
CREATE INDEX idx_evaluaciones_completadas ON evaluaciones(estado, fecha_completada) WHERE estado = 'completada';

-- Índices compuestos para reportes
CREATE INDEX idx_evaluacion_completa ON evaluaciones(docente_id, materia_id, periodo_id, estado);
CREATE INDEX idx_respuesta_analisis ON respuestas(pregunta_id, valor_numerico) WHERE valor_numerico IS NOT NULL;
```

### Estrategias de Optimización

#### Particionamiento por Período
```sql
-- Para bases de datos más grandes, considerar particionamiento
-- Ejemplo conceptual (no soportado nativamente en SQLite)
CREATE TABLE evaluaciones_2024_1 AS SELECT * FROM evaluaciones WHERE periodo_id IN (SELECT id FROM periodos_evaluacion WHERE fecha_inicio >= '2024-01-01' AND fecha_inicio < '2024-07-01');
```

#### Archivado de Datos Históricos
```sql
-- Procedimiento para archivar datos antiguos
CREATE TABLE evaluaciones_archivo AS SELECT * FROM evaluaciones WHERE 1=0;
-- Mover evaluaciones de más de 2 años a tabla de archivo
INSERT INTO evaluaciones_archivo SELECT * FROM evaluaciones WHERE fecha_completada < date('now', '-2 years');
```

## 🛡️ Seguridad y Integridad

### Restricciones de Integridad

```sql
-- Triggers para mantener integridad de datos
CREATE TRIGGER validar_evaluacion_unica
BEFORE INSERT ON evaluaciones
FOR EACH ROW
WHEN EXISTS (
    SELECT 1 FROM evaluaciones 
    WHERE estudiante_id = NEW.estudiante_id 
      AND docente_id = NEW.docente_id 
      AND materia_id = NEW.materia_id 
      AND periodo_id = NEW.periodo_id
      AND estado IN ('iniciada', 'completada')
)
BEGIN
    SELECT RAISE(ABORT, 'Ya existe una evaluación para este estudiante, docente y materia en el período actual');
END;
```

### Auditoría Automática

```sql
-- Trigger para auditoría de cambios en evaluaciones
CREATE TRIGGER auditoria_evaluaciones
AFTER UPDATE ON evaluaciones
FOR EACH ROW
BEGIN
    INSERT INTO logs_auditoria (
        usuario_id, accion, tabla_afectada, registro_id, 
        datos_anteriores, datos_nuevos, fecha_accion
    ) VALUES (
        NEW.estudiante_id, 'UPDATE', 'evaluaciones', NEW.id,
        json_object('estado', OLD.estado, 'fecha_completada', OLD.fecha_completada),
        json_object('estado', NEW.estado, 'fecha_completada', NEW.fecha_completada),
        CURRENT_TIMESTAMP
    );
END;
```

## 📊 Consultas de Análisis Frecuentes

### Reporte de Desempeño por Docente

```sql
SELECT 
    d.nombres || ' ' || d.apellidos as docente,
    m.nombre as materia,
    COUNT(e.id) as total_evaluaciones,
    ROUND(AVG(r.valor_numerico), 2) as promedio_general,
    ROUND(
        AVG(CASE WHEN pr.categoria = 'metodologia' THEN r.valor_numerico END), 2
    ) as promedio_metodologia,
    ROUND(
        AVG(CASE WHEN pr.categoria = 'comunicacion' THEN r.valor_numerico END), 2
    ) as promedio_comunicacion,
    ROUND(
        AVG(CASE WHEN pr.categoria = 'puntualidad' THEN r.valor_numerico END), 2
    ) as promedio_puntualidad
FROM usuarios d
JOIN evaluaciones e ON d.id = e.docente_id
JOIN materias m ON e.materia_id = m.id
JOIN respuestas r ON e.id = r.evaluacion_id
JOIN preguntas pr ON r.pregunta_id = pr.id
WHERE d.tipo_usuario = 'docente' 
  AND e.estado = 'completada'
  AND r.valor_numerico IS NOT NULL
GROUP BY d.id, m.id
ORDER BY promedio_general DESC;
```

### Análisis de Tendencias Temporales

```sql
SELECT 
    pe.nombre as periodo,
    d.nombres || ' ' || d.apellidos as docente,
    ROUND(AVG(r.valor_numerico), 2) as promedio,
    COUNT(e.id) as num_evaluaciones,
    RANK() OVER (PARTITION BY pe.id ORDER BY AVG(r.valor_numerico) DESC) as ranking_periodo
FROM periodos_evaluacion pe
JOIN evaluaciones e ON pe.id = e.periodo_id
JOIN usuarios d ON e.docente_id = d.id
JOIN respuestas r ON e.id = r.evaluacion_id
WHERE e.estado = 'completada' 
  AND r.valor_numerico IS NOT NULL
GROUP BY pe.id, d.id
ORDER BY pe.fecha_inicio DESC, promedio DESC;
```

## 🔄 Procedimientos de Mantenimiento

### Respaldo de Base de Datos

```sql
-- Script para respaldo completo
.backup 'backup_evaluaciones_' || date('now') || '.db'

-- Respaldo incremental (solo cambios recientes)
CREATE TABLE backup_log (
    tabla VARCHAR(50),
    ultimo_backup DATETIME,
    registros_respaldados INTEGER
);
```

### Limpieza de Datos

```sql
-- Limpieza de sesiones expiradas
DELETE FROM logs_auditoria 
WHERE fecha_accion < date('now', '-1 year');

-- Limpieza de evaluaciones incompletas antiguas
DELETE FROM evaluaciones 
WHERE estado = 'iniciada' 
  AND fecha_inicio < date('now', '-30 days');
```

## 📈 Métricas de Rendimiento

### Consultas de Monitoreo

```sql
-- Tamaño de tablas principales
SELECT 
    name as tabla,
    COUNT(*) as registros
FROM sqlite_master 
WHERE type = 'table' 
  AND name NOT LIKE 'sqlite_%';

-- Evaluaciones por estado
SELECT 
    estado,
    COUNT(*) as cantidad,
    ROUND(COUNT(*) * 100.0 / (SELECT COUNT(*) FROM evaluaciones), 2) as porcentaje
FROM evaluaciones 
GROUP BY estado;

-- Actividad por período
SELECT 
    pe.nombre as periodo,
    COUNT(e.id) as evaluaciones_completadas,
    COUNT(DISTINCT e.estudiante_id) as estudiantes_participantes,
    COUNT(DISTINCT e.docente_id) as docentes_evaluados
FROM periodos_evaluacion pe
LEFT JOIN evaluaciones e ON pe.id = e.periodo_id AND e.estado = 'completada'
GROUP BY pe.id
ORDER BY pe.fecha_inicio DESC;
```

## ✅ Validación del Modelo

### Casos de Prueba de Integridad

1. **Evaluación Duplicada**: Verificar que no se permitan evaluaciones duplicadas
2. **Referencia Circular**: Confirmar que no existan referencias circulares
3. **Eliminación en Cascada**: Validar comportamiento al eliminar registros padre
4. **Restricciones de Dominio**: Probar valores fuera de rangos permitidos

### Pruebas de Rendimiento

1. **Carga de Datos**: Inserción de 10,000 evaluaciones con respuestas
2. **Consultas Complejas**: Reportes con múltiples JOINs y agregaciones
3. **Concurrencia**: Múltiples usuarios realizando evaluaciones simultáneamente
4. **Respaldo/Restauración**: Tiempo de operaciones de mantenimiento

---

*Este modelo de datos proporciona una base sólida y escalable para el sistema e-VALuacion, balanceando eficiencia, integridad y flexibilidad para futuras expansiones del sistema.*