# Pasos del Proyecto: Análisis de Tarifarios Bancarios 🇧🇴

A continuación se detalla el flujo de trabajo completo y las etapas para la construcción del sistema de agentes de análisis de tarifarios:

### 1. Buscador (Extracción)
Agente encargado de navegar automáticamente por las páginas web de los bancos bolivianos, identificar las secciones relevantes y descargar los documentos de tarifarios (PDFs o textos web) en su formato original.

### 2. Organización
Agente responsable de estructurar los archivos descargados. Se encarga de separar los PDFs originales en carpetas de resguardo y convertirlos a texto plano utilizando herramientas como `xpdf` para facilitar su procesamiento posterior por LLMs.

### 3. Identificación de Productos
Fase de procesamiento donde se lee la información en texto plano para detectar y clasificar sistemáticamente los diferentes productos financieros presentes (por ejemplo: cuentas de ahorro, depósitos a plazo fijo, tipos de créditos, servicios complementarios, etc.).

### 4. Análisis por cada Banco
Evaluación individualizada y estructuración de los datos extraídos para cada entidad financiera. Se analizan las tasas, comisiones, requisitos y condiciones particulares de los productos identificados.

### 5. Generación de Documento / Infografía
Creación de reportes resumidos, documentos consolidados o infografías que presenten los datos clave de manera visualmente atractiva y fácil de consumir para el usuario final o cliente.

### 6. Muestras de Propuestas o Diferencias entre Bancos
Elaboración de comparativas o "benchmarks" finales que resalten las ventajas, desventajas y diferencias en tasas de interés (tasas activas y pasivas) entre los distintos bancos. Esto permite generar propuestas de valor informadas.
