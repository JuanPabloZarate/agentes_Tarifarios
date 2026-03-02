---
name: organizacion-de-tarifarios
description: Consolida los archivos descargados. Convierte PDFs en texto y genera un inventario legible y compararable de productos financieros.
---

# Organización de Tarifarios (Agente de Análisis)

Tu tarea es tomar la información en estado crudo recolectada en la etapa anterior, extraer su texto de forma automatizada y estructurar los datos extraídos para que las tasas sean fáciles de comparar.

Este agente actúa como la **Fase 2** del flujo de trabajo general.

### 📥 Origen (Input)
La carpeta raíz generada en la fase previa que contiene los archivos crudos (Ej: `/Tarifarios_Bancos_Bolivia_[FECHA]/`).

### 📤 Salida (Output)
La reestructuración de dicha carpeta generará:
- 📁 `PDFs_Originales/`: Subcarpeta que hospedará todos los PDF descargados originalmente para su resguardo.
- 📁 `Textos_Convertidos/`: Subcarpeta que contendrá textos legibles (convertidos por consola).
- 📄 `Inventario_Productos.md`: Documento consolidado con la organización y comparación de las tasas encontradas.

---

## Pasos para la Organización

1. **Reestructuración de la Carpeta de Origen:**
   Accede a la carpeta raíz indicada por el usuario como Origen y crea en su interior dos subcarpetas: `PDFs_Originales` y `Textos_Convertidos`.

2. **Transformación de PDF a texto plano (`.txt`):**
   Para poder analizar la información eficientemente usando un LLM, primero debes convertir los PDFs a texto.
   - Si no lo has hecho, descarga `xpdf-tools-win` y extráelo localmente.
   - Para cada PDF que esté en la raíz de la carpeta de origen, ejecuta la utilidad `pdftotext.exe` asegurando emplear el flag `-layout`.
   - El archivo de texto `.txt` generado guárdalo en la subcarpeta `Textos_Convertidos`.
   - Luego, mueve el archivo `.pdf` en crudo que ya verificaste a la carpeta `PDFs_Originales`.
   - Al finalizar, la base de la carpeta deberá quedar limpia sin PDFs.

3. **Análisis e Identificación de Productos (Generación de Conocimiento):**
   Lee los `.txt` generados e identifica sistemáticamente los siguientes productos e información en los textos:
   * **Cuentas de Ahorro:** Condiciones generales, saldos mínimos y tasas o comisiones aplicables.
   * **Depósitos a Plazo Fijo (DPF):** Tasas de interés según plazo y moneda.
   * **Tarifas de Créditos (Tasas Activas):** Tasas para consumo, vivienda o microcréditos empresariales.
   * **Servicios Complementarios bancarios:** Comisiones por transferencias, estado de cuenta, emisión de tarjetas, etc.
   * **Boletas de Garantía y Comerciales:** Costos vinculados y exportaciones.

4. **Reporte Consolidado (Inventario_Productos.md):**
   Con todos los datos detectados, crea en la base de la carpeta el archivo `Inventario_Productos.md`. Documenta cuáles bancos brindan qué productos, sus tasas clave de referencia y toda observación relevante encontrada de forma estructurada.

## Resultado Esperado Final
Al concluir el análisis, le informarás al usuario que la organización fue completada con éxito. Muéstrale las modificaciones realizadas en las subcarpetas de la ruta original y bríndale extractos de la información detectada en el gran inventario final (las tasas de rendimiento generales encontradas del sistema financiero, etc.).
