# spa-html-editor-architecture
Documentación técnica y arquitectura de una plataforma SPA para la gestión automatizada de formatos HTML desarrollada con React 19 y PHP API REST
**IMPORTANTE**: 
Este repositorio contiene únicamente la documentación técnica y arquitectura del proyecto por acuerdos de confidencialidad (NDA). El código fuente no está disponible para su distribución pública.

# 📋 EFINFO FORMATS - Editor de Formatos HTML

## 📖 Descripción

**EFINFO FORMATS** es una aplicación web que permite crear, editar y personalizar formatos HTML para diferentes proyectos. La aplicación proporciona una interfaz visual intuitiva donde los usuarios pueden seleccionar entre múltiples formatos predefinidos y personalizar sus propiedades (colores, imágenes, metadatos, etc.) sin necesidad de conocimientos técnicos avanzados.

---

## 🎯 ¿Qué hace esta aplicación?

### **Funcionalidad Principal:**

1. **Galería de Formatos**: Permite seleccionar entre 10 formatos diferentes (KONFIO, FITURCA, AMIS, WEBER, ELECCIONES, MAZDA, ADI, DISNEY, SCANBASE, DELL)

2. **Editor Visual**: Interfaz de edición en tiempo real donde se pueden:
   - Personalizar colores del formato
   - Subir imágenes personalizadas (headers, footers)
   - Configurar metadatos a mostrar
   - Ajustar opciones de visualización
   - Previsualizar cambios instantáneamente

3. **Gestión de Configuraciones**: 
   - Guardar configuraciones en base de datos
   - Actualizar formatos existentes
   - Eliminar formatos
   - Modo temporal para previsualizar sin guardar

4. **Almacenamiento de Imágenes**: 
   - Subida de imágenes personalizadas
   - Almacenamiento local en el proyecto
   - Gestión automática de imágenes antiguas
  
### Flujo de la Aplicación
![Flujo General](Diagrama%20sin%20título.jpg)

---


## 🏗️ Arquitectura

### **Frontend (React)**
- **Framework**: React 19.x
- **Routing**: React Router DOM 7.x
- **Build Tool**: react-scripts 5.0.1
- **Tipo**: Single Page Application (SPA)

- ### Estructura del Frontend (React 19)
![Arquitectura Frontend](diagramaFrontend.drawio.jpg)

### **Backend (PHP)**
- **Lenguaje**: PHP 7.4+ (recomendado 8.0+)
- **Arquitectura**: API REST sin frameworks
- **Base de Datos**: Externa (API remota)

- ### Estructura del Backend (PHP API REST)
![Arquitectura Backend](estructura%20del%20proyecto%20formats.jpg)

---

## 📁 Estructura del Proyecto

```
formats/
├── backend/                    # Backend PHP
│   ├── configs/               # Configuraciones
│   │   ├── config.php         # Configuración principal
│   │   ├── environment.php    # Detección de entorno
│   │   └── formats/           # Configuraciones por formato
│   │       ├── KONFIO.php
│   │       ├── FITURCA.php
│   │       └── ... (otros formatos)
│   ├── controllers/           # Controladores
│   │   ├── SintesisController.php
│   │   └── helpers/
│   │       └── SintesisControllerHelper.php
│   ├── core/                  # Núcleo del sistema
│   │   ├── Router.php
│   │   └── services/
│   │       └── FormatConfigLoader.php
│   └── public/                # Punto de entrada
│       ├── index.php
│       └── img/                # Imágenes subidas
│
└── frontend/                   # Frontend React
    ├── src/
    │   ├── components/         # Componentes React
    │   │   ├── Gallery/       # Galería de formatos
    │   │   ├── Editor/        # Editor de formatos
    │   │   └── Modal/         # Modales
    │   ├── services/           # Servicios API
    │   ├── config/            # Configuraciones
    │   └── styles/            # Estilos CSS
    └── build/                 # Build de producción
```

---

## 🚀 Características Principales

### **1. Galería de Formatos**
- Visualización de 10 formatos disponibles
- Previsualización de cada formato
- Selección intuitiva con imágenes de referencia
- Modo creación y edición

### **2. Editor Visual**
- **Panel de Propiedades**: Configuración detallada de cada formato
- **Vista Previa en Tiempo Real**: Iframe con actualización instantánea
- **Subida de Imágenes**: Headers y footers personalizados
- **Selector de Colores**: Personalización de paleta de colores
- **Configuración de Metadatos**: Selección de metadatos a mostrar

### **3. Gestión de Configuraciones**
- Guardar configuraciones en base de datos
- Actualizar formatos existentes
- Eliminar formatos con confirmación
- Modo temporal para pruebas sin guardar

### **4. Formatos Disponibles**
- **KONFIO**: Formato corporativo con colores morados
- **FITURCA**: Formato con doble color y opciones avanzadas
- **AMIS**: Formato con colores naranjas
- **WEBER**: Formato personalizado
- **ELECCIONES**: Formato con clasificación de colores
- **MAZDA**: Formato corporativo
- **ADI**: Formato personalizado
- **DISNEY**: Formato con imágenes de header y footer
- **SCANBASE**: Formato con múltiples headers
- **DELL**: Formato corporativo

---

## 🛠️ Tecnologías Utilizadas

### **Frontend:**
- React 19.x
- React Router DOM 7.x
- react-scripts 5.0.1
- CSS3 (sin frameworks CSS)

