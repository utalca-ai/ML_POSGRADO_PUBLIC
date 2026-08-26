# Semana 12 · Transferencia y el costo como criterio


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
| **Unidad** | 5 · Fundamentos operativos del aprendizaje profundo |
| **Sesión de clase** | Transferencia y ajuste fino · el costo como criterio |
| **Actividad** | **Taller 6** (2 hp) |
| **Hito calificado** | **Entrega del taller 6** —el último |
| **Trabajo sincrónico** | 4 hp: 2 de clase + 2 de taller |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Dos temas que en la práctica van juntos.

El primero es la **transferencia**: reutilizar lo aprendido en una tarea
con muchos datos para resolver otra con pocos. Como todo en este módulo,
descansa en un supuesto —que ambas tareas comparten estructura— y cuando
el supuesto falla no solo no ayuda: **perjudica**.

El segundo es el **costo**, que hemos ignorado durante once semanas. No
es un detalle de implementación: es parte de la afirmación. Un método
que gana con cien veces más cómputo no ha ganado en el mismo sentido.

## 2. Qué debería poder hacer al terminar la semana

1.  Distinguir transferencia, ajuste fino y extracción de
    características.
2.  Elegir la estrategia según cuántos datos tiene y cuánto se parecen
    los dominios.
3.  Reconocer la **transferencia negativa**, y saber que solo una línea
    base entrenada desde cero la detecta.
4.  Nombrar los cuatro tipos de costo y cuál domina en cada horizonte.
5.  Declarar un presupuesto de cómputo en unidades verificables.
6.  Construir y leer una **frontera de Pareto** de desempeño frente a
    costo.

## 3. La sesión sincrónica

| Bloque | Duración | Material |
|----|----|----|
| Transferencia y ajuste fino | 50 min | `clase12a`, 17 láminas |
| El costo como criterio | 50 min | `clase12b`, 17 láminas |
| **Taller 6** | 2 hp aparte | Profundo frente a ensamble, con presupuesto declarado |

## 4. Notación y definiciones

**Transferencia.** Con dominio $\mathcal{D}=\{\mathcal{X}, P(X)\}$ y
tarea $\mathcal{T}=\{\mathcal{Y}, f\}$, hay transferencia cuando

$$\mathcal{D}_{\text{origen}}\neq\mathcal{D}_{\text{destino}}
\qquad\text{o}\qquad
\mathcal{T}_{\text{origen}}\neq\mathcal{T}_{\text{destino}}$$

**Las tres estrategias**, ordenadas por cuántos datos propios exigen:
extracción de características (congelar y usar las activaciones), ajuste
fino parcial (descongelar las últimas capas), ajuste fino total.

|  | Dominio parecido | Dominio distinto |
|----|----|----|
| **Pocos datos** | Extracción de características | **Situación difícil** |
| **Muchos datos** | Ajuste fino parcial | Ajuste fino total o desde cero |

**Los cuatro costos**: desarrollo (el mayor y el menos reportado),
entrenamiento final (el único que suele aparecer), **inferencia** (el
que domina a lo largo de la vida del sistema) y mantenimiento.

**Costo energético**:

$$E \approx P \times t \times \text{PUE},
\qquad
\text{CO}_2 = E \times I$$

La intensidad de carbono $I$ varía por país en más de un orden de
magnitud, así que lo que se declara son **unidades físicas
verificables** —kWh, horas de GPU— y no una estimación de CO₂ sin
contexto.

**Dominancia de Pareto.** $A$ domina a $B$ si no es peor en ningún eje y
es mejor en al menos uno. Las configuraciones no dominadas forman la
**frontera**, y entre ellas la elección la hace el problema, no el
método.

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Leer Rudin (2019) y Lundberg y Lee (2017) — **obligatorias** | 2,5 h | Notas | Antes de la reseña |
| 2 | Escribir la **reseña 5** —la última | 2,0 h | 2 páginas | **48 h antes de la semana 13** |
| 3 | Completar y entregar el **taller 6** | 1,5 h | Cuaderno + bitácora | Fin de semana 12 |
| 4 | Preparar resultados preliminares del proyecto | 0,5 h | — | **Tutoría 3, semana 13** |

### 5.1 El taller 6

