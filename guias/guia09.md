# Semana 9 · Representación y reducción de dimensionalidad


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
| **Sesión de clase** | Ingeniería de atributos · PCA y reducción de dimensionalidad |
| **Actividad** | **Tutoría 2** (individual) |
| **Hito** | **Diseño experimental del proyecto** (formativo, obligatorio, sin nota) |
| **Trabajo sincrónico** | 2 hp de clase + 2 hp de tutoría |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Ocho semanas escribiendo $h:\mathcal{X}\to\mathcal{Y}$ como si
$\mathcal{X}$ viniera dado. No viene dado: **definirlo es la primera
decisión modeladora**, y en una tesis de ingeniería suele importar más
que la elección del algoritmo.

La primera parte trata la construcción, transformación y selección de
atributos, y por qué todo lo que mira la etiqueta es entrenamiento. La
segunda trata la extracción —PCA— y su supuesto más peligroso: que
varianza sea lo mismo que información.

## 2. Qué debería poder hacer al terminar la semana

1.  Justificar su representación como decisión modeladora, no como
    preprocesamiento.
2.  Decidir qué transformaciones necesita su modelo y cuáles no.
3.  Distinguir qué pasos van dentro del pliegue y por qué.
4.  Explicar qué maximiza PCA, y por qué eso puede no tener relación con
    $y$.
5.  Tratar el número de componentes como hiperparámetro.

## 3. La sesión sincrónica

| Bloque                       | Duración         | Material               |
|------------------------------|------------------|------------------------|
| Ingeniería de atributos      | 50 min           | `clase09a`, 16 láminas |
| Reducción de dimensionalidad | 50 min           | `clase09b`, 17 láminas |
| **Tutoría 2**                | 2 hp, individual | Diseño experimental    |

## 4. Notación y definiciones

**La representación codifica la geometría.** Con «hora del día» como
número de 0 a 23, las 23:00 y las 00:00 quedan a 23 unidades de
distancia. La codificación
$(\sin\frac{2\pi t}{24},\ \cos\frac{2\pi t}{24})$ respeta la
circularidad. Lo mismo vale para ángulos, días de la semana y
direcciones.

**Qué necesita escalado.** Lineales regularizadas, $k$-NN, SVM con
kernel, agrupamiento y redes: **sí**. Árboles y ensambles de árboles:
**no**.

**Qué va dentro del pliegue.** Escalado, imputación, codificación por
objetivo, selección de atributos, PCA, remuestreo, hiperparámetros,
recalibración. En la práctica: use una tubería.

**PCA.** Busca las direcciones de máxima varianza de los datos
centrados:

$$w_1=\operatorname*{arg\,max}_{\lVert w\rVert=1}\;w^\top\Sigma\,w,
\qquad
\Sigma w_j=\lambda_j w_j,
\qquad
\text{var. explicada}_j=\frac{\lambda_j}{\sum_l \lambda_l}$$

**La etiqueta no aparece.** Esa es su virtud —no filtra información
sobre $y$— y su limitación: puede descartar la dirección que discrimina.

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | **Redactar el diseño experimental** de su proyecto | 3,0 h | Documento | **Tutoría 2, esta semana** |
| 2 | Ejecutar y estudiar el cuaderno de la clase | 1,5 h | Cuaderno corrido | Antes de la semana 10 |
| 3 | Revisar la representación de sus propios datos | 1,5 h | Media página | Con el diseño |
| 4 | Preparar el taller 5 | 0,5 h | — | Semana 10 |

### 5.1 El diseño experimental

Es el segundo hito formativo, y el que evita rehacer el trabajo en la
semana 15. Se entrega **antes de correr el primer experimento** —esa es
su razón de ser— y debe declarar:

1.  **La representación**: qué atributos, cómo construidos, con qué
    justificación del dominio.
2.  **El protocolo de partición**, justificado por la estructura de los
    datos. Si no son i.i.d., cuál de las particiones de la semana 7
    corresponde.
3.  **Qué se ajusta dentro del pliegue** y qué puede quedar fuera.
4.  **La métrica**, justificada por los costos del problema (semana 6),
    y el umbral si aplica.
5.  **La comparación**: contra qué referencia, sobre cuántos conjuntos,
    con qué prueba y qué corrección (semana 8).
6.  **El presupuesto de hiperparámetros**, igual para todos los métodos.
7.  **Qué resultado refutaría su hipótesis.** Si ninguno, no es una
    hipótesis.

### 5.2 Qué mirar en el cuaderno

`clase09_pca_y_varianza.ipynb` construye un banco de 20 sensores con un
**modo común** dominante —la carga del equipo, que no informa— y la
señal en el **desequilibrio** entre grupos de sensores.

|                              | Varianza explicada | Acierto   |
|------------------------------|--------------------|-----------|
| PCA, 1 componente            | **97,0 %**         | **0,535** |
| LDA, 1 componente (mira $y$) | —                  | **0,922** |
| Los 20 sensores originales   | 100 %              | 0,927     |

La primera componente explica el 97 % de la varianza, así que el
criterio del «90 % acumulado» se queda **exactamente con ella**, y el
resultado es una moneda. Con la **misma** dimensionalidad, el criterio
supervisado recupera casi todo.

Dos detalles que conviene no pasar por alto:

- **Todo eso ocurre estandarizando.** Estandarizar iguala la varianza de
  cada *columna*, no la de cada *dirección*. Son dos problemas distintos
  y solo uno lo arregla la estandarización.
- La **bitácora del cuaderno documenta un intento fallido**: una primera
  versión ponía la señal en columnas de baja varianza y no funcionaba,
  porque estandarizar borraba el orden fabricado. Está declarado a
  propósito: es exactamente el tipo de detalle que invalida un
  experimento sin que nadie lo note, y el ítem 7 de la lista de cotejo
  pide justamente eso.

## 6. Lecturas

> Hastie, Tibshirani y Friedman (2009), §14.5 (componentes principales)
> y cap. 3 sobre selección de atributos.
>
> Murphy (2022), cap. 20, para métodos no lineales de reducción.

Sin lectura obligatoria nueva: el seminario 4 es en la semana 11, y su
artículo —Grinsztajn et al. (2022)— conviene empezarlo la semana que
viene.

## 7. Preguntas de comprobación

1.  ¿Por qué codificar «hora del día» como un número de 0 a 23 es una
    decisión modeladora y no un formato?
2.  ¿Cuáles de sus pasos de preprocesamiento miran la etiqueta? Esos son
    entrenamiento.
3.  ¿Por qué la codificación por objetivo es tan propensa a la fuga?
4.  Sus datos tienen faltantes porque el sensor se satura en régimen
    extremo. ¿Qué hace, y por qué borrar esas filas sesga el estudio?
5.  ¿Por qué PC1 puede explicar el 97 % de la varianza y no servir para
    nada?
6.  ¿Por qué no se debe usar $t$-SNE como preprocesamiento de un modelo?

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase09a_atributos.*` | Construcción, transformación y selección |
| `slides/clase09b_pca.*` | PCA, sus supuestos y sus alternativas |
| `codigo/clase09_pca_y_varianza.ipynb` | El banco de sensores con modo común |
| `guia/guia09.md` | Esta guía |

## 9. La próxima semana

**Semana 10 · Agrupamiento y el problema de su validación.** Detección
de anomalías. Evaluación en ausencia de etiquetas —que es donde todo lo
que llevamos aprendido sobre evaluación deja de aplicarse tal cual.

**Taller 5**: validación de agrupamientos; por qué el índice interno no
zanja la discusión.
