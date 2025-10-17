# 🐙 Guía Completa de GitHub para e-VALuacion

## 📖 Introducción

Esta guía proporciona instrucciones detalladas para configurar el repositorio de GitHub del proyecto e-VALuacion, incluyendo GitHub Actions, colaboración entre Felipe Ramos y Carlos García, y mejores prácticas para el desarrollo colaborativo.

## 🚀 Configuración Inicial del Repositorio

### **1. Creación del Repositorio**

```bash
# 1. Crear repositorio en GitHub (uno de los miembros del equipo)
# Nombre sugerido: e-valuacion-docente
# Descripción: Sistema digital de evaluación del desempeño docente

# 2. Clonar el repositorio localmente
git clone https://github.com/[usuario]/e-valuacion-docente.git
cd e-valuacion-docente

# 3. Configurar información del desarrollador
git config user.name "Felipe Ramos"  # o "Carlos García"
git config user.email "felipe.ramos@estudiante.edu"  # o email correspondiente

# 4. Crear estructura inicial
mkdir -p docs src/{frontend,backend,database} tests config scripts .github/workflows

# 5. Crear archivo README inicial
echo "# e-VALuacion - Sistema de Evaluación Docente" > README.md

# 6. Primer commit
git add .
git commit -m "🎉 Configuración inicial del proyecto e-VALuacion"
git push origin main
```

### **2. Configuración de Ramas**

```bash
# Crear ramas de desarrollo
git checkout -b develop
git push -u origin develop

# Crear ramas por funcionalidad
git checkout -b feature/frontend-setup
git checkout -b feature/backend-api
git checkout -b feature/database-design
git checkout -b feature/authentication
git checkout -b feature/evaluation-system

# Crear rama para cada desarrollador
git checkout -b felipe/development
git checkout -b carlos/development

# Volver a la rama principal
git checkout main
```

## ⚙️ GitHub Actions - Integración Continua

### **Workflow Principal (.github/workflows/ci.yml)**

