# Semana 4 · Modelos lineales y regularización


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
| **Unidad** | 2 · Modelos supervisados y su fundamento |
| **Sesión de clase** | Lineal y logística como máxima verosimilitud · Regularización $L_1$ y $L_2$ |
| **Actividad** | **Taller 2** (2 hp) |
| **Hito calificado** | **Entrega del taller 2** |
| **Trabajo sincrónico** | 4 hp: 2 de clase + 2 de taller |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

> **Semana cargada.** Además del taller hay que leer los dos Breiman y
> entregar la **reseña 2**, que vence 48 h antes de la sesión de la
> semana 5. Y en la semana 5 hay **tutoría 1**, para la que necesita su
> problema de tesis formulado. Empiece por las lecturas.

------------------------------------------------------------------------

## 1. De qué trata esta semana

En la semana 1 dijimos que elegir la función de pérdida es codificar la
estructura de costos del problema. Esta semana descubrimos algo más
fuerte: **la pérdida no es una elección, es un supuesto
probabilístico**. Minimizar error cuadrático *es* estimar por máxima
verosimilitud bajo ruido gaussiano; minimizar entropía cruzada *es*
hacerlo bajo una Bernoulli.

La segunda parte añade al ajuste un término que no viene de los datos:
la **regularización**. Y resulta que ese término también es un supuesto
—una distribución previa sobre los coeficientes—, de modo que la lección
de la primera mitad se repite: lo que parecía técnica es modelado.

## 2. Qué debería poder hacer al terminar la semana

1.  Derivar el error cuadrático desde la verosimilitud gaussiana, y la
    entropía cruzada desde la Bernoulli.
2.  Nombrar tres supuestos de mínimos cuadrados y decir cómo se verifica
    cada uno.
3.  Explicar por qué $L_1$ produce ceros exactos y $L_2$ no.
4.  Elegir entre $L_1$ y $L_2$ con un argumento sobre el problema, no
    sobre el método.
5.  **Seleccionar $\lambda$ sin contaminar el conjunto de prueba.**

## 3. La sesión sincrónica

| Bloque | Duración | Material |
|----|----|----|
| Modelos lineales como máxima verosimilitud | 50 min | `clase04a`, 18 láminas |
| Regularización $L_1$, $L_2$ y lectura bayesiana | 50 min | `clase04b`, 17 láminas |
| **Taller 2** | 2 hp aparte | Regularización y frontera de decisión |

## 4. Notación y definiciones

**Regresión lineal.** $h_\beta(x)=\beta^\top\tilde x$, lineal **en
$\beta$**, no necesariamente en $x$. Mínimos cuadrados ordinarios:

$$\hat\beta = \bigl(X^\top X\bigr)^{-1}X^\top y$$

**De dónde sale el cuadrado.** Con
$y_i=\beta^\top\tilde x_i+\varepsilon_i$ y
$\varepsilon_i\sim N(0,\sigma^2)$ independientes:

$$-\log\mathcal{L}(\beta)=\frac{1}{2\sigma^2}\sum_{i=1}^n\bigl(y_i-\beta^\top\tilde x_i\bigr)^2+\text{const}$$

**Regresión logística.** Lo lineal son las log-probabilidades relativas:

$$\log\frac{\Pr(y=1\mid x)}{\Pr(y=0\mid x)}=\beta^\top\tilde x
\qquad\Longleftrightarrow\qquad
\Pr(y=1\mid x)=\frac{1}{1+e^{-\beta^\top\tilde x}}$$

y de la verosimilitud Bernoulli sale la entropía cruzada:

$$-\log\mathcal{L}(\beta)=-\sum_{i=1}^n\Bigl[y_i\log\pi_i+(1-y_i)\log(1-\pi_i)\Bigr]$$

**Ridge y Lasso.**

$$\hat\beta_{\text{ridge}}=\operatorname*{arg\,min}_\beta \sum_i (y_i-\beta^\top\tilde x_i)^2+\lambda\sum_j \beta_j^2
\qquad
\hat\beta_{\text{ridge}}=\bigl(X^\top X+\lambda I\bigr)^{-1}X^\top y$$

$$\hat\beta_{\text{lasso}}=\operatorname*{arg\,min}_\beta \sum_i (y_i-\beta^\top\tilde x_i)^2+\lambda\sum_j \lvert\beta_j\rvert$$

**Lectura bayesiana.**
$\hat\beta_{\text{MAP}}=\operatorname*{arg\,max}_\beta \log p(y\mid X,\beta)+\log p(\beta)$.
Previa gaussiana sobre $\beta$ da $L_2$; previa de Laplace da $L_1$. Y
$\lambda = \sigma^2/\tau^2$: la razón entre el ruido de los datos y la
dispersión que usted admite en los coeficientes.

