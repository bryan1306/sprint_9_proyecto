# sprint_9_proyecto

📊 Proyecto: Priorización de hipótesis y análisis A/B para optimización de ingresos en e-commerce
📌 Descripción del proyecto

Este proyecto tiene como objetivo identificar, priorizar y validar iniciativas de mejora que puedan aumentar los ingresos de una tienda online.
Para ello se implementan dos etapas:

Priorización de hipótesis mediante los métodos ICE y RICE, con el fin de identificar las ideas más prometedoras para implementar rápidamente.

Análisis estadístico de un experimento A/B, evaluando métricas clave como:

Ingreso acumulado

Ticket promedio

Tasa de conversión

Impacto de outliers

Significancia estadística con pruebas z-test y Mann-Whitney

El análisis permite fundamentar decisiones estratégicas en evidencia cuantitativa y determinar si el experimento debe finalizar, continuar o si existe un grupo claramente ganador.

🛠️ Librerías utilizadas
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
from statsmodels.stats.proportion import proportions_ztest
from datetime import timedelta

📂 1. Carga y exploración de los datos

Se cargaron los siguientes datasets:

hypotheses_us.csv → contiene las hipótesis y sus parámetros (Reach, Impact, Confidence, Effort)

orders_us.csv → pedidos realizados por usuarios

visits_us.csv → visitas diarias por grupo

No se encontraron valores nulos.
Se realizó la conversión de columnas de fecha al tipo datetime para facilitar el análisis.

🚦 2. Priorización de hipótesis (ICE y RICE)
✔️ Fórmulas utilizadas


<img width="627" height="226" alt="image" src="https://github.com/user-attachments/assets/8c8499d7-3885-4e7b-a390-f0efe5a982fc" />
	​

✔️ Resultados clave

RICE prioriza más fuertemente las hipótesis con mayor alcance.

ICE destaca ideas rápidas de implementar con alto impacto.

La hipótesis más prioritaria según RICE fue:
"Agregar un formulario de suscripción en todas las páginas principales" (112 puntos).

📝 Conclusión

Las hipótesis que aparecen en puestos altos en ambos rankings deben considerarse prioritarias, ya que presentan un equilibrio óptimo entre alcance, impacto y esfuerzo.

🧪 3. Análisis del Test A/B
3.1 Ingreso acumulado

El grupo B muestra un crecimiento más acelerado desde mitad del experimento, separándose significativamente del grupo A.

3.2 Ticket promedio acumulado

El grupo B supera al A luego de un incremento abrupto en la segunda mitad del experimento, manteniendo una tendencia estable al alza.

3.3 Diferencia relativa del ticket promedio

Desde el 18 de agosto, B mantiene una ventaja relativa estable de ~40% sobre A.

3.4 Conversión diaria

El grupo B tiene mejores tasas de conversión a lo largo de la prueba, alcanzando picos superiores al 5%.

🔍 4. Análisis de outliers

Pedidos por usuario (percentiles):

P95 = 2 pedidos

P99 = 4 pedidos
➝ Usuarios con más de 4 pedidos se consideran anomalías.

Revenue por pedido (percentiles):

P95 = 435.54

P99 = 900.90
➝ Pedidos > 901 USD se consideran outliers.

Se filtraron los datos eliminando usuarios y pedidos atípicos para repetir las pruebas estadísticas.

📊 5. Pruebas estadísticas
✔️ Conversión (sin filtrar)

p-valor = 0.0232 (< 0.05)
→ diferencia significativa entre A y B.

✔️ Ticket promedio (sin filtrar)

p-valor = 0.6915 (> 0.05)
→ no hay diferencias significativas.

✔️ Conversión (filtrado)

p-valor = 0.0142 (< 0.05)
→ la diferencia sigue siendo significativa.

✔️ Ticket promedio (filtrado)

p-valor = 0.9332 (> 0.05)
→ no hay diferencia.

🧠 6. Conclusiones

El grupo B presenta una mejor tasa de conversión, incluso tras el filtrado.

No existe diferencia significativa en el ticket promedio entre A y B.

El ingreso acumulado muestra una tendencia más favorable para el grupo B.

El efecto positivo parece estar impulsado por mayor conversión, no por aumento del valor de compra.

📝 7. Decisión final
✅ Decisión: Continuar la prueba

Aunque el grupo B muestra ventaja significativa en conversión, aún no existe evidencia suficiente en ticket promedio o ingresos totales para declarar un ganador definitivo. Se recomienda extender el experimento para confirmar si la diferencia se mantiene y se traduce en mayor rentabilidad.

🚀 8. Líneas de mejora futura

Implementar un análisis por segmentos (nuevos vs recurrentes, tramos de ingreso).

Evaluar efectos de estacionalidad.

Realizar un test A/B con más variantes.

Integrar dashboards interactivos con Plotly o Power BI.

Automatizar todo el pipeline con scripts modulares.
