# Semana 1 · El aprendizaje como estimación de riesgo


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
> con qué se corrige. Es el contrato de la semana: si algo se le exige y
> no está aquí, reclámelo.

|  |  |
|----|----|
| **Unidad** | 1 · Formulación del aprendizaje inductivo |
| **Sesión de clase** | Presentación del módulo · Riesgo esperado y riesgo empírico |
| **Actividad** | Diagnóstico de entrada (no calificado) |
| **Hito calificado** | Ninguno |
| **Trabajo sincrónico** | 2 horas pedagógicas (100 minutos) |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Toda tesis que use aprendizaje automático hace, en algún momento, una
afirmación sobre datos que nunca observó. Esta semana establece el
aparato que justifica esa afirmación —y las condiciones en que deja de
justificarla.

La idea central es una distinción entre dos cantidades que se parecen y
no son lo mismo: el **riesgo esperado**, que es el objetivo pero no se
puede calcular, y el **riesgo empírico**, que sí se calcula pero no es
el objetivo. Confundirlos es el error fundacional del área, y las quince
semanas siguientes son, en buena medida, respuestas a ese problema.

## 2. Qué debería poder hacer al terminar la semana

1.  Escribir la definición de riesgo esperado y de riesgo empírico, y
    explicar por qué el primero no es calculable.
2.  Explicar por qué el riesgo empírico es un estimador insesgado
    **solo** para una hipótesis fijada antes de ver la muestra, y por
    qué el entrenamiento rompe esa condición.
3.  Reconocer el sesgo optimista en un resultado publicado, y decir en
    qué dirección sesga.
4.  Formular su propio problema de investigación en los términos de la
    clase: qué es un caso, qué se observa, qué se predice, de qué
    población salen los datos y a cuál se van a aplicar.

## 3. La sesión sincrónica

Dos horas pedagógicas, 100 minutos en total.

| Bloque | Duración | Material |
|----|----|----|
| Presentación del profesor y del curso | ~10 min | `Clase01a`, láminas 1–2 |
| **Diagnóstico de entrada** | 20 min | Cuestionario, 20 preguntas |
| Presentación del módulo: evaluación, calendario y reglas | ~30 min | `Clase01a`, láminas 3–18 |
| Contenido: riesgo esperado y riesgo empírico | ~40 min | `Clase01b`, 22 láminas |

**Por qué el diagnóstico va al inicio y no al final.** El bloque de
contenido responde tres de las cinco preguntas del área D. Aplicarlo
después mediría lo que usted acaba de escuchar en vez de lo que trae.
Es, literalmente, el problema que se explica en la segunda mitad de la
sesión: un instrumento contaminado por información que no debía tener.

El diagnóstico **no se califica y no incide en su nota**. Se devuelve la
semana siguiente, desglosado por área, con material de nivelación para
las áreas que queden bajo el umbral.

## 4. Notación y definiciones

Esta sección es la referencia para estudiar. Todo lo que sigue en el
semestre usa esta notación.

**Los objetos.** Un espacio de entrada $\mathcal{X}$ y uno de salida
$\mathcal{Y}$; una distribución conjunta $\mathcal{D}$ sobre
$\mathcal{X}\times\mathcal{Y}$, fija y desconocida; y una muestra de $n$
casos extraídos de manera independiente e idénticamente distribuida:

$$S = \bigl\{(x_1,y_1),\ldots,(x_n,y_n)\bigr\} \overset{\text{i.i.d.}}{\sim} \mathcal{D}^{\,n}$$

**Las decisiones del investigador.** Una familia de hipótesis
$\mathcal{H}$ de la que se elegirá $h:\mathcal{X}\to\mathcal{Y}$, y una
función de pérdida $L(h(x),y)\geq 0$ que dice cuánto cuesta equivocarse.

**Riesgo esperado.** El objetivo. La pérdida promedio sobre toda la
distribución:

$$R_{\mathcal{D}}(h)\;=\;\mathbb{E}_{(x,y)\sim\mathcal{D}}\bigl[L(h(x),y)\bigr]$$

No depende de la muestra que a usted le tocó. **No se puede evaluar**,
porque $\mathcal{D}$ es desconocida.

**Riesgo empírico.** Lo único calculable. La misma pérdida, promediada
sobre la muestra:

$$R_S(h)\;=\;\frac{1}{n}\sum_{i=1}^{n} L\bigl(h(x_i),y_i\bigr)$$

**La propiedad que lo justifica, y su condición.** Para una hipótesis
$h$ **fijada antes de ver $S$**:

$$\mathbb{E}_{S\sim\mathcal{D}^n}\bigl[R_S(h)\bigr] \;=\; R_{\mathcal{D}}(h)$$

**Minimización del riesgo empírico (ERM).** Lo que hace todo algoritmo
de entrenamiento —y lo que rompe la condición anterior:

$$\hat{h}\;=\;\operatorname*{arg\,min}_{h\in\mathcal{H}}\;R_S(h)$$

**Descomposición del exceso de riesgo.** Con $h^\star$ la mejor función
posible, $h^\star_{\mathcal{H}}$ la mejor dentro de $\mathcal{H}$,
$\hat h$ el minimizador del riesgo empírico y $\tilde h$ lo que el
algoritmo efectivamente devuelve:

$$R(\tilde h)-R(h^\star)=
\underbrace{R(h^\star_{\mathcal{H}})-R(h^\star)}_{\text{aproximación}}+
\underbrace{R(\hat h)-R(h^\star_{\mathcal{H}})}_{\text{estimación}}+
\underbrace{R(\tilde h)-R(\hat h)}_{\text{optimización}}$$

## 5. Trabajo autónomo de la semana

