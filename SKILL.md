---
name: buscador-de-tarifarios
description: Ingresa a las páginas web de bancos de Bolivia, busca la sección "Tarifario", extrae la información (texto o PDF) y la guarda en una carpeta.
---

# Buscador de Tarifarios

Tu tarea es recorrer una lista predefinida de páginas web correspondientes a los bancos de Bolivia, buscar la información de sus tarifarios y extraer dicha información, ya sea descargando los archivos PDF o copiando el texto de las subpáginas a archivos de texto. Todo esto debe almacenarse ordenadamente en una carpeta.

## Pasos de Ejecución

1. **Creación de Carpeta de Almacenamiento:**
   Crea una carpeta local (por defecto puede llamarse `Tarifarios_Bancos_Bolivia` o usar la ruta que el usuario indique) que servirá como repositorio de toda la información extraída.

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
   Debido a que las páginas bancarias suelen incluir modales emergentes (pop-ups) y diseños complejos, **usa `browser_subagent`** para recorrer visualmente la web y ubicar el acceso al "Tarifario" (generalmente en el pie de página o menús transparentes).
   **¡Importante!** Varios bancos (como BCP, FIE, Prodem, etc.) tienen sus tarifarios divididos en **múltiples documentos** (Tasas Activas, Tasas Pasivas, Servicios Complementarios). Asegúrate de obtener todas las URLs, no te detengas al encontrar el primer PDF.

4. **Extracción y Guardado de Información (Técnica Robusta):**
   * **Si el enlace dirige a uno o varios PDFs:** Descárgalos al equipo. **Obligatorio:** Para evitar errores de seguridad SSL/TLS muy comunes en sitios de bancos, utiliza en la terminal de Windows un comando PowerShell que fuerce TLS 1.2. Ejemplo:
     `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; Invoke-WebRequest -Uri "URL_DEL_PDF" -OutFile "Ruta_Destino\[Banco] - [Categoría].pdf"`
   * **Si el enlace dirige a una subpágina HTML:** Extrae manualmente el texto más relevante sobre las tasas, crea un archivo de texto (`[Banco] - Tarifario InfoWeb.txt`) y guárdalo en la misma carpeta.

5. **Manejo de Errores e Incidencias:**
   * Si no encuentras el enlace "Tarifario" en una página, o si la página principal no está disponible, registra el evento en un archivo resumen llamado `Estado_Extraccion.txt` dentro de la misma carpeta indicando qué pasó con ese banco.
   * Continúa con el siguiente banco de la lista sin detener la ejecución global.

6. **Creación de Tabla de Comparación y Resumen:**
   * Al finalizar la extracción de todos los bancos, consolida la información extraída (leyendo los PDFs descargados y los archivos de texto InfoWeb).
   * Agrupa los datos y genera un archivo final (puede ser `Resumen_Comparativo.md` o un archivo CSV) que contenga una tabla comparativa con los principales tipos de tasas, comisiones y servicios de cada banco.
   * Esto permitirá al usuario tener una vista rápida y consolidada de todos los tarifarios recopilados.

## Resultado Esperado
Al finalizar, la skill debe reportar al usuario que ha terminado y mostrar un resumen de cuántos tarifarios fueron exitosamente extraídos (PDFs y textos) y cuántos fallaron. El usuario debe poder ir directamente a la carpeta para consultar la información resultante.
