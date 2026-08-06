# Simulador AR / MA / ARMA e IRF

<img width="1882" height="802" alt="image" src="https://github.com/user-attachments/assets/070157c2-858b-41f7-879c-4a415dd6fe5c" />



Aplicación interactiva desarrollada en **Python** y **Streamlit** para simular procesos autorregresivos, de media móvil y ARMA, analizar sus condiciones de estacionariedad e invertibilidad, y visualizar sus funciones de respuesta al impulso.

Esta aplicación nace como material computacional complementario del artículo:

**Monrocle Arribas, P. (2025). *Análisis de Modelos de Series Temporales Univariantes: Modelos ARMA*. Notas de trabajo/ Working Notes.**

El artículo desarrolla una introducción didáctica y rigurosa al análisis de modelos estadísticos de series temporales univariantes, especificamente los procesos AR, MA y ARMA, mediante la metodología Box-Jenkins, basado en las etapas de identificación, estimación, diagnosis y predicción de modelos.

La aplicación permite trasladar parte de esa discusión teórica a un entorno interactivo, de forma que el lector pueda modificar parámetros, simular procesos y observar visualmente cómo cambia la dinámica temporal del modelo.

## Aplicación en línea

La aplicación puede ejecutarse en Streamlit Community Cloud:

[Acceder a la aplicación](https://arma-irf-simulator-jpsuygmgjdb6jaweagyvfu.streamlit.app/)

## Objetivo

El objetivo del proyecto es ofrecer una herramienta sencilla e interactiva para estudiar el comportamiento dinámico de modelos de series temporales univariantes:

* Modelos AR(p)
* Modelos MA(q)
* Modelos ARMA(p, q)
* Simulación de procesos estocásticos
* Estacionariedad
* Invertibilidad
* Funciones de respuesta al impulso
* Comparación entre IRF teórica e IRF estimada

La aplicación está pensada como apoyo visual y computacional al estudio de la econometría de series temporales.

## Relación con el artículo

El artículo asociado estudia los fundamentos de los modelos ARMA dentro del análisis de series temporales univariantes. En particular, aborda:

* la diferencia entre datos replicables y no replicables;
* la noción de estacionariedad en sentido débil;
* los procesos de ruido blanco;
* los procesos de media móvil MA(q);
* los procesos autorregresivos AR(p);
* la representación ARMA(p, q);
* la metodología Box-Jenkins;
* la identificación, estimación, diagnosis y predicción;
* la aplicación empírica a series del mercado laboral.

Este simulador no sustituye la explicación teórica del artículo. Su finalidad es complementarla mediante una herramienta interactiva que permita visualizar la dinámica de los procesos AR, MA y ARMA.

## Funcionalidades principales

La aplicación permite:

* seleccionar el tipo de modelo: AR, MA o ARMA;
* elegir el orden del proceso, con valores de `p` y `q` entre 1 y 5;
* modificar interactivamente los parámetros autorregresivos y de media móvil;
* simular una serie temporal artificial a partir del proceso especificado;
* configurar el tamaño muestral, la desviación típica de la innovación, el burn-in y la semilla aleatoria;
* comprobar automáticamente si el proceso AR es estacionario;
* comprobar automáticamente si el proceso MA es invertible;
* visualizar las raíces de los polinomios AR y MA;
* calcular la función de respuesta al impulso teórica;
* estimar un modelo ARIMA(p, 0, q) sobre la serie simulada;
* comparar la IRF teórica con la IRF estimada.

## Metodología

El simulador utiliza la clase `ArmaProcess` de `statsmodels` para construir el proceso ARMA definido por el usuario.

Dado un modelo ARMA(p, q):

```math
y_t =
\phi_1 y_{t-1}
+ \cdots
+ \phi_p y_{t-p}
+ \varepsilon_t
+ \theta_1 \varepsilon_{t-1}
+ \cdots
+ \theta_q \varepsilon_{t-q}
\quad
\varepsilon_t \sim WN(0, \sigma^2)
```

la aplicación genera una serie simulada y calcula la función de respuesta al impulso a partir de la representación MA infinita del proceso.

La **IRF teórica** se obtiene directamente del proceso AR, MA o ARMA introducido por el usuario.

La **IRF estimada** se obtiene ajustando un modelo `ARIMA(p, 0, q)` sobre la serie simulada y calculando posteriormente la respuesta al impulso del modelo estimado.

Las diferencias entre ambas respuestas pueden deberse al error muestral y al error de estimación.

## Instalación

Para ejecutar la aplicación en local, primero clona el repositorio:

```bash
git clone https://github.com/pmonrocle/ARMA-IRF-Simulator.git
cd ARMA-IRF-Simulator
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

El proyecto utiliza las siguientes librerías:

```txt
streamlit
numpy
matplotlib
statsmodels
```

## Estructura básica del repositorio

```text
ARMA-IRF-Simulator/
│
├── app.py
├── requirements.txt
├── README.md
└── .gitignore
└── paper
```

## Interpretación económica y estadística

La aplicación permite observar de forma intuitiva cómo los parámetros afectan a la dinámica del proceso.

Algunos ejemplos:

* un proceso AR con parámetros persistentes genera respuestas al impulso más duraderas;
* parámetros negativos pueden generar dinámicas oscilatorias;
* un proceso MA tiene memoria finita respecto a los shocks pasados;
* un proceso ARMA combina persistencia autorregresiva y propagación de innovaciones pasadas;
* la IRF estimada se aproxima mejor a la teórica cuando aumenta el tamaño muestral;
* las raíces del polinomio AR permiten evaluar la estacionariedad;
* las raíces del polinomio MA permiten evaluar la invertibilidad.

## Autor

**Pablo Monrocle Arribas**

## Referencia del artículo asociado

Monrocle Arribas, P. (2025). *Análisis de Modelos de Series Temporales Univariantes: Modelos ARMA*. Notas de trabajo/ Working Notes.

## Cómo citar este repositorio

Si se utiliza esta aplicación como material de apoyo, puede citarse como:

```bibtex
@misc{monrocle2025armairf,
  author = {Monrocle Arribas, Pablo},
  title = {Simulador AR / MA / ARMA e IRF},
  year = {2025},
  note = {Aplicación computacional complementaria del working note Análisis de Modelos de Series Temporales Univariantes: Modelos ARMA},
  url = {https://github.com/pmonrocle/ARMA-IRF-Simulator}
}
```

## Licencia

Este proyecto se publica con fines educativos y divulgativos.

El artículo asociado es un documento de trabajo del autor. Para citar o distribuir el artículo, debe respetarse la indicación establecida en el propio documento.
