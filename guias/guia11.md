# Semana 11 · Perceptrón multicapa y retropropagación


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
| **Sesión de clase** | MLP, retropropagación, optimización estocástica y regularización |
| **Actividad** | **Seminario 4** — Grinsztajn, Oyallon y Varoquaux (2022) |
| **Hito calificado** | **Reseña 4**, 48 h antes de la sesión |
| **Trabajo sincrónico** | 2 hp: 1 de clase + 1 de seminario |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

La clase se abre con una afirmación que conviene tomar en serio: **nada
de lo anterior deja de valer**. Una red es una familia $\mathcal{H}$
más, con su sesgo inductivo, su capacidad y su compromiso
sesgo-varianza. Se entrena minimizando riesgo empírico regularizado, su
pérdida sale de una verosimilitud, se evalúa con los mismos protocolos y
se compara con las mismas pruebas.

Lo específico es **cuál** es su sesgo inductivo —suavidad y composición
jerárquica—, y de ahí sale la pregunta del seminario: en qué problemas
ese supuesto vale y en cuáles no.

## 2. Qué debería poder hacer al terminar la semana

1.  Explicar por qué sin no linealidad la profundidad es decorativa.
2.  Decir qué afirma y qué **no** afirma el teorema de aproximación
    universal.
3.  Distinguir retropropagación (calcular el gradiente) de optimización
    (aprender).
4.  Explicar por qué el ruido del descenso estocástico es
    **regularización implícita**, y en qué lugar del sesgo inductivo de
    la semana 2 encaja.
5.  Diagnosticar una curva de aprendizaje.
6.  Argumentar cuándo un ensamble es preferible a una red en datos
    tabulares.

## 3. La sesión sincrónica

**Semana de seminario**: una hora de clase y una de discusión.

| Bloque          | Duración | Material                               |
|-----------------|----------|----------------------------------------|
| Clase           | 50 min   | `clase11`, 18 láminas                  |
| **Seminario 4** | 50 min   | Grinsztajn, Oyallon y Varoquaux (2022) |

## 4. Notación y definiciones

**Una capa**: transformación afín más no linealidad.

$$h^{(l)}=\sigma\bigl(W^{(l)}h^{(l-1)}+b^{(l)}\bigr)$$

Sin $\sigma$, componer capas da otra transformación afín y **toda la red
colapsa a una regresión lineal**.

**Retropropagación**: la regla de la cadena, organizada para reutilizar
cálculos.

$$\frac{\partial \mathcal{L}}{\partial W^{(l)}}
=\frac{\partial \mathcal{L}}{\partial h^{(l)}}\cdot\frac{\partial h^{(l)}}{\partial W^{(l)}}$$

No es un algoritmo de aprendizaje: es un método eficiente de derivar.

**Descenso estocástico**:

$$\theta_{t+1}=\theta_t-\eta\,\nabla_\theta \mathcal{L}_{\text{lote}}(\theta_t)$$

El ruido del muestreo sesga la solución hacia mínimos anchos. Ese sesgo
del optimizador es el **tercer lugar** del sesgo inductivo de la semana
2.

**Aproximación universal.** Una red con una capa oculta y suficientes
unidades aproxima cualquier función continua en un compacto. Dice que
**existe** tal red; no dice cuántas unidades, ni que se pueda encontrar,
ni nada sobre generalización. Es el término de **aproximación** de la
semana 1, y solo ese.

**Regularización**: decaimiento de pesos es $L_2$ de la semana 4;
abandono se aproxima a un ensamble de la semana 5; **detención temprana
es un hiperparámetro de capacidad** —y el conjunto con que se decide
cuándo parar queda gastado.

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Ejecutar y estudiar el cuaderno de la clase | 1,5 h | Cuaderno corrido | Antes de la semana 12 |
| 2 | Leer Hastie et al., cap. 11 | 2,0 h | Notas | Antes de la semana 12 |
| 3 | **Avanzar en el proyecto**: primeros resultados según el diseño | 2,5 h | Resultados preliminares | **Tutoría 3, semana 13** |
| 4 | Preparar el taller 6 | 0,5 h | — | Semana 12 |

