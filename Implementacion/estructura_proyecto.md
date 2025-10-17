# 🏗️ Estructura del Proyecto e-VALuacion

## 📖 Introducción

Este documento detalla la estructura completa del proyecto e-VALuacion, incluyendo la organización de archivos, configuración del entorno de desarrollo, arquitectura de carpetas y las mejores prácticas para el desarrollo colaborativo entre Felipe Ramos y Carlos García.

## 📁 Estructura de Directorios

```
e-VALuacion/
├── 📁 docs/                          # Documentación del proyecto
│   ├── 📄 README.md                  # Documentación principal
│   ├── 📄 introduccion.md            # Introducción y contexto
│   ├── 📄 requerimientos.md          # Análisis de requerimientos
│   ├── 📄 casos_uso.md               # Casos de uso detallados
│   ├── 📄 modelos_datos.md           # Modelos de base de datos
│   ├── 📄 diagramas.md               # Diagramas del sistema
│   └── 📄 cronograma.md              # Cronograma del proyecto
│
├── 📁 src/                           # Código fuente principal
│   ├── 📁 frontend/                  # Aplicación frontend
│   │   ├── 📁 assets/                # Recursos estáticos
│   │   │   ├── 📁 css/               # Hojas de estilo
│   │   │   │   ├── 📄 main.css       # Estilos principales
│   │   │   │   ├── 📄 components.css # Estilos de componentes
│   │   │   │   ├── 📄 responsive.css # Estilos responsive
│   │   │   │   └── 📄 themes.css     # Temas y variables
│   │   │   ├── 📁 js/                # Scripts JavaScript
│   │   │   │   ├── 📄 app.js         # Aplicación principal
│   │   │   │   ├── 📄 auth.js        # Autenticación
│   │   │   │   ├── 📄 dashboard.js   # Dashboard
│   │   │   │   ├── 📄 evaluations.js # Evaluaciones
│   │   │   │   ├── 📄 reports.js     # Reportes
│   │   │   │   ├── 📄 admin.js       # Administración
│   │   │   │   └── 📄 utils.js       # Utilidades
│   │   │   ├── 📁 images/            # Imágenes y gráficos
│   │   │   │   ├── 📄 logo.svg       # Logo del sistema
│   │   │   │   ├── 📄 icons.svg      # Iconos SVG
│   │   │   │   └── 📁 avatars/       # Avatares de usuario
│   │   │   └── 📁 fonts/             # Fuentes personalizadas
│   │   ├── 📁 components/            # Componentes reutilizables
│   │   │   ├── 📄 header.html        # Cabecera del sitio
│   │   │   ├── 📄 sidebar.html       # Barra lateral
│   │   │   ├── 📄 footer.html        # Pie de página
│   │   │   ├── 📄 modal.html         # Componente modal
│   │   │   └── 📄 form-elements.html # Elementos de formulario
│   │   ├── 📁 pages/                 # Páginas principales
│   │   │   ├── 📄 index.html         # Página de inicio/login
│   │   │   ├── 📄 dashboard.html     # Dashboard principal
│   │   │   ├── 📄 student-dashboard.html # Dashboard estudiante
│   │   │   ├── 📄 teacher-dashboard.html # Dashboard docente
│   │   │   ├── 📄 admin-dashboard.html   # Dashboard admin
│   │   │   ├── 📄 evaluation-form.html  # Formulario evaluación
│   │   │   ├── 📄 reports.html       # Página de reportes
│   │   │   ├── 📄 user-management.html  # Gestión usuarios
│   │   │   └── 📄 settings.html      # Configuraciones
│   │   └── 📄 manifest.json          # Manifiesto de la app
│   │
│   ├── 📁 backend/                   # Aplicación backend
│   │   ├── 📁 api/                   # APIs REST
│   │   │   ├── 📄 auth.js            # API de autenticación
│   │   │   ├── 📄 users.js           # API de usuarios
│   │   │   ├── 📄 evaluations.js     # API de evaluaciones
│   │   │   ├── 📄 reports.js         # API de reportes
│   │   │   ├── 📄 forms.js           # API de formularios
│   │   │   └── 📄 admin.js           # API de administración
│   │   ├── 📁 models/                # Modelos de datos
│   │   │   ├── 📄 User.js            # Modelo de usuario
│   │   │   ├── 📄 Evaluation.js      # Modelo de evaluación
│   │   │   ├── 📄 Form.js            # Modelo de formulario
│   │   │   ├── 📄 Question.js        # Modelo de pregunta
│   │   │   ├── 📄 Response.js        # Modelo de respuesta
│   │   │   └── 📄 Report.js          # Modelo de reporte
│   │   ├── 📁 middleware/            # Middleware personalizado
│   │   │   ├── 📄 auth.js            # Middleware de autenticación
│   │   │   ├── 📄 validation.js      # Validaciones
│   │   │   ├── 📄 cors.js            # Configuración CORS
│   │   │   └── 📄 logger.js          # Sistema de logs
│   │   ├── 📁 services/              # Servicios de negocio
│   │   │   ├── 📄 authService.js     # Servicio de autenticación
│   │   │   ├── 📄 evaluationService.js # Servicio de evaluaciones
│   │   │   ├── 📄 reportService.js   # Servicio de reportes
│   │   │   ├── 📄 emailService.js    # Servicio de email
│   │   │   └── 📄 analyticsService.js # Servicio de analytics
│   │   ├── 📁 utils/                 # Utilidades del backend
│   │   │   ├── 📄 database.js        # Conexión a BD
│   │   │   ├── 📄 helpers.js         # Funciones auxiliares
│   │   │   ├── 📄 constants.js       # Constantes del sistema
│   │   │   └── 📄 validators.js      # Validadores personalizados
│   │   └── 📄 server.js              # Servidor principal
│   │
│   └── 📁 database/                  # Base de datos
│       ├── 📄 schema.sql             # Esquema de la BD
│       ├── 📄 seed-data.sql          # Datos de prueba
│       ├── 📄 migrations/            # Migraciones de BD
│       │   ├── 📄 001_create_users.sql
│       │   ├── 📄 002_create_evaluations.sql
│       │   └── 📄 003_create_reports.sql
│       └── 📄 evaluacion.db          # Base de datos SQLite
│
├── 📁 tests/                         # Pruebas del sistema
│   ├── 📁 unit/                      # Pruebas unitarias
│   │   ├── 📄 auth.test.js           # Pruebas de autenticación
│   │   ├── 📄 evaluations.test.js    # Pruebas de evaluaciones
│   │   └── 📄 reports.test.js        # Pruebas de reportes
│   ├── 📁 integration/               # Pruebas de integración
│   │   ├── 📄 api.test.js            # Pruebas de API
│   │   └── 📄 database.test.js       # Pruebas de BD
│   └── 📁 e2e/                       # Pruebas end-to-end
│       ├── 📄 login.test.js          # Pruebas de login
│       └── 📄 evaluation-flow.test.js # Flujo de evaluación
│
├── 📁 config/                        # Configuraciones
│   ├── 📄 development.json           # Config desarrollo
│   ├── 📄 production.json            # Config producción
│   ├── 📄 database.json              # Config base de datos
│   └── 📄 security.json              # Config seguridad
│
├── 📁 scripts/                       # Scripts de automatización
│   ├── 📄 setup.js                   # Script de configuración inicial
│   ├── 📄 build.js                   # Script de construcción
│   ├── 📄 deploy.js                  # Script de despliegue
│   └── 📄 backup.js                  # Script de respaldo
│
├── 📁 .github/                       # Configuración GitHub
│   ├── 📁 workflows/                 # GitHub Actions
│   │   ├── 📄 ci.yml                 # Integración continua
│   │   └── 📄 deploy.yml             # Despliegue automático
│   ├── 📄 ISSUE_TEMPLATE.md          # Plantilla de issues
│   └── 📄 PULL_REQUEST_TEMPLATE.md   # Plantilla de PR
│
├── 📄 .gitignore                     # Archivos ignorados por Git
├── 📄 package.json                   # Dependencias del proyecto
├── 📄 README.md                      # Documentación principal
├── 📄 LICENSE                        # Licencia del proyecto
└── 📄 CHANGELOG.md                   # Registro de cambios
```

