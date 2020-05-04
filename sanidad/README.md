## Descripción
Este conjunto de datos recoge información sobre la sanidad en España durante el periodo 2006-2019. Se incluyen tanto datos sobre hospitales como el gasto destinado a sanidad. Se ofrecen tres versiones del dataset:
   - Original: unifica los catálogos de hospitales facilitados por el Ministerio de Sanidad (periodo 2006-2019).
   - Simplificado: homogeniza el tipo de financiación de cada hospital a pública, privada o concertada, y realiza otras operaciones sobre los datos (véase Metodología) que hace más sencillo su uso para análisis de datos.
   - Gastos: agrega el número de hospitales y camas por comunidad autónoma y añade información sobre los gastos de sanidad de cada una de ellas.

#### *Dataset* catálogos unificados (originales)
Se unifican las diferentes tablas de cada catálogo (formato `mdb`) para facilitar las comparativas entre años. No incluye la dotación/equipación de cada centro.

#### *Dataset* catálogos simplificados
Parte de los catálogos unificados y es el recomendado para utilizar en análisis de datos. En esta versión del dataset se ha simplificado la columna `PATRIMONIAL` para poder distinguir directamente los centros públicos, privados, y concertados (ver la sección Metodología para más detalles). Este *dataset* no incluye los hospitales que forman un complejo hospitalario (incluyen únicamente el complejo que los engloba). Además, se retiran algunas columnas sin interés estadístico, como los datos de contacto de los hospitales.

#### *Dataset* enriquecido con datos de gastos
Parte del conjunto de datos simplificado. Agrega por comunidad autónoma el número de hospitales y camas, y añade información sobre las partidas destinadas a sanidad. Para cada año y comunidad autónoma se tiene:

    - Número de hospitales públicos, privados y concertados.

    - Número de camas públicas, privadas y concertadas.

    - Gasto total consolidado.

    - Gasto en conciertos.

    - Porcentaje de gasto sobre el PIB.

    - Gasto por habitante.

No se tienen datos de gastos de Ceuta y Melilla durante todo el periodo, y de ninguna comunidad autónoma en 2019 ya que el gasto público consolidado solo está publicado hasta 2018.

## Origen de los datos
- Catálogos: [fuente](https://www.mscbs.gob.es/ciudadanos/prestaciones/centrosServiciosSNS/hospitales/home.htm).
- Gastos en sanidad (gasto consolidado, gasto en conciertos, gasto en porcentaje sobre el del PIB y gasto en porcentaje por habitante): [fuente](|https://www.mscbs.gob.es/estadEstudios/estadisticas/sisInfSanSNS/pdf/egspGastoReal.pdf).

## Metodología
- Metodología sobre la unificación de los catálogos:
    * Se han mantenido el formato de los datos y los nombres de las columnas originales, es decir, los que se utilizan en los catálogos facilitados por el Ministerio de Sanidad, realizando únicamente los siguientes cambios:
      * Unificación de las columnas `OBSERVACIONES` y `OBSERVACIONESPUBLI` utilizando el nombre de la primera.
      * El código identificativo se los hospitales se ha bajo `CODCNH`, el nombre usado en el catálogo más reciente (2019), en lugar del usado en los años anteriores (`CODID`).
      * Se ha retirado del catálogo de 2019 la columna `CODCCN` por falta de información sobre a qué hace referencia su valor.
      * Se ha añadido la columna `AÑO`.
- Metodología sobre el *dataset* simplificado:
    * Los complejos hospitalarios se registran como un único hospital, en lugar de contar el número de unidades que lo conforman.
    * Se ha simplificado el valor `PATRIMONIAL` para poder distinguir los centros públicos, privados, y concertados:
      * **Públicos**: Entidades públicas, Seguridad social, Ministerio de Defensa, Comunidad Autónoma, Ministerio de Interior, Municipio, Diputación o Cabildo.
      * **Privados**: Privado benéfico (Iglesias), Privado no benéfico, Otro privado benéfico, MATEP y Privado benéfico (Cruz Roja).
      * **Conciertos**: se contabilizan como **concertados** los marcados en el catálogo como tal y los hospitales catalanes de la Xarxa Hospitalària d'Utilització Pública (XHUP).
    * Se han *booleanizado* las columnas `ALTA` y `CERRADO`.

- Metodología sobre el *dataset* enriquecido con datos de presupuestos:
    * Los datos se muestran en miles de millones de euros.
    * Agrega el número de camas y de hospitales por comunidad autónoma.
    * Se han eliminado del catálogo de cada año aquellos hospitales que se cierran durante ese año. Esta decisión viene motivada porque en los datos agregados que Sanidad da en sus reportes no se tienen en cuenta los hospitales en su año de cierre.
    * El valor del *gasto total* utiliza el gasto consolidado.