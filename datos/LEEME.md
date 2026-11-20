# Datos del laboratorio

Datos **sintéticos**: generados por combinación de frases, con la etiqueta correcta conocida
(verdad de terreno). No contienen datos de personas.

| Archivo | Filas | Columnas | Para qué |
|---|---|---|---|
| `mensajes_soporte.csv` | 900 | `id`, `mensaje`, `motivo`, `dificultad`, `alternativa`, `frase`, `grupo` | Clasificar mensajes de soporte en 4 motivos |
| `opiniones.csv` | 700 | `id`, `opinion`, `sentimiento`, `dificultad`, `frase`, `grupo` | Clasificar opiniones como positivas o negativas |

## Columnas para partir bien los datos

- `grupo`: casi-duplicados (el mismo mensaje con otro saludo, otro producto o sin tildes).
- `frase`: la intención o frase principal. **Partir por `frase` es la prueba más exigente**: la
  prueba trae formas de decir las cosas que el modelo nunca vio.

Partir por fila deja casi-duplicados a los dos lados y da resultados demasiado optimistas.

## Casos difíciles

`dificultad` marca los mensajes con **negación** («No quiero devolver nada, solo saber cuándo
llega el pedido»), los **ambiguos** (con `alternativa`: otra etiqueta razonable) y, en opiniones,
la **ironía**.

## Límites

Son frases generadas: el vocabulario es más limitado que el de mensajes reales. Un resultado
alto con estos datos no garantiza el mismo resultado con datos de una organización.

Carga en una línea:

```python
import pandas as pd
df = pd.read_csv("https://raw.githubusercontent.com/Fedgutcor/lab-ia-intermedio/main/datos/mensajes_soporte.csv")
```
