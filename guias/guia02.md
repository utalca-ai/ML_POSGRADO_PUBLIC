# Semana 2 · Sesgo inductivo y No Free Lunch


- [1. De qué trata esta semana](#1-de-qué-trata-esta-semana)
- [2. Qué debería poder hacer al terminar la
  semana](#2-qué-debería-poder-hacer-al-terminar-la-semana)
- [3. La sesión sincrónica](#3-la-sesión-sincrónica)
- [4. Notación y definiciones](#4-notación-y-definiciones)
- [5. Trabajo autónomo de la semana](#5-trabajo-autónomo-de-la-semana)
- [6. Lecturas](#6-lecturas)
- [7. La reseña 1](#7-la-reseña-1)
- [8. Preguntas de comprobación](#8-preguntas-de-comprobación)
- [9. Materiales de esta semana](#9-materiales-de-esta-semana)
- [10. La próxima semana](#10-la-próxima-semana)

> **Cómo usar esta guía.** Dice qué pasa en la sesión sincrónica, qué
> tiene que hacer usted por su cuenta, cuánto tiempo tomar cada cosa y
> con qué se corrige. Es el contrato de la semana.

|  |  |
|----|----|
| **Unidad** | 1 · Formulación del aprendizaje inductivo |
| **Sesión de clase** | Espacios de hipótesis y sesgo inductivo · No Free Lunch |
| **Actividad** | **Taller 1 · Entorno reproducible** (2 hp) |
| **Hito calificado** | **Entrega del taller 1** |
| **Trabajo sincrónico** | 4 horas pedagógicas (2 de clase + 2 de taller) |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

> [!WARNING]
>
> **Es la semana más cargada del primer tercio.** Además del taller, hay
> que leer Wolpert para el seminario 1 y entregar la reseña 1, que vence
> **48 horas antes de la sesión de la semana 3**. Empiece por la
> lectura, no por el taller.

------------------------------------------------------------------------

## 1. De qué trata esta semana

La semana 1 dejó un problema abierto: si el error de entrenamiento no
basta para elegir una hipótesis, ¿qué la elige? Esta semana responde que
la elige el **sesgo inductivo** —los supuestos que usted impone sobre
$\mathcal{H}$ antes de ver los datos— y muestra que sin él la
generalización es literalmente imposible, no solo difícil.

La segunda parte pone precio a esa respuesta. El teorema de **No Free
Lunch** dice que ningún sesgo es mejor a priori: toda ventaja en una
clase de problemas se paga con una desventaja exacta en otra. De ahí se
sacan con frecuencia tres conclusiones falsas, y buena parte de la clase
consiste en desmontarlas.

## 2. Qué debería poder hacer al terminar la semana

1.  Reproducir el argumento de conteo que muestra que una muestra no
    restringe las predicciones sobre los puntos no observados.
2.  Definir sesgo inductivo, y nombrar los **tres lugares** donde opera:
    el espacio $\mathcal{H}$, el criterio de preferencia y el algoritmo
    de búsqueda.
3.  Enunciar qué supone sobre el mundo cada familia de modelos que usted
    use.
4.  Enunciar No Free Lunch con precisión, e identificar las tres
    lecturas incorrectas cuando aparezcan en un artículo o en una
    discusión.
5.  Escribir una afirmación de superioridad con sus tres complementos:
    clase de problemas, pérdida y evidencia.

## 3. La sesión sincrónica

**Clase: 2 horas pedagógicas** (100 minutos), en dos bloques de 50.

| Bloque             | Duración | Material               |
|--------------------|----------|------------------------|
| El sesgo inductivo | 50 min   | `clase02a`, 17 láminas |
| No Free Lunch      | 50 min   | `clase02b`, 17 láminas |

**Taller 1: 2 horas pedagógicas**, en sesión aparte.

## 4. Notación y definiciones

**El conteo.** Con $n$ atributos binarios hay $2^n$ entradas posibles y
$2^{2^n}$ funciones. Observados $m$ casos sin ruido, las funciones
compatibles con la muestra son:

$$\#\{h \text{ consistentes con } S\} \;=\; 2^{\,2^n - m}$$

y para **cada** punto no observado, exactamente la mitad de ellas
predice 1.

**Sesgo inductivo** (Mitchell, 1980). El conjunto $B$ de supuestos que,
añadidos a la muestra, hacen que la predicción se siga deductivamente:

$$S \;\cup\; B \;\vdash\; h(x) \qquad \text{para todo } x\in\mathcal{X}$$

**Restricción dura y blanda.** Acotar $\mathcal{H}$ de entrada, o
admitirlo grande y penalizar la complejidad:

$$\hat h \;=\; \operatorname*{arg\,min}_{h\in\mathcal{H}} \; R_S(h) \;+\; \lambda\,\Omega(h)$$

**No Free Lunch** (Wolpert, 1996). Para dos algoritmos $a_1$ y $a_2$,
tamaño de muestra $m$ y error fuera de la muestra $e$:

$$\sum_{f} P\bigl(e \mid m,\, a_1,\, f\bigr) \;=\; \sum_{f} P\bigl(e \mid m,\, a_2,\, f\bigr)$$

donde la suma recorre **todas** las funciones objetivo posibles. El
supuesto oculto, y decisivo, es que esa suma equivale a una distribución
**uniforme** sobre las funciones.

## 5. Trabajo autónomo de la semana

Aproximadamente **6,5 horas cronológicas**.

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Leer Wolpert (1996) — **obligatoria** | 2,0 h | Notas propias | Antes de escribir la reseña |
| 2 | Escribir la **reseña 1** | 2,0 h | 2 páginas | **48 h antes de la sesión de la semana 3** |
| 3 | Completar y entregar el **taller 1** | 2,0 h | Cuaderno + bitácora | Fin de semana 2 |
| 4 | Ejecutar el cuaderno de la clase | 0,5 h | Cuaderno corrido | Antes de la semana 3 |

### 5.1 El taller 1

**Entorno reproducible: control de versiones, semillas y registro de
experimentos.**

Se entrega **cuaderno + bitácora de una página** en su repositorio
privado. La fecha de entrega es la del *commit*, no la del correo.

Se corrige con la lista de cotejo de ocho ítems, que es **la misma para
los seis talleres del semestre**:

1.  El cuaderno se ejecuta completo, de cero, en un entorno limpio.
2.  Semillas, versiones de bibliotecas y entorno están fijados y
    declarados.
3.  El protocolo de partición está explicitado y no admite fuga de
    información.
4.  Toda transformación ajustada sobre datos se estima solo con
    entrenamiento.
5.  Los resultados se reportan con su variabilidad, no solo con el valor
    medio.
6.  La métrica está justificada por el problema y no por costumbre.
7.  La bitácora declara una decisión alternativa descartada, con su
    razón.
8.  Las afirmaciones de la bitácora se sostienen en la salida y no la
    exceden.

Se aprueba con **7 de 8**. Cada ítem es logrado o no logrado: no hay
puntos intermedios. Se admite **una reentrega** dentro de la semana
siguiente; el taller aprobado en reentrega cuenta como media aprobación.

**Los dos cuadernos de clase son el estándar esperado.** Tanto
`clase01_riesgo_empirico_vs_esperado.ipynb` como
`clase02_conteo_de_hipotesis.ipynb` cumplen los ocho ítems uno por uno,
con la bitácora incluida. Mírelos antes de entregar, no después.

Un detalle del ítem 5 que suele malinterpretarse: **reportar
variabilidad no significa siempre calcular una desviación estándar.** El
cuaderno de esta semana declara explícitamente que no hay variabilidad
que reportar, porque su resultado es un conteo exacto, y verifica esa
afirmación en vez de inventar un estadístico. Eso también es cumplir el
ítem.

### 5.2 Qué mirar en el cuaderno de la clase

`clase02_conteo_de_hipotesis.ipynb` enumera **exhaustivamente** las 65
536 funciones sobre cuatro atributos binarios, y comprueba tres cosas:

| Paso | Resultado |
|----|----|
| Con $\mathcal{H}$ = todas las funciones | La fracción que predice 1 en cada punto no visto es **exactamente** 0,5 |
| Con $\mathcal{H}$ = conjunciones, sesgo correcto | La muestra informa: las predicciones se determinan |
| Con $\mathcal{H}$ = conjunciones, sesgo incorrecto | En el **98 %** de los objetivos aleatorios no sobrevive ninguna hipótesis |

El tercer resultado es el más importante y el menos intuitivo: cuando el
sesgo es incorrecto, el método **falla ruidosamente**. Eso parece un
defecto y es una virtud. Lo peligroso es el sesgo que siempre devuelve
una respuesta, porque nunca se entera de estar equivocado —y usted
tampoco.

## 6. Lecturas

**Obligatoria — se discute en el seminario 1**

> Wolpert, D. H. (1996). The lack of a priori distinctions between
> learning algorithms. *Neural Computation*, 8(7), 1341–1390.

Es largo y técnico. **No lo lea entero de corrido.** La estrategia
razonable es: leer la introducción y las conclusiones, identificar el
enunciado formal del resultado, y volver sobre las secciones técnicas
solo lo necesario para reconstruir el argumento. Su reseña se califica
por reconstruir el argumento y sus supuestos, no por resumir el artículo
sección por sección.

Al leerlo, busque específicamente: **dónde entra el supuesto de
uniformidad** sobre las funciones objetivo, y qué dice Wolpert sobre lo
que su resultado *no* implica.

**Ya leída en la semana 1, y también se discute**

> Domingos, P. (2012). A few useful things to know about machine
> learning. *Communications of the ACM*, 55(10), 78–87.

Vuelva sobre las secciones 3 y 6: son la versión práctica del mismo
argumento.

## 7. La reseña 1

**Dos páginas, entregadas 48 horas antes de la sesión de la semana 3.**
Cuatro criterios en escala 1 a 4, máximo 16 puntos:

$$\text{nota} \;=\; 1{,}0 \;+\; 6{,}0 \times \frac{\text{puntaje}}{16}$$

| Criterio | Qué se evalúa |
|----|----|
| Reconstrucción del argumento | Afirmación central, evidencia, alcance declarado; distinguir lo demostrado de lo sugerido |
| Supuestos y amenazas a la validez | Al menos un supuesto no declarado, y cómo cambia la conclusión si no se cumple |
| Juicio metodológico | Particiones, fuga, variabilidad, pertinencia de la comparación |
| Posicionamiento propio | Conexión con su problema y una objeción que abra trabajo posterior |

Se promedian **las 4 mejores de 5**, así que la reseña 1 funciona en la
práctica como calibración: es la entrega en la que descubre qué se le
está pidiendo. Aproveche eso y arriesgue.

Tiene la rúbrica completa y **una reseña de ejemplo ya corregida** desde
la semana 1.

## 8. Preguntas de comprobación

1.  Con 4 atributos binarios y 10 casos observados, ¿cuántas funciones
    quedan consistentes? ¿Y qué predicen sobre los 6 puntos restantes?
2.  Nombre los tres lugares donde opera el sesgo inductivo. ¿Cuál de los
    tres declara su método favorito, y cuáles dos no?
3.  ¿Qué supone sobre el mundo un modelo de $k$ vecinos más cercanos? ¿Y
    uno convolucional?
4.  Enuncie No Free Lunch. ¿Sobre qué se está promediando, y por qué ese
    promedio no describe los problemas reales?
5.  Un colega dice: «el teorema demuestra que da igual qué algoritmo
    uses». ¿Dónde está el error?
6.  Escriba, para su propio problema de tesis, la frase completa de
    superioridad con sus tres complementos.

## 9. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase02a_sesgo_inductivo.*` | Primera parte: el problema de la inducción y el sesgo |
| `slides/clase02b_no_free_lunch.*` | Segunda parte: el teorema y sus lecturas |
| `codigo/clase02_conteo_de_hipotesis.ipynb` | Enumeración exhaustiva del espacio de funciones |
| `guia/guia02.md` | Esta guía |

## 10. La próxima semana

**Semana 3 · Compromiso sesgo-varianza.** Capacidad y complejidad:
dimensión VC, márgenes, regularización. Cuál es el alcance real de las
garantías teóricas. Es la forma cuantitativa de la tensión que esta
semana quedó planteada en términos cualitativos.

**Seminario 1** (1 hp): Wolpert (1996) y Domingos (2012). Recuerde que
hay un **expositor** y un **discutidor** designados, sorteados en la
semana 1. El discutidor entrega su objeción por escrito **antes** de la
sesión.
