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

### Vocabulario mínimo

Cuatro términos que la clase usa constantemente. Si alguno le resulta
nuevo, léalo aquí antes de la sesión: el resto se sigue sin dificultad.

**Minimizador.** El *punto* donde una función alcanza su valor más
pequeño, no el valor mismo. Se escribe
$\hat\beta=\operatorname*{arg\,min}_\beta R_S(\beta)$: el $\beta$ que
hace $R_S$ lo menor posible. $R_S(\hat\beta)$ es el mínimo —un número—;
$\hat\beta$ es dónde se alcanza —un vector—, y es lo que interesa,
porque es el modelo ajustado. El gorro marca siempre «estimado a partir
de los datos».

**Bernoulli.** La distribución de una variable que solo puede valer 0 o
1: vale 1 con probabilidad $\pi$ y 0 con probabilidad $1-\pi$. Es el
modelo de una moneda, posiblemente cargada. Su media es $\pi$ y su
varianza $\pi(1-\pi)$ —máxima en $\pi=0{,}5$, casi nula cerca de 0 o de
1—. No es una elección entre varias: es *la* distribución de un
resultado binario, y por eso aparece sola en cuanto la etiqueta es
sí/no.

**Entropía cruzada.** La pérdida que cobra a cada caso $-\log$ de la
probabilidad que el modelo asignó al resultado que efectivamente
ocurrió. Si el modelo dio $0{,}99$ a la clase correcta, paga $0{,}01$;
si dio $0{,}01$, paga $4{,}6$; si dio 0 y ocurrió, paga infinito. Premia
la confianza acertada y castiga sin piedad la confianza equivocada: por
eso empuja a calibrar probabilidades y no solo a acertar la clase. El
nombre viene de teoría de la información —es el costo en bits de
codificar la realidad usando la distribución predicha—, pero para este
curso basta la lectura del precio.

**Descenso de gradiente.** Procedimiento para encontrar un minimizador
cuando no hay fórmula. Se parte de un $\beta$ cualquiera y se repite

$$\beta \;\leftarrow\; \beta - \eta\,\nabla R_S(\beta)$$

hasta que el error deje de bajar. El gradiente $\nabla R_S$ apunta en la
dirección de máximo *ascenso*, así que restarlo es bajar; $\eta$, la
tasa de aprendizaje, es el largo del paso: demasiado corto no llega en
un tiempo razonable, demasiado largo se pasa de largo y rebota. La
imagen útil es bajar un cerro con niebla palpando la pendiente bajo los
pies. Cuando la función es **convexa** —forma de tazón, un solo fondo—
se llega al mismo punto se parta de donde se parta, y por eso en
regresión logística el error de optimización es despreciable. En redes
profundas (semana 11) no es convexa, hay muchos fondos, y el punto de
partida importa. En la práctica `sklearn` no usa descenso de gradiente
puro sino métodos de segundo orden (`lbfgs`, Newton-Raphson), que
convergen en muchas menos iteraciones con la misma idea.

**ERM.** *Minimización del riesgo empírico*: quedarse con la hipótesis
que menor error comete sobre los datos de entrenamiento, sin nada más.
Se definió en la semana 1 y es lo que se hace por defecto. «ERM puro»
quiere decir sin penalización añadida.

**Teorema de Bayes.** La regla para dar vuelta un condicional. Si sé qué
tan probables son los datos suponiendo unos coeficientes, me dice qué
tan creíbles son esos coeficientes habiendo visto los datos:

$$\underbrace{p(\beta\mid X,y)}_{\text{posterior}}=
\frac{\overbrace{p(y\mid X,\beta)}^{\text{verosimilitud}}\;
\overbrace{p(\beta)}^{\text{previa}}}{p(y\mid X)}
\;\;\propto\;\; p(y\mid X,\beta)\,p(\beta)$$

- La **previa** $p(\beta)$ es lo que usted considera creíble sobre los
  coeficientes *antes* de mirar los datos.
- La **verosimilitud** $p(y\mid X,\beta)$ es lo de la primera parte de
  la clase: qué tan bien unos coeficientes dados explican lo observado.
- La **posterior** $p(\beta\mid X,y)$ es lo que usted cree *después*.
- El denominador $p(y\mid X)$ no depende de $\beta$, así que al buscar
  el máximo se descarta: de ahí el $\propto$, que se lee «proporcional
  a».

