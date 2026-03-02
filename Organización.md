---
name: organizacion-de-tarifarios
description: Organiza y clasifica la información de los productos financieros extraídos de los tarifarios de bancos bolivianos.
---

# Organización de Tarifarios

Tu tarea es analizar la información recopilada en la carpeta `Tarifarios_Bancos_Bolivia` y organizar los productos financieros identificados para facilitar su comparación y consulta.

## Productos Identificados en los Tarifarios

Basado en la extracción realizada, se han identificado los siguientes productos y categorías principales:

1.  **Cuentas de Ahorro:** Condiciones, tasas y comisiones para cajas de ahorro (Ej: Banco Prodem).
2.  **Depósitos a Plazo Fijo (DPF):** Tasas de interés según el plazo y moneda (Ej: Banco Prodem, Banco Nacional de Bolivia).
3.  **Tarifas de Créditos (Tasas Activas):** Comisiones y tasas para créditos de consumo, vivienda, microcrédito y PyME (Ej: BCP, Banco FIE, Banco Unión).
4.  **Tasas Pasivas:** Tasas de interés pagadas por el banco a los ahorristas (Ej: Banco FIE).
5.  **Servicios Complementarios:** Comisiones por giros, transferencias, uso de cajeros, emisión de tarjetas y bóveda (Ej: Banco Económico, Banco Unión, Banco FIE).
6.  **Boletas de Garantía y Fianzas:** Costos asociados a garantías bancarias (Ej: Banco Prodem).
7.  **Operaciones de Comercio Exterior:** Comisiones por cartas de crédito y transferencias internacionales (Ej: BCP).
8.  **Tarifarios Generales:** Documentos consolidados que abarcan múltiples servicios normados por ASFI.

## Pasos para la Organización

1.  **Clasificación por Carpeta:**
    Crea subcarpetas dentro de la carpeta con fecha para agrupar los archivos por tipo de producto si el usuario lo solicita.

2.  **Identificación de Datos Clave:**
    Por cada documento, identifica:
    - Nombre del Banco.
    - Tipo de Producto / Categoría.
    - Fecha de vigencia del tarifario.

3.  **Mantenimiento del Inventario:**
    Actualiza el archivo `Estado_Extraccion.txt` o crea uno nuevo llamado `Inventario_Productos.md` que liste qué productos han sido actualizados por cada banco.

## Resultado Esperado
Un repositorio de tarifarios perfectamente clasificado donde el usuario pueda localizar rápidamente las tasas de un producto específico (ej: "DPF") entre todos los bancos analizados.