### **Backend:**
- PHP 7.4+ (recomendado 8.0+)
- Extensiones: curl, json, session, fileinfo, mbstring, openssl

### **Servidor:**
- Apache 2.4+ o Nginx 1.18+
- SSL/HTTPS (producción)

### **Herramientas de Desarrollo:**
- Node.js 16.x+ (solo para desarrollo/build)
- npm 8.x+

---

## 📦 Instalación

### **Requisitos Previos:**
- PHP 7.4+ instalado
- Node.js 16.x+ (solo para desarrollo)
- Servidor web (Apache/Nginx)
- Acceso a API externa: `https://www.efinf.com/api/formatConfigData.php`

### **Pasos de Instalación:**

1. **Clonar o descargar el proyecto**
   ```bash
   cd formats/
   ```

2. **Instalar dependencias del frontend**
   ```bash
   cd frontend/
   npm install
   ```

3. **Construir el frontend para producción**
   ```bash
   npm run build
   ```

4. **Configurar el servidor web**
   - Configurar Virtual Host apuntando a `formats/`
   - Habilitar módulos: mod_rewrite, mod_headers, mod_ssl
   - Configurar permisos de escritura en `backend/public/img/`

5. **Verificar configuración**
   - Acceder a `http://dominio/app/`
   - Verificar que la galería de formatos se muestra correctamente

---

## 🎮 Uso

### **Flujo de Trabajo:**

1. **Seleccionar Formato**
   - Acceder a la galería de formatos
   - Hacer clic en el formato deseado
   - Confirmar selección

2. **Editar Propiedades**
   - Usar el panel de propiedades para personalizar:
     - Colores del formato
     - Imágenes (header, footer)
     - Metadatos a mostrar
     - Opciones de visualización
   - Ver cambios en tiempo real en la vista previa

3. **Guardar Cambios**
   - Presionar botón "Guardar"
   - La configuración se guarda en la base de datos
   - Redirección automática a la página principal

4. **Eliminar Formato**
   - Presionar botón "Eliminar"
   - Confirmar en el modal
   - El formato se elimina de la base de datos
   - Redirección automática con mensaje de éxito

---

## 🔧 Configuración

### **Entorno de Desarrollo:**
- URLs se detectan automáticamente
- Debug activado
- Errores visibles

### **Entorno de Producción:**
- Detección automática por dominio (`efinf.com`)
- Debug desactivado
- Errores solo en logs

### **Variables de Entorno:**
- No requiere archivos `.env`
- Configuración dinámica basada en `window.location.origin` (frontend)
- Configuración dinámica basada en `$_SERVER` (backend)

---

## 📊 Recursos Necesarios

### **Servidor Mínimo:**
- **RAM**: 512 MB - 1 GB
- **CPU**: 1-2 cores
- **Disco**: 1-2 GB

### **Servidor Recomendado:**
- **RAM**: 1-2 GB
- **CPU**: 2 cores
- **Disco**: 2-5 GB

**Nota**: Es una aplicación ligera que no requiere muchos recursos.

---

## 🔐 Seguridad

- Validación de tipos de archivo en subida de imágenes
- Límite de tamaño de archivos (5MB máximo)
- Sanitización de inputs
- Headers de seguridad configurados
- Sesiones seguras (httponly, samesite)

---

## 📝 Formatos Soportados

La aplicación soporta 10 formatos diferentes, cada uno con sus propias características:

| Formato | Características Especiales |
|---------|---------------------------|
| KONFIO | Valores Reps, Tipo de cambio |
| FITURCA | Doble color, Páginas frontales |
| AMIS | Configuración personalizada |
| WEBER | Configuración personalizada |
| ELECCIONES | Clasificación de colores |
| MAZDA | Configuración corporativa |
| ADI | Configuración personalizada |
| DISNEY | Header y footer personalizados |
| SCANBASE | Múltiples headers (frontpage, económicas, políticas) |
| DELL | Configuración corporativa |

---

## 🐛 Solución de Problemas

### **Error: "No se puede conectar al servidor"**
- Verificar que el servidor PHP esté corriendo
- Verificar que la API externa esté accesible
- Revisar logs del servidor

### **Error: "Imagen no se sube"**
- Verificar permisos de escritura en `backend/public/img/`
- Verificar tamaño de archivo (máximo 5MB)
- Verificar tipo de archivo (JPG, PNG, GIF)

### **Error: "React Router no funciona"**
- Verificar que `.htaccess` esté en `frontend/build/`
- Verificar que `mod_rewrite` esté habilitado
- Verificar configuración del Virtual Host

---

## 📚 Documentación Adicional

- **Requisitos de Producción**: Ver documentación de despliegue
- **Especificaciones Técnicas**: Ver documentación de servidor
- **API Backend**: Ver código en `backend/controllers/SintesisController.php`

---

## 👥 Contribución

Este es un proyecto interno de EFINFO. Para contribuir:
1. Crear una rama para la funcionalidad
2. Realizar cambios y pruebas
3. Solicitar revisión antes de merge

---

## 📄 Licencia

Proyecto interno de EFINFO - Todos los derechos reservados.

---

## 🔄 Versión

**Versión Actual**: 1.0.0

**Última Actualización**: 2025-01-27

---

## 📞 Soporte

Para problemas o preguntas:
1. Revisar logs del servidor
2. Verificar configuración de entorno
3. Consultar documentación técnica

---

**Desarrollado para EFINFO** 🚀

