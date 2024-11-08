# Telecomunicaciones-identificar-operadores-ineficaces
__Proyecto de análisis a la plataforma de delivery Instacart, análisis exploratiorio y visualización de datos__

<image src="https://github.com/BastianLQ/Analisis-Instacart/blob/main/N3.jpg" alt="Collage de gráficos">

_Fragmentos del notebook, para ver proyecto completo hacer click [aquí](https://portfoliodabastianlopez.on.drv.tw/Portafolio/An%C3%A1lisis%20Instacart.html)_

## Descripción del Proyecto
El servicio de telefonía virtual CallMeMaybe está desarrollando una nueva función que brindará a los supervisores y las supervisores información sobre los operadores menos eficaces. Se considera que un operador es ineficaz si tiene una gran cantidad de llamadas entrantes perdidas (internas y externas) y un tiempo de espera prolongado para las llamadas entrantes. Además, si se supone que un operador debe realizar llamadas salientes, un número reducido de ellas también será un signo de ineficacia.
  
## Herramientas Utilizadas
- __Lenguaje de Programación:__ Python.
- __Entorno de Desarrollo:__ Jupyter Notebook.
- __Bibliotecas:__ Pandas, Matplotlib.

## Proceso del Proyecto
- Descomposición de tareas.
- __Pre-procesamiento de datos__: En esta etapa inicial se procurará realizar todos los preparativos necesarios para comenzar el análisis.
  - __Importar librerías y datos__.
  - __Trabajar los valores ausentes, duplicados y tipos de datos erróneos__.
  - __Completar los datos__: Crear una columnna con los tiempos de espera de las llamadas.
- __Análisis exploratorio de datos__: En esta etapa se trabajará en la integridad de los datos y se observarán las distribuciones de los datos, rescatando conclusiones valiosas que se puedan apreciar a simple vista.
  - __Analizar la integridad de los datos:__ esto requiere trabajar en.
      - __Determinar las fechas mínimas y máximas de recolección de datos__.
      - __Determinar si hay datos suficientes por día__.
      - __Llamadas de duración 0:__ Descubrir si hay registros de llamadas de duración 0 que no sean consideradas como perdidas, en caso de que así sea, serán debidamente omitidas de los análisis posteriores, mediante un drop si son una cantidad mínima, o una omisión puntual, en caso de que representen un porcentaje significativo de las llamadas.
      - __Outliers:__ Buscar y trabajar (en caso de ser necesario) outliers, mediante uso de percentiles extremos (entre el 95 y el 99), en los tiempos de espera de llamadas, cantidad de llamadas perdidas y en la cantidad de llamadas realizadas
  - __Llamadas perdidas:__ Crear una métrica llamada "Tasa de contestación de llamadas" basada en promediar 0 y 1 según si la llamada fue perdida o contestada, para este campo no se considerarán las llamadas salientes ni las internas. El comportamiento de esta nueva métrica se visualizará con un histograma.
  - __Tiempos de espera promedio:__ Construir un histograma con la distribución total de los tiempos de espera las llamadas, se dejarán fuera de este gráfico los tiempos de espera de llamadas salientes y, también, las llamadas internas.
  - __Llamadas salientes semanales:__ Este campo se trabajará de manera semanal ya que es fácilmente actualizable y permite la incorporación de nuevos operadores al sistema sin desconfigurarlo, para este item no se contarán las llamadas internas y las llamadas salientes perdidas. Para visualizar este campo se usará un histograma.

- __Identificar operadores ineficaces__: Mediante un análisis de la cantidad de llamadas perdidas, tiempo de espera y cantidad de llamadas salientes, se categorizará a los operadores como; excelentes, buenos, regulares, malos y muy malos. El sistema estará basado en percentiles, para lo cual se calcularán los percentiles 10, 20, 30, 40, 50, 60, 70, 80, 90 y 100 de los campos a evaluar. Lo anterior será traducido en notas que al promediarse/ponderarse nos entregarán una calificación final sobre los operadores.

Antes de comenzar con los cálculos, se dividirán los operadores en dos grupos:

  - Quienes hacen y reciben llamadas.
  - Quienes solo reciben llamadas

Esto debido a que se usarán indices diferentes para cada uno de estos grupos. Una vez hecha la divsión, se comienza a crear el sistema de clasificación calculando:

  - __Tasa de contestación de llamadas:__ Aplicar los filtros de outliers y de tipo de llamadas, agrupar por operador y sacar los 10 percentiles requeridos para el índice.
  - __Tiempo medio de espera:__ Aplicar los filtros de outliers y de tipo de llamadas, agrupar por operador y sacar los 10 percentiles requeridos para el índice. Este valor deberá ser invertido, ya que a diferencia de los otros, mientras más grande es el valor, es menor la calificación que debe entregar.
  - __Llamadas salientes semanales__: Aplicar los filtros de outliers y de tipo de llamadas, agrupar por operador y por semana, y sacar los 10 percentiles requeridos para el índice.
  - __Desarrollar funciones de clasificación:__ Usando los percentiles obtenidos en conjunto con funciones se ingresarán las calificaciones de 1 a 10 al dataset agrupado por operador.
  - __Ponderación:__ Para el grupo de operadores que solo reciben llamadas, se calculará la media entre las dos medidas usadas: Tiempo medio de espera y Tasa de contestación de llamadas, en cambio, para el grupo que hace y recibe llamadas, se construirá un índice ponderado de la siguiente manera:
      - __Tasa de contestación de llamadas__: 40% de la calificación final.
      - __Tiempo medio de espera__: 40% de la calificación final.
      - __Llamadas salientes semanales__: 20% de la calificación final.
  - __Categorización:__ Finalmente, se categorizarán las calificaciones finales de la siguiente manera:
      - __Excelente__: Más de 8.
      - __Bueno__: Entre 6 y 8.
      - __Regular__: Entre 4 y 6.
      - __Malo__: Entre 2 y 4.
      - __Muy Malo__: Menos de 2.
- Pruebas de hipótesis.
- Clustering.
- Conclusiones.

## Relevancia de los descubrimientos
El análisis de datos de Instacart reveló patrones importantes en el comportamiento de compra de los clientes. Estos insights pueden ser utilizados para optimizar las estrategias de marketing, gestión de inventarios y mejorar la experiencia del cliente.

## Ejecuta el proyecto [aquí](https://portfoliodabastianlopez.on.drv.tw/Portafolio/An%C3%A1lisis%20Instacart.html)
Para ver el diccionario de datos, el desarrollo completo en código, todos los gráficos y las conclusiones, haga click en el enlace de arriba.