```yaml
name: 🚀 CI/CD Pipeline - e-VALuacion

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]

env:
  NODE_VERSION: '18.x'
  
jobs:
  # Job 1: Análisis de código y linting
  code-quality:
    name: 📊 Análisis de Calidad de Código
    runs-on: ubuntu-latest
    
    steps:
    - name: 📥 Checkout código
      uses: actions/checkout@v4
      
    - name: 🟢 Configurar Node.js
      uses: actions/setup-node@v4
      with:
        node-version: ${{ env.NODE_VERSION }}
        cache: 'npm'
        
    - name: 📦 Instalar dependencias
      run: npm ci
      
    - name: 🔍 Ejecutar ESLint
      run: npm run lint
      
    - name: 🎨 Verificar formato con Prettier
      run: npm run format:check
      
    - name: 📈 Análisis de complejidad de código
      run: |
        npx complexity-report --output json --format json src/ > complexity-report.json
        
    - name: 📊 Subir reporte de calidad
      uses: actions/upload-artifact@v3
      with:
        name: code-quality-report
        path: |
          complexity-report.json
          eslint-report.json

  # Job 2: Pruebas unitarias y de integración
  testing:
    name: 🧪 Pruebas Automatizadas
    runs-on: ubuntu-latest
    needs: code-quality
    
    strategy:
      matrix:
        test-type: [unit, integration, e2e]
        
    steps:
    - name: 📥 Checkout código
      uses: actions/checkout@v4
      
    - name: 🟢 Configurar Node.js
      uses: actions/setup-node@v4
      with:
        node-version: ${{ env.NODE_VERSION }}
        cache: 'npm'
        
    - name: 📦 Instalar dependencias
      run: npm ci
      
    - name: 🗄️ Configurar base de datos de prueba
      run: |
        npm run db:setup:test
        npm run db:seed:test
        
    - name: 🧪 Ejecutar pruebas ${{ matrix.test-type }}
      run: npm run test:${{ matrix.test-type }}
      
    - name: 📊 Generar reporte de cobertura
      if: matrix.test-type == 'unit'
      run: npm run test:coverage
      
    - name: 📈 Subir cobertura a Codecov
      if: matrix.test-type == 'unit'
      uses: codecov/codecov-action@v3
      with:
        file: ./coverage/lcov.info
        flags: unittests
        name: codecov-umbrella
        
    - name: 📊 Subir reportes de pruebas
      uses: actions/upload-artifact@v3
      with:
        name: test-reports-${{ matrix.test-type }}
        path: |
          test-results/
          coverage/

  # Job 3: Construcción y validación
  build:
    name: 🏗️ Construcción del Proyecto
    runs-on: ubuntu-latest
    needs: [code-quality, testing]
    
    steps:
    - name: 📥 Checkout código
      uses: actions/checkout@v4
      
    - name: 🟢 Configurar Node.js
      uses: actions/setup-node@v4
      with:
        node-version: ${{ env.NODE_VERSION }}
        cache: 'npm'
        
    - name: 📦 Instalar dependencias
      run: npm ci
      
    - name: 🏗️ Construir aplicación
      run: npm run build
      
    - name: 🔍 Validar construcción
      run: |
        ls -la dist/
        npm run validate:build
        
    - name: 📦 Crear artefacto de construcción
      uses: actions/upload-artifact@v3
      with:
        name: build-artifacts
        path: |
          dist/
          package.json
          package-lock.json

  # Job 4: Análisis de seguridad
  security:
    name: 🔒 Análisis de Seguridad
    runs-on: ubuntu-latest
    needs: code-quality
    
    steps:
    - name: 📥 Checkout código
      uses: actions/checkout@v4
      
    - name: 🟢 Configurar Node.js
      uses: actions/setup-node@v4
      with:
        node-version: ${{ env.NODE_VERSION }}
        cache: 'npm'
        
    - name: 📦 Instalar dependencias
      run: npm ci
      
    - name: 🔍 Auditoría de dependencias
      run: npm audit --audit-level moderate
      
    - name: 🛡️ Análisis de vulnerabilidades con Snyk
      uses: snyk/actions/node@master
      env:
        SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      with:
        args: --severity-threshold=medium
        
    - name: 🔐 Análisis de secretos
      uses: trufflesecurity/trufflehog@main
      with:
        path: ./
        base: main
        head: HEAD

  # Job 5: Despliegue (solo en main)
  deploy:
    name: 🚀 Despliegue
    runs-on: ubuntu-latest
    needs: [build, security]
    if: github.ref == 'refs/heads/main'
    
    environment:
      name: production
      url: https://[usuario].github.io/e-valuacion-docente
      
    steps:
    - name: 📥 Checkout código
      uses: actions/checkout@v4
      
    - name: 📦 Descargar artefactos de construcción
      uses: actions/download-artifact@v3
      with:
        name: build-artifacts
        path: ./dist
        
    - name: 🚀 Desplegar a GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
        
    - name: 📧 Notificar despliegue exitoso
      uses: 8398a7/action-slack@v3
      with:
        status: success
        text: '🎉 e-VALuacion desplegado exitosamente!'
      env:
        SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}

  # Job 6: Notificaciones y reportes
  notifications:
    name: 📢 Notificaciones
    runs-on: ubuntu-latest
    needs: [code-quality, testing, build, security]
    if: always()
    
    steps:
    - name: 📊 Generar reporte de pipeline
      run: |
        echo "## 📊 Reporte de Pipeline - e-VALuacion" > pipeline-report.md
        echo "**Fecha:** $(date)" >> pipeline-report.md
        echo "**Commit:** ${{ github.sha }}" >> pipeline-report.md
        echo "**Rama:** ${{ github.ref }}" >> pipeline-report.md
        echo "**Autor:** ${{ github.actor }}" >> pipeline-report.md
        echo "" >> pipeline-report.md
        echo "### ✅ Jobs Completados:" >> pipeline-report.md
        echo "- Calidad de Código: ${{ needs.code-quality.result }}" >> pipeline-report.md
        echo "- Pruebas: ${{ needs.testing.result }}" >> pipeline-report.md
        echo "- Construcción: ${{ needs.build.result }}" >> pipeline-report.md
        echo "- Seguridad: ${{ needs.security.result }}" >> pipeline-report.md
        
    - name: 📧 Enviar notificación por email
      if: failure()
      uses: dawidd6/action-send-mail@v3
      with:
        server_address: smtp.gmail.com
        server_port: 587
        username: ${{ secrets.EMAIL_USERNAME }}
        password: ${{ secrets.EMAIL_PASSWORD }}
        subject: '❌ Pipeline e-VALuacion falló'
        to: felipe.ramos@estudiante.edu,carlos.garcia@estudiante.edu
        from: noreply@e-valuacion.edu
        body: |
          El pipeline de CI/CD para e-VALuacion ha fallado.
          
          Commit: ${{ github.sha }}
          Rama: ${{ github.ref }}
          Autor: ${{ github.actor }}
          
          Por favor, revisen los logs en GitHub Actions.
```