**Modelo profundo frente a ensamble sobre el mismo problema, con
presupuesto de cómputo declarado.**

Es el último taller y el que integra la unidad 3 con la 5. Además de los
ocho ítems, se corrige:

- Que el **presupuesto sea idéntico** para ambos métodos, declarado en
  número de configuraciones y en tiempo, con el hardware especificado.
- Que haya una **línea base simple** ajustada con el mismo cuidado —una
  regresión regularizada o una potenciación por defecto.
- Que se presente la **frontera de desempeño frente a costo**, y que la
  elección se justifique sobre ella.
- Que se reporte el **costo de inferencia**, no solo el de
  entrenamiento.

### 5.2 Qué mirar en el cuaderno

`clase12_desempeno_frente_a_costo.ipynb` compara siete configuraciones
—desde una regresión logística hasta una red— midiendo AUC, tiempo de
entrenamiento y tiempo de inferencia, y construye **dos** fronteras de
Pareto.

El resultado que importa: **las dos fronteras no coinciden.**

| Frontera                       | Configuraciones no dominadas |
|--------------------------------|------------------------------|
| Por costo de **entrenamiento** | $k$-NN, Red                  |
| Por costo de **inferencia**    | Logística, Red               |

$k$-NN es el ejemplo perfecto de por qué hay que separar los dos ejes:
**no entrena** —su costo de ajuste es cero— y su inferencia cuesta 15,7
ms por mil casos, unas 80 veces más que una logística. Si su sistema va
a predecir durante cinco años, la frontera que decide es la segunda.

Y el costo marginal, que es la pregunta del taller: la mejor
configuración gana **+0,113 de AUC** sobre la línea base, a cambio de
**80×** el tiempo de entrenamiento y **2,8×** el de inferencia. Si la
ganancia hubiera sido de 0,004, la conclusión sería la contraria.

**Una advertencia que el cuaderno declara**: los tiempos medidos no son
una propiedad del algoritmo. Dependen del hardware, de la implementación
y de la carga de la máquina. Lo transferible son las **razones** entre
métodos y la forma de la frontera, no los valores absolutos.

## 6. Lecturas

**Obligatorias — seminario 5, semana 13**

> Rudin, C. (2019). Stop explaining black box machine learning models
> for high stakes decisions and use interpretable models instead.
> *Nature Machine Intelligence*, 1, 206–215.
>
> Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to
> interpreting model predictions. *NeurIPS*, 30.

Se leen **juntas y en tensión**: la segunda propone el método que la
primera argumenta que no deberíamos necesitar. Es el mejor par de
artículos del semestre para el rol de discutidor.

**De reserva, pertinente esta semana**

> Sculley, D., et al. (2015). Hidden technical debt in machine learning
> systems. *NeurIPS*. Sobre el costo de mantenimiento, que es el que
> nadie presupuesta.

## 7. Preguntas de comprobación

1.  ¿En qué se distingue el ajuste fino de la extracción de
    características, y cuál elige con 300 casos propios?
2.  ¿Qué es la transferencia negativa y cómo la detectaría?
3.  ¿Por qué la transferencia funciona mal entre tablas distintas?
4.  De los cuatro costos, ¿cuál domina la huella total de un sistema que
    opera cinco años?
5.  Un método gana 0,004 de AUC con 40× más cómputo. ¿Qué reporta, y qué
    concluye?
6.  ¿Por qué la frontera por costo de entrenamiento y la de inferencia
    pueden ordenar los métodos de forma distinta?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase12a_transferencia.*` | Transferencia, ajuste fino y transferencia negativa |
| `slides/clase12b_costo.*` | Los cuatro costos, energía y la frontera de Pareto |
| `codigo/clase12_desempeno_frente_a_costo.ipynb` | Las dos fronteras |
| `guia/guia12.md` | Esta guía |

## 9. La próxima semana

**Semana 13 · Interpretabilidad.** Modelos transparentes frente a
explicaciones *post hoc*. LIME y SHAP, y las objeciones a su uso en
decisiones de alto riesgo.

**Seminario 5** —el último—: Rudin (2019) y Lundberg y Lee (2017).
**Tutoría 3**: revisión de resultados preliminares del proyecto.