Aproximadamente **6,5 horas cronológicas**, que es el ritmo semanal que
supone el régimen de 5 SCT (95 horas de trabajo autónomo repartidas en
15 semanas).

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Leer Domingos (2012) — **obligatoria** | 1,5 h | Notas propias | Antes de la semana 2 |
| 2 | Ejecutar y estudiar el cuaderno de la semana | 1,5 h | Cuaderno corrido de cero | Antes de la semana 2 |
| 3 | Leer Hastie et al. (2009), §2.4 y §2.9 — recomendada | 1,5 h | Notas propias | Antes de la semana 3 |
| 4 | Crear la cuenta del repositorio y **enviar su nombre de usuario** | 1,0 h | Correo al profesor | **Esta semana** |
| 5 | Formular su problema de tesis en los términos de la clase | 1,0 h | Media página de borrador | Para la tutoría 1 |

**Nada de esto se califica esta semana.** Las actividades 4 y 5 son las
que tienen consecuencia práctica: sin la 4 no puedo crearle el
repositorio antes del taller 1, y la 5 es la conversación de la tutoría
1 y el germen de su proyecto individual.

### 5.1 Cómo ejecutar el cuaderno

``` bash
cd "S01 Riesgo/codigo"
python3 -m venv .venv
source .venv/bin/activate            # en Windows: .venv\Scripts\activate
pip install -r "../../02 Entorno/requirements.txt"
jupyter lab clase01_riesgo_empirico_vs_esperado.ipynb
```

Ejecute **todas** las celdas en orden, desde un kernel limpio. La última
celda comprueba que los valores calculados coinciden con los de la
lámina; si el cuaderno deja de reproducir, esa celda falla y usted se
entera.

Requiere Python 3.10 o superior.

### 5.2 Qué mirar en el cuaderno

No es solo la figura. El cuaderno es el **estándar esperado del taller
1**: cumple, uno por uno, los ocho ítems de la lista de cotejo con que
se corrigen todos los talleres del semestre. Vale la pena recorrerlo con
esa lista al lado.

Preste atención particular a la **sección 7**. Ahí el cuaderno calcula
media y desviación estándar sobre 20 semillas y descubre que «media
menos una desviación» sale **negativa** para un error cuadrático medio.
Esa imposibilidad no es un error de cálculo: es el diagnóstico de que la
distribución tiene cola pesada y esos dos estadísticos no la resumen. El
cuaderno cambia entonces a mediana y rango intercuartílico en escala
logarítmica, y explica por qué.

Ese cambio de decisión, con su razón, es exactamente lo que se espera de
una bitácora de taller.

## 6. Lecturas

**Obligatoria**

> Domingos, P. (2012). A few useful things to know about machine
> learning. *Communications of the ACM*, 55(10), 78–87.

Corto y sin matemáticas pesadas. Las secciones 3, 6 y 7 son esta clase
dicha con otras palabras. Al leerlo, busque dónde aparece la distinción
entre riesgo esperado y empírico bajo otros nombres.

**Recomendada**

> Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of
> Statistical Learning* (2ª ed.), capítulo 2, secciones 2.4 y 2.9.

La misma formulación con más detalle formal. Si además lee esto, llega
sobrado a la semana 3.

Ambos se discuten en el **seminario 1 (semana 3)**, junto con Wolpert
(1996). La reseña 1 se entrega **48 horas antes** de esa sesión.

## 7. Preguntas de comprobación

Si puede responderlas sin mirar las láminas, la semana está lograda.

1.  ¿Por qué $R_{\mathcal{D}}(h)$ no se puede calcular, ni siquiera con
    muchos datos?
2.  La igualdad $\mathbb{E}_S[R_S(h)] = R_{\mathcal{D}}(h)$ tiene una
    condición. ¿Cuál es, y por qué el entrenamiento la viola?
3.  La hipótesis que memoriza la muestra tiene $R_S(h)=0$. Si el error
    de entrenamiento fuera un buen criterio, ¿qué debería concluirse?
    ¿Qué falla?
4.  ¿En qué dirección sesga el sesgo optimista, y qué dos cosas lo hacen
    crecer?
5.  Un artículo reporta «0,91 de AUC frente a 0,89 del método de
    referencia». Nombre tres objeciones metodológicas antes de leer nada
    más.
6.  En su propio problema de investigación: ¿qué es un caso, y por qué
    esa elección afecta el supuesto i.i.d.?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase01a_presentacion_del_modulo.html` · `.pdf` | Deck administrativo: evaluación, calendario, reglas |
| `slides/clase01b_riesgo_esperado_y_empirico.html` · `.pdf` | Deck de contenido |
| `codigo/clase01_riesgo_empirico_vs_esperado.ipynb` | Cuaderno: genera las figuras y verifica sus valores |
| `guia/guia01.md` | Esta guía |
| `01 Instrumentos/Diagnostico_de_entrada_cuestionario.pdf` | Cuestionario del diagnóstico |
| `02 Entorno/requirements.txt` | Entorno de ejecución |

Los archivos `.html` son las diapositivas navegables; se abren en
cualquier navegador y funcionan sin conexión. Los `.pdf` son la versión
para repasar e imprimir.

## 9. La próxima semana

**Semana 2 · Espacios de hipótesis y sesgo inductivo.** Si el riesgo
empírico no basta para elegir $h$, ¿qué lo hace? La respuesta es el
sesgo inductivo: las restricciones que imponemos sobre $\mathcal{H}$
antes de ver los datos. Y el teorema de No Free Lunch dice qué precio
tiene esa decisión.

**Taller 1 · Entorno reproducible** (2 hp). Control de versiones,
fijación de semillas, declaración del entorno y registro de
experimentos. Se entrega **cuaderno + bitácora de una página**. Es el
taller que fija el estándar con que se corrigen los cinco siguientes.