**Cuidado con qué es lo incierto.** La mayoría recordará el teorema de
Bayes aplicado a clasificar: dado un síntoma, qué enfermedad. Eso es una
posterior sobre la **etiqueta**, y es lo que calcula la regresión
logística cuando entrega $\Pr(y=1\mid x)$. Aquí la posterior es sobre
los **parámetros**. Es la misma operación aplicada a otro objeto, y
confundir ambas es el enredo más común de esta parte de la clase.

**MAP.** *Máximo a posteriori*: el valor de $\beta$ donde la posterior
alcanza su máximo. Tomando logaritmo, el producto se vuelve suma:

$$\hat\beta_{\text{MAP}}=\operatorname*{arg\,max}_\beta\;
\log p(y\mid X,\beta)+\log p(\beta)$$

y como maximizar $\log p$ es minimizar $-\log p$, eso es exactamente
«error $+\ \lambda\times$ complejidad». MAP no es hacer estadística
bayesiana completa: un análisis bayesiano usa la posterior entera —con
su incertidumbre—, y MAP se queda solo con su punto más alto. La
posterior completa es la semana 14.

**Distribución de Laplace.** Densidad
$p(\beta)\propto e^{-\lvert\beta\rvert/b}$. Tiene un **pico** en cero,
no una curva redondeada como la gaussiana, y colas más gruesas.
Traducida a supuesto: «es muy creíble que un coeficiente valga cero, y
también que unos pocos sean grandes». Es la misma distribución que en la
primera parte daba el error absoluto; allí describía el ruido de $y$,
aquí la magnitud de $\beta$.

**Validación cruzada de $k$ pliegues.** Partir el conjunto de
entrenamiento en $k$ trozos, ajustar $k$ veces dejando uno fuera cada
vez, y promediar el error medido sobre el trozo excluido. Cada dato
sirve de prueba exactamente una vez, y el conjunto de prueba real no se
toca. Con $k=5$ o $k=10$ el ajuste cuesta $k$ veces más. El desarrollo
completo —incluida la validación anidada, para cuando además se comparan
modelos— es la semana 7.

### Notación de la sesión

**Vector aumentado.** $\tilde x=(1,x_1,\dots,x_p)^\top$ —«equis tilde»—
es el vector de atributos con un 1 al frente, y
$\beta=(\beta_0,\beta_1,\dots,\beta_p)^\top$. El 1 multiplica a
$\beta_0$, así que $\beta^\top\tilde x=\beta_0+\sum_j\beta_j x_j$
incluye el intercepto. Se usa en toda la sesión. Sin relación con la
$\tilde h$ de la semana 1.

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

**Por qué $\lambda I$ vuelve invertible la matriz.** Una matriz no tiene
inversa cuando alguno de sus valores propios es cero. Los valores
propios de $X^\top X$ nunca son negativos, pero valen cero justamente
cuando hay colinealidad perfecta o $p>n$: hay una dirección del espacio
de atributos que la matriz aplasta, y lo aplastado no se puede
recuperar. Sumar $\lambda I$ desplaza **todos** los valores propios en
$+\lambda$; los que valían $0$ pasan a valer $\lambda>0$ y ninguno queda
en cero. Es la diferencia entre dividir por $0$ y dividir por
$0+\lambda$. Ese fue el motivo original de ridge —Hoerl y Kennard
(1970)—, antes de que se entendiera como control de capacidad; la
demostración está en Hastie et al., §3.4.1.

**Lectura bayesiana.**
$\hat\beta_{\text{MAP}}=\operatorname*{arg\,max}_\beta \log p(y\mid X,\beta)+\log p(\beta)$.
Previa gaussiana sobre $\beta$ da $L_2$; previa de Laplace da $L_1$. Y
$\lambda = \sigma^2/\tau^2$: la razón entre el ruido de los datos y la
dispersión que usted admite en los coeficientes.

**Dos detalles operativos que se corrigen en el taller:** el intercepto
**no** se penaliza, y los atributos deben estandarizarse antes —con la
media y la desviación estimadas **solo con entrenamiento**.

### Cuando el supuesto gaussiano falla: tres remedios

La clase menciona tres correcciones sin desarrollarlas. Ninguna se
evalúa en este curso, pero cada una resuelve un problema que es muy
probable que usted tenga en su tesis, así que conviene saber que existen
y cómo se llaman.

