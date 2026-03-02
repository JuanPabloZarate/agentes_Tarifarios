# Agentes Tarifarios - Bolivia 🇧🇴

Este repositorio contiene un conjunto de **skills** (agentes) diseñadas para la extracción, descarga y organización automatizada de Tarifarios y Tasas de Interés de la banca boliviana.

## 🚀 Skills Disponibles

1. **Buscador de Tarifarios (`SKILL.md`)**
   Una skill que navega automáticamente por los sitios web de 12 entidades financieras (privadas y públicas) de Bolivia, busca las secciones de "Tarifario" y descarga todos los PDFs y la información web a una carpeta estructurada y fechada.

2. **Organización de Tarifarios (`Organización.md`)**
   Una skill que procesa la carpeta obtenida, convierte los PDFs a formato texto simple manejable y consolida las tasas y productos financieros en inventarios y tablas comparativas.

---

## ⚙️ Requisitos y Portabilidad

Para que la ejecución de la skill de **Organización** sea **100% portable y funcional** en cualquier sistema Windows **SIN necesidad de instalar Python, Node.js u otros lenguajes de programación**, este agente utiliza herramientas de línea de comandos precompiladas.

### Dependencia Principal: Xpdf (Lector de PDF por consola)
Dado que los bancos proveen la información en formato PDF, el agente necesita convertir estos archivos en texto plano (`.txt`) para poder extraer los datos (como las tasas y comisiones).

**Instalación Rápida Automática:**
El agente está instruido para descargar autónomamente la herramienta oficial `xpdf-tools-win` y desempaquetarla en la ruta de trabajo actual. Utiliza un simple script en PowerShell que hace todo el trabajo por ti:
```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Invoke-WebRequest -Uri "https://dl.xpdfreader.com/xpdf-tools-win-4.06.zip" -OutFile "xpdf.zip"
Expand-Archive -Path "xpdf.zip" -DestinationPath "xpdf"
```

**Uso Portable (Incorpóralo a la recolección):**
Una vez extraído el programa, el agente llama directamente al ejecutable (`pdftotext.exe`) para todos los PDFs recogidos, asegurando que cualquier usuario, sin conocimientos técnicos o software pesado instalado, obtenga documentos `.txt` ligeros, transparentes y listos para leer en un Bloc de Notas o para nutrir al modelo:
```powershell
xpdf\xpdf-tools-win-4.06\bin64\pdftotext.exe -layout "Archivo_Banco.pdf" "Archivo_Banco.txt"
```

### Otras Consideraciones Técnicas
- **Sistema Operativo:** Diseñado primordialmente para entornos **Windows 10/11** (Requiere PowerShell).
- **Conexiones Seguras:** Muchos bancos bolivianos requieren protocolos seguros y modernos; el agente inyecta un bypass para Windows forzando conexiones TLS 1.2 (`[Net.SecurityProtocolType]::Tls12`), evitando que fallen las descargas.
- **Sin Instalaciones Permanentes:** Al terminar, la carpeta simplemente contendrá los datos y la utilidad `xpdf` extraída ahí mismo sin ensuciar tu sistema.

## 💡 Cómo Usar
Llama a tu asistente Antigravity en esta carpeta y solicita:
> *"Ejecuta la skill Buscador de Tarifarios (SKILL.md)"*

O, una vez descargados los archivos:
> *"Realiza la Organización según el archivo Organización.md"*
