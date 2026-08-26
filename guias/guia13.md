# Semana 13 · Interpretabilidad


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
| **Unidad** | 6 · Interpretabilidad, incertidumbre y confiabilidad |
| **Sesión de clase** | Modelos transparentes frente a explicaciones *post hoc* |
| **Actividad** | **Seminario 5** (el último) · **Tutoría 3** |
| **Hito calificado** | **Reseña 5**, 48 h antes de la sesión |
| **Trabajo sincrónico** | 2 hp de bloque común + 2 hp de tutoría |
| **Trabajo autónomo** | ≈ 6,5 horas cronológicas |

------------------------------------------------------------------------

## 1. De qué trata esta semana

Un modelo marca una bomba como próxima a fallar y alguien pregunta por
qué. Hay dos respuestas posibles —«el modelo es transparente y aquí está
la regla» o «un segundo método dice que estos atributos pesaron»— y la
diferencia entre ellas es el contenido de la clase.

El seminario enfrenta las dos posiciones: Lundberg y Lee proponen el
método que Rudin argumenta que no deberíamos necesitar.

## 2. Qué debería poder hacer al terminar la semana

1.  Separar los cuatro sentidos de «interpretable»: transparencia,
    explicación local, importancia global y contrafactual.
2.  Decir **para quién** es la interpretabilidad, porque depurar y
    justificar no son lo mismo.
3.  Explicar por qué la importancia por permutación engaña con atributos
    correlacionados.
4.  Enunciar qué garantizan los axiomas de SHAP y qué **no**.
5.  Explicar el conjunto Rashomon y qué implica para cualquier
    explicación.
6.  Reconstruir el argumento de Rudin en sus cuatro pasos, y sus
    réplicas.

## 3. La sesión sincrónica

**Semana de seminario**: una hora de clase y una de discusión. La
tutoría es individual y va fuera del bloque común.

| Bloque          | Duración         | Material                             |
|-----------------|------------------|--------------------------------------|
| Clase           | 50 min           | `clase13`, 18 láminas                |
| **Seminario 5** | 50 min           | Rudin (2019) · Lundberg y Lee (2017) |
| **Tutoría 3**   | 2 hp, individual | Resultados preliminares del proyecto |

## 4. Notación y definiciones

**Los cuatro sentidos.** Transparencia (seguir el cálculo), explicación
local (por qué este caso), importancia global (qué usa en general) y
contrafactual (qué habría que cambiar). Los métodos que se anuncian como
«interpretabilidad» responden a filas distintas.

**Importancia por permutación**: se permuta una columna y se mide el
deterioro.

$$I_j = R_{\text{permutado}(j)} - R_{\text{original}}$$

Con atributos correlacionados **engaña**: permutar uno no destruye la
información, que sigue en su correlacionado. Y genera puntos imposibles.

**Valores de Shapley (SHAP)**:

$$\phi_j=\sum_{S\subseteq F\setminus\{j\}}\frac{|S|!\,(|F|-|S|-1)!}{|F|!}\Bigl[f(S\cup\{j\})-f(S)\Bigr]$$

Es el **único** reparto que satisface eficiencia, simetría, nulidad y
aditividad. Pero los axiomas garantizan **el reparto, no la verdad**: un
valor SHAP alto significa «este atributo movió la predicción **de este
modelo**», no «este atributo causa el fenómeno».

**Conjunto Rashomon**: el conjunto de modelos casi igual de buenos. Con
atributos correlacionados es grande, y sus miembros **discrepan sobre
qué importa**.

## 5. Trabajo autónomo de la semana

| \# | Actividad | Tiempo | Producto | Plazo |
|----|----|----|----|----|
| 1 | Ejecutar y estudiar el cuaderno de la clase | 1,5 h | Cuaderno corrido | Antes de la semana 14 |
| 2 | **Redactar el informe final**: métodos y resultados | 3,0 h | Borrador | Semana 15 |
| 3 | Aplicar la exigencia 2 de la clase a su proyecto | 1,5 h | Media página | Con el informe |
| 4 | Leer Molnar (2022), caps. 5 y 9 | 0,5 h | — | — |

