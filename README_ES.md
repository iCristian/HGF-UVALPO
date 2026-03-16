# **Statistical Analysis of the CBM Project (HGF_UVALPO)**

Este repositorio contiene el análisis estadístico detallado del **Proyecto CBM (Childbirth Experience Questionnaire / BMSP2)** realizado para el Hospital Dr. Gustavo Fricke (HGF) y la Universidad de Valparaíso (UVALPO).

El objetivo principal de este documento y del código adjunto es asegurar la **transparencia, rigurosidad y reproducibilidad** metodológica en concordancia con los estándares exigidos por revisores y editores de revistas indexadas en Web of Science (WOS) u otras bases de datos científicas de alto impacto.

---

## 📌 **Resumen (Overview)**

Se examinó la evaluación de la calidad asistencial y la experiencia del parto en mujeres a través de la herramienta BMSP2. Para garantizar la validez del análisis inferencial, se emplearon modelos estadísticos paramétricos y robustos que ajustan por covariables demográficas relevantes, mitigando el impacto de posibles sesgos en los datos observacionales.

## 📂 **Datos y Consideraciones Éticas (Dataset)**

- Los datos analizados proceden de un conjunto anonimizado, respetando así la confidencialidad de las participantes.
- El conjunto de datos ha sido preprocesado para proteger el anonimato, cumpliendo con los lineamientos de la Declaración de Helsinki (datos_encuestas.csv obtenidos de repositorio privado). Ningún dato sensible que permita la identificación directa de las pacientes está expuesto.

---

## 📊 **Metodología y Estructura del Análisis**

El código fuente iterativo en el archivo Jupyter Notebook (`Statistical Analysis of the CBM Project (HGF_UVALPO) IJGO.ipynb`) documenta exhaustivamente cada fase del flujo de datos, descompuesta en las siguientes etapas:

### 1. **Limpieza y Preprocesamiento de Datos**

- **Estandarización:** Normalización de formatos numéricos en ítems escalares e imputación controlada de valores (NaN = 0 / neutral según corresponda lógicamente) para asegurar la compatibilidad con los métodos estadísticos.
- **Puntuaciones Inversas:** Procesamiento codificado de los ítems de control del BMSP2 cuya redacción implica un constructo invertido (ej. preguntas de polaridad negativa), mapeando los valores de forma paramétrica de acuerdo con las especificaciones del instrumento.

### 2. **Análisis Descriptivo**

- Estadísticas univariadas de la cohorte (media, mediana, desviación estándar).
- Distribuciones demográficas centradas en **Edad, Nivel Educacional y Paridad**.
- Tabulaciones de frecuencia para el recuento de respuestas (Escala Likert de 1 a 5) ítem por ítem.

### 3. **Cálculo de Dimensiones (Instrumento BMSP2)**

Se agruparon estadísticamente los ítems individuales en las correspondientes siete dimensiones teóricas validadas previamente:

1. *Cuidado relacional de calidad*
2. *Cuidado despersonalizado*
3. *Participación familiar continua*
4. *Cuidado oportuno y respetuoso*
5. *Ambiente físico confortable*
6. *Condiciones de contacto madre-hijo*
7. *Autocuidado y confort*

### 4. **Análisis Inferencial Bivariado**

Se ejecutaron pruebas inferenciales seguidas de comparaciones post-hoc (como la prueba de Kruskal-Wallis o Mann-Whitney U y test de Dünn) si cabía rechazo de normalidad de varianzas, analizando las dimensiones por:

- **Tipo de Parto** (Vaginal vs. Cesárea). *Nota Metodológica:* El parto instrumentalizado con fórceps se excluyó intencionalmente del modelo principal por baja frecuencia amostral (Outliers) que introducía varianza desmedida (falta de potencia estadística).
- **Paridad** (Nulípara vs. Multípara).
- **Nivel Educacional** y agrupación por **Edad**.

### 5. **Análisis Multivariado: Regresión Lineal Robusta (RLM)**

Diseñado para controlar la heterocedasticidad y la presencia posible de valores atípicos clínicos, se formuló una **Regresión Lineal Robusta** utilizando el normado de Huber (Norma T de Huber o estimador M).

- **Modelo Principal:** El efecto de interés primario analizado fue el *Impacto del Tipo de Parto (Cesárea vs. Vaginal)* en cada dimensión clínica, **ajustando simultáneamente** el modelo por covariables explicativas críticas (`Edad`, `Nivel_educacional`, y `Paridad`).
- **Verificación de Supuestos:** Visualización rigurosa exploratoria de los residuos vs. valores ajustados, garantizando la independencia estadística, dispersión esperada y linealidad.

---

## 🛠️ **Requisitos y Reproducibilidad**

El pipeline fue escrito y testeado en entorno **Python 3**. El análisis depende extensivamente de la arquitectura de la librería `statsmodels` (Regresiones Robustas RLM) y `pingouin` para pruebas de validación cruzada.

Para reproducir este análisis localmente en una instancia de Jupyter Notebook o en Google Colab, se requieren las siguientes dependencias (librerías listadas según los imports del bloque #0):

```python
pandas
numpy
matplotlib
seaborn
scipy
statsmodels
scikit-posthocs
pingouin
```

*(Puede instalarlas rápidamente dentro del entorno ejecutando: `pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-posthocs pingouin -q`)*

### Ejecución

Abra el notebook `.ipynb` y ejecute todas las celdas secuencialmente en un kernel de Python. El notebook incluye comentarios intraestrucutrales y conectará con el Dataframe hospedando el CSV instanciando los modelos estadísticos de forma automatizada sobre la sesión.

---

## 👨‍🔬 **Autoría y Afiliación**

- **Autor:** Cristian Carreño León
- **Correo:** <cristian.carreno@uv.cl>
- **Institución:** Universidad de Valparaíso, Chile.
- **Dependencia:** Facultad de Medicina. Escuela de Obstetricia y Puericultura.

---

## 📄 **Licencia**

Este trabajo y los documentos contenidos en este repositorio están bajo la licencia **Creative Commons Reconocimiento-NoComercial-CompartirIgual 4.0 Internacional (CC BY-NC-SA 4.0) © 2026**.

Usted es libre de:

- **Compartir** — copiar y redistribuir el material en cualquier medio o formato.
- **Adaptar** — remezclar, transformar y construir a partir del material.

Bajo las siguientes condiciones:

- **Reconocimiento (Attribution)** — Debe otorgar el crédito correspondiente, proporcionar un enlace a la licencia e indicar si se realizaron cambios.
- **No Comercial (NonCommercial)** — No puede utilizar el material para fines comerciales.
- **Compartir Igual (ShareAlike)** — Si remezcla, transforma o crea a partir del material, debe distribuir sus contribuciones bajo la misma licencia que el original.

Para ver una copia de esta licencia, visite <http://creativecommons.org/licenses/by-nc-sa/4.0/> o revise el archivo `LICENSE` adjunto en este repositorio.
