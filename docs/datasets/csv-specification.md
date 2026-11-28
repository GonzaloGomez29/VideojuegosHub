# Especificación del CSV de videojuegos

**Proyecto:** VideojuegosHub  
**Issue:** #12 — Definir la estructura y validez del CSV de videojuegos  
**Versión:** 1.0 (pendiente de consenso del equipo)

## 1. Objetivo

Definir el contrato de datos que deben cumplir los archivos CSV de VideojuegosHub. Esta especificación será la referencia para la implementación de la subida, almacenamiento, validación, métricas, búsqueda y filtrado. Cada registro representa un videojuego, independientemente del número de plataformas en las que esté disponible.

## 2. Formato del fichero

| Característica | Requisito |
| --- | --- |
| Extensión | `.csv` |
| Codificación | UTF-8 (se admite BOM inicial) |
| Separador de columnas | Coma (`,`) |
| Separador de elementos de listas | Punto y coma (`;`) |
| Separador decimal | Punto (`.`) |
| Fechas | `YYYY-MM-DD` (ISO 8601) |
| Booleanos | `true` o `false`, en minúsculas |
| Cabecera | Obligatoria, con las 13 columnas indicadas abajo |
| Registros | Al menos un videojuego |
| Moneda | EUR, sin símbolo monetario |
| Valoración | Escala de 0 a 10 |

Se admiten saltos de línea LF y CRLF. Los campos que contengan comas, comillas o saltos de línea deben seguir el escapado habitual de CSV: comillas dobles alrededor del campo y duplicación de las comillas internas. No se admiten filas con distinto número de campos, cabeceras duplicadas ni columnas desconocidas. Se propone exigir el orden de cabecera mostrado a continuación para que el contrato sea inequívoco.

```csv
title,developer,genres,price,release_date,rating,platforms,saga,has_sequel,online_multiplayer,local_multiplayer,competitive,crossplay
```

## 3. Diccionario de datos

Todas las columnas deben estar presentes. La obligatoriedad se refiere al valor de cada registro, no a la presencia de la columna.

| Columna | Tipo | Valor obligatorio | Descripción y restricciones |
| --- | --- | --- | --- |
| `title` | Texto | Sí | Título del videojuego; no vacío ni compuesto solo por espacios. |
| `developer` | Texto | Sí | Desarrolladora; no vacío ni compuesto solo por espacios. |
| `genres` | Lista de textos | Sí | Uno o más géneros del catálogo definido en el apartado 4. |
| `price` | Decimal | Sí | Precio de referencia en EUR, mayor o igual a 0, con hasta dos decimales. Un juego gratuito tiene precio `0`. |
| `release_date` | Fecha | Sí | Fecha de lanzamiento de referencia; fecha real del calendario en formato `YYYY-MM-DD`. |
| `rating` | Decimal | Sí | Valoración de usuarios entre 0 y 10, ambos incluidos, con hasta dos decimales. |
| `platforms` | Lista de textos | Sí | Una o más plataformas del catálogo definido en el apartado 5. |
| `saga` | Texto | No | Nombre de la saga; vacío si no pertenece a ninguna o el dato se desconoce. |
| `has_sequel` | Booleano | No | `true` si existe una continuación, `false` si no existe y vacío si se desconoce. |
| `online_multiplayer` | Booleano | Sí | Disponibilidad de multijugador online. |
| `local_multiplayer` | Booleano | Sí | Disponibilidad de multijugador local. |
| `competitive` | Booleano | Sí | Disponibilidad de un modo competitivo. |
| `crossplay` | Booleano | Sí | Compatibilidad con multijugador online entre plataformas distintas. |

El precio y la fecha de lanzamiento son valores generales de referencia, no valores específicos de cada plataforma. Para los números se admite notación decimal ordinaria (por ejemplo, `0`, `9.5`, `29.99`), no exponentes, porcentajes, símbolos de moneda, NaN o infinitos. No se admiten separadores de miles.

## 4. Catálogo de géneros

Valores admitidos (sensibles a mayúsculas y minúsculas):

- Action
- Adventure
- RPG
- Shooter
- Strategy
- Simulation
- Sports
- Racing
- Platformer
- Puzzle
- Horror
- Survival
- Sandbox
- Fighting
- Stealth
- Rhythm
- Battle Royale
- MMO
- Roguelike
- Other

Ejemplo: `Action;Adventure;RPG`.

## 5. Catálogo de plataformas

Valores admitidos (sensibles a mayúsculas y minúsculas):

- PC
- PS3
- PS4
- PS5
- Xbox 360
- Xbox One
- Xbox Series X/S
- Nintendo Switch
- Nintendo Switch 2
- Nintendo 3DS
- Wii
- Wii U
- Android
- iOS
- Other

Ejemplo: `PC;PS5;Xbox Series X/S`.

En ambos catálogos, `Other` representa categorías no contempladas. Cada elemento debe coincidir exactamente con un valor del catálogo; no se admiten elementos vacíos ni repetidos en una lista. Las ampliaciones de los catálogos deberán consensuarse y reflejarse en esta especificación.

## 6. Reglas de validación generales

1. El archivo debe cumplir el formato y la cabecera establecidos en el apartado 2.
2. Todos los campos obligatorios deben tener un valor válido.
3. Los campos opcionales desconocidos se representan mediante un campo vacío, no mediante `null`, `N/A` o equivalentes.
4. No se permiten registros duplicados según la combinación de `title` y `developer`. Se propone comparar ambos valores sin distinguir mayúsculas y minúsculas y eliminando espacios exteriores.
5. Si `crossplay` es `true`, `online_multiplayer` debe ser `true`.
6. El archivo completo se considera inválido si cualquiera de sus registros incumple estas reglas.

## 7. Origen y recopilación de datos

La fuente de referencia para el atributo rating será Metacritic (https://www.metacritic.com/).

Se utilizará exclusivamente el indicador User Score, correspondiente a las valoraciones de los usuarios, cuya escala comprende valores entre 0 y 10.

No se utilizará el Metascore, puesto que representa las valoraciones de la crítica especializada.

Los videojuegos que no dispongan de User Score no se incluirán en el dataset real, dado que el atributo rating es obligatorio.

Las valoraciones corresponderán al momento de recopilación de los datos y permanecerán estáticas dentro del CSV.

El resto de los atributos podrá obtenerse de diferentes fuentes web.

## 8. Ejemplos

Los archivos de `examples/` contienen videojuegos ficticios y datos sintéticos, exclusivamente para comprobar el contrato de datos. No constituyen el dataset definitivo.

| Archivo | Resultado esperado | Motivo |
| --- | --- | --- |
| `valid-videogames.csv` | Válido | Registros con listas, valores opcionales vacíos y límites admitidos. |
| `invalid-rating.csv` | Inválido | Rating superior a 10. |
| `invalid-date.csv` | Inválido | Fecha con formato incorrecto. |
| `invalid-platform.csv` | Inválido | Plataforma fuera del catálogo. |
| `invalid-crossplay.csv` | Inválido | Crossplay sin multijugador online. |
| `invalid-required.csv` | Inválido | Rating obligatorio vacío. |
| `invalid-duplicate.csv` | Inválido | Combinación de título y desarrolladora repetida. |
| `invalid-header.csv` | Inválido | Falta la columna `rating`. |

## 9. Alcance

La issue #12 define las reglas y aporta ejemplos. La implementación del validador, la subida y almacenamiento, los metadatos, las métricas y la visualización corresponden a las subissues respectivas de WI-newdataset.
