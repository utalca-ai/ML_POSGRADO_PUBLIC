# Semana 6 · Métricas y calibración


- [1. De qué trata esta semana](#1-de-qué-trata-esta-semana)
- [2. Qué debería poder hacer al terminar la
  semana](#2-qué-debería-poder-hacer-al-terminar-la-semana)
- [3. La sesión sincrónica](#3-la-sesión-sincrónica)
- [4. Notación y definiciones](#4-notación-y-definiciones)
- [5. Trabajo autónomo de la semana](#5-trabajo-autónomo-de-la-semana)
- [6. Lecturas](#6-lecturas)
- [7. Preguntas de comprobación](#7-preguntas-de-comprobación)
- [8. Materiales de esta semana](#8-materiales-de-esta-semana)
- [9. La próxima semana](#9-la-próxima-semana)

> **Cómo usar esta guía.** Dice qué pasa en la sesión sincrónica, qué
> tiene que hacer usted por su cuenta, cuánto tiempo tomar cada cosa y
> con qué se corrige.

|  |  |
|----|----|
| **Unidad** | 3 · Evaluación y diseño experimental |
| **Sesión de clase** | Métricas y su pertinencia · calibración de probabilidades |
| **Actividad** | **Taller 3** (2 hp) |
| **Hito calificado** | **Entrega del taller 3** |
| **Trabajo sincrónico** | 4 hp: 2 de clase + 2 de taller |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Desde la semana 1 aparece una pregunta que hasta ahora quedaba retórica:
*¿qué cuesta cada tipo de error?* Esta semana deja de serlo.

La primera parte muestra que **la métrica por defecto casi siempre
miente** en problemas desbalanceados, y que la elección de métrica es
una decisión sobre costos disfrazada de tecnicismo. La segunda añade un
supuesto que la primera necesita y que casi nadie comprueba: que las
probabilidades del modelo **signifiquen** algo.

## 2. Qué debería poder hacer al terminar la semana

1.  Explicar por qué el acierto es inútil con clases desbalanceadas, y
    qué referencia hay que reportar en su lugar.
2.  Decir qué pregunta responde la sensibilidad y cuál la precisión, y
    por qué solo la segunda depende de la prevalencia.
3.  Elegir entre ROC y precisión-exhaustividad con un argumento, y
    conocer la trampa de cada una.
4.  Derivar el umbral de operación de una razón de costos.
5.  Comprobar si un modelo está calibrado, y recalibrarlo **sin** gastar
    el conjunto de prueba.

## 3. La sesión sincrónica

| Bloque                        | Duración    | Material                       |
|-------------------------------|-------------|--------------------------------|
| Métricas y costos asimétricos | 50 min      | `clase06a`, 17 láminas         |
| Calibración de probabilidades | 50 min      | `clase06b`, 17 láminas         |
| **Taller 3**                  | 2 hp aparte | Métrica y curva de calibración |

## 4. Notación y definiciones

**La matriz de confusión.** Cuatro números: VP, FN, FP, VN. Todo lo
demás son razones entre ellos, y **todo escalar descarta información**.

$$\text{Sensibilidad}=\frac{VP}{VP+FN}
\qquad
\text{Precisión}=\frac{VP}{VP+FP}$$

La diferencia está en el denominador: la sensibilidad divide entre los
positivos reales y **no depende de la prevalencia**; la precisión divide
entre las alertas emitidas y **sí depende**.

**$F_1$** es la media armónica de ambas, y por tanto **afirma que
precisión y sensibilidad valen lo mismo**. Si en su problema no es
cierto, es la métrica equivocada.

**Curvas.** La ROC grafica $\text{TVP}=VP/(VP+FN)$ contra
$\text{TFP}=FP/(FP+VN)$. Ambos denominadores están **dentro de una sola
clase**, así que la ROC no cambia con la prevalencia —y por eso engaña
con desbalance fuerte. La curva de precisión-exhaustividad sí lo nota, y
su línea base es la prevalencia, no 0,5.

**Costo esperado y umbral óptimo.**

$$\text{Costo}=c_{FN}\cdot FN+c_{FP}\cdot FP
\qquad\Longrightarrow\qquad
t^\star=\frac{c_{FP}}{c_{FP}+c_{FN}}$$

No hace falta conocer los costos exactos: **basta la razón**. Si una
falla cuesta 100 inspecciones, $t^\star\approx 0{,}01$ —no 0,5.

**Calibración.**

$$\Pr\bigl(y=1\mid \hat p(x)=q\bigr)=q\quad\text{para todo }q$$

Es **independiente** de la capacidad de discriminar. El AUC-ROC es
invariante a transformaciones monótonas, así que **no ve la calibración
en absoluto**.

$$\text{ECE}=\sum_{m=1}^{M}\frac{|B_m|}{n}\Bigl|\,\overline{y}(B_m)-\overline{p}(B_m)\Bigr|
\qquad
\text{Brier}=\frac{1}{n}\sum_{i=1}^{n}\bigl(\hat p_i-y_i\bigr)^2$$

**El umbral óptimo supone probabilidades calibradas.** Si no lo están,
la fórmula no significa nada.

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Leer Kapoor y Narayanan (2023) — **obligatoria** | 2,0 h | Notas propias | Antes de la reseña |
| 2 | Escribir la **reseña 3** | 2,0 h | 2 páginas | **48 h antes de la sesión de la semana 7** |
| 3 | Completar y entregar el **taller 3** | 1,5 h | Cuaderno + bitácora | Fin de semana 6 |
| 4 | Ejecutar y estudiar el cuaderno de la clase | 1,0 h | Cuaderno corrido | Antes de la semana 7 |

Demšar (2006) es la segunda lectura del seminario 3 y es técnica;
conviene empezarla esta semana aunque se termine la siguiente.

### 5.1 El taller 3

**Elección de métrica y curva de calibración sobre un problema
desbalanceado.**

Los ítems de la lista de cotejo que concentran los problemas esta
semana:

- **Ítem 6 (métrica justificada por el problema).** La justificación se
  escribe **antes** de ver los resultados. Elegir la métrica después de
  mirarlos es seleccionar la fluctuación favorable: el sesgo optimista
  de la semana 1.
- **Ítem 3 (protocolo sin fuga).** Recalibrar es una decisión. Si ajusta
  la función de recalibración con los datos de entrenamiento no
  funciona, y si la ajusta con el conjunto de prueba, el error que
  reporta ya no es insesgado. Necesita **tres particiones**, no dos.

### 5.2 Qué mirar en el cuaderno

`clase06_metricas_y_calibracion.ipynb` simula detección de fallas con 40
000 casos y **0,5 % de prevalencia**. Los números que produce:

| Resultado | Valor |
|----|----|
| Ventaja del modelo sobre «predecir siempre no» | **+0,0002** |
| Fallas no detectadas con umbral 0,5 | **95 %** |
| AUC-ROC frente a AUC precisión-exhaustividad | **0,840** frente a **0,268** |
| Inspecciones inútiles por cada falla encontrada, con TFP = 0,045 | **15** |
| Umbral óptimo derivado de costos | **0,014**, y ahorra **47 %** |
| AUC tras recalibrar con datos de entrenamiento | **0,840 → 0,608** |

La última fila es la más instructiva y no estaba en el guion: recalibrar
mal no solo no arregla la calibración, sino que **destruye parte de la
discriminación**, porque la isotónica ajustada sobre datos
sobreajustados colapsa puntajes distintos en un mismo valor.

Y hay una advertencia metodológica que el propio cuaderno hace visible:
con prevalencia del 0,5 %, **el ECE global es poco informativo**, porque
está dominado por la masa de predicciones cercanas a cero. Es el mismo
argumento que la clase hace contra el acierto, aplicado a la
calibración.

## 6. Lecturas

**Obligatoria — seminario 3, semana 7**

> Kapoor, S., & Narayanan, A. (2023). Leakage and the reproducibility
> crisis in machine-learning-based science. *Patterns*, 4(9), 100804.

Documenta fuga de información en **294 artículos publicados de 17
disciplinas**. Léala con su propio protocolo al lado: la taxonomía de
fugas del artículo es una lista de cotejo aplicable a su tesis.

**También del seminario 3**

> Demšar, J. (2006). Statistical comparisons of classifiers over
> multiple data sets. *Journal of Machine Learning Research*, 7, 1–30.

Técnica. Empiécela esta semana; se cierra en la 8.

**De apoyo a la clase**

> Guo, C., et al. (2017). On calibration of modern neural networks.
> *ICML*. Pertinente si su proyecto usa modelos profundos.

## 7. Preguntas de comprobación

1.  Su clasificador acierta el 99 %. ¿Qué necesita saber antes de
    considerarlo un buen resultado?
2.  ¿Por qué la sensibilidad no depende de la prevalencia y la precisión
    sí?
3.  Un artículo reporta AUC-ROC 0,94 sobre un problema con 1 % de
    positivos. ¿Qué pregunta le hace?
4.  Una falla no anticipada cuesta 50 inspecciones. ¿Cuál es su umbral,
    y qué supone esa fórmula?
5.  ¿Puede un modelo con AUC 0,95 tener probabilidades sin significado?
    ¿Por qué el AUC no lo detecta?
6.  ¿Por qué no se puede recalibrar con los datos de entrenamiento?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase06a_metricas.*` | Métricas, curvas y costos asimétricos |
| `slides/clase06b_calibracion.*` | Calibración: qué es, por qué falla, cómo se arregla |
| `codigo/clase06_metricas_y_calibracion.ipynb` | El problema desbalanceado, de punta a punta |
| `guia/guia06.md` | Esta guía |

## 9. La próxima semana

**Semana 7 · Protocolos de validación y fuga de información.**
*Hold-out*, validación cruzada, validación anidada, particiones
temporales y por grupos. Es la semana que pone orden en todo lo que
llevamos diciendo sobre gastar el conjunto de prueba.

**Seminario 3**: Kapoor y Narayanan (2023) y Demšar (2006). **Reseña
3**, 48 horas antes.
