# TechStore — Consultas Básicas SELECT y Alias de Columnas

Repositorio correspondiente a la práctica de extracción de datos SQL para el equipo de finanzas de TechStore.

## Estructura del Proyecto
- `consultas_basicas.sql`: Script SQL con el esquema de prueba y las 3 consultas requeridas (exploración, columnas específicas y alias).
- `README.md`: Documentación y fundamentación técnica de las decisiones de consulta.

---

## Preguntas Teóricas y Fundamentación

### 1. ¿Por qué es mala práctica usar `SELECT *` en producción?
El uso de `SELECT *` en entornos productivos o reportes automatizados debe evitarse por las siguientes razones:
- **Rendimiento y consumo de red:** Obliga al motor de base de datos a transferir todas las columnas por la red hacia el cliente o reporte, aumentando la latencia y saturando la memoria del servidor de manera innecesaria.
- **Mantenibilidad y rotura de aplicaciones:** Si el esquema de la tabla cambia en el futuro (por ejemplo, si se agrega, renombra o elimina una columna), los procesos dependientes (APIs, modelos de Power BI, scripts de Python) pueden fallar por discrepancias en el orden o tipo de campos esperados.
- **Seguridad:** Puede exponer datos sensibles o confidenciales que no forman parte de la necesidad del reporte (datos personales, tokens, costos internos).

### 2. ¿Por qué son importantes los alias para un stakeholder no técnico?
Los alias (`AS`) permiten traducir la nomenclatura técnica o estructurada de las bases de datos a un lenguaje de negocio comprensible y amigable.
- **Ejemplo práctico:** Una columna llamada originalmente `total_amount` puede generar dudas en finanzas sobre si se refiere a costo bruto, margen o valor facturado. Al renombrarla mediante:
  ```sql
  SELECT total_amount AS monto_total_facturado FROM sales;
