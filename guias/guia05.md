# Semana 5 · Márgenes, árboles y ensambles


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
| **Sesión de clase** | SVM y kernels · árboles · bagging, bosques y potenciación |
| **Actividad** | **Seminario 2** (Breiman ×2) · **Tutoría 1** |
| **Hito** | **Reseña 2** · **Propuesta de proyecto** (formativa, obligatoria, sin nota) |
| **Trabajo sincrónico** | 2 hp de bloque común + 2 hp de tutoría individual |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Tres familias con sesgos inductivos **completamente distintos**, y una
idea —el ensamble— que no es un modelo sino una forma de combinar
cualquiera de ellos.

El hilo es el de la semana 2: cada familia afirma algo sobre la forma
del problema. Las SVM suponen que existe un margen amplio en algún
espacio; los árboles, que la frontera es paralela a los ejes y
escalonada. Los ensambles no suponen nada nuevo: atacan directamente los
términos de la descomposición de la semana 3 —bagging la varianza,
potenciación el sesgo.

## 2. Qué debería poder hacer al terminar la semana

1.  Explicar qué preferencia introduce el margen entre hipótesis que
    ajustan igual.
2.  Decir qué afirma sobre el problema un kernel gaussiano, y por qué la
    escala de los atributos deja de ser un detalle.
3.  Enunciar el sesgo inductivo de un árbol, y por qué su varianza es
    tan alta.
4.  Explicar por qué añadir árboles a un bosque deja de ayudar a partir
    de cierto punto, y qué sí ayuda.
5.  Decidir entre bagging y potenciación a partir del diagnóstico de
    sesgo o varianza de la semana 3.

## 3. La sesión sincrónica

Es **semana de seminario**: el bloque de 2 hp se reparte en una hora de
clase y una de discusión. La tutoría es individual y va fuera del bloque
común.

| Bloque          | Duración         | Material                          |
|-----------------|------------------|-----------------------------------|
| Clase           | 50 min           | `clase05`, 17 láminas             |
| **Seminario 2** | 50 min           | Breiman (2001a) y Breiman (2001b) |
| **Tutoría 1**   | 2 hp, individual | Su propuesta de proyecto          |

## 4. Notación y definiciones

**Margen máximo.** Entre los infinitos hiperplanos que separan dos
clases, el de mayor margen:

$$\min_{w,b}\;\tfrac{1}{2}\lVert w\rVert^2
\quad\text{sujeto a}\quad y_i\bigl(w^\top x_i+b\bigr)\geq 1\;\;\forall i$$

El margen vale $2/\lVert w\rVert$. Solo importan los **vectores de
soporte**: los puntos que tocan el margen.

**Margen blando.** Se admiten violaciones $\xi_i\geq0$ con precio $C$:

$$\min_{w,b,\xi}\;\tfrac{1}{2}\lVert w\rVert^2+C\sum_{i=1}^n\xi_i$$

$C$ hace el papel de $1/\lambda$: es el mismo mando de sesgo y varianza
de la semana 4, con otro nombre.

**Kernel.** $K(x,x')=\phi(x)^\top\phi(x')$, calculado sin construir
nunca $\phi$. El kernel gaussiano corresponde a un $\phi$ de dimensión
infinita, y **afirma que la similitud decae con la distancia euclídea**
en los atributos tal como usted los escaló.

**Bagging.** Con $B$ modelos independientes de varianza $\sigma^2$:

$$\operatorname{Var}\!\left(\frac{1}{B}\sum_{b=1}^{B}\hat h_b\right)=\frac{\sigma^2}{B}$$

**Bosques aleatorios.** Los modelos no son independientes. Con
correlación $\rho$:

$$\operatorname{Var}\!\left(\frac{1}{B}\sum_b \hat h_b\right)=\rho\,\sigma^2+\frac{1-\rho}{B}\,\sigma^2\;\xrightarrow[B\to\infty]{}\;\rho\,\sigma^2$$

**Esta es la fórmula que conviene recordar.** Dice que añadir árboles no
baja de $\rho\sigma^2$: para mejorar hay que reducir $\rho$, y eso es lo
que hace sortear atributos en cada corte.

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Ejecutar y estudiar el cuaderno de la clase | 1,5 h | Cuaderno corrido | Antes de la semana 6 |
| 2 | Leer Hastie et al., cap. 12 (SVM) y cap. 15 (bosques) | 2,5 h | Notas propias | Antes de la semana 6 |
| 3 | Incorporar la retroalimentación de la tutoría 1 | 1,5 h | Propuesta revisada | Semana 6 |
| 4 | Preparar el taller 3 | 1,0 h | — | Semana 6 |