## ⚙️ Configuración del Entorno

### **Archivo package.json**

```json
{
  "name": "e-valuacion",
  "version": "1.0.0",
  "description": "Sistema de evaluación docente digital",
  "main": "src/backend/server.js",
  "scripts": {
    "start": "node src/backend/server.js",
    "dev": "nodemon src/backend/server.js",
    "test": "jest",
    "test:watch": "jest --watch",
    "build": "node scripts/build.js",
    "deploy": "node scripts/deploy.js",
    "setup": "node scripts/setup.js",
    "lint": "eslint src/",
    "format": "prettier --write src/"
  },
  "keywords": [
    "evaluacion",
    "docente",
    "educacion",
    "web-app"
  ],
  "authors": [
    "Felipe Ramos",
    "Carlos García"
  ],
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.2",
    "sqlite3": "^5.1.6",
    "bcryptjs": "^2.4.3",
    "jsonwebtoken": "^9.0.2",
    "cors": "^2.8.5",
    "helmet": "^7.0.0",
    "express-rate-limit": "^6.8.1",
    "express-validator": "^7.0.1",
    "multer": "^1.4.5",
    "nodemailer": "^6.9.4"
  },
  "devDependencies": {
    "nodemon": "^3.0.1",
    "jest": "^29.6.2",
    "supertest": "^6.3.3",
    "eslint": "^8.45.0",
    "prettier": "^3.0.0"
  },
  "engines": {
    "node": ">=16.0.0",
    "npm": ">=8.0.0"
  }
}
```

