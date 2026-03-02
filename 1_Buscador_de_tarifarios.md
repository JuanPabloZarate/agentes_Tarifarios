---
name: buscador-de-tarifarios
description: Ingresa a las páginas web de bancos de Bolivia, extrae los tarifarios y consolida los documentos en una carpeta base.
---

# Buscador de Tarifarios (Agente de Extracción)

Tu tarea es recorrer una lista predefinida de páginas web correspondientes a los bancos de Bolivia, buscar la información de sus tarifarios y descargarlos de forma ordenada.

Este agente actúa como la **Fase 1** del flujo de trabajo general.

### 📥 Origen (Input)
Uso de URLs predefinidas de 12 entidades financieras bolivianas.

### 📤 Salida (Output)
Carpeta creada (ej. `Tarifarios_Bancos_Bolivia_[FECHA]`) que funcionará como raíz para contener los PDFs descargados, textos web y un `Estado_Extraccion.txt`.

---

## Pasos de Ejecución

1. **Creación de Carpeta de Almacenamiento:**
   Crea una carpeta local que obligatoriamente contenga la fecha de ejecución (por ejemplo, `Tarifarios_Bancos_Bolivia_2026-03-02`). Todas las descargas deben ir directamente a la raíz de esta nueva carpeta.

2. **Recorrer la Lista de Bancos:**
   Accede a las páginas web de las siguientes entidades financieras:

   **Bancos Privados:**
   * Banco Nacional de Bolivia (BNB) - `www.bnb.com.bo`
   * Banco Mercantil Santa Cruz - `www.bmsc.com.bo`
   * Banco Bisa - `www.bisa.com`
   * Banco de Crédito de Bolivia (BCP) - `www.bcp.com.bo`
   * Banco Económico - `www.baneco.com.bo`
   * Banco Ganadero - `www.bg.com.bo`
   * Banco Solidario (BancoSol) - `www.bancosol.com.bo`
   * Banco FIE - `www.bancofie.com.bo`
   * Banco Fortaleza - `www.bancofortaleza.com.bo`
   * Banco Prodem - `www.prodem.com.bo`

   **Bancos Públicos y de Desarrollo:**
   * Banco Unión - `www.bancounion.com.bo`
   * Banco de Desarrollo Productivo (BDP) - `www.bdp.com.bo`

3. **Búsqueda del "Tarifario" (Uso de `browser_subagent`):**
   Debido a que las páginas bancarias suelen tener un diseño complejo o pop-ups, **usa el `browser_subagent`** para recorrer la web y ubicar el enlace a "Tarifario".
   **¡Importante!** Varios bancos (como BCP, FIE, Prodem) tienen sus tarifarios divididos en **múltiples documentos** (Tasas Activas, Pasivas, Servicios). Descarga siempre TODOS los documentos del tarifario, no solo el primero.

4. **Extracción y Guardado robusto:**
   * **Descarga de PDFs (Obligatorio TLS 1.2):** Evita errores SSL ejecutando la descarga mediante PowerShell desde la terminal de Windows:
     `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; Invoke-WebRequest -Uri "URL_DEL_PDF" -OutFile "Ruta_Destino\[Banco] - [Categoría].pdf"`
   * **Extracción de Texto:** Si las tarifas están escritas en la propia página HTML en vez de en un PDF, extrae el texto en un archivo `[Banco] - Tarifario_Web.txt` dentro de la misma carpeta raíz.

5. **Mantenimiento de Logs de Errores e Incidencias:**
   Si la página falla o no se puede hallar el tarifario, registra el evento en un archivo resumen llamado `Estado_Extraccion.txt` en la misma carpeta raíz, e inmediatamente continúa con el siguiente banco de la lista.

## Resultado Esperado Final
Debes informarle al usuario la ruta exacta de la carpeta creada y mostrarle en pantalla un resumen de la información extraída, indicando qué se pudo bajar y qué no basándote en el archivo de log. Aclara que la carpeta de destino actuará como **Origen (Input)** para la siguiente etapa de organización.
