# Aprendizaje Automático · Doctorado en Ingeniería

Material público del módulo **Aprendizaje Automático** del Doctorado en
Ingeniería de la Universidad de Talca.

El módulo trata el aprendizaje automático como un problema de **estimación de
riesgo**: qué se puede afirmar sobre datos que no se observaron, y bajo qué
condiciones esa afirmación deja de sostenerse. Está orientado a tesistas, así
que el énfasis está en el juicio metodológico —protocolos de validación, fuga
de información, comparación estadística, reporte— más que en la implementación.

## Las quince semanas

| # | Tema | Guía | Decks |
|---|---|---|---|
| 1 | El aprendizaje como estimación de riesgo | [`guia01.md`](guias/guia01.md) | 2 |
| 2 | Sesgo inductivo y No Free Lunch | [`guia02.md`](guias/guia02.md) | 2 |
| 3 | El compromiso sesgo-varianza | [`guia03.md`](guias/guia03.md) | 1 |
| 4 | Modelos lineales y regularización | [`guia04.md`](guias/guia04.md) | 2 |
| 5 | Márgenes, árboles y ensambles | [`guia05.md`](guias/guia05.md) | 1 |
| 6 | Métricas y calibración | [`guia06.md`](guias/guia06.md) | 2 |
| 7 | Protocolos de validación y fuga de información | [`guia07.md`](guias/guia07.md) | 1 |
| 8 | Comparación estadística de algoritmos | [`guia08.md`](guias/guia08.md) | 2 |
| 9 | Representación y reducción de dimensionalidad | [`guia09.md`](guias/guia09.md) | 2 |
| 10 | Agrupamiento y el problema de su validación | [`guia10.md`](guias/guia10.md) | 2 |
| 11 | Perceptrón multicapa y retropropagación | [`guia11.md`](guias/guia11.md) | 1 |
| 12 | Transferencia y el costo como criterio | [`guia12.md`](guias/guia12.md) | 2 |
| 13 | Interpretabilidad | [`guia13.md`](guias/guia13.md) | 1 |
| 14 | Incertidumbre, predicción conforme y robustez | [`guia14.md`](guias/guia14.md) | 2 |
| 15 | Equidad, reporte y cierre del módulo | [`guia15.md`](guias/guia15.md) | 2 |
## Qué hay aquí

| Carpeta | Contenido |
|---|---|
| [`guias/`](guias) | La guía de cada semana: qué pasa en la sesión, el trabajo autónomo con sus tiempos, las lecturas y las preguntas de comprobación |
| [`slides/`](slides) | Las diapositivas de cada clase, en PDF |
| [`cuadernos/`](cuadernos) | Los cuadernos de Python de cada semana, ejecutados, con sus figuras |
| [`instrumentos/`](instrumentos) | El cuestionario del diagnóstico de entrada |
| [`entorno/`](entorno) | `requirements.txt` con las versiones fijadas |

**La guía de la semana es el documento principal.** Dice qué se hace, cuánto
tiempo toma y con qué se corrige. Las diapositivas son el apoyo de la sesión
sincrónica, no el material de estudio.

## Cómo ejecutar los cuadernos

Requiere Python 3.10 o superior.

```bash
python3 -m venv .venv
source .venv/bin/activate          # en Windows: .venv\Scripts\activate
pip install -r entorno/requirements.txt
jupyter lab
```

Ejecute todas las celdas en orden desde un kernel limpio. Varios cuadernos
terminan con una celda que **verifica** que los valores calculados coinciden
con los de las láminas: si el cuaderno deja de reproducir, esa celda falla.

Algunos cuadernos documentan **resultados negativos a propósito** —un
estadístico que no resume lo que se cree, un índice que encuentra estructura
donde no la hay—. No son errores: son el argumento de la clase.

## Sobre este repositorio

Contiene solo las **salidas**. Las fuentes `.qmd` con que se generan viven en un
repositorio privado, y este se actualiza publicando desde allí.

## Licencia

<a rel="license" href="https://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Atribución-NoComercial-CompartirIgual 4.0 Internacional</a> (CC BY-NC-SA 4.0).

Puede copiar, distribuir y adaptar este material, incluso para un curso propio,
siempre que **cite la autoría**, **no lo use con fines comerciales** y
**comparta sus adaptaciones bajo esta misma licencia**. El texto legal completo
está en [`LICENSE`](LICENSE).

Cita sugerida:

> Astudillo, C. A. (2026). *Aprendizaje Automático* [material docente].
> Doctorado en Ingeniería, Universidad de Talca.
> https://github.com/utalca-ai/ML_POSGRADO_PUBLIC