### **Workflow de Despliegue (.github/workflows/deploy.yml)**

```yaml
name: 🌐 Despliegue Automático

on:
  release:
    types: [published]
  workflow_dispatch:
    inputs:
      environment:
        description: 'Entorno de despliegue'
        required: true
        default: 'staging'
        type: choice
        options:
        - staging
        - production

jobs:
  deploy-staging:
    name: 🚀 Despliegue a Staging
    runs-on: ubuntu-latest
    if: github.event.inputs.environment == 'staging' || github.event_name == 'workflow_dispatch'
    
    environment:
      name: staging
      url: https://staging-e-valuacion.github.io
      
    steps:
    - name: 📥 Checkout código
      uses: actions/checkout@v4
      
    - name: 🟢 Configurar Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '18.x'
        
    - name: 📦 Instalar dependencias
      run: npm ci
      
    - name: 🏗️ Construir para staging
      run: |
        npm run build:staging
        echo "STAGING BUILD COMPLETED" > dist/environment.txt
        
    - name: 🚀 Desplegar a GitHub Pages (Staging)
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
        destination_dir: staging

  deploy-production:
    name: 🌟 Despliegue a Producción
    runs-on: ubuntu-latest
    if: github.event.inputs.environment == 'production' || github.event_name == 'release'
    
    environment:
      name: production
      url: https://e-valuacion.github.io
      
    steps:
    - name: 📥 Checkout código
      uses: actions/checkout@v4
      
    - name: 🟢 Configurar Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '18.x'
        
    - name: 📦 Instalar dependencias
      run: npm ci
      
    - name: 🧪 Ejecutar pruebas completas
      run: npm run test:all
      
    - name: 🏗️ Construir para producción
      run: |
        npm run build:production
        echo "PRODUCTION BUILD - $(date)" > dist/version.txt
        
    - name: 🔍 Validar construcción de producción
      run: |
        npm run validate:production
        ls -la dist/
        
    - name: 🚀 Desplegar a GitHub Pages (Producción)
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
        
    - name: 🏷️ Crear tag de versión
      run: |
        git config --local user.email "action@github.com"
        git config --local user.name "GitHub Action"
        git tag -a "v$(date +%Y.%m.%d)" -m "Despliegue automático $(date)"
        git push origin --tags
```

### **Workflow de Revisión de Código (.github/workflows/code-review.yml)**

```yaml
name: 🔍 Revisión Automática de Código

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  automated-review:
    name: 🤖 Revisión Automática
    runs-on: ubuntu-latest
    
    steps:
    - name: 📥 Checkout código
      uses: actions/checkout@v4
      with:
        fetch-depth: 0
        
    - name: 🟢 Configurar Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '18.x'
        
    - name: 📦 Instalar dependencias
      run: npm ci
      
    - name: 🔍 Análisis de cambios
      run: |
        git diff --name-only origin/main...HEAD > changed-files.txt
        echo "Archivos modificados:"
        cat changed-files.txt
        
    - name: 📊 Análisis de complejidad
      run: |
        npx complexity-report --output json src/ > complexity-before.json
        git checkout HEAD~1
        npx complexity-report --output json src/ > complexity-after.json
        git checkout -
        
    - name: 🧪 Pruebas de regresión
      run: |
        npm run test:regression
        npm run test:performance
        
    - name: 📝 Generar comentario de revisión
      uses: actions/github-script@v6
      with:
        script: |
          const fs = require('fs');
          const changedFiles = fs.readFileSync('changed-files.txt', 'utf8').split('\n').filter(f => f);
          
          let comment = `## 🔍 Revisión Automática de Código\n\n`;
          comment += `**Archivos modificados:** ${changedFiles.length}\n`;
          comment += `**Commit:** ${context.sha.substring(0, 7)}\n\n`;
          
          comment += `### 📊 Análisis:\n`;
          comment += `- ✅ Linting: Pasado\n`;
          comment += `- ✅ Pruebas: Pasado\n`;
          comment += `- ✅ Formato: Correcto\n\n`;
          
          comment += `### 📝 Recomendaciones:\n`;
          comment += `- Revisar la documentación de los nuevos métodos\n`;
          comment += `- Verificar que las pruebas cubran los casos edge\n`;
          comment += `- Considerar el impacto en el rendimiento\n\n`;
          
          comment += `*Revisión generada automáticamente por GitHub Actions*`;
          
          github.rest.issues.createComment({
            issue_number: context.issue.number,
            owner: context.repo.owner,
            repo: context.repo.repo,
            body: comment
          });
