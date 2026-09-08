# Semana 3 · El compromiso sesgo-varianza


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
| **Unidad** | 1 · Formulación del aprendizaje inductivo |
| **Sesión de clase** | Compromiso sesgo-varianza · capacidad y garantías teóricas |
| **Actividad** | **Seminario 1** — Wolpert (1996) y Domingos (2012) |
| **Hito calificado** | **Reseña 1**, entregada 48 h antes de la sesión |
| **Trabajo sincrónico** | 2 hp: 1 de clase + 1 de seminario |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Las semanas 1 y 2 dejaron planteada una tensión sin cuantificar:
restringir $\mathcal{H}$ hace posible aprender, y restringir de más
impide acertar. Esta semana le pone números.

La herramienta es la **descomposición sesgo-varianza**: el error
esperado se parte en tres sumandos, dos de los cuales se compensan entre
sí y uno que no se puede tocar. Después vemos la maquinaria teórica
—capacidad, dimensión VC, cotas de generalización— y, sobre todo,
**hasta dónde llega**: esas cotas son correctas y numéricamente
inútiles, y conviene saber por qué antes de citarlas en una tesis.

## 2. Qué debería poder hacer al terminar la semana

1.  Escribir la descomposición sesgo-varianza y decir qué mide cada
    término.
2.  Diagnosticar, ante un resultado, si el problema es de sesgo o de
    varianza —y saber que el remedio es distinto en cada caso.
3.  Explicar por qué la capacidad no es el número de parámetros.
4.  Enunciar qué garantiza una cota VC, y por qué su valor numérico no
    sirve para predecir el error de su modelo.
5.  Estimar, o acotar, el piso de ruido de su propio problema.

## 3. La sesión sincrónica

Esta es una **semana de seminario**: el bloque de 2 hp se reparte en una
hora de clase y una de discusión.

| Bloque                           | Duración | Material                         |
|----------------------------------|----------|----------------------------------|
| Clase: compromiso sesgo-varianza | 50 min   | `clase03`, 18 láminas            |
| **Seminario 1**                  | 50 min   | Wolpert (1996) · Domingos (2012) |

### Cómo funciona el seminario

| Rol | Qué hace | Se califica |
|----|----|----|
| **Expositor** | Presenta el artículo en 12–15 min | Que identifique la contribución y el método sin recorrer el artículo linealmente; que respete el tiempo; que responda a las objeciones con argumentos y no con autoridad |
| **Discutidor** | Abre la discusión con una objeción **entregada por escrito antes de la sesión** | Que la objeción sea específica de ese artículo y que admita respuesta |

En las semanas con dos artículos —esta, la 5, la 7 y la 13— usted toma
los dos roles en la misma sesión: expone uno y objeta el otro. En la
semana 11, que tiene un solo artículo, expone y el profesor abre la
discusión. Ese 5 % del módulo es el promedio de todas sus actuaciones
del semestre.

Quien audita el módulo participa con los mismos roles, sin calificación.

### Qué es una objeción, y qué contiene la media página

Una objeción no es una crítica al artículo ni una lista de lo que le
faltó. Es **una afirmación concreta del texto que usted sostiene que no
queda establecida por lo que el artículo mismo ofrece**.

Se califican dos cosas, y solo dos:

1.  **Que sea específica de ese artículo.** Si su objeción se puede
    copiar y pegar en la reseña de cualquier otro trabajo, no es una
    objeción.
2.  **Que admita respuesta.** Es decir, que usted mismo pueda decir qué
    tendría que mostrarse para que quede resuelta. Una objeción que nada
    podría responder no abre la discusión: la cierra.

La entrega es de **media página**, en cuatro partes. Una o dos frases
cada una, salvo la segunda.

