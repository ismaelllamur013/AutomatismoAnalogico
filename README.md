# Automatismo Analógico: Digitalización Semiautomática de Barovacuómetros

Herramienta desarrollada en Python para extraer y digitalizar mediciones de **barovacuómetros (manovacuómetros) analógicos** a partir de grabaciones de video, reemplazando la transcripción manual fotograma a fotograma por un sistema guiado de calibración angular y exportación directa a Excel.

## Problema y Solución

En entornos industriales o de laboratorio, registrar mediciones de instrumentos analógicos grabados en video suele requerir observar el reloj y transcribir cada valor manualmente.

Este proyecto agiliza ese proceso mediante una interfaz interactiva en **Jupyter Notebook** que permite:

1. **Calibrar la geometría del dial:** Definir la circunferencia por donde se desplaza la aguja del instrumento.
2. **Establecer puntos de referencia:** Marcar las posiciones conocidas en la escala (por ejemplo: `-1`, `0`, `1`, `2`, `3`, etc.).
3. **Inferencia interna:** Interpolar matemáticamente cualquier posición intermedia a lo largo del arco del dial a partir de los ángulos de referencia.
4. **Registro asistido con validación visual:** Avanzar automáticamente cada cierta cantidad de fotogramas, hacer clic sobre la punta de la aguja y verificar en tiempo real el valor calculado en pantalla antes de guardarlo en una planilla de cálculo.

## Flujo de Funcionamiento

1. **Encuadre del sensor:** Se selecciona el área de interés (ROI) y se traza la circunferencia correspondiente al recorrido de la aguja del barovacuómetro.
2. **Referenciación de escala:** El usuario marca sobre el círculo los puntos clave de la escala del instrumento (`-1`, `0`, `1`, `2`, `3`, etc.) para mapear posiciones espaciales y angulares con valores de presión o vacío.
3. **Muestreo por fotogramas:** El programa recorre el video saltando cada *N* fotogramas configurados y muestra el cuadro correspondiente.
4. **Lectura e inferencia:** Al hacer clic sobre la posición actual de la aguja, el sistema calcula el valor exacto por interpolación entre las referencias y lo muestra en pantalla para verificación visual inmediata.
5. **Exportación:** Al finalizar el recorrido del video, toda la serie de datos queda almacenada automáticamente en un archivo **Excel (`.xlsx`)**.

## Requisitos y Limitaciones

* **Cámara estática (Requisito crítico):** El video debe haberse grabado con cámara fija (sin movimiento ni vibraciones respecto al instrumento), ya que las coordenadas del círculo y las marcas de referencia permanecen fijas durante toda la ejecución.
* **Iluminación y enfoque:** La aguja y las marcas principales de la escala deben ser claramente distinguibles para facilitar la calibración inicial y el clic sobre la aguja.

## Estructura del Repositorio

* `Informes automatizados.ipynb`: Notebook principal con la lógica de carga de video, calibración interactiva del dial, interpolación de valores, visualización en pantalla y exportación a Excel.

## Tecnologías Utilizadas

* **Python 3**
* **Jupyter Notebook**
* **OpenCV (`cv2`)**: procesamiento de video, dibujo de referencias e interacción con el mouse.
* **NumPy / Pandas**: cálculos geométricos, interpolación y estructuración de datos.
* **OpenPyXL**: exportación de resultados a Excel.

## Cómo Ejecutar el Proyecto

1. **Clonar el repositorio:**
   `git clone https://github.com/ismaelllamur013/AutomatismoAnalogico.git`
2. **Instalar dependencias:**
   `pip install jupyter opencv-python numpy pandas openpyxl`
3. **Iniciar Jupyter Notebook:**
   `jupyter notebook "Informes automatizados.ipynb"`
4. **Ejecutar el flujo:**
   * Indica la ruta de tu archivo de video estático en la celda de configuración.
   * Define el salto de fotogramas deseado.
   * Sigue las instrucciones en la ventana emergente para trazar el círculo, marcar las referencias de escala y registrar los puntos a lo largo del video.

## Autor

* **Ismael Llamur** - [@ismaelllamur013](https://github.com/ismaelllamur013)
