# Agentes Tarifarios - Bolivia 🇧🇴

Este repositorio contiene un flujo de trabajo (workflow) compuesto por dos **skills** (agentes) diseñadas para la extracción, descarga y organización automatizada de Tarifarios y Tasas de Interés de la banca boliviana.

El proceso completo se divide en dos etapas interconectadas: **Extracción** y **Organización**.

---

## 🏗️ Flujo de Trabajo y Estructura de Directorios

El flujo de trabajo sigue una cadena de valor clara donde la salida de un agente es la entrada del siguiente:

```text
🌎 [Webs de Bancos Bolivianos]
       │
       ▼
🤖 Agente 1: Buscador de Tarifarios (1_Buscador_de_tarifarios.md)
       │
       ├─ 📥 Origen (Input): URLs de 12 entidades financieras listadas internamente.
       ├─ ⚙️ Proceso: Navegación automatizada, evasión de pop-ups y descarga de PDFs.
       └─ 📤 Salida (Output): Carpeta 📁 /Tarifarios_Bancos_[FECHA]/ (Contiene PDFs crudos y logs).
       
       │
       ▼
🤖 Agente 2: Organización de Tarifarios (2_Organizacion_tarifarios.md)
       │
       ├─ 📥 Origen (Input): Carpeta 📁 /Tarifarios_Bancos_[FECHA]/ generada por el Agente 1.
       ├─ ⚙️ Proceso: Conversión de PDF a texto (pdftotext) y extracción de información clave.
       └─ 📤 Salida (Output): Modificación de la carpeta en:
                ├─ 📁 /PDFs_Originales/
                ├─ 📁 /Textos_Convertidos/
                └─ 📄 Inventario_Productos.md
```

---

## 🚀 Skills Disponibles

### 1. Extracción: Buscador de Tarifarios (`1_Buscador_de_tarifarios.md`)
Es el punto de partida responsable de la recolección de los datos en bruto. Navega automáticamente por los sitios web de 12 bancos (privados y públicos), busca las secciones de "Tarifario" y descarga todos los documentos relevantes.

### 2. Análisis: Organización de Tarifarios (`2_Organizacion_tarifarios.md`)
Procesa la carpeta obtenida por el buscador, convierte los pesados archivos PDF a formato texto simple manejable, e identifica y consolida las tasas y productos financieros en inventarios fáciles de leer.

---

## ⚙️ Requisitos y Portabilidad

Para que la ejecución de la skill de **Organización** sea **100% portable y funcional** en cualquier sistema Windows **SIN necesidad de instalar Python, Node.js u otros lenguajes de programación**, este agente utiliza herramientas de línea de comandos precompiladas.

### Dependencia Principal: Xpdf (Lector de PDF por consola)
Dado que los bancos proveen la información en formato PDF, el agente necesita convertir estos archivos en texto plano (`.txt`) para poder extraer los datos.

**Instalación Rápida Automática:**
El agente está instruido para descargar autónomamente la herramienta oficial `xpdf-tools-win` y desempaquetarla en la ruta de trabajo actual mediante un simple puente de PowerShell:
```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Invoke-WebRequest -Uri "https://dl.xpdfreader.com/xpdf-tools-win-4.06.zip" -OutFile "xpdf.zip"
Expand-Archive -Path "xpdf.zip" -DestinationPath "xpdf"
```

**Uso Portable (Incorpóralo a la recolección):**
Una vez extraído el programa, el agente llama directamente al ejecutable (`pdftotext.exe`) para todos los PDFs recogidos, asegurando documentos `.txt` rápidos y listos para analizar:
```powershell
xpdf\xpdf-tools-win-4.06\bin64\pdftotext.exe -layout "Archivo_Banco.pdf" "Archivo_Banco.txt"
```

### Otras Consideraciones Técnicas
- **Sistema Operativo:** Diseñado primordialmente para entornos **Windows 10/11** (Requiere PowerShell).
- **Conexiones Seguras:** Muchos bancos bolivianos requieren protocolos seguros; el agente inyecta un bypass forzando conexiones TLS 1.2 (`[Net.SecurityProtocolType]::Tls12`), evitando que fallen las descargas.
- **Sin Instalaciones Permanentes:** Al terminar, la carpeta simplemente contendrá los datos y la utilidad `xpdf` sin instalar bloatware en el sistema.

## 💡 Cómo Usar
Llama a tu asistente Antigravity en esta carpeta y solicita:
> *"Ejecuta la skill Buscador de Tarifarios de acuerdo a 1_Buscador_de_tarifarios.md"*

Una vez que el primer agente finalice y genere la carpeta de archivos:
> *"Inicia la Organización de los tarifarios descargados usando 2_Organizacion_tarifarios.md"*