### **Archivo .gitignore**

```gitignore
# Dependencias
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Base de datos
*.db
*.sqlite
*.sqlite3
database/evaluacion.db

# Logs
logs/
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Archivos de configuración sensibles
config/production.json
config/security.json
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# Archivos temporales
tmp/
temp/
.tmp/

# Archivos del sistema operativo
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# IDEs y editores
.vscode/
.idea/
*.swp
*.swo
*~

# Archivos de construcción
dist/
build/
coverage/

# Archivos de respaldo
*.bak
*.backup
```

## 🔧 Configuración de Desarrollo

### **Configuración de VSCode (.vscode/settings.json)**

```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "files.associations": {
    "*.html": "html",
    "*.css": "css",
    "*.js": "javascript"
  },
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  },
  "html.format.indentInnerHtml": true,
  "css.validate": true,
  "javascript.validate.enable": true,
  "files.exclude": {
    "**/node_modules": true,
    "**/.git": true,
    "**/.DS_Store": true,
    "**/tmp": true
  }
}
```

### **Configuración ESLint (.eslintrc.json)**

```json
{
  "env": {
    "browser": true,
    "es2021": true,
    "node": true,
    "jest": true
  },
  "extends": [
    "eslint:recommended"
  ],
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "rules": {
    "indent": ["error", 2],
    "linebreak-style": ["error", "unix"],
    "quotes": ["error", "single"],
    "semi": ["error", "always"],
    "no-unused-vars": "warn",
    "no-console": "warn",
    "prefer-const": "error",
    "no-var": "error"
  }
}
```

## 🗄️ Configuración de Base de Datos

### **Schema Principal (database/schema.sql)**

```sql
-- Configuración inicial de SQLite
PRAGMA foreign_keys = ON;
PRAGMA journal_mode = WAL;
PRAGMA synchronous = NORMAL;
PRAGMA cache_size = 1000;
PRAGMA temp_store = memory;

-- Tabla de usuarios
CREATE TABLE IF NOT EXISTS usuarios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    codigo VARCHAR(20) UNIQUE NOT NULL,
    nombres VARCHAR(100) NOT NULL,
    apellidos VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    tipo_usuario ENUM('estudiante', 'docente', 'administrador') NOT NULL,
    programa_id INTEGER,
    estado ENUM('activo', 'inactivo', 'suspendido') DEFAULT 'activo',
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    fecha_actualizacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (programa_id) REFERENCES programas(id)
);

-- Tabla de programas académicos
CREATE TABLE IF NOT EXISTS programas (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    codigo VARCHAR(20) UNIQUE NOT NULL,
    nombre VARCHAR(200) NOT NULL,
    descripcion TEXT,
    facultad VARCHAR(150) NOT NULL,
    estado ENUM('activo', 'inactivo') DEFAULT 'activo',
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- Tabla de materias
CREATE TABLE IF NOT EXISTS materias (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    codigo VARCHAR(20) UNIQUE NOT NULL,
    nombre VARCHAR(200) NOT NULL,
    descripcion TEXT,
    creditos INTEGER NOT NULL,
    programa_id INTEGER NOT NULL,
    docente_id INTEGER,
    semestre INTEGER NOT NULL,
    estado ENUM('activo', 'inactivo') DEFAULT 'activo',
    fecha_creacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (programa_id) REFERENCES programas(id),
    FOREIGN KEY (docente_id) REFERENCES usuarios(id)
);

-- Índices para optimización
CREATE INDEX idx_usuarios_email ON usuarios(email);
CREATE INDEX idx_usuarios_codigo ON usuarios(codigo);
CREATE INDEX idx_usuarios_tipo ON usuarios(tipo_usuario);
CREATE INDEX idx_materias_programa ON materias(programa_id);
CREATE INDEX idx_materias_docente ON materias(docente_id);
```