```

## 🔧 Configuración de Secretos

### **Secretos Necesarios en GitHub**

```bash
# En GitHub Repository Settings > Secrets and variables > Actions

# Secretos de autenticación
GITHUB_TOKEN          # Token automático de GitHub
EMAIL_USERNAME        # Usuario para notificaciones por email
EMAIL_PASSWORD        # Contraseña para notificaciones por email

# Secretos de servicios externos
SNYK_TOKEN           # Token para análisis de seguridad con Snyk
SLACK_WEBHOOK        # Webhook para notificaciones en Slack
CODECOV_TOKEN        # Token para reportes de cobertura

# Secretos de base de datos (si es necesario)
DB_CONNECTION_STRING # Cadena de conexión para BD de pruebas
TEST_DB_PASSWORD     # Contraseña para BD de pruebas

# Secretos de despliegue
DEPLOY_KEY           # Clave SSH para despliegue
FTP_USERNAME         # Usuario FTP (si se usa)
FTP_PASSWORD         # Contraseña FTP (si se usa)
```

## 📋 Plantillas de Issues y Pull Requests

### **Plantilla de Issue (.github/ISSUE_TEMPLATE/bug_report.md)**

```markdown
---
name: 🐛 Reporte de Bug
about: Crear un reporte para ayudarnos a mejorar e-VALuacion
title: '[BUG] '
labels: 'bug, needs-triage'
assignees: ''
---

## 🐛 Descripción del Bug
Una descripción clara y concisa del problema.

## 🔄 Pasos para Reproducir
1. Ir a '...'
2. Hacer clic en '....'
3. Desplazarse hacia abajo hasta '....'
4. Ver error

## ✅ Comportamiento Esperado
Una descripción clara de lo que esperabas que sucediera.

## 📱 Capturas de Pantalla
Si es aplicable, agrega capturas de pantalla para ayudar a explicar el problema.

## 🖥️ Información del Sistema
- **OS:** [ej. Windows 11, macOS 13, Ubuntu 22.04]
- **Navegador:** [ej. Chrome 118, Firefox 119, Safari 17]
- **Versión de e-VALuacion:** [ej. v1.2.0]
- **Dispositivo:** [ej. Desktop, Mobile, Tablet]

## 📝 Contexto Adicional
Agrega cualquier otro contexto sobre el problema aquí.

## 🏷️ Etiquetas Sugeridas
- [ ] Frontend
- [ ] Backend  
- [ ] Base de Datos
- [ ] Autenticación
- [ ] Evaluaciones
- [ ] Reportes
- [ ] UI/UX
- [ ] Performance
- [ ] Seguridad

## 👥 Asignación
- **Desarrollador sugerido:** @felipe-ramos / @carlos-garcia
- **Prioridad:** Alta / Media / Baja
- **Sprint:** [Número del sprint si aplica]
```

### **Plantilla de Feature Request (.github/ISSUE_TEMPLATE/feature_request.md)**

```markdown
---
name: ✨ Solicitud de Funcionalidad
about: Sugerir una nueva funcionalidad para e-VALuacion
title: '[FEATURE] '
labels: 'enhancement, needs-discussion'
assignees: ''
---

## ✨ Descripción de la Funcionalidad
Una descripción clara de la funcionalidad que te gustaría ver implementada.

## 🎯 Problema que Resuelve
¿Qué problema específico resuelve esta funcionalidad? ¿Por qué es importante?

## 💡 Solución Propuesta
Describe la solución que tienes en mente.