**Semana sin reseña nueva.** El seminario 3 es en la semana 7, así que
las lecturas de Kapoor y Narayanan y de Demšar pueden empezar la semana
que viene. Aproveche para dejar la propuesta de proyecto en buen estado:
es la base del diseño experimental de la semana 9.

### 5.1 La propuesta de proyecto

Es **formativa y obligatoria**: se retroalimenta por escrito, no lleva
nota, y es requisito para presentar el informe final. Debe responder,
sobre su propio problema:

1.  **¿Qué es un caso?** Y qué implica esa elección para el supuesto
    i.i.d.
2.  **¿Qué se observa y qué se predice?** Incluida la construcción de la
    etiqueta, si aún no existe.
3.  **¿De qué población salen los datos y a cuál se aplicarán?** Si
    difieren, eso va en limitaciones desde ya.
4.  **¿Qué cuesta cada tipo de error?** Y por tanto qué pérdida
    corresponde.
5.  **¿Qué familia de modelos, y qué supone sobre el fenómeno?** Con las
    cuatro preguntas de la lámina «Cómo se elige entre estas familias».
6.  **¿Cuál es el piso de ruido?** El ejercicio de la semana 3.

### 5.2 Qué mirar en el cuaderno

`clase05_sesgos_inductivos.ipynb` da a cuatro familias exactamente los
mismos datos y dibuja la frontera de cada una. **La frontera es el sesgo
inductivo, hecho imagen**: la logística traza una recta porque no puede
otra cosa, el árbol traza una escalera con islas alrededor de casos
aislados, y el bosque suaviza esas islas.

Después mide la afirmación cuantitativa de la clase:

|                         | Varianza relativa al árbol único |
|-------------------------|----------------------------------|
| Árbol único             | 100 %                            |
| Bagging de 300 árboles  | **25,1 %**                       |
| Bosque aleatorio de 300 | **20,7 %**                       |

La diferencia entre las dos últimas filas es exactamente $\rho$: con
$B=300$ el término $(1-\rho)\sigma^2/B$ ya es despreciable, así que lo
único que separa bagging de un bosque es la correlación entre árboles.

## 6. Lecturas

**Del seminario de esta semana**

> Breiman, L. (2001). Random forests. *Machine Learning*, 45(1), 5–32.
>
> Breiman, L. (2001). Statistical modeling: The two cultures.
> *Statistical Science*, 16(3), 199–231.

Un método y, a la vez, una crítica a la cultura estadística que lo
rodea. La discusión publicada junto a *Two Cultures*, con réplicas de
Cox, Efron y Parzen, es una mina de objeciones para el rol de
discutidor.

**De apoyo a la clase**

> Hastie, Tibshirani y Friedman (2009), cap. 12 (SVM y kernels) y cap.
> 15 (bosques aleatorios). El §15.2 contiene la derivación de la fórmula
> de la varianza con correlación.

## 7. Preguntas de comprobación

1.  Si dos clases son separables, hay infinitos hiperplanos con riesgo
    empírico cero. ¿Qué criterio adicional introduce una SVM, y de qué
    semana es esa idea?
2.  ¿Por qué la escala de los atributos importa para un kernel gaussiano
    y no para un árbol?
3.  ¿Por qué la varianza de un árbol es tan alta? Piense en qué pasa si
    cambia el primer corte.
4.  Tiene un bosque de 100 árboles. ¿Mejora si pone 1000? ¿Y si sortea
    menos atributos por corte? Justifique con la fórmula de la varianza.
5.  Su modelo tiene sesgo alto y varianza baja. ¿Bagging o potenciación?
    ¿Por qué?
6.  ¿Por qué más iteraciones de potenciación **sí** pueden sobreajustar
    y más árboles en un bosque no?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase05_svm_arboles_ensambles.*` | Las 17 láminas de la clase |
| `codigo/clase05_sesgos_inductivos.ipynb` | Fronteras de decisión y medición de varianza |
| `guia/guia05.md` | Esta guía |

## 9. La próxima semana

**Semana 6 · Métricas y calibración.** Clases desbalanceadas, costos
asimétricos y calibración de probabilidades. Es donde la pregunta «¿qué
cuesta cada tipo de error?», que aparece desde la semana 1, deja de ser
retórica.

**Taller 3**: elección de métrica y curva de calibración sobre un
problema desbalanceado.
