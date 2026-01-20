# Proyecto 6 — Análisis de una empresa de telecomunicaciones (ConnectaTel)

## Objetivo del proyecto
Analizar cómo los clientes usan los servicios móviles de **ConnectaTel** (llamadas y mensajes) en México y Colombia para:
- identificar patrones de uso,
- detectar comportamientos atípicos (outliers),
- segmentar clientes por edad y nivel de uso,
- proponer recomendaciones para optimizar la oferta comercial y mejorar la experiencia del usuario.

---

## Datasets utilizados
Este proyecto utiliza **tres fuentes de datos**:

1. **`plans.csv`**
   - Catálogo de planes actuales (precio, minutos/GB incluidos, costo por extras, etc.).

2. **`users_latam.csv`**
   - Información de clientes: `user_id`, edad, ciudad, fecha de registro, plan contratado, churn.

3. **`usage.csv`**
   - Uso real de servicios: registros por usuario de llamadas y mensajes (tipo, fecha, duración y longitud).

---

## Etapas del análisis realizadas
1. **Carga y exploración inicial**
   - Revisión de estructura, tipos de datos, tamaño y primeras filas.
   - Conteo de duplicados y valores faltantes.

2. **Calidad de datos**
   - Identificación de valores inválidos o sentinels (ej. `age = -999`, `city = '?'`).
   - Revisión y estandarización de fechas (detección de años fuera de rango).

3. **Limpieza básica**
   - Reemplazo de sentinels:
     - `age = -999` → reemplazado por la mediana.
     - `city = '?'` → marcado como nulo.
   - Fechas fuera de rango:
     - `reg_date` con años > 2024 → marcado como nulo (NaT).
   - Validación de valores faltantes MAR:
     - `duration` y `length` se dejan como nulos al depender de `type` (call/text).

4. **Construcción del perfil de uso por usuario**
   - Agregación de `usage` por `user_id` para obtener:
     - total de mensajes (`cant_mensajes`)
     - total de llamadas (`cant_llamadas`)
     - total de minutos de llamadas (`cant_minutos_llamada`)
   - Unión del perfil agregado con `users` para crear `user_profile`.

5. **Summary statistics**
   - Resumen estadístico de variables numéricas.
   - Distribución porcentual del tipo de plan.

6. **Visualización y detección de outliers**
   - Histogramas (con `hue='plan'`) para comparar distribuciones por plan:
     - `age`, `cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`
   - Boxplots para identificación visual de outliers.
   - Cálculo de límites IQR por variable (para cuantificar outliers).

7. **Segmentación de clientes**
   - Segmentación por uso:
     - `Bajo uso`, `Uso medio`, `Alto uso` según llamadas y mensajes.
   - Segmentación por edad:
     - `Joven`, `Adulto`, `Adulto Mayor`.
   - Visualización con `countplot`.

8. **Insight ejecutivo**
   - Conclusiones accionables para stakeholders:
     - problemas de datos detectados,
     - comportamiento por segmentos,
     - implicaciones de outliers,
     - recomendaciones comerciales.

---