**Mínimos cuadrados ponderados** (*weighted least squares*). Para cuando
la varianza del error no es constante —crece con la magnitud de $y$, o
cambia entre instrumentos o entre sitios—. Cada caso entra en la suma
con un peso:

$$\hat\beta=\operatorname*{arg\,min}_\beta \sum_i w_i\bigl(y_i-\beta^\top\tilde x_i\bigr)^2,
\qquad w_i \propto 1/\sigma_i^2$$

Los datos más ruidosos pesan menos, que es exactamente lo que dice la
verosimilitud cuando cada $\varepsilon_i\sim N(0,\sigma_i^2)$ con
$\sigma_i$ distinto. El problema práctico es que hay que estimar los
$\sigma_i$; lo habitual es modelarlos en función de la predicción o de
la variable que se sospecha responsable. *Lectura:* Faraway, **Linear
Models with R**, el capítulo sobre problemas con el error (mínimos
cuadrados generalizados y ponderados).

**Pérdida de Huber.** Para cuando hay valores atípicos y no quiere que
uno solo le arrastre el ajuste. Es cuadrática cerca de cero y lineal más
allá de un umbral $\delta$:

$$L_\delta(r)=\begin{cases} \tfrac{1}{2}r^2 & \lvert r\rvert\le\delta\\[2pt]
\delta\bigl(\lvert r\rvert-\tfrac{1}{2}\delta\bigr) & \lvert r\rvert>\delta\end{cases}$$

Así conserva la buena estadística del cuadrático en la zona normal y
deja de castigar cuadráticamente los desvíos grandes: el atípico paga
mucho, pero no lo domina todo. Es un punto intermedio entre error
cuadrático y error absoluto, y corresponde a una verosimilitud de colas
más pesadas que la gaussiana. *Lecturas:* Huber, P. J. (1964). Robust
estimation of a location parameter. *Annals of Mathematical Statistics*,
35(1), 73–101 —el artículo fundacional—; y Hastie, Tibshirani y Friedman
(2009), la sección sobre funciones de pérdida y robustez del capítulo de
*boosting*, que las compara gráficamente.

**Modelos mixtos** (*mixed-effects models*, o multinivel). Para cuando
los datos vienen agrupados y los errores dentro de un grupo están
correlacionados: varias mediciones del mismo equipo, parcelas del mismo
predio, visitas repetidas del mismo paciente, estudiantes de la misma
sala. El modelo añade un término aleatorio propio de cada grupo $g$:

$$y_{ig}=\beta^\top\tilde x_{ig}+u_g+\varepsilon_{ig},\qquad u_g\sim N(0,\tau^2)$$

Ese $u_g$ es lo que hace que dos observaciones del mismo grupo se
parezcan más entre sí que dos de grupos distintos, que es justo lo que
la verosimilitud con errores independientes negaba. Ignorarlo no sesga
tanto los coeficientes como los **errores estándar**: los deja demasiado
pequeños, y con eso salen significancias que no existen. *Lecturas:*
Gelman y Hill (2007), **Data Analysis Using Regression and
Multilevel/Hierarchical Models** —la introducción más legible—; Bates,
Mächler, Bolker y Walker (2015). Fitting linear mixed-effects models
using lme4. *Journal of Statistical Software*, 67(1), 1–48 —la
referencia de implementación—.

Las tres tienen algo en común, y es el punto de la clase: no son trucos
de ajuste, son **la verosimilitud correcta escrita correctamente**.

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
>
> Hoerl, A. E. y Kennard, R. W. (1970). Ridge regression: Biased
> estimation for nonorthogonal problems. *Technometrics*, 12(1), 55–67.
> El artículo original, si quiere ver de dónde salió $\lambda I$.

**Si el supuesto gaussiano no le sirve** — opcionales, para quien las
necesite en su tesis. Están comentadas en la §4:

> Huber, P. J. (1964). Robust estimation of a location parameter.
> *Annals of Mathematical Statistics*, 35(1), 73–101.
>
> Bates, D., Mächler, M., Bolker, B. y Walker, S. (2015). Fitting linear
> mixed-effects models using lme4. *Journal of Statistical Software*,
> 67(1), 1–48.
>
> Gelman, A. y Hill, J. (2007). *Data Analysis Using Regression and
> Multilevel/Hierarchical Models*. Cambridge University Press.

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
