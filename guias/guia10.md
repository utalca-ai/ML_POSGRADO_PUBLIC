# Semana 10 · Agrupamiento y el problema de su validación


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
| **Unidad** | 4 · Representación, dimensionalidad y aprendizaje no supervisado |
| **Sesión de clase** | Agrupamiento · validación sin etiquetas · anomalías |
| **Actividad** | **Taller 5** (2 hp) |
| **Hito calificado** | **Entrega del taller 5** |
| **Trabajo sincrónico** | 4 hp: 2 de clase + 2 de taller |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Nueve semanas de aprendizaje supervisado. Todo el aparato —riesgo,
validación, métricas, comparación estadística— descansaba en tener $y$.

Esta semana se quitan las etiquetas y **casi nada de eso sobrevive**. No
hay riesgo que estimar, no hay conjunto de prueba que gastar, y no hay
forma directa de decir que un resultado es correcto. Y sin embargo hay
que decidir: cuántos grupos, con qué algoritmo, con qué distancia. Todas
siguen siendo decisiones de sesgo inductivo; solo que ahora nada las
verifica.

## 2. Qué debería poder hacer al terminar la semana

1.  Explicar por qué no existe una definición de «grupo» independiente
    del algoritmo.
2.  Enunciar los supuestos de $k$-medias, del enlace jerárquico y de
    DBSCAN.
3.  Justificar la distancia elegida como decisión de modelado.
4.  Explicar por qué un índice interno **no** puede responder «¿hay
    grupos?».
5.  Construir una referencia nula y usarla para decidir si hay
    estructura.
6.  Distinguir detección de anomalías de clasificación desbalanceada.

## 3. La sesión sincrónica

| Bloque | Duración | Material |
|----|----|----|
| Agrupamiento: tres algoritmos, tres supuestos | 50 min | `clase10a`, 15 láminas |
| Validar sin etiquetas · anomalías | 50 min | `clase10b`, 17 láminas |
| **Taller 5** | 2 hp aparte | Validación de agrupamientos |

## 4. Notación y definiciones

**$k$-medias** minimiza la dispersión dentro de los grupos:

$$\min_{C_1,\ldots,C_k}\;\sum_{j=1}^{k}\sum_{x\in C_j}\lVert x-\mu_j\rVert^2$$

y con ello supone grupos **esféricos, de tamaño similar y de varianza
similar**, con $k$ conocido. Converge a un óptimo local: hacen falta
varios reinicios.

**Silueta**, con $a(i)$ la distancia media al propio grupo y $b(i)$ al
grupo vecino más cercano:

$$s(i)=\frac{b(i)-a(i)}{\max\{a(i),\,b(i)\}}\in[-1,1]$$

**Dimensión alta.** La distancia entre el punto más cercano y el más
lejano tiende a igualarse:

$$\frac{d_{\max}-d_{\min}}{d_{\min}}\longrightarrow 0
\qquad\text{cuando } p\to\infty$$

Si todos los puntos están a la misma distancia de todos, la noción de
vecindad se vacía.

**Estadística de brecha**, comparando contra datos sin estructura:

$$\text{Brecha}(k)=\mathbb{E}_{\text{nulo}}\bigl[\log W_k\bigr]-\log W_k$$

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Leer Grinsztajn, Oyallon y Varoquaux (2022) — **obligatoria** | 2,0 h | Notas | Antes de la reseña |
| 2 | Escribir la **reseña 4** | 2,0 h | 2 páginas | **48 h antes de la semana 11** |
| 3 | Completar y entregar el **taller 5** | 1,5 h | Cuaderno + bitácora | Fin de semana 10 |
| 4 | Ejecutar y estudiar el cuaderno de la clase | 1,0 h | Cuaderno corrido | Antes de la semana 11 |

### 5.1 El taller 5

**Validación de agrupamientos: por qué el índice interno no zanja la
discusión.**

Además de los ocho ítems, se corrige que el trabajo **no se quede en el
índice interno**. La jerarquía de evidencia, de más a menos convincente:

1.  **Utilidad para una tarea posterior** — los grupos mejoran una
    decisión medible.