### 5.1 El ejercicio que se pide

La clase plantea cuatro exigencias, y la segunda es la que hay que
ejercer esta semana: **mida el compromiso en su problema**.

Entrene un modelo transparente —una logística regularizada, un árbol
poco profundo, un modelo aditivo— con el mismo protocolo y el mismo
presupuesto que su modelo principal, y reporte cuánto pierde.

Si pierde poco, tiene que explicar por qué usa la caja negra. Si pierde
mucho, tiene un argumento. En ambos casos ha convertido una discusión de
principios en una medición, que es lo que este módulo pide siempre.

### 5.2 Qué mirar en el cuaderno

`clase13_conjunto_rashomon.ipynb` construye datos donde **`x1` es casi
copia de `x0`** —sensores redundantes, la situación normal en
instrumentación— y entrena seis modelos.

|               | AUC | Reparto de importancia hacia `x0` |
|---------------|-----|-----------------------------------|
| Logística     |     | **88,8 %**                        |
| Potenciación  |     | 57,5 %                            |
| Bosque        |     | 49,5 %                            |
| Árboles extra |     | 44,5 %                            |
| Red (64,32)   |     | **12,1 %**                        |

El rango de AUC entre los seis es de **0,041**: son indistinguibles. Y
señalan **tres atributos distintos** como el más importante.

Ninguno se equivoca. La información de `x0` y `x1` es la misma, así que
la pregunta «¿cuál de los dos importa?» **no tiene respuesta en los
datos** —y sin embargo cada modelo entrega una explicación con aspecto
de respuesta.

Hay un segundo resultado, y es el matiz justo: **todos descartan
correctamente los atributos que no intervienen**. Ese es el uso legítimo
de estos métodos —depurar, detectar fuga, encontrar atributos
ilegítimos— y no está en disputa.

Lo que está en disputa es usarlos para fundamentar una intervención.

## 6. Lecturas

**Del seminario de esta semana**

> Rudin, C. (2019). Stop explaining black box machine learning models
> for high stakes decisions and use interpretable models instead.
> *Nature Machine Intelligence*, 1, 206–215.
>
> Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to
> interpreting model predictions. *NeurIPS*, 30.

Se leen **en tensión**. El argumento de Rudin tiene cuatro pasos: una
explicación *post hoc* es una aproximación; una aproximación fiel es
inútil si el modelo es opaco y una simple es infiel; en alto riesgo una
explicación infiel es peor que ninguna; y en datos estructurados el
compromiso que justificaría la caja negra a menudo no existe.

El cuarto paso es una **afirmación empírica** y por tanto refutable: es
el mejor punto de ataque para el discutidor.

**De apoyo**

> Molnar, C. (2022). *Interpretable Machine Learning* (2ª ed.), caps. 5
> y 9. De acceso abierto.

## 7. Preguntas de comprobación

1.  ¿En qué se distingue una explicación local de una importancia
    global?
2.  Sus dos sensores de vibración están correlacionados a 0,98. ¿Qué le
    dice la importancia por permutación, y por qué?
3.  ¿Qué garantizan los axiomas de Shapley? ¿Garantizan que la
    explicación sea correcta?
4.  ¿Puede usar valores SHAP para decidir sobre qué variable intervenir?
    Justifique.
5.  Explique el conjunto Rashomon y qué implica para la explicación de
    su modelo.
6.  Reconstruya el argumento de Rudin en cuatro pasos, y dé una réplica
    a cada uno.

## 8. Materiales de esta semana

| Archivo | Qué es |
|----|----|
| `slides/clase13_interpretabilidad.*` | Las 18 láminas de la clase |
| `codigo/clase13_conjunto_rashomon.ipynb` | Seis modelos equivalentes, explicaciones distintas |
| `guia/guia13.md` | Esta guía |

## 9. La próxima semana

**Semana 14 · Cuantificación de la incertidumbre.** Calibración y
predicción conforme. Robustez y desplazamiento de distribución.

Sin seminario ni taller: es la semana con menos carga sincrónica del
semestre, y la última antes del cierre. Aproveche para avanzar el
informe final.
