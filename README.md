# 📊 People Analytics: Estrategia de Retención de Talento

## 1. Contexto del proyecto
En un mercado laboral competitivo, la rotación de personal (*Attrition*) representa uno de los costos ocultos más altos para las organizaciones. Este proyecto simula un encargo de consultoría de Business Intelligence con el objetivo de transformar datos de RRHH en decisiones estratégicas.

**Objetivo:** Identificar los patrones de comportamiento que preceden a la renuncia de un empleado y proponer acciones preventivas basadas en datos.

## 2. La pregunta de negocio
El dashboard busca responder:
> **"¿Qué factores (carga laboral, salario, estancamiento profesional) son los principales detonantes de la fuga de talento y qué segmentos de empleados están en mayor riesgo hoy?"**

## 3. Fuente de datos
Se utilizó el dataset público **IBM HR Analytics Employee Attrition**.
- **Volumen:** 1,470 registros históricos.
- **Naturaleza:** Datos demográficos, métricas de satisfacción, historial de promociones y estatus de salida.

## 4. Arquitectura de la solución
### A. Procesamiento de datos (Python & Pandas)
El script `etl_hr_process.py` se encargó de la ingesta y preparación inicial (`Extract & Transform`):
* **Enriquecimiento Semántico:** Se decodificaron variables numéricas (ej. `Education=1` → 'Below College') para hacer los datos comprensibles al usuario de negocio.
* **Segmentación (Binning):** Creación de cohortes generacionales (`Age_Group`) y rangos salariales para permitir comparativas justas.
* **Limpieza:** Estandarización de tipos de datos para su correcta lectura en la herramienta de visualización.

### B. Lógica de negocio (Dashboard)
Para el cálculo del **Riesgo de Burnout**, se optó por implementar una **Columna Calculada (DAX/Campos Calculados)** directamente en la herramienta de visualización en lugar de pre-calcularla en Python.
* *Justificación:* Esto permite al usuario ajustar los umbrales de riesgo (ej. cambiar qué se considera "baja satisfacción") dinámicamente sin necesidad de ejecutar nuevamente el script ETL.
* *Regla aplicada:* Si el empleado hace Horas Extras (`OverTime=1`) Y su satisfacción ambiental es baja (<=2) → **🔴 Alto Riesgo**.

## 5. Diseño del Dashboard y UX
El panel visual sigue una narrativa de tres niveles:
1.  **Nivel Ejecutivo (KPIs):** Visión inmediata de la Tasa de Rotación Global (16.1%) y volumen de empleados en riesgo.
2.  **Nivel Táctico (Causas Raíz):** Gráficos de relación que validan hipótesis (ej. Impacto de las Horas Extra en la renuncia).
3.  **Nivel Operativo (Detalle):** Desglose por Departamento y Rol para focalizar las intervenciones de RRHH.

## 6. Hallazgos Clave (Insights)
* **El impacto del Burnout:** Los empleados que realizan horas extra tienen una tasa de renuncia del **30.5%**, triplicando la tasa de quienes tienen jornada estándar (**10.4%**).
* **Áreas Críticas:** El departamento de Ventas y el rol de "Sales Representative" presentan la mayor vulnerabilidad, sugiriendo la necesidad de revisar los esquemas de incentivos y carga laboral en esa área específica.

---
*Herramientas utilizadas: Python (Pandas, Kagglehub), Power BI, GitHub.*