2.  **Validación externa** — corresponden a algo que **no se usó** para
    construirlos.
3.  **Referencia nula** — hay más estructura que en datos permutados.
4.  **Estabilidad** — solo refuta: baja refuta, alta no confirma.
5.  **Índice interno solo** — no distingue nada.

Si su trabajo llega solo al nivel 5, la conclusión debe ser
proporcionalmente modesta. Eso también se corrige.

### 5.2 Qué mirar en el cuaderno

`clase10_validacion_de_agrupamientos.ipynb` compara dos conjuntos con el
mismo número de puntos y el mismo rango: uno con cuatro grupos
gaussianos y otro **uniforme, sin ninguna estructura**.

| Método | ¿Separa los dos casos? |
|----|----|
| Silueta sola | **No.** Da un máximo en ambos |
| Silueta frente a referencia nula | **Sí**: 0,737 \> 0,414 frente a 0,441 ≤ 0,467 |
| Estabilidad | **No.** Ambos son estables |

**Los dos resultados negativos son el contenido.** El primero es el
esperado: el índice no avisa de que no hay nada.

El segundo **no lo era**, y conviene leerlo con cuidado. Al escribir el
cuaderno se esperaba que la estabilidad separase los casos, y no lo
hace: sobre un rectángulo uniforme, $k$-medias con $k=2$ siempre parte
por la mitad del lado más largo, así que es perfectamente estable sin
que haya ningún grupo. Se comprobó en todo el rango de $k$ antes de
afirmarlo.

La lección: **la estabilidad mide si la solución del algoritmo se
reproduce, no si hay estructura en los datos.** Es un resultado conocido
—Ben-David, von Luxburg y Pál (2006)— y contradice el uso habitual de la
estabilidad como evidencia de existencia.

El cuaderno conserva ese resultado negativo y la corrección de la
expectativa inicial en su bitácora, porque suprimirlo sería exactamente
el sesgo que este módulo enseña a evitar.

## 6. Lecturas

**Obligatoria — seminario 4, semana 11**

> Grinsztajn, L., Oyallon, E., & Varoquaux, G. (2022). Why do tree-based
> models still outperform deep learning on typical tabular data?
> *NeurIPS Datasets and Benchmarks Track*.

Al leerla, busque los tres complementos de la semana 2: qué clase de
problemas, qué pérdida, qué evidencia. Y fíjese especialmente en cómo
tratan el **presupuesto de ajuste de hiperparámetros**, que es lo que
hace válida o inválida la comparación (semana 8).

**De apoyo a la clase**

> Hastie, Tibshirani y Friedman (2009), §14.3.
>
> Ben-David, S., von Luxburg, U., & Pál, D. (2006). A sober look at
> clustering stability. *COLT*. El resultado que el cuaderno reproduce
> sin querer.

## 7. Preguntas de comprobación

1.  ¿Por qué $k$-medias tiende a partir un grupo grande y a fusionar dos
    pequeños?
2.  Su silueta media es 0,42. ¿Qué concluye? ¿Y qué necesitaría para
    concluir algo?
3.  ¿Por qué comparar algoritmos de agrupamiento por silueta favorece a
    $k$-medias?
4.  Un colega dice: «mis grupos son estables en submuestras, luego son
    reales». ¿Dónde está el error?
5.  ¿Cómo construiría una referencia nula para **sus** datos? ¿Uniforme
    o por permutación de columnas, y por qué?
6.  Tiene 200 fallas etiquetadas de un tipo conocido. ¿Detección de
    anomalías o clasificación?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase10a_agrupamiento.*` | Tres algoritmos, tres definiciones de grupo |
| `slides/clase10b_validacion.*` | Validar sin etiquetas · anomalías |
| `codigo/clase10_validacion_de_agrupamientos.ipynb` | Con grupos frente a uniforme |
| `guia/guia10.md` | Esta guía |

## 9. La próxima semana

**Semana 11 · Perceptrón multicapa y retropropagación.** Optimización
estocástica, regularización y dinámica de entrenamiento.

**Seminario 4**: Grinsztajn et al. (2022). **Reseña 4**, 48 horas antes.
