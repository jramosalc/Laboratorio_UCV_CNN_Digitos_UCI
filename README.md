# Informe de Laboratorio N.º 13: Sistemas Inteligentes
**Tema:** Manuscrito a texto con CNN (Clasificación de dígitos escritos a mano)  
**Ciclo:** VII | **Turno:** Noche  
**Semestre:** 2026-1  
**Universidad:** Universidad César Vallejo  
**Facultad:** Ingeniería y Arquitectura  
**Escuela Profesional:** Ingeniería de Sistemas  
**Autor:** Ramos Alcarraz Jesús Andrés  
**Docente:** Mgtr. Luis Paraguay Arzapalo  
**Ubicación:** Lima – Ate  

---

## 24. Respuestas a las Preguntas de Análisis

### 1. ¿Qué diferencia existe entre una red densa y una CNN?
Una red densa (*Fully Connected*) aplana la imagen en un vector unidimensional y procesa cada píxel de forma aislada, perdiendo por completo la relación y estructura espacial. En cambio, una **CNN (Red Neuronal Convolucional)** preserva la estructura bidimensional original utilizando filtros que escanean la imagen, capturando patrones locales y relaciones de proximidad entre píxeles.

### 2. ¿Qué función cumple una capa convolucional?
Su función principal es la **extracción de características**. Aplica operaciones matemáticas de convolución mediante un conjunto de filtros sobre la imagen de entrada para detectar elementos visuales, generando mapas de características (*feature maps*) que resaltan la presencia de dichos patrones.

### 3. ¿Qué representa un filtro en una CNN?
Representa una pequeña matriz de pesos (por ejemplo, de tamaño $3 \times 3$ o $5 \times 5$) que se desliza por toda la imagen. Cada filtro aprende de forma automática a activarse o reaccionar ante una característica visual específica, como bordes verticales, líneas diagonales, esquinas o curvas.

### 4. ¿Qué función cumple MaxPooling?
Cumple la función de **reducción dimensional (submuestreo)**. Al quedarse únicamente con el valor máximo de una región (por ejemplo, de bloques de $2 \times 2$), disminuye el tamaño espacial del mapa de características. Esto reduce el costo computacional, el número de parámetros del modelo (previniendo el sobreajuste) y otorga invariancia frente a pequeñas traslaciones del patrón.

### 5. ¿Por qué normalizamos los valores de píxeles?
Porque los píxeles originales del dataset UCI varían en un rango numérico de 0 a 16. Al dividirlos entre 16.0, transformamos sus valores a una escala estándar entre **0 y 1**. Esto homogeniza la magnitud de las entradas, estabilizando y acelerando el proceso de optimización del descenso de gradiente durante el entrenamiento.

### 6. ¿Por qué usamos softmax en la capa de salida?
Porque estamos resolviendo un problema de **clasificación multiclase** (10 clases independientes, correspondientes a los dígitos del 0 al 9). La función `softmax` toma los valores numéricos de la última capa (*logits*) y los convierte en una distribución de probabilidades que suman exactamente 1 (100%), permitiendo identificar con qué certeza el modelo asigna una imagen a cada dígito.

### 7. ¿Qué dígitos se confundieron más en la matriz de confusión?
*Nota: Basado en las tendencias de ejecución de este dataset de baja resolución ($8 \times 8$ píxeles), las confusiones más recurrentes suelen darse entre los pares **1 y 8**, **3 y 9**, o **5 y 9**.* Esto ocurre porque, al digitalizarse en tan pocos píxeles, la morfología de sus trazos se vuelve casi idéntica, borrando los detalles geométricos que los diferencian.

### 8. ¿Por qué algunos dígitos escritos a mano son difíciles de clasificar?
Debido a la **alta variabilidad del estilo de escritura humana** (trazos muy inclinados, grosores irregulares, números abiertos o mal formados) combinada con la **baja resolución de la imagen**. Cuando un dígito tiene anomalías en su trazo original y se reduce a una cuadrícula de $8 \times 8$, se genera una ambigüedad visual que confunde incluso al ojo humano.

### 9. ¿Qué ventajas tendría usar imágenes de mayor resolución?
Permitiría capturar detalles morfológicos mucho más precisos y finos, como los ángulos exactos de las intersecciones, la curvatura limpia de los trazos y los espacios vacíos internos. Esto eliminaría la ambigüedad en dígitos similares y aumentaría drásticamente la precisión del clasificador.

### 10. ¿Qué limitaciones tiene este laboratorio frente a un sistema OCR real?
Un sistema OCR real se enfrenta a escenarios masivos y desestructurados: imágenes de alta resolución, páginas completas con texto continuo alineado, diferentes fuentes tipográficas, ruidos de fondo, rotaciones físicas del papel y variaciones de iluminación. Este laboratorio es un entorno controlado de caracteres individuales previamente recortados y limpios, por lo que un OCR real requiere fases complejas de segmentación previa y arquitecturas híbridas más profundas (como CNNs combinadas con redes recurrentes o Transformers).

---

## 25. Conclusión Final del Laboratorio

En este laboratorio se demostró la superioridad de las Redes Neuronales Convolucionales (CNN) frente a las redes densas tradicionales para el procesamiento de datos visuales, logrando una clasificación precisa del dataset de dígitos de la UCI. Mediante la aplicación de operaciones de convolución y pooling, el modelo logró extraer y abstraer de forma eficiente características espaciales esenciales como bordes y curvas de los dígitos manuscritos. Asimismo, la experimentación con diferentes variantes evidenció que la correcta calibración de la arquitectura —añadiendo capas convolucionales y mecanismos de regularización como Dropout— es fundamental para estabilizar el aprendizaje y optimizar la capacidad de generalización del modelo. Estos hallazgos sientan las bases técnicas necesarias para el diseño de sistemas OCR de escala comercial más robustos y complejos.