| \# | Parte | Qué va ahí |
|----|----|----|
| 1 | **La afirmación que objeta** | Citada o parafraseada con precisión, con la sección o el teorema donde aparece. Se objeta una afirmación, no un artículo. |
| 2 | **Por qué no queda establecida** | O bajo qué condición deja de estarlo. La razón sale del material del propio artículo —su evidencia, su alcance declarado, sus supuestos—, no de una opinión externa ni de lo que usted habría hecho en su lugar. |
| 3 | **Qué la resolvería** | Un resultado, un dato, un supuesto verificado. Es la parte que hace que la objeción admita respuesta, y la que casi siempre falta. |
| 4 | **La pregunta con la que abre** | Una sola, dirigida al expositor. |

#### Un ejemplo, sobre un artículo hipotético

Suponga un artículo que concluye que el método A supera al método B
porque obtiene mejor promedio en 12 conjuntos de datos.

> **Objeción que no sirve.** «El artículo no valida suficientemente sus
> resultados.»

Sirve para cualquier artículo, y por eso no dice nada de este.

> **La misma intuición, convertida en objeción.** «Los autores concluyen
> la superioridad de A a partir de la media sobre 12 conjuntos, pero no
> reportan la dispersión entre repeticiones ni corrigen por
> comparaciones múltiples. Con 12 conjuntos y una diferencia de esa
> magnitud, el resultado es compatible con la variabilidad de las
> particiones. La objeción quedaría resuelta si mostraran el resultado
> por conjunto con su variabilidad, o una prueba de rangos con signo.
> ¿Sobre qué base descartan que la diferencia sea ruido de partición?»

Es específica, se sostiene en lo que el artículo reporta y dice qué la
resolvería. Eso es lo que se evalúa.

### El criterio de juicio metodológico, esta semana

La rúbrica de reseña pide evaluar el protocolo experimental:
particiones, fuga de información, variabilidad reportada. Wolpert es un
teorema y Domingos un ensayo, y ninguno de los dos tiene protocolo
experimental que juzgar.

Esta semana el criterio se lee, entonces, como **qué tipo de argumento
es y qué evidencia lo sostiene: dónde termina lo demostrado y dónde
empieza lo sugerido**. Desde la reseña 3 —Kapoor y Narayanan, en la
semana 7— el criterio aplica en su sentido literal.

## 4. Notación y definiciones

**La descomposición.** Con $y = f(x)+\varepsilon$,
$\mathbb{E}[\varepsilon]=0$ y
$\operatorname{Var}(\varepsilon)=\sigma^2$, y llamando
$\bar h(x_0)=\mathbb{E}_S[\hat h_S(x_0)]$ a la predicción promedio sobre
muestras:

$$\mathbb{E}\bigl[(y-\hat h_S(x_0))^2\bigr]=
\underbrace{\bigl(f(x_0)-\bar h(x_0)\bigr)^2}_{\text{sesgo}^2}+
\underbrace{\mathbb{E}\bigl[(\hat h_S(x_0)-\bar h(x_0))^2\bigr]}_{\text{varianza}}+
\underbrace{\sigma^2}_{\text{ruido}}$$

*Cómo se deriva:* sume y reste $\bar h(x_0)$ dentro del cuadrado y
desarrolle. El término cruzado se anula porque
$\mathbb{E}_S[\hat h_S(x_0)-\bar h(x_0)]=0$ por definición de $\bar h$.

*Qué varía en esa esperanza.* $\mathbb{E}_S$ promedia sobre **muestras
de entrenamiento**, y sobre nada más. Quedan fijos la familia
$\mathcal{H}$, el algoritmo de ajuste, el tamaño $n$ y el punto $x_0$;
lo único que cambia son los datos con los que se ajusta, y por
consecuencia los coeficientes y la predicción en $x_0$. Conviene no
confundir $\mathcal{H}$ —la familia, una sola— con
$\hat h_{S_1}, \hat h_{S_2}, \ldots$, que son muchas hipótesis **dentro
de esa misma familia**. El subíndice $S$ es la marca de que el modelo es
función de la muestra, y por lo tanto una variable aleatoria.