### **Datos de Prueba (database/seed-data.sql)**

```sql
-- Insertar programas académicos
INSERT INTO programas (codigo, nombre, descripcion, facultad) VALUES
('ING-SIS', 'Ingeniería de Sistemas', 'Programa de Ingeniería de Sistemas y Computación', 'Facultad de Ingeniería'),
('ING-IND', 'Ingeniería Industrial', 'Programa de Ingeniería Industrial', 'Facultad de Ingeniería'),
('ADM-EMP', 'Administración de Empresas', 'Programa de Administración de Empresas', 'Facultad de Ciencias Económicas');

-- Insertar usuarios de prueba
INSERT INTO usuarios (codigo, nombres, apellidos, email, password_hash, tipo_usuario, programa_id) VALUES
('ADMIN001', 'Carlos', 'García', 'carlos.garcia@universidad.edu', '$2b$10$example_hash_admin', 'administrador', NULL),
('DOC001', 'María', 'Rodríguez', 'maria.rodriguez@universidad.edu', '$2b$10$example_hash_doc1', 'docente', 1),
('DOC002', 'Juan', 'Martínez', 'juan.martinez@universidad.edu', '$2b$10$example_hash_doc2', 'docente', 1),
('EST001', 'Felipe', 'Ramos', 'felipe.ramos@estudiante.edu', '$2b$10$example_hash_est1', 'estudiante', 1),
('EST002', 'Ana', 'López', 'ana.lopez@estudiante.edu', '$2b$10$example_hash_est2', 'estudiante', 1);

-- Insertar materias
INSERT INTO materias (codigo, nombre, descripcion, creditos, programa_id, docente_id, semestre) VALUES
('SIS-101', 'Programación I', 'Fundamentos de programación', 4, 1, 2, 1),
('SIS-201', 'Base de Datos', 'Diseño y administración de bases de datos', 3, 1, 2, 3),
('SIS-301', 'Ingeniería de Software', 'Metodologías de desarrollo de software', 4, 1, 3, 5);
```

## 🌐 Configuración del Servidor

### **Servidor Principal (src/backend/server.js)**

```javascript
const express = require('express');
const cors = require('cors');
const helmet = require('helmet');
const rateLimit = require('express-rate-limit');
const path = require('path');

// Importar rutas
const authRoutes = require('./api/auth');
const userRoutes = require('./api/users');
const evaluationRoutes = require('./api/evaluations');
const reportRoutes = require('./api/reports');

// Importar middleware
const authMiddleware = require('./middleware/auth');
const logger = require('./middleware/logger');

const app = express();
const PORT = process.env.PORT || 3000;

// Configuración de seguridad
app.use(helmet());
app.use(cors({
  origin: process.env.FRONTEND_URL || 'http://localhost:3000',
  credentials: true
}));

// Rate limiting
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutos
  max: 100 // máximo 100 requests por ventana
});
app.use(limiter);

// Middleware de parsing
app.use(express.json({ limit: '10mb' }));
app.use(express.urlencoded({ extended: true }));

// Middleware de logging
app.use(logger);

// Servir archivos estáticos
app.use(express.static(path.join(__dirname, '../frontend')));

// Rutas de la API
app.use('/api/auth', authRoutes);
app.use('/api/users', authMiddleware, userRoutes);
app.use('/api/evaluations', authMiddleware, evaluationRoutes);
app.use('/api/reports', authMiddleware, reportRoutes);

// Ruta principal - servir la aplicación frontend
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, '../frontend/pages/index.html'));
});

// Manejo de errores 404
app.use('*', (req, res) => {
  res.status(404).json({ 
    error: 'Ruta no encontrada',
    message: 'La ruta solicitada no existe en el servidor'
  });
});

// Manejo global de errores
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ 
    error: 'Error interno del servidor',
    message: process.env.NODE_ENV === 'development' ? err.message : 'Algo salió mal'
  });
});

// Iniciar servidor
app.listen(PORT, () => {
  console.log(`🚀 Servidor e-VALuacion ejecutándose en puerto ${PORT}`);
  console.log(`📱 Frontend disponible en: http://localhost:${PORT}`);
  console.log(`🔌 API disponible en: http://localhost:${PORT}/api`);
});

