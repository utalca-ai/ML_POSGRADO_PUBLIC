# Semana 8 · Comparación estadística de algoritmos


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
| **Sesión de clase** | Comparar dos algoritmos · varios conjuntos y comparaciones múltiples |
| **Actividad** | **Taller 4** (2 hp) |
| **Hito calificado** | **Entrega del taller 4** |
| **Trabajo sincrónico** | 4 hp: 2 de clase + 2 de taller |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Desde la semana 2 quedó abierta una pregunta: ¿qué significa que un
método sea «mejor»? Esta semana se cierra.

La primera parte trata la comparación sobre **un** conjunto de datos y
desmonta el procedimiento que casi todo el mundo usa. La segunda trata
la comparación sobre **una población de problemas**, que es la que
sostiene una afirmación metodológica, y da el procedimiento estándar del
área —Demšar (2006).

## 2. Qué debería poder hacer al terminar la semana

1.  Distinguir las tres preguntas: mejor *en este conjunto*, mejor *en
    esta clase de problemas*, y mejor *en general* —que no tiene
    respuesta.
2.  Diseñar una comparación pareada con protocolo y presupuesto
    idénticos.
3.  Explicar por qué la prueba $t$ sobre un remuestreo no es válida, y
    **cuánto** se equivoca según el esquema.
4.  Aplicar el procedimiento de Demšar: rangos, Friedman, prueba
    posterior y corrección de Holm.
5.  Leer y producir un diagrama de diferencia crítica.
6.  Reportar el tamaño del efecto en las unidades del problema.

## 3. La sesión sincrónica

| Bloque | Duración | Material |
|----|----|----|
| Comparar dos algoritmos | 50 min | `clase08a`, 18 láminas |
| Varios conjuntos, varios algoritmos | 50 min | `clase08b`, 16 láminas |
| **Taller 4** | 2 hp aparte | Comparación de tres algoritmos |

## 4. Notación y definiciones

**Las tres preguntas.** La prueba que corresponde es distinta según cuál
se esté respondiendo. Confundirlas es el error de fondo.

**El diseño pareado.** Compare siempre sobre los **mismos datos y las
mismas particiones**. La variabilidad común se cancela y queda solo lo
que separa a los métodos. Es gratis y multiplica la potencia.

**El presupuesto.** Mismo protocolo, mismo presupuesto de
hiperparámetros —declarado en configuraciones o en tiempo—, mismo
preprocesamiento. *Si su método recibió más cómputo que la referencia,
usted midió el cómputo.*

**McNemar**, para dos clasificadores sobre un conjunto de prueba, usando
solo los casos en que discrepan:

$$\chi^2=\frac{\bigl(\lvert n_{01}-n_{10}\rvert-1\bigr)^2}{n_{01}+n_{10}}$$

**Rangos, no valores.** Los desempeños no son comparables entre
conjuntos: un 0,72 en un problema difícil puede ser mejor que un 0,95 en
uno fácil. Se sustituye cada fila por los rangos y se trabaja con el
rango medio:

$$R_j=\frac{1}{N}\sum_{i=1}^{N} r_{ij}$$

**Friedman**, prueba ómnibus sobre los rangos medios:

$$\chi_F^2=\frac{12N}{k(k+1)}\left[\sum_{j=1}^{k}R_j^2-\frac{k(k+1)^2}{4}\right]$$

Si **no** se rechaza, el análisis termina ahí. No se buscan pares.

**Nemenyi**, diferencia crítica entre rangos medios:

$$DC=q_\alpha\sqrt{\frac{k(k+1)}{6N}}$$

**Comparaciones múltiples.** Con $m$ pruebas independientes al nivel
$\alpha$ y ninguna diferencia real, la probabilidad de al menos un falso
positivo es $1-(1-\alpha)^m$: con $m=10$ ya es del **40 %**.

Use **Holm**, no Bonferroni: misma garantía sobre la tasa de error
familiar y uniformemente más potencia.

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Ejecutar y estudiar el cuaderno de la clase | 1,5 h | Cuaderno corrido | Antes de la semana 9 |
| 2 | Completar y entregar el **taller 4** | 2,0 h | Cuaderno + bitácora | Fin de semana 8 |
| 3 | **Redactar el diseño experimental** de su proyecto | 2,5 h | Borrador | **Tutoría 2, semana 9** |
| 4 | Repasar Demšar (2006) sobre el propio diseño | 0,5 h | — | — |

