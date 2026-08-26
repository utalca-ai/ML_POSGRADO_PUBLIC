# Semana 14 · Incertidumbre, predicción conforme y robustez


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
| **Unidad** | 6 · Interpretabilidad, incertidumbre y confiabilidad |
| **Sesión de clase** | Predicción conforme · robustez y desplazamiento de distribución |
| **Actividad** | Ninguna |
| **Hito** | Ninguno |
| **Trabajo sincrónico** | 2 hp de clase |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

> **Es la semana con menos carga sincrónica del semestre** —sin taller,
> sin seminario y sin tutoría— y la última de contenido técnico.
> Aproveche para avanzar el informe final, que se entrega la semana que
> viene.

------------------------------------------------------------------------

## 1. De qué trata esta semana

Dos temas que cierran el arco del módulo.

El primero, **predicción conforme**, responde a lo que la semana 6 dejó
abierto: existe una forma de acompañar una predicción con una garantía
**demostrable**, sin suponer que el modelo está bien especificado ni que
los errores siguen una distribución conocida, y válida a muestra finita.

El segundo, **desplazamiento de distribución**, retira el supuesto sobre
el que descansan las catorce semanas anteriores: que $\mathcal{D}$ es la
misma. En producción no lo es.

## 2. Qué debería poder hacer al terminar la semana

1.  Construir un conjunto de predicción conforme en cuatro pasos.
2.  Explicar qué garantiza —cobertura marginal— y qué **no** —cobertura
    condicional.
3.  Reportar cobertura **y** tamaño, y decir por qué la segunda es la
    medida de utilidad.
4.  Distinguir desplazamiento de covariable, de etiqueta y de concepto.
5.  Detectar desplazamiento con la prueba del clasificador.
6.  Declarar el horizonte de validez de su modelo.

## 3. La sesión sincrónica

| Bloque                    | Duración | Material               |
|---------------------------|----------|------------------------|
| Predicción conforme       | 50 min   | `clase14a`, 17 láminas |
| Robustez y desplazamiento | 50 min   | `clase14b`, 17 láminas |

## 4. Notación y definiciones

**La garantía conforme.** Con $\alpha$ elegido de antemano:

$$\Pr\bigl(y_{n+1}\in C(x_{n+1})\bigr)\;\geq\;1-\alpha$$

Vale para **cualquier** modelo, a **muestra finita**, y su único
supuesto es la **intercambiabilidad** —más débil que i.i.d., pero que
las series temporales no cumplen.

**El procedimiento dividido.** Particionar en entrenamiento y
calibración; entrenar; puntuar la no conformidad de cada caso de
calibración ($s_i=\lvert y_i-\hat y_i\rvert$ en regresión); y tomar el
cuantil

$$\hat q = \text{cuantil}_{\lceil (n+1)(1-\alpha)\rceil / n}\bigl(\{s_i\}\bigr)
\qquad\Longrightarrow\qquad
C(x)=\bigl[\hat y - \hat q,\;\hat y + \hat q\bigr]$$

La corrección $\lceil (n+1)(1-\alpha)\rceil/n$ **no es cosmética**: es
lo que convierte el resultado en un teorema a muestra finita.

**En clasificación**, con $\hat p(x)_y$ la probabilidad de la clase
verdadera:

$$s_i = 1-\hat p(x_i)_{y_i}
\qquad\Longrightarrow\qquad
C(x)=\bigl\{\,y:\;1-\hat p(x)_y\leq \hat q\,\bigr\}$$

**Los tres desplazamientos**, de $P(x,y)=P(y\mid x)\,P(x)$: covariable
(cambia $P(x)$, corregible por reponderación), etiqueta (cambia $P(y)$)
y **concepto** (cambia $P(y\mid x)$, exige datos nuevos).

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | **Redactar el informe final** | 4,0 h | Borrador completo | **Semana 15** |
| 2 | Ejecutar y estudiar el cuaderno de la clase | 1,5 h | Cuaderno corrido | Antes de la semana 15 |
| 3 | Declarar el horizonte de validez de su modelo | 1,0 h | Media página, va en el informe | Semana 15 |

