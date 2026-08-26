# Semana 7 · Protocolos de validación y fuga de información


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
| **Sesión de clase** | Protocolos de validación · fuga de información |
| **Actividad** | **Seminario 3** — Kapoor y Narayanan (2023) · Demšar (2006) |
| **Hito calificado** | **Reseña 3**, 48 h antes de la sesión |
| **Trabajo sincrónico** | 2 hp: 1 de clase + 1 de seminario |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Seis semanas advirtiendo que el conjunto de prueba se gasta. Esta semana
dejamos de advertirlo y damos el procedimiento.

Y mostramos que el problema **no es de estudiantes**: Kapoor y Narayanan
documentan fuga de información en 294 artículos publicados de 17
disciplinas, con efectos que en varios casos anulaban por completo el
resultado reportado.

## 2. Qué debería poder hacer al terminar la semana

1.  Elegir entre *hold-out*, validación cruzada, repetida y anidada, con
    un argumento sobre su problema.
2.  Explicar qué estima el bucle externo de una validación anidada, y
    por qué no es lo mismo que el riesgo de un modelo.
3.  Reconocer las cinco categorías de fuga de la taxonomía de Kapoor y
    Narayanan.
4.  Decidir qué pasos van **dentro** del pliegue y cuáles pueden ir
    fuera.
5.  Elegir la partición que corresponde cuando sus datos **no** son
    i.i.d.

## 3. La sesión sincrónica

**Semana de seminario**: una hora de clase y una de discusión.

| Bloque          | Duración | Material                                  |
|-----------------|----------|-------------------------------------------|
| Clase           | 50 min   | `clase07`, 17 láminas                     |
| **Seminario 3** | 50 min   | Kapoor y Narayanan (2023) · Demšar (2006) |

## 4. Notación y definiciones

**Validación cruzada de $k$ pliegues.**

$$\widehat{R}_{VC}=\frac{1}{k}\sum_{j=1}^{k} R_{S_j}\bigl(\hat h_{-j}\bigr)$$

Cada caso se usa $k-1$ veces para entrenar y **exactamente una** para
evaluar. En clasificación, **estratificada**: cada pliegue conserva la
proporción de clases. Con desbalance fuerte no es opcional.

**Validación anidada.** Dos bucles: el interno elige hiperparámetros, el
externo estima el riesgo. Lo que el externo estima **no es el riesgo de
un modelo**: es el riesgo de *su procedimiento de construir modelos*,
que es lo que otro laboratorio replicaría.

**Una advertencia sobre la dispersión.** La desviación entre pliegues
**no es un intervalo de confianza**. Los conjuntos de entrenamiento de
dos pliegues comparten $(k-2)/(k-1)$ de los datos, así que no son
independientes y esa desviación subestima la variabilidad real. Llámela
*medida de estabilidad*, no *incertidumbre*.

**Fuga de información.** El procedimiento usa, directa o indirectamente,
información que no estará disponible al predecir. Cinco categorías:

| Tipo | En qué consiste |
|----|----|
| Sin conjunto de prueba limpio | No hay partición, o se usó más de una vez |
| Preprocesamiento sobre todos los datos | Escalado, imputación, selección de atributos |
| Atributo ilegítimo | Codifica la etiqueta o el futuro |
| Partición inválida | Los datos no son i.i.d. |
| Muestreo no representativo | La población de prueba no es la de aplicación |

**La regla operativa.** Todo lo que mira los datos —escalado,
imputación, selección, reducción de dimensionalidad, remuestreo,
hiperparámetros, recalibración— va **dentro** del pliegue. En la
práctica: use una tubería.

**Cuando i.i.d. es falso.**

| Si sus datos…                             | Use                   |
|-------------------------------------------|-----------------------|
| Son una serie temporal                    | Partición temporal    |
| Tienen medidas repetidas del mismo sujeto | Partición por grupos  |
| Vienen de varios centros                  | Dejar un centro fuera |
| Están agrupados espacialmente             | Partición por bloques |

La pregunta que decide la partición es: **¿qué tendrá que predecir el
modelo cuando se use?**

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Ejecutar y estudiar el cuaderno de la clase | 1,5 h | Cuaderno corrido | Antes de la semana 8 |
| 2 | Terminar Demšar (2006) | 1,5 h | Notas propias | Antes de la semana 8 |
| 3 | **Auditar su propio protocolo** con la taxonomía de fugas | 2,0 h | Una página | Para el diseño experimental (semana 9) |
| 4 | Preparar el taller 4 | 1,5 h | — | Semana 8 |

