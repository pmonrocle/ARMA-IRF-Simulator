# Simulador AR / MA / ARMA e IRF

Aplicación interactiva desarrollada en **Python** y **Streamlit** para simular procesos autorregresivos, de media móvil y ARMA, analizar sus condiciones de estacionariedad e invertibilidad, y visualizar sus funciones de respuesta al impulso.

La herramienta permite modificar de forma dinámica los parámetros del modelo y observar cómo cambian la serie simulada, las raíces del proceso y la respuesta ante un shock unitario.

## Objetivo

El objetivo de este proyecto es construir una aplicación didáctica para estudiar el comportamiento dinámico de modelos de series temporales univariantes:

* Modelos AR(p)
* Modelos MA(q)
* Modelos ARMA(p, q)
* Simulación de procesos estocásticos
* Condiciones de estacionariedad e invertibilidad
* Funciones de respuesta al impulso teóricas y estimadas

El simulador está orientado a estudiantes, investigadores y perfiles cuantitativos interesados en econometría, macroeconomía aplicada y análisis de series temporales.

## Funcionalidades principales

La aplicación permite:

* Seleccionar el tipo de modelo: AR, MA o ARMA.
* Elegir el orden del proceso, con valores de `p` y `q` entre 1 y 5.
* Modificar interactivamente los parámetros autorregresivos y de media móvil.
* Simular una serie temporal artificial a partir del proceso especificado.
* Configurar el tamaño muestral, la desviación típica de la innovación, el burn-in y la semilla aleatoria.
* Comprobar automáticamente si el proceso AR es estacionario.
* Comprobar automáticamente si el proceso MA es invertible.
* Visualizar las raíces de los polinomios AR y MA.
* Comparar la IRF teórica con la IRF estimada a partir de un modelo ARIMA ajustado sobre la serie simulada.

## Metodología

El simulador utiliza la clase `ArmaProcess` de `statsmodels` para construir el proceso ARMA definido por el usuario.

Dado un modelo ARMA(p, q):

```math
y_t = \phi_1 y_{t-1} + \cdots + \phi_p y_{t-p}
+ \varepsilon_t
+ \theta_1 \varepsilon_{t-1} + \cdots + \theta_q \varepsilon_{t-q}
```

donde:

```math
\varepsilon_t \sim WN(0, \sigma^2)
```

la aplicación genera una serie simulada y calcula la función de respuesta al impulso a partir de la representación MA infinita del proceso.

La IRF teórica se obtiene directamente del modelo poblacional especificado por el usuario. La IRF estimada se obtiene ajustando un modelo `ARIMA(p, 0, q)` sobre la serie simulada y calculando posteriormente la respuesta al impulso del modelo estimado.

Las diferencias entre ambas respuestas pueden deberse al error muestral y al error de estimación.

## Instalación

Para ejecutar la aplicación en local, primero clona el repositorio:

```bash
git clone https://github.com/tu-usuario/nombre-del-repositorio.git
cd nombre-del-repositorio
```

Después instala las dependencias:

```bash
pip install -r requirements.txt
```

## Ejecución

Para lanzar la aplicación, ejecuta:

```bash
streamlit run app.py
```

La aplicación se abrirá automáticamente en el navegador.

## Dependencias

El proyecto utiliza las siguientes librerías principales:

```txt
streamlit
numpy
matplotlib
statsmodels
```

## Estructura de la aplicación

La interfaz se organiza en tres bloques principales:

### 1. Parámetros

Permite seleccionar los coeficientes del modelo AR, MA o ARMA.

### 2. Simulación

Permite definir la desviación típica de las innovaciones, el tamaño muestral, el burn-in y la semilla aleatoria.

### 3. IRF

Permite elegir el horizonte de la función de respuesta al impulso y decidir si se muestra también la IRF estimada.

## Interpretación

La aplicación permite ver de forma intuitiva cómo los parámetros afectan a la dinámica del proceso.

Por ejemplo:

* Un proceso AR con raíces fuera del círculo unidad será estacionario.
* Un proceso MA con raíces fuera del círculo unidad será invertible.
* Parámetros autorregresivos elevados generan respuestas más persistentes.
* Parámetros negativos pueden generar dinámicas oscilatorias.
* La IRF estimada se aproxima mejor a la teórica cuando el tamaño muestral aumenta.

## Posibles extensiones

Algunas mejoras futuras del proyecto podrían ser:

* Añadir modelos ARIMA con diferenciación.
* Incorporar modelos SARIMA con estacionalidad.
* Permitir la descarga de los datos simulados.
* Añadir intervalos de confianza para la IRF estimada.
* Incluir un panel con los coeficientes estimados del modelo ARIMA.
* Añadir gráficos de ACF y PACF.
* Publicar la aplicación en Streamlit Community Cloud.

## Autor

**Pablo Monrocle Arribas**

Economista cuantitativo con interés en econometría aplicada, series temporales, macroeconomía cuantitativa, análisis de datos y modelos de riesgo.

## Licencia

Este proyecto se publica con fines educativos y divulgativos.