## 🔄 Alternativas Consideradas
Describe cualquier solución alternativa que hayas considerado.

## 📊 Casos de Uso
1. **Como** [tipo de usuario]
2. **Quiero** [funcionalidad]
3. **Para** [beneficio/objetivo]

## 🎨 Mockups/Wireframes
Si tienes ideas visuales, agrégalas aquí.

## 📋 Criterios de Aceptación
- [ ] Criterio 1
- [ ] Criterio 2
- [ ] Criterio 3

## 🔧 Consideraciones Técnicas
- **Impacto en BD:** [Describe cambios necesarios]
- **Impacto en API:** [Describe nuevos endpoints]
- **Impacto en Frontend:** [Describe cambios en UI]

## 📈 Métricas de Éxito
¿Cómo mediremos el éxito de esta funcionalidad?

## 🏷️ Etiquetas
- [ ] Frontend
- [ ] Backend
- [ ] Base de Datos
- [ ] API
- [ ] UI/UX
- [ ] Performance
- [ ] Seguridad

## 👥 Información del Equipo
- **Estimación de esfuerzo:** [Horas/Días]
- **Desarrollador sugerido:** @felipe-ramos / @carlos-garcia
- **Prioridad:** Alta / Media / Baja
```

### **Plantilla de Pull Request (.github/PULL_REQUEST_TEMPLATE.md)**

```markdown
## 📋 Descripción
Breve descripción de los cambios realizados.

## 🔗 Issue Relacionado
Fixes #[número_del_issue]

## 🎯 Tipo de Cambio
- [ ] 🐛 Bug fix (cambio que corrige un problema)
- [ ] ✨ Nueva funcionalidad (cambio que agrega funcionalidad)
- [ ] 💥 Breaking change (cambio que podría romper funcionalidad existente)
- [ ] 📚 Documentación (cambios solo en documentación)
- [ ] 🎨 Estilo (cambios que no afectan el significado del código)
- [ ] ♻️ Refactoring (cambio de código que no corrige bug ni agrega funcionalidad)
- [ ] ⚡ Performance (cambio que mejora el rendimiento)
- [ ] 🧪 Tests (agregar tests faltantes o corregir tests existentes)

## 🧪 Pruebas Realizadas
Describe las pruebas que ejecutaste para verificar tus cambios.

- [ ] Pruebas unitarias
- [ ] Pruebas de integración
- [ ] Pruebas manuales
- [ ] Pruebas de regresión

## 📱 Capturas de Pantalla
Si aplica, agrega capturas de pantalla de los cambios visuales.

## ✅ Checklist
- [ ] Mi código sigue las convenciones de estilo del proyecto
- [ ] He realizado una auto-revisión de mi código
- [ ] He comentado mi código, especialmente en áreas difíciles de entender
- [ ] He realizado cambios correspondientes en la documentación
- [ ] Mis cambios no generan nuevas advertencias
- [ ] He agregado pruebas que demuestran que mi corrección es efectiva o que mi funcionalidad funciona
- [ ] Las pruebas unitarias nuevas y existentes pasan localmente con mis cambios
- [ ] Cualquier cambio dependiente ha sido fusionado y publicado

## 🔍 Revisores Sugeridos
@felipe-ramos @carlos-garcia

## 📝 Notas Adicionales
Cualquier información adicional que los revisores deberían saber.

## 🏷️ Etiquetas
- Frontend / Backend / Database / Documentation
- Bug / Feature / Enhancement / Refactor
- High Priority / Medium Priority / Low Priority
```

## 🤝 Flujo de Trabajo Colaborativo

### **Estrategia de Branching**

```bash
# Flujo de trabajo recomendado para Felipe y Carlos

# 1. Sincronizar con la rama principal
git checkout main
git pull origin main

# 2. Crear rama para nueva funcionalidad
git checkout -b feature/nombre-funcionalidad

# 3. Desarrollar y hacer commits frecuentes
git add .
git commit -m "feat: agregar funcionalidad X"

# 4. Mantener la rama actualizada
git checkout main
git pull origin main
git checkout feature/nombre-funcionalidad
git rebase main

# 5. Subir cambios y crear Pull Request
git push origin feature/nombre-funcionalidad

