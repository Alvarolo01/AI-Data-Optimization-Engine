# 🚀 AI Data Optimization & Validation Engine

Este proyecto implementa una infraestructura de **Ingeniería de Software** para la validación y limpieza de datasets destinados al entrenamiento de modelos de lenguaje (LLM). Está diseñado bajo principios de **Arquitectura Limpia** para garantizar escalabilidad y alto rendimiento.

## 🛠️ Stack Tecnológico
* **Lenguaje:** Python 3.10+ (con Tipado Estático).
* **Procesamiento:** NumPy & Pandas (Lógica vectorizada para evitar latencia).
* **Validación de Datos:** SQL avanzado para auditoría de integridad.

## 📊 Módulo SQL Avanzado (Validación de Producción)
Como parte del proceso de calidad, se incluye la lógica de validación para bases de datos relacionales:

```sql
WITH RawMetrics AS (
    SELECT 
        prompt_id,
        accuracy_score,
        latency_ms,
        AVG(accuracy_score) OVER(PARTITION BY batch_id) as batch_avg
    FROM IA_Production_Logs
    WHERE timestamp >= CURRENT_DATE - INTERVAL '30 days'
)
SELECT * FROM RawMetrics
WHERE accuracy_score > batch_avg AND latency_ms < 250
ORDER BY accuracy_score DESC;