**Dimensión VC.** Antes de la definición, el supuesto que la hace
legible: aquí $h$ **clasifica**. Es una función discriminante —en el
caso lineal, $h(x)=\operatorname{signo}(w^\top x + b)$— y la recta que
la representa es la **frontera de decisión**: parte el plano en dos
mitades y asigna una etiqueta a cada lado. **No pasa por los puntos, los
separa.** Leída como si la recta ajustara los datos, la definición que
sigue no tiene sentido.

Se dice que $\mathcal{H}$ **pulveriza** un conjunto de $d$ puntos si,
para cada una de las $2^d$ maneras de etiquetarlos, existe algún
$h\in\mathcal{H}$ que la reproduce. La **dimensión VC** es el mayor $d$
tal que existe **algún** conjunto de $d$ puntos que $\mathcal{H}$
pulveriza.

En esa asimetría está el contenido: **mejor caso sobre la elección de
los puntos, peor caso sobre las etiquetaciones.** Basta con que funcione
una configuración, pero en ella tienen que salir todas las
etiquetaciones.

*Rectas en el plano:* $d_{VC}=3$. Tres puntos en triángulo se pulverizan
—las dos etiquetaciones de «todos iguales» se consiguen dejando el
triángulo entero de un lado, y las seis restantes cortando un vértice—.
Tres puntos **colineales** no se pulverizan: la etiquetación $+,-,+$ es
imposible, porque una recta que deje los extremos del mismo lado deja
también todo lo que hay entre ellos. Eso no baja la dimensión a 2,
porque basta el triángulo. Con cuatro puntos, en cambio, no sobrevive
ninguna configuración: en posición convexa falla el caso de las
diagonales opuestas —el XOR— y, si uno queda dentro del triángulo de los
otros tres, falla separar el interior de los vértices.

*Otros casos:* hiperplanos en $\mathbb{R}^p$, $d_{VC}=p+1$. Y
$h(x)=\operatorname{signo}(\sin(\alpha x))$, con un solo parámetro,
$d_{VC}=\infty$: la razón de que contar parámetros no mida la capacidad.

**Cota de generalización.** Con probabilidad $\geq 1-\delta$, para toda
$h\in\mathcal{H}$ simultáneamente:

$$R_{\mathcal{D}}(h)\;\leq\;R_S(h)\;+\;\sqrt{\frac{d_{VC}\bigl(\log\frac{2n}{d_{VC}}+1\bigr)+\log\frac{4}{\delta}}{n}}$$

La palabra decisiva es **«para toda $h$ simultáneamente»**: por eso la
cota sobrevive al hecho de que el entrenamiento elige $h$ mirando la
muestra.

**Márgenes, o por qué el SVM funciona igual.** La objeción natural es el
kernel. Si el problema no es linealmente separable se pasa a un espacio
de características donde sí lo es —agregar $x_1x_2$ como tercera
coordenada ya resuelve el XOR— y la frontera, vista de vuelta en el
plano original, es una curva. Eso no contradice que $d_{VC}=3$: esa
cifra era de las rectas, y usted cambió de familia. Las cónicas en el
plano tienen $d_{VC}=6$, y el cambio se paga en varianza.

El caso interesante es el kernel gaussiano, cuyo espacio de
características es de dimensión infinita: $d_{VC}=\infty$ y la cota de
arriba queda **vacía**, no dice nada. Y sin embargo el método funciona.
La resolución es que existe otra cota, en la que la capacidad efectiva
no depende de la dimensión sino del **margen**: si los datos caben en
una bola de radio $R$ y el separador deja un margen $\gamma$, esa
capacidad se acota por $R^2/\gamma^2$, sin que la dimensión aparezca por
ninguna parte. Maximizar el margen —y el parámetro $C$, que lo negocia
contra los errores— **es** el control de capacidad. Es la misma moraleja
un escalón más arriba: la capacidad no es el número de parámetros, y
tampoco es la dimensión del espacio de características.

Y un cierre con el seminario del mismo día: elegir el kernel *es* elegir
el sesgo inductivo, es decir, comprometerse con una priori. No hay
almuerzo gratis en esa elección; el gaussiano funciona porque la
suavidad que supone resulta ser cierta en los problemas que solemos
encontrar.