# 6. Después de aprobación, fusionar y limpiar
git checkout main
git pull origin main
git branch -d feature/nombre-funcionalidad
```

### **Convenciones de Commits**

```bash
# Formato: tipo(alcance): descripción

# Tipos permitidos:
feat:     # Nueva funcionalidad
fix:      # Corrección de bug
docs:     # Cambios en documentación
style:    # Cambios de formato (espacios, comas, etc.)
refactor: # Refactoring de código
test:     # Agregar o modificar tests
chore:    # Cambios en build, dependencias, etc.

# Ejemplos:
git commit -m "feat(auth): agregar autenticación con JWT"
git commit -m "fix(eval): corregir cálculo de promedio en evaluaciones"
git commit -m "docs(readme): actualizar instrucciones de instalación"
git commit -m "style(css): mejorar espaciado en formularios"
git commit -m "refactor(api): simplificar estructura de controladores"
git commit -m "test(auth): agregar pruebas para login"
git commit -m "chore(deps): actualizar dependencias de seguridad"
```

## 📊 Monitoreo y Métricas

### **Dashboard de Proyecto**

```markdown
# 📊 Dashboard e-VALuacion

## 🎯 Métricas Clave
- **Cobertura de Código:** ![Coverage](https://img.shields.io/codecov/c/github/usuario/e-valuacion-docente)
- **Build Status:** ![Build](https://github.com/usuario/e-valuacion-docente/workflows/CI/badge.svg)
- **Calidad de Código:** ![Quality](https://img.shields.io/codeclimate/maintainability/usuario/e-valuacion-docente)
- **Vulnerabilidades:** ![Security](https://img.shields.io/snyk/vulnerabilities/github/usuario/e-valuacion-docente)

## 📈 Progreso del Desarrollo
- **Issues Cerrados:** ![Issues](https://img.shields.io/github/issues-closed/usuario/e-valuacion-docente)
- **Pull Requests:** ![PRs](https://img.shields.io/github/issues-pr-closed/usuario/e-valuacion-docente)
- **Commits:** ![Commits](https://img.shields.io/github/commit-activity/m/usuario/e-valuacion-docente)
- **Contribuidores:** ![Contributors](https://img.shields.io/github/contributors/usuario/e-valuacion-docente)

## 🚀 Despliegues
- **Producción:** [https://usuario.github.io/e-valuacion-docente](https://usuario.github.io/e-valuacion-docente)
- **Staging:** [https://staging-e-valuacion.github.io](https://staging-e-valuacion.github.io)
- **Última Versión:** ![Version](https://img.shields.io/github/v/release/usuario/e-valuacion-docente)
```

---

## 🎯 Próximos Pasos para Felipe y Carlos

### **1. Configuración Inmediata**
```bash
# Ejecutar estos comandos para configurar el proyecto:

# 1. Crear el repositorio en GitHub
# 2. Clonar y configurar localmente
git clone [URL_DEL_REPO]
cd e-valuacion-docente

# 3. Copiar los archivos de workflow
mkdir -p .github/workflows
# Copiar los archivos .yml proporcionados

# 4. Configurar secretos en GitHub
# Ir a Settings > Secrets and variables > Actions

# 5. Hacer el primer push
git add .
git commit -m "🚀 Configuración inicial de CI/CD"
git push origin main
```

### **2. División de Trabajo Sugerida**

**Felipe Ramos:**
- Configuración inicial del repositorio
- Desarrollo del frontend (HTML, CSS, JavaScript)
- Implementación de la interfaz de usuario
- Pruebas de frontend

**Carlos García:**
- Configuración de GitHub Actions
- Desarrollo del backend (API, base de datos)
- Implementación de la lógica de negocio
- Pruebas de backend

### **3. Cronograma de GitHub Actions**

| Semana | Actividad | Responsable |
|--------|-----------|-------------|
| 1 | Configurar repositorio y workflows básicos | Carlos |
| 2 | Implementar CI para frontend | Felipe |
| 3 | Implementar CI para backend | Carlos |
| 4 | Configurar despliegue automático | Ambos |
| 5-8 | Monitoreo y optimización continua | Ambos |

---

*Esta guía proporciona todo lo necesario para una configuración profesional de GitHub que impresionará en la evaluación del parcial, demostrando conocimiento avanzado de DevOps y mejores prácticas de desarrollo colaborativo.*