### 5.1 Qué mirar en el cuaderno

`clase14_prediccion_conforme.ipynb` comprueba las tres afirmaciones de
la clase.

**Primera y segunda: la cobertura se cumple con cualquier modelo, y el
precio está en el ancho.**

| Configuración                     | Cobertura | Ancho medio |
|-----------------------------------|-----------|-------------|
| Lineal, un mal modelo a propósito | 0,902     | **5,08**    |
| Bosque                            | 0,902     | 4,73        |
| Bosque normalizado                | 0,902     | 4,79        |

Las tres cubren el 90 % declarado. La regresión lineal es objetivamente
mala —no puede representar un seno— y cumple igual, con intervalos más
anchos.

**Tercera: la garantía es marginal, no condicional.** Con el mismo 90 %
de cobertura marginal:

| Región de $\lvert x_0\rvert$ | Ancho fijo | Normalizado |
|------------------------------|------------|-------------|
| baja (ruido bajo)            | **0,997**  | 0,907       |
| media-baja                   | 0,968      | 0,913       |
| media-alta                   | 0,877      | 0,895       |
| alta (ruido alto)            | **0,753**  | 0,907       |

El intervalo de ancho fijo **sobra** donde no hace falta y **falta**
justo donde el modelo es menos fiable. Su promedio del 90 % esconde las
dos cosas.

Y aquí hay una corrección que el cuaderno declara en su bitácora: al
escribirlo se esperaba que normalizar redujera el **ancho medio**, y no
lo hace —4,79 frente a 4,73. Lo que hace es **redistribuirlo**. Un
promedio igual puede esconder dos comportamientos completamente
distintos, que es el argumento de la propia clase aplicado a sí misma.

**Y la garantía se rompe bajo desplazamiento:**

| Magnitud del desplazamiento | Cobertura |
|-----------------------------|-----------|
| 0,0                         | 0,899     |
| 1,0                         | 0,864     |
| 2,0                         | **0,765** |

No es un defecto del método: es lo que el teorema anuncia. La garantía
era condicional a la intercambiabilidad, y la intercambiabilidad se
rompió. **Toda garantía vale mientras valga su supuesto.**

## 6. Lecturas

> Angelopoulos, A. N., & Bates, S. (2023). Conformal prediction: A
> gentle introduction. *Foundations and Trends in Machine Learning*,
> 16(4).

Es la referencia del módulo para esta semana, y es genuinamente
accesible. Los capítulos 1 a 3 bastan.

> Molnar, C. (2022), cap. 9, para la conexión con interpretabilidad.

Sin lectura obligatoria nueva ni reseña: el seminario 5 fue la semana
pasada.

## 7. Preguntas de comprobación

1.  ¿Qué supone la predicción conforme, y por qué es más débil que
    i.i.d.?
2.  Su modelo es pésimo. ¿Se cumple la cobertura conforme? ¿Qué pasa
    entonces?
3.  ¿Por qué reportar solo la cobertura no dice nada?
4.  Su cobertura marginal es del 90 %. ¿Qué le garantiza eso sobre las
    bombas del fabricante B?
5.  Distinga desplazamiento de covariable y de concepto. ¿Cuál puede
    corregir sin etiquetas nuevas?
6.  Su modelo alerta y por eso se inspecciona, y por eso deja de haber
    fallas. ¿Cómo evalúa si funcionó?
7.  ¿Cuál es el horizonte de validez de su modelo, y qué lo invalidaría?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase14a_conforme.*` | Predicción conforme: idea, procedimiento y límites |
| `slides/clase14b_robustez.*` | Desplazamiento de distribución y vigilancia |
| `codigo/clase14_prediccion_conforme.ipynb` | Las tres afirmaciones, medidas |
| `guia/guia14.md` | Esta guía |

## 9. La próxima semana

**Semana 15 · Sesgo y equidad · reporte y cierre.** Listas de
verificación de reproducibilidad, publicación y revisión por pares.

**Se entrega el informe final del proyecto.** Y en la semana de
exámenes, la defensa oral ante el curso.