### 5.1 Qué mirar en el cuaderno

`clase11_redes_frente_a_arboles.ipynb` reproduce en pequeño el
experimento del seminario, con **el mismo presupuesto de ajuste para
ambas familias** —12 configuraciones cada una, que es la condición que
hace válida la comparación (semana 8).

| Objetivo                             | Red (MLP) | Potenciación de árboles |
|--------------------------------------|-----------|-------------------------|
| **Suave** (senos y productos)        | **0,824** | 0,795                   |
| **A trozos** (umbrales de operación) | 0,793     | **0,822**               |
| A trozos, **+20 atributos ruidosos** | **0,743** | **0,822**               |

Las tres filas reproducen las dos tesis del artículo:

1.  **La forma del objetivo decide.** La red gana cuando la función es
    suave y pierde cuando es a trozos. No es que una familia sea mejor:
    es que el sesgo inductivo calza o no calza.
2.  **Los atributos ruidosos dañan a la red y no a los árboles.** Al
    añadir 20 columnas de ruido, la red cae 0,050 y el ensamble **no se
    mueve**. Es la segunda razón que da el artículo.

Y una advertencia que el propio cuaderno declara: **cinco réplicas y
datos simulados no son un estudio concluyente.** El artículo usa decenas
de conjuntos reales y el procedimiento de Demšar. El cuaderno renuncia a
reproducir el resultado y opta por **aislar el mecanismo**, que es lo
que la clase necesita.

## 6. Lecturas

**Del seminario de esta semana**

> Grinsztajn, L., Oyallon, E., & Varoquaux, G. (2022). Why do tree-based
> models still outperform deep learning on typical tabular data?
> *NeurIPS Datasets and Benchmarks Track*.

Sus tres razones son sesgo inductivo puro: las redes están sesgadas
hacia funciones suaves; los atributos poco informativos les dañan más; y
no son invariantes a la rotación, lo que en datos tabulares es una
desventaja.

El tercer punto es el menos intuitivo y el más interesante para
discutir: en imágenes la invarianza a rotación es deseable, pero en una
tabla las columnas tienen significado individual y mezclarlas destruye
información.

**De apoyo a la clase**

> Hastie, Tibshirani y Friedman (2009), cap. 11.
>
> Bishop y Bishop (2024), *Deep Learning: Foundations and Concepts*,
> caps. 6–7.
>
> Guo, C., et al. (2017). On calibration of modern neural networks.
> Pertinente si su proyecto usa redes: la descalibración **crece con la
> capacidad**.

## 7. Preguntas de comprobación

1.  ¿Qué pasa si quita todas las activaciones de una red de cinco capas?
2.  El teorema de aproximación universal, ¿le garantiza que su red
    generalizará?
3.  ¿En qué se distingue retropropagación de descenso de gradiente?
4.  ¿Por qué el ruido del descenso estocástico ayuda, y de qué semana es
    esa idea?
5.  Sus curvas de entrenamiento y validación no bajan. ¿Qué revisa
    primero?
6.  Usó detención temprana con un conjunto de validación. ¿Puede
    reportar el error sobre ese mismo conjunto? ¿Por qué?
7.  Su problema es tabular, con umbrales de operación y 40 atributos de
    los que pocos importan. ¿Red o ensamble? Justifique con el sesgo
    inductivo.

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase11_redes.*` | Las 18 láminas de la clase |
| `codigo/clase11_redes_frente_a_arboles.ipynb` | El experimento con presupuesto igual |
| `guia/guia11.md` | Esta guía |

## 9. La próxima semana

**Semana 12 · Transferencia y ajuste fino.** Criterios para decidir
cuándo un modelo profundo es preferible a un ensamble. Costo
computacional y energético.

**Taller 6**: modelo profundo frente a ensamble sobre el mismo problema,
**con presupuesto de cómputo declarado**. Es el taller que ejercita todo
lo de esta semana y de la 8.