### 5.1 El taller 4

**Comparación estadística de tres algoritmos sobre varios conjuntos de
datos.**

Lo que se corrige, además de los ocho ítems habituales:

- Que el protocolo y el presupuesto sean **idénticos** para los tres
  métodos.
- Que la unidad de análisis sea el **conjunto de datos** y no el
  pliegue.
- Que la prueba y la corrección se declaren **antes**, no después de
  mirar.
- Que haya un **diagrama de diferencia crítica** o equivalente.
- Que se reporte el **tamaño del efecto** en las unidades del problema.

### 5.2 Qué mirar en el cuaderno

`clase08_comparacion_estadistica.ipynb` tiene dos experimentos.

**El primero** compara dos algoritmos sobre datos **sin ninguna señal**
—ambos valen 0,5, así que la hipótesis nula es verdadera por
construcción— y cuenta cuántas veces la prueba $t$ rechaza:

| Esquema de remuestreo           | Rechaza    | Inflación |
|---------------------------------|------------|-----------|
| Validación cruzada, 10 pliegues | 7,0 %      | 1,4×      |
| Validación cruzada, 5 pliegues  | 9,5 %      | 1,9×      |
| Submuestreo repetido, 30 veces  | **40,5 %** | **8,1×**  |
| Submuestreo repetido, 100 veces | **63,0 %** | **12,6×** |

El resultado va contra el instinto: **la validación cruzada infla
poco**, y lo catastrófico es el submuestreo repetido —que **empeora
cuantas más repeticiones se hagan**.

La razón: cada remuestreo adicional no aporta datos nuevos, son los
mismos casos barajados otra vez, pero sí reduce la varianza aparente del
promedio. La prueba lee esa reducción como certeza.

**Regla que conviene memorizar:** su $n$ estadístico son los casos, o
los conjuntos de datos. Nunca las veces que barajó los mismos casos.

**El segundo** aplica el procedimiento completo de Demšar sobre 4
algoritmos y 18 conjuntos de datos, y produce el diagrama de diferencia
crítica.

## 6. Lecturas

**Ya leída, y es el contenido de esta semana**

> Demšar, J. (2006). Statistical comparisons of classifiers over
> multiple data sets. *JMLR*, 7, 1–30.

**De reserva, directamente pertinentes**

> Dietterich, T. G. (1998). Approximate statistical tests for comparing
> supervised classification learning algorithms. *Neural Computation*,
> 10(7). Es el origen del resultado del primer experimento del cuaderno.
>
> Bouthillier, X., et al. (2021). Accounting for variance in machine
> learning benchmarks. *MLSys*.

## 7. Preguntas de comprobación

1.  Nombre las tres preguntas de comparación. ¿Cuál está respondiendo su
    tesis?
2.  ¿Por qué la prueba $t$ sobre 100 submuestreos repetidos rechaza el
    63 % de las veces cuando no hay ninguna diferencia?
3.  ¿Por qué promediar AUC sobre 15 conjuntos de datos no significa
    nada?
4.  Friedman no rechaza. ¿Qué hace a continuación?
5.  Con 6 algoritmos hay 15 comparaciones por pares. Sin corregir, ¿cuál
    es la probabilidad de encontrar «algo»?
6.  ¿Por qué Holm domina a Bonferroni?
7.  Su diferencia es significativa con $p=0{,}001$ y vale 0,003 de AUC.
    ¿Qué reporta?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase08a_comparar_dos.*` | Comparación pareada y la trampa del remuestreo |
| `slides/clase08b_multiples.*` | Demšar, Friedman, Nemenyi y multiplicidad |
| `codigo/clase08_comparacion_estadistica.ipynb` | Los dos experimentos |
| `guia/guia08.md` | Esta guía |

## 9. La próxima semana

**Semana 9 · Ingeniería de atributos y aprendizaje de
representaciones.** PCA y métodos no lineales.

**Tutoría 2** y el hito de **diseño experimental**: el protocolo de
evaluación de su proyecto, declarado por escrito **antes** de correr el
primer experimento. Formativo, obligatorio, sin nota —y requisito para
presentar el informe final.
