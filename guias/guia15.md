# Semana 15 · Equidad, reporte y cierre del módulo


- [1. De qué trata esta semana](#1-de-qué-trata-esta-semana)
- [2. Qué debería poder hacer al terminar la
  semana](#2-qué-debería-poder-hacer-al-terminar-la-semana)
- [3. La sesión sincrónica](#3-la-sesión-sincrónica)
- [4. Notación y definiciones](#4-notación-y-definiciones)
- [5. Trabajo autónomo de la semana](#5-trabajo-autónomo-de-la-semana)
- [6. Lecturas](#6-lecturas)
- [7. Preguntas de comprobación](#7-preguntas-de-comprobación)
- [8. Materiales de esta semana](#8-materiales-de-esta-semana)
- [9. Y después](#9-y-después)

> **Cómo usar esta guía.** Dice qué pasa en la sesión sincrónica, qué
> tiene que hacer usted por su cuenta, cuánto tiempo tomar cada cosa y
> con qué se corrige.

|  |  |
|----|----|
| **Unidad** | 7 · Investigación reproducible y comunicación de resultados |
| **Sesión de clase** | Sesgo y equidad · reporte, reproducibilidad y cierre |
| **Actividad** | Ninguna |
| **Hito calificado** | **Informe final del proyecto** — 40 % del módulo |
| **Trabajo sincrónico** | 2 hp de clase |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

La primera parte, **equidad**, no es un apéndice ético: es la misma
pregunta de la semana 1 hecha por subgrupos. Si un promedio sobre una
población heterogénea no describe a ninguno de sus subgrupos —lo dijimos
con el acierto en la semana 6 y con la cobertura conforme en la 14—
entonces el módulo entero venía apuntando aquí.

Y hay un resultado duro: **las definiciones de equidad son incompatibles
entre sí por un teorema**, no por falta de técnica.

La segunda parte cierra el módulo con cómo se comunica un resultado que
se sostenga, y con el arco completo de las quince semanas.

## 2. Qué debería poder hacer al terminar la semana

1.  Nombrar los cinco orígenes del sesgo, y explicar por qué el
    algoritmo casi nunca es uno de ellos.
2.  Explicar por qué quitar el atributo de grupo es peor que inútil.
3.  Enunciar paridad demográfica, igualdad de oportunidades y
    calibración por grupo, y decir cuándo corresponde cada una.
4.  Explicar el teorema de imposibilidad y su aritmética.
5.  Distinguir reproducible, replicable y generalizable.
6.  Escribir conclusiones proporcionales a la evidencia.

## 3. La sesión sincrónica

| Bloque                             | Duración | Material               |
|------------------------------------|----------|------------------------|
| Sesgo y equidad                    | 50 min   | `clase15a`, 17 láminas |
| Reporte, reproducibilidad y cierre | 50 min   | `clase15b`, 17 láminas |

## 4. Notación y definiciones

**Los cinco orígenes del sesgo**: histórico, de representación, **de
medición**, de agregación y de despliegue. El algoritmo casi nunca es el
origen: es el amplificador.

**Las tres definiciones**, con $A$ el atributo de grupo:

$$\underbrace{\Pr(\hat y=1\mid A=a)}_{\text{paridad demográfica}}
\qquad
\underbrace{\Pr(\hat y=1\mid y=1, A=a)}_{\text{igualdad de oportunidades}}
\qquad
\underbrace{\Pr(y=1\mid \hat p=q, A=a)=q}_{\text{calibración por grupo}}$$

**La identidad de Chouldechova**, que produce la imposibilidad:

$$\text{TFP} \;=\; \frac{\pi}{1-\pi}\cdot\frac{1-\text{VPP}}{\text{VPP}}\cdot\text{TVP}$$

Con VPP fijado por la calibración y prevalencia $\pi$ distinta entre
grupos, **TVP y TFP no pueden igualarse a la vez**. La razón forzada
entre las dos tasas de falsos positivos es

$$\frac{\pi_A/(1-\pi_A)}{\pi_B/(1-\pi_B)}$$

y **no depende del modelo ni del umbral**. Solo hay dos escapes:
predicción perfecta, o prevalencias iguales.

**Los tres niveles**: reproducible (mismos datos y código, mismo
resultado), replicable (datos nuevos, misma conclusión) y generalizable
(otra población, misma conclusión).

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | **Terminar y entregar el informe final** | 4,5 h | Informe | **Esta semana** |
| 2 | Añadir el desempeño desagregado por grupos | 1,0 h | Tabla del informe | Con el informe |
| 3 | Preparar la defensa oral | 1,0 h | — | Semana de exámenes |

### 5.1 El informe final

**40 % del módulo.** Se corrige con una rúbrica de cinco criterios:
formulación del problema como tarea de aprendizaje, pertinencia de la
elección metodológica, corrección del diseño experimental, sustento de
las conclusiones en la evidencia, y calidad del reporte.

La estructura, con la semana de la que sale cada sección:

| Sección | Qué contiene | Semana |
|----|----|----|
| **Problema** | La tarea de aprendizaje, qué es un caso, qué se predice | 1 |
| **Datos** | Origen, población, representación, faltantes | 1, 9 |
| **Método** | Familia, sesgo inductivo declarado, regularización | 2, 4, 5 |
| **Protocolo** | Partición justificada, sin fuga, con presupuesto | 7, 8, 12 |
| **Resultados** | Métrica justificada, con variabilidad y desagregada | 3, 6, 15 |
| **Limitaciones** | Alcance, horizonte de validez, qué lo invalidaría | 2, 14 |

**La sección de limitaciones es la que un revisor experto lee primero**,
y la que casi todos escriben al final y con desgana. Debe decir bajo qué
condiciones su conclusión dejaría de valer. «Se necesitan más datos» no
es una limitación: es relleno.

Y las cinco reglas para reportar números, cada una de una semana
distinta: con variabilidad y diciendo sobre qué se calculó; con el
tamaño del efecto en las unidades del problema; desagregados por grupo
con sus tamaños; con la línea base ajustada con el mismo cuidado; y con
el presupuesto de cómputo por método.

### 5.2 Qué mirar en el cuaderno

`clase15_imposibilidad_equidad.ipynb` verifica el teorema de dos
maneras.

**Primero sin entrenar nada**, evaluando la identidad de Chouldechova:
con prevalencias de 0,30 y 0,10, la razón forzada entre las tasas de
falsos positivos es **3,86**, y es la misma para cualquier VPP y
cualquier TVP. No depende del modelo.

**Después con un modelo real**, en el caso **más favorable posible**:
los dos grupos tienen la misma relación entre atributos y etiqueta, el
grupo no se usa como predictor, y el modelo discrimina igual de bien en
ambos (AUC 0,839 y 0,846). Solo difieren las tasas base.

| Estrategia de umbral      | Iguala        | Δ del valor predictivo positivo |
|---------------------------|---------------|---------------------------------|
| Umbral único              | TVP y TFP     | **0,32**                        |
| Paridad demográfica       | tasa positiva | **0,41**                        |
| Igualdad de oportunidades | TVP           | **0,32**                        |

Un aviso positivo significa una probabilidad del **66 % en un grupo y
del 34 % en el otro**, con las tres estrategias. Ninguna lo corrige,
porque la identidad lo prohíbe.

Se pueden igualar las probabilidades condicionadas a la clase, **o** se
puede igualar lo que significa un aviso. No ambas. Y esa elección es
normativa, no técnica.

## 6. Lecturas

> Chouldechova, A. (2017). Fair prediction with disparate impact. *Big
> Data*, 5(2), 153–163.
>
> Kleinberg, J., Mullainathan, S., & Raghavan, M. (2016). Inherent
> trade-offs in the fair determination of risk scores. *ITCS*.

Los dos artículos del teorema. El primero es más accesible.

> Mitchell, M., et al. (2019). Model cards for model reporting. *FAccT*.
> Una plantilla de reporte que vale la pena conocer.

## 7. Preguntas de comprobación

1.  Su etiqueta es «se registró una falla». ¿Qué está midiendo realmente
    el modelo?
2.  Quitó el atributo de grupo del conjunto de datos. ¿Qué consiguió y
    qué perdió?
3.  Enuncie las tres definiciones de equidad. ¿Cuál corresponde a su
    problema?
4.  ¿Por qué la razón entre las TFP no depende del modelo?
5.  ¿Qué diferencia hay entre reproducible, replicable y generalizable?
    ¿Cuál afirma su tesis?
6.  Escriba la sección de limitaciones de su proyecto en cinco líneas.
    ¿Bajo qué condiciones deja de valer su conclusión?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase15a_equidad.*` | Orígenes del sesgo, definiciones, imposibilidad |
| `slides/clase15b_reporte.*` | Reproducibilidad, estructura del informe y cierre |
| `codigo/clase15_imposibilidad_equidad.ipynb` | El teorema, verificado |
| `guia/guia15.md` | Esta guía |

## 9. Y después

**Semana de exámenes: defensa oral del proyecto ante el curso.** 20 %
del módulo.

Se califica **la capacidad de sostener las decisiones metodológicas bajo
interrogación** —no la presentación ni los resultados. Preguntan el
profesor y los pares.

Se le va a preguntar por qué eligió cada cosa y qué habría pasado si
hubiera elegido otra. **«No lo sé» es una respuesta aceptable; «no lo
pensé» es la que cuesta.**