**Dos detalles operativos que se corrigen en el taller:** el intercepto
**no** se penaliza, y los atributos deben estandarizarse antes —con la
media y la desviación estimadas **solo con entrenamiento**.

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Leer Breiman (2001) ×2 — **obligatoria** | 2,0 h | Notas propias | Antes de la reseña |
| 2 | Escribir la **reseña 2** | 2,0 h | 2 páginas | **48 h antes de la sesión de la semana 5** |
| 3 | Completar y entregar el **taller 2** | 1,5 h | Cuaderno + bitácora | Fin de semana 4 |
| 4 | Ejecutar y estudiar el cuaderno de la clase | 1,0 h | Cuaderno corrido | Antes de la semana 5 |

**Además, para la tutoría 1 de la semana 5** tenga listo el borrador de
su problema de tesis formulado como tarea de aprendizaje: qué es un
caso, qué se observa, qué se predice, de qué población salen los datos,
a cuál se aplicarán, y qué cuesta cada tipo de error. Es la **propuesta
de proyecto**, hito formativo obligatorio.

### 5.1 El taller 2

**Regularización y frontera de decisión; efecto sobre la varianza del
estimador.**

La misma lista de cotejo de ocho ítems. Dos que esta semana concentran
los problemas:

- **Ítem 3 (protocolo sin fuga).** $\lambda$ se elige por validación
  cruzada **dentro del conjunto de entrenamiento**. Si lo elige mirando
  el test, el error que reporta ya no es insesgado —y la sección 7 del
  cuaderno mide cuánto.
- **Ítem 4 (transformaciones solo con entrenamiento).** La
  estandarización de los atributos es una transformación ajustada sobre
  datos. Su media y su desviación se calculan con el conjunto de
  entrenamiento y se **aplican** al de prueba, nunca al revés.

### 5.2 Qué mirar en el cuaderno

`clase04_regularizacion.ipynb` simula 40 atributos correlacionados de
los que solo 5 importan, con $n=60$, y mide tres cosas:

| Resultado | Número |
|----|----|
| Reducción de error del mejor $\lambda$ frente a mínimos cuadrados | **34,7 %** |
| Coeficientes anulados: ridge frente a lasso | **0** frente a **27** de 40 |
| Sesgo optimista al elegir $\lambda$ contra el conjunto de prueba | **7 %** |

El tercero es el que corrige el taller. El segundo muestra la diferencia
cualitativa entre $L_1$ y $L_2$ que la clase explica con la geometría
del rombo.

Y hay un cuarto resultado que conviene mirar con calma: **la selección
de Lasso es inestable**. Sobre 50 réplicas, los atributos verdaderamente
relevantes se seleccionan entre el 68 % y el 100 % de las veces, pero
algunos irrelevantes correlacionados con ellos entran hasta en el 40 %.
Si usted va a interpretar *qué atributos seleccionó el modelo*, esa
frecuencia importa más que el resultado de una sola corrida.

## 6. Lecturas

**Obligatorias — seminario 2, semana 5**

> Breiman, L. (2001). Random forests. *Machine Learning*, 45(1), 5–32.
>
> Breiman, L. (2001). Statistical modeling: The two cultures.
> *Statistical Science*, 16(3), 199–231.

Son un método y, a la vez, una crítica a la cultura estadística que lo
rodea. Léalos en ese orden: *Two Cultures* es el argumento y *Random
Forests* es la respuesta técnica. La discusión publicada junto a *Two
Cultures* —con réplicas de Cox, Efron y Parzen— vale la pena y suele dar
buenas objeciones para el rol de discutidor.

**De apoyo a la clase**

> Hastie, Tibshirani y Friedman (2009), §3.4 (encogimiento) y §4.4
> (logística).

## 7. Preguntas de comprobación

1.  ¿Qué supone sobre los datos quien minimiza error cuadrático? Nombre
    tres supuestos y diga cómo verificaría cada uno.
2.  Su variable de respuesta es un conteo de fallas por mes. ¿Por qué el
    error cuadrático es una mala elección, y qué usaría?
3.  ¿Por qué la regresión logística no converge cuando las clases son
    separables? ¿Cómo lo arregla la regularización?
4.  Dibuje el rombo de $L_1$ y la bola de $L_2$ en dos dimensiones, y
    explique de ahí por qué solo el primero produce ceros.
5.  ¿Qué previa sobre $\beta$ corresponde a ridge? ¿Y a lasso? ¿Qué
    significa $\lambda$ en esa lectura?
6.  Un colega ajustó 20 valores de $\lambda$ y reporta el mejor error de
    prueba. ¿Qué está mal, y cuánto puede valer el error?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase04a_verosimilitud.*` | Primera parte: de dónde salen las pérdidas |
| `slides/clase04b_regularizacion.*` | Segunda parte: $L_1$, $L_2$ y la lectura bayesiana |
| `codigo/clase04_regularizacion.ipynb` | Barrido en $\lambda$, comparación $L_1$/$L_2$ y el sesgo optimista |
| `guia/guia04.md` | Esta guía |

## 9. La próxima semana

**Semana 5 · SVM, árboles y ensambles.** Márgenes y funciones kernel;
árboles de decisión; bagging, bosques aleatorios y potenciación de
gradiente.

**Seminario 2**: los dos Breiman. **Tutoría 1**: su problema de tesis
formulado como tarea de aprendizaje —entrega formativa obligatoria, sin
nota, con retroalimentación por escrito.