### Dos ejes que se confunden

La varianza no se mide en el conjunto de validación. Se mide sobre los
datos con los que usted **entrenó**.

| La pregunta | El eje que define |
|----|----|
| ¿Con qué datos ajusté el modelo? | El de la **varianza**: si repitiera el estudio con otra muestra de la misma población, ¿me saldría el mismo modelo? |
| ¿En qué datos lo evalúo? | El del **error de prueba**, que estima la suma de los tres términos, no la varianza sola. |

La piedra de toque es el modelo lineal. Ajuste una recta a muchas
muestras distintas del mismo fenómeno y obtendrá otras tantas rectas
casi superpuestas: todas parecidas entre sí, y todas errándole a la
curva verdadera de la misma manera. Eso es **varianza baja y sesgo
alto**. Que le vaya mal en validación no lo convierte en un modelo de
varianza alta: es un modelo consistente y equivocado. Varianza baja no
significa «acierta», significa «no cambia de opinión».

De ahí que un error de prueba alto, por sí solo, no diagnostique nada.
La recta y el polinomio de grado 12 pueden dar un número parecido y
necesitar remedios opuestos —más capacidad en un caso, menos en el
otro—. Para separarlos hacen falta los dos números, y el delator es el
error de entrenamiento: la recta falla también ahí, porque ni siquiera
puede ajustar los datos que vio; el grado 12 los clava.

Un último punto, sobre el alcance. La descomposición vive sobre el
experimento de las muchas muestras, así que solo el cuaderno la puede
calcular: tiene las 3000 réplicas y además conoce $f$. Con una sola
muestra —su caso, siempre— la validación estima el error total, no su
descomposición. De un conjunto de validación no se leen el sesgo y la
varianza por separado.

## 5. Trabajo autónomo de la semana

Aproximadamente **6,5 horas cronológicas**.

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Ejecutar y estudiar el cuaderno de la clase | 1,5 h | Cuaderno corrido de cero | Antes de la semana 4 |
| 2 | Leer Hastie et al. (2009), §7.1–7.3 | 2,0 h | Notas propias | Antes de la semana 4 |
| 3 | **Estimar el piso de ruido de su problema** | 1,5 h | Media página, para la tutoría 1 | Semana 5 |
| 4 | Repasar Shalev-Shwartz y Ben-David, cap. 6 — opcional | 1,5 h | — | — |

### 5.1 El ejercicio del piso de ruido

Es el que más rinde y el que casi nadie hace. Para su propio problema de
tesis, responda por escrito:

1.  ¿Cuál es el error mínimo que un predictor perfecto cometería, dado
    lo que se mide? Es decir, ¿cuánta información sobre $y$ **no** está
    en $x$?
2.  ¿Cómo podría acotarlo con los datos que tiene? Dos vías habituales:
    **mediciones repetidas del mismo caso** —la dispersión entre
    repeticiones es una cota inferior del ruido— y el **acuerdo entre
    anotadores**, si las etiquetas son juicios humanos.
3.  Si no puede estimarlo, ¿qué tendría que medir para poder hacerlo?

Esto importa porque define **cuánto margen de mejora existe realmente**.
Si dos expertos coinciden en el 85 % de los casos, un clasificador del
95 % es sospechoso, no excelente.

### 5.2 Qué mirar en el cuaderno

`clase03_sesgo_varianza.ipynb` repite el estudio **3000 veces** con
muestras independientes —el experimento mental de la clase, hecho de
verdad— y mide los tres términos por separado. El diseño es el de Bishop
(2006), §3.2, figura 3.5, con su mismo tamaño de muestra: 24 funciones
base gaussianas más el sesgo, $n=25$ y ajuste por regresión de cresta.

**La capacidad se recorre con $\lambda$, no con el número de
parámetros.** El modelo tiene 25 coeficientes de principio a fin del
barrido; lo único que cambia es cuánto los aplasta la regularización.
Ese $\lambda$ es exactamente el de la semana 4.

Tres resultados que conviene ver con cuidado:

- La identidad se **verifica numéricamente**: la suma de los tres
  términos reproduce el error total medido de forma independiente. Si no
  lo hiciera, el cuaderno falla ruidosamente.
- El mínimo del error total está en $\ln\lambda = 0$: total $0{,}0784$,
  de los cuales $0{,}0625$ son ruido. Es decir, **el 80 % del error del
  mejor modelo es irreducible**, y el margen real de mejora era
  $0{,}0159$ —mucho menor de lo que sugiere el error absoluto—.
- **La curva en U aparece sin agregar un solo parámetro.** Es la
  afirmación de la clase —que la capacidad no es el número de
  parámetros— convertida en medición.

Y una advertencia de lectura: el eje horizontal es $\ln\lambda$, de modo
que la capacidad efectiva **disminuye hacia la derecha**. La figura está
espejada respecto de la curva en U de la semana 1.

## 6. Lecturas

**Del seminario de esta semana** (ya leídas)

> Wolpert, D. H. (1996). The lack of a priori distinctions between
> learning algorithms. *Neural Computation*, 8(7), 1341–1390.
>
> Domingos, P. (2012). A few useful things to know about machine
> learning. *Communications of the ACM*, 55(10), 78–87.

**De apoyo a la clase**

> Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of
> Statistical Learning* (2ª ed.), §7.1–7.3.

Cubre la descomposición y el «optimismo» del error de entrenamiento, que
es el sesgo optimista de la semana 1 con otro nombre.

> Bishop, C. M. (2006). *Pattern Recognition and Machine Learning*.
> Springer, §1.1 y §3.2.

De donde salen el ejemplo de $\operatorname{sen}(2\pi x)$ que se usa
desde la semana 1 y el experimento del cuaderno de esta semana, incluido
su tamaño de muestra. Consúltelo si quiere ver el original; no es
obligatorio.

> Geman, S., Bienenstock, E., & Doursat, R. (1992). Neural networks and
> the bias/variance dilemma. *Neural Computation*, 4(1), 1–58.

El artículo donde se formula el compromiso. Se cita aquí por
procedencia, no como lectura de la semana.

> Shalev-Shwartz, S., & Ben-David, S. (2014). *Understanding Machine
> Learning*, capítulo 6.

La dimensión VC con demostraciones. Opcional, y solo si le interesa la
parte teórica: nada de lo que se evalúa en el módulo la exige.

## 7. Preguntas de comprobación

1.  Escriba la descomposición y explique por qué el término cruzado se
    anula.
2.  Su modelo tiene error de entrenamiento alto y error de prueba
    parecido. ¿Sesgo o varianza? ¿Y qué hace al respecto?
3.  Su modelo tiene error de entrenamiento casi nulo y error de prueba
    cinco veces mayor. ¿Sesgo o varianza? ¿Y qué hace?
4.  Un modelo lineal le falla tanto en entrenamiento como en prueba. ¿Su
    varianza es alta o baja? Justifique.
5.  ¿Por qué $h(x)=\operatorname{signo}(\sin(\alpha x))$, con un solo
    parámetro, tiene dimensión VC infinita?
6.  ¿Qué le garantiza una cota VC, y por qué no le sirve para reportar
    el error esperado de su modelo?
7.  ¿Cuál es el piso de ruido de su problema de tesis, y cómo lo sabe?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase03_sesgo_varianza.*` | Las 18 láminas de la clase |
| `codigo/clase03_sesgo_varianza.ipynb` | Descomposición medida sobre 3000 réplicas, barriendo $\lambda$ |
| `guia/guia03.md` | Esta guía |

## 9. La próxima semana

**Semana 4 · Regresión lineal y logística como máxima verosimilitud.**
Regularización $L_1$ y $L_2$, y su lectura bayesiana. Es el mecanismo
concreto para controlar la capacidad de la que hablamos esta semana.

**Taller 2** (2 hp): regularización y frontera de decisión; efecto sobre
la varianza del estimador. Se entrega cuaderno + bitácora, con la misma
lista de cotejo de ocho ítems.