### 5.1 La auditoría de su propio protocolo

Es el ejercicio que más rinde de todo el semestre y es insumo directo
del hito de la semana 9. Recorra las cinco categorías de la taxonomía y
responda, por escrito y para su propio trabajo:

1.  ¿Cuántas veces ha mirado su conjunto de prueba? Cuente honestamente.
2.  ¿Qué pasos de preprocesamiento ajusta, y sobre qué datos los ajusta?
3.  ¿Alguno de sus atributos podría codificar la etiqueta o información
    futura? Piense en identificadores, fechas y variables derivadas.
4.  ¿Son sus casos independientes? Si hay repeticiones del mismo equipo,
    sujeto o sitio, ¿su partición los separa?
5.  ¿La población de la que salen sus datos es la misma en la que se
    aplicará el modelo?

Si alguna respuesta es incómoda, **eso es el hallazgo**, y va en el
diseño experimental o en las limitaciones.

### 5.2 Qué mirar en el cuaderno

`clase07_fuga_de_informacion.ipynb` es el más incómodo del módulo y el
más breve de explicar.

Genera **50 casos y 5 000 atributos completamente aleatorios**, con una
etiqueta que es una moneda. No hay ninguna señal: el acierto verdadero
es 0,5 por construcción. Después aplica dos procedimientos que difieren
en **una línea de código**:

| Procedimiento                                   | Mediana sobre 40 réplicas |
|-------------------------------------------------|---------------------------|
| Selección de atributos **antes** de particionar | **1,000**                 |
| Selección **dentro** de cada pliegue            | 0,540                     |

Acierto perfecto sobre ruido puro, y en **40 de 40 réplicas** el
procedimiento con fuga supera el 0,75.

La razón es simple: con 5 000 atributos aleatorios, algunos se parecen a
la etiqueta por azar. La selección los encuentra —es su trabajo— y al
hacerlo mira las etiquetas de los casos que después harán de validación.
Ese pliegue dejó de ser información nueva.

**Ningún revisor puede detectar esto leyendo los resultados.** Solo
mirando el orden de las operaciones en el código. Por eso los talleres
de este módulo se corrigen sobre el cuaderno y no sobre el informe.

## 6. Lecturas

**Del seminario de esta semana**

> Kapoor, S., & Narayanan, A. (2023). Leakage and the reproducibility
> crisis in machine-learning-based science. *Patterns*, 4(9), 100804.
>
> Demšar, J. (2006). Statistical comparisons of classifiers over
> multiple data sets. *JMLR*, 7, 1–30.

El segundo es el contenido de la semana 8; conviene llegar con él leído.

**De reserva, pertinente esta semana**

> Bouthillier, X., et al. (2021). Accounting for variance in machine
> learning benchmarks. *MLSys*. Cuantifica cuánto subestima la
> variabilidad real la desviación entre pliegues.

## 7. Preguntas de comprobación

1.  ¿Por qué la desviación entre pliegues de una validación cruzada no
    es un intervalo de confianza?
2.  ¿Qué estima el bucle externo de una validación anidada? ¿Por qué no
    es el riesgo de un modelo?
3.  Escaló sus atributos antes de particionar. ¿Qué información se
    filtró, y por qué el código no da ningún error?
4.  Sus datos son mediciones mensuales de 400 bombas durante tres años.
    ¿Qué partición usa, y por qué la aleatoria es inválida?
5.  En el cuaderno, ¿por qué el procedimiento con fuga alcanza acierto
    perfecto y no simplemente «alto»?
6.  Recorra la taxonomía sobre su propio trabajo. ¿Cuál de las cinco
    categorías es la más probable en su caso?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase07_validacion_y_fuga.*` | Las 17 láminas de la clase |
| `codigo/clase07_fuga_de_informacion.ipynb` | Acierto perfecto sobre ruido puro, y cómo evitarlo |
| `guia/guia07.md` | Esta guía |

## 9. La próxima semana

**Semana 8 · Comparación estadística de algoritmos.** Wilcoxon,
Friedman, comparaciones múltiples y tamaño del efecto. Es lo que falta
para poder decir «mejor» con respaldo, que es la pregunta abierta desde
la semana 2.

**Taller 4**: comparación estadística de tres algoritmos sobre varios
conjuntos de datos.