module.exports = app;
```

## 🎨 Estructura CSS

### **Estilos Principales (src/frontend/assets/css/main.css)**

```css
/* Variables CSS para consistencia */
:root {
  /* Colores principales */
  --primary-color: #2563EB;
  --secondary-color: #3B82F6;
  --success-color: #10B981;
  --warning-color: #F59E0B;
  --error-color: #EF4444;
  --text-color: #374151;
  --light-gray: #F9FAFB;
  --white: #FFFFFF;
  
  /* Tipografía */
  --font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --font-size-base: 1rem;
  --font-size-sm: 0.875rem;
  --font-size-lg: 1.125rem;
  --font-size-xl: 1.25rem;
  --font-size-2xl: 1.5rem;
  --font-size-3xl: 2rem;
  
  /* Espaciado */
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;
  --spacing-xl: 2rem;
  --spacing-2xl: 3rem;
  
  /* Bordes y sombras */
  --border-radius: 0.5rem;
  --border-radius-lg: 0.75rem;
  --box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
  --box-shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  
  /* Transiciones */
  --transition: all 0.3s ease;
}

/* Reset y base */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: var(--font-family);
  font-size: var(--font-size-base);
  line-height: 1.6;
  color: var(--text-color);
  background-color: var(--light-gray);
}

/* Layout principal */
.app-container {
  display: flex;
  min-height: 100vh;
}

.sidebar {
  width: 250px;
  background: var(--white);
  box-shadow: var(--box-shadow);
  transition: var(--transition);
}

.main-content {
  flex: 1;
  padding: var(--spacing-xl);
  overflow-y: auto;
}

/* Componentes reutilizables */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: var(--spacing-sm) var(--spacing-lg);
  border: none;
  border-radius: var(--border-radius);
  font-size: var(--font-size-base);
  font-weight: 500;
  text-decoration: none;
  cursor: pointer;
  transition: var(--transition);
}

.btn-primary {
  background-color: var(--primary-color);
  color: var(--white);
}

.btn-primary:hover {
  background-color: var(--secondary-color);
  transform: translateY(-1px);
}

.card {
  background: var(--white);
  border-radius: var(--border-radius-lg);
  box-shadow: var(--box-shadow);
  padding: var(--spacing-xl);
  margin-bottom: var(--spacing-lg);
}

.form-group {
  margin-bottom: var(--spacing-lg);
}

.form-label {
  display: block;
  margin-bottom: var(--spacing-sm);
  font-weight: 500;
  color: var(--text-color);
}

.form-input {
  width: 100%;
  padding: var(--spacing-sm) var(--spacing-md);
  border: 1px solid #D1D5DB;
  border-radius: var(--border-radius);
  font-size: var(--font-size-base);
  transition: var(--transition);
}

.form-input:focus {
  outline: none;
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

/* Utilidades */
.text-center { text-align: center; }
.text-right { text-align: right; }
.mb-0 { margin-bottom: 0; }
.mb-1 { margin-bottom: var(--spacing-sm); }
.mb-2 { margin-bottom: var(--spacing-md); }
.mb-3 { margin-bottom: var(--spacing-lg); }
.mt-0 { margin-top: 0; }
.mt-1 { margin-top: var(--spacing-sm); }
.mt-2 { margin-top: var(--spacing-md); }
.mt-3 { margin-top: var(--spacing-lg); }

.hidden { display: none; }
.visible { display: block; }

/* Estados de carga */
.loading {
  opacity: 0.6;
  pointer-events: none;
}

.spinner {
  border: 2px solid #f3f3f3;
  border-top: 2px solid var(--primary-color);
  border-radius: 50%;
  width: 20px;
  height: 20px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
```

## 📱 Configuración Responsive

### **Estilos Responsive (src/frontend/assets/css/responsive.css)**

```css
/* Breakpoints */
@media (max-width: 768px) {
  .sidebar {
    position: fixed;
    left: -250px;
    top: 0;
    height: 100vh;
    z-index: 1000;
    transition: left 0.3s ease;
  }
  
  .sidebar.active {
    left: 0;
  }
  
  .main-content {
    padding: var(--spacing-md);
  }
  
  .app-container {
    flex-direction: column;
  }
  
  /* Tablas responsive */
  .table-responsive {
    overflow-x: auto;
  }
  
  /* Formularios en móvil */
  .form-row {
    flex-direction: column;
  }
  
  .form-col {
    width: 100%;
    margin-bottom: var(--spacing-md);
  }
}

@media (min-width: 769px) and (max-width: 1024px) {
  .sidebar {
    width: 200px;
  }
  
  .main-content {
    padding: var(--spacing-lg);
  }
}

@media (min-width: 1025px) {
  .container {
    max-width: 1200px;
    margin: 0 auto;
  }
}
```

## 🔐 Configuración de Seguridad

### **Middleware de Autenticación (src/backend/middleware/auth.js)**

```javascript
const jwt = require('jsonwebtoken');
const { promisify } = require('util');

const JWT_SECRET = process.env.JWT_SECRET || 'e-valuacion-secret-key-2024';

const authMiddleware = async (req, res, next) => {
  try {
    // Obtener token del header
    const authHeader = req.headers.authorization;
    
    if (!authHeader || !authHeader.startsWith('Bearer ')) {
      return res.status(401).json({
        error: 'Token de acceso requerido',
        message: 'Debe proporcionar un token válido para acceder a este recurso'
      });
    }
    
    const token = authHeader.substring(7); // Remover 'Bearer '
    
    // Verificar token
    const decoded = await promisify(jwt.verify)(token, JWT_SECRET);
    
    // Agregar información del usuario a la request
    req.user = {
      id: decoded.id,
      email: decoded.email,
      tipo_usuario: decoded.tipo_usuario,
      programa_id: decoded.programa_id
    };
    
    next();
  } catch (error) {
    if (error.name === 'JsonWebTokenError') {
      return res.status(401).json({
        error: 'Token inválido',
        message: 'El token proporcionado no es válido'
      });
    }
    
    if (error.name === 'TokenExpiredError') {
      return res.status(401).json({
        error: 'Token expirado',
        message: 'El token ha expirado, por favor inicie sesión nuevamente'
      });
    }
    
    return res.status(500).json({
      error: 'Error de autenticación',
      message: 'Error interno al verificar el token'
    });
  }
};

module.exports = authMiddleware;
```

## 📊 Scripts de Automatización

### **Script de Configuración (scripts/setup.js)**

```javascript
const fs = require('fs');
const path = require('path');
const sqlite3 = require('sqlite3').verbose();

console.log('🚀 Configurando proyecto e-VALuacion...');

// Crear directorios necesarios
const directories = [
  'src/frontend/assets/css',
  'src/frontend/assets/js',
  'src/frontend/assets/images',
  'src/frontend/components',
  'src/frontend/pages',
  'src/backend/api',
  'src/backend/models',
  'src/backend/middleware',
  'src/backend/services',
  'src/backend/utils',
  'src/database',
  'tests/unit',
  'tests/integration',
  'tests/e2e',
  'config',
  'scripts',
  'logs'
];

directories.forEach(dir => {
  const fullPath = path.join(__dirname, '..', dir);
  if (!fs.existsSync(fullPath)) {
    fs.mkdirSync(fullPath, { recursive: true });
    console.log(`✅ Directorio creado: ${dir}`);
  }
});

// Crear base de datos inicial
const dbPath = path.join(__dirname, '..', 'src', 'database', 'evaluacion.db');
const db = new sqlite3.Database(dbPath);

// Leer y ejecutar schema
const schemaPath = path.join(__dirname, '..', 'src', 'database', 'schema.sql');
if (fs.existsSync(schemaPath)) {
  const schema = fs.readFileSync(schemaPath, 'utf8');
  db.exec(schema, (err) => {
    if (err) {
      console.error('❌ Error creando schema:', err);
    } else {
      console.log('✅ Base de datos creada exitosamente');
    }
    db.close();
  });
}

console.log('🎉 Configuración completada!');
console.log('📝 Próximos pasos:');
console.log('   1. npm install');
console.log('   2. npm run dev');
console.log('   3. Abrir http://localhost:3000');
```

---

*Esta estructura proporciona una base sólida y escalable para el desarrollo del sistema e-VALuacion, siguiendo las mejores prácticas de desarrollo web y facilitando la colaboración entre Felipe Ramos y Carlos García.*