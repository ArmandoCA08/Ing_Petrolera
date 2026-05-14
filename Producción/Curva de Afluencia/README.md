# Curva de Afluencia

Aplicación desarrollada en **MATLAB App Designer** para calcular y visualizar curvas de comportamiento de afluencia de pozos petroleros mediante distintos modelos IPR. La herramienta permite ingresar datos de prueba presión-producción, seleccionar el sistema de unidades, calcular gastos máximos y comparar gráficamente los métodos implementados.

## Autor

**Armando CA**

## Captura de la aplicación

![Captura de ventana de la aplicación](Images/CurvadeAfluencia%20captura%20de%20ventana%20app%20dark%20mode.png)

## Características principales

- Cálculo del índice de productividad.
- Construcción de curvas IPR para diferentes métodos.
- Comparación gráfica de curvas de afluencia.
- Tabla de resultados para mostrar `Qo max` por método.
- Selección de sistema de unidades:
  - **Inglés:** presión en `psi` y gasto en `STB/d`.
  - **Métrico:** presión en `kg/cm²` y gasto en `m³/d`.
- Conversión automática de resultados para visualización.

## Datos de entrada

| Variable | Descripción | Unidades en sistema inglés | Unidades en sistema métrico |
|---|---|---:|---:|
| `Pb` | Presión de burbuja | `psi` | `kg/cm²` |
| `Pwf` | Presión de fondo fluyente | `psi` | `kg/cm²` |
| `Pws` | Presión de fondo estática | `psi` | `kg/cm²` |
| `Qo` | Gasto de aceite medido | `STB/d` | `m³/d` |
| `EF` | Eficiencia de flujo | adimensional | adimensional |

## Métodos implementados

### 1. Método de Moore

El índice de productividad se calcula como:

$$
J = \frac{q_o}{P_{ws} - P_{wf}}
$$

El gasto máximo se obtiene mediante:

$$
q_{o\,max} = J P_{ws}
$$

La curva de gasto para diferentes valores de presión se calcula con:

$$
q_o = J(P_{ws} - P_{wf})
$$

### 2. Método de Vogel

El modelo de Vogel se utiliza para estimar el comportamiento de afluencia en yacimientos con flujo bifásico. La relación adimensional se expresa como:

$$
\frac{q_o}{q_{o\,max}} = 1 - 0.2\left(\frac{P_{wf}}{P_{ws}}\right) - 0.8\left(\frac{P_{wf}}{P_{ws}}\right)^2
$$

Despejando el gasto máximo:

$$
q_{o\,max} = \frac{q_o}{1 - 0.2\left(\frac{P_{wf}}{P_{ws}}\right) - 0.8\left(\frac{P_{wf}}{P_{ws}}\right)^2}
$$

Para construir la curva IPR:

$$
q_o = q_{o\,max}\left[1 - 0.2\left(\frac{P_{wf}}{P_{ws}}\right) - 0.8\left(\frac{P_{wf}}{P_{ws}}\right)^2\right]
$$

### 3. Método de Standing

Para considerar una eficiencia de flujo diferente de uno, se calcula una presión corregida:

$$
P'_{wf} = P_{ws} - (P_{ws} - P_{wf})EF
$$

La curva corregida se expresa como:

$$
q_o = q_{o\,max}\left[1 - 0.2\left(\frac{P'_{wf}}{P_{ws}}\right) - 0.8\left(\frac{P'_{wf}}{P_{ws}}\right)^2\right]
$$

### 4. Método de Harrison

El método de Harrison se aplica cuando la presión corregida `P'wf` toma valores negativos. El gasto máximo se calcula como:

$$
q_{o\,max} = \frac{q_o}{1.2 - 0.2e^{1.792\left(\frac{P'_{wf}}{P_{ws}}\right)}}
$$

La curva de gasto queda definida por:

$$
q_o = q_{o\,max}\left[1.2 - 0.2e^{1.792\left(\frac{P'_{wf}}{P_{ws}}\right)}\right]
$$

### 5. Método de Vogel generalizado

Primero se calcula el gasto a la presión de burbuja:

$$
q_b = J(P_{ws} - P_b)
$$

Posteriormente, para presiones menores o iguales a la presión de burbuja:

$$
q_o = q_b + \frac{JP_b}{1.8}\left[1 - 0.2\left(\frac{P_{wf}}{P_b}\right) - 0.8\left(\frac{P_{wf}}{P_b}\right)^2\right]
$$

## Conversión de unidades

Los cálculos internos se realizan en sistema inglés. Cuando el usuario selecciona el sistema métrico, la aplicación convierte los datos y resultados mediante los siguientes factores:

$$
1\ \text{kg/cm}^2 = 14.2233\ \text{psi}
$$

$$
1\ \text{m}^3/\text{d} = 6.28981\ \text{STB/d}
$$

Conversión de presión de sistema métrico a sistema inglés:

$$
P_{psi} = P_{kg/cm^2}(14.2233)
$$

Conversión de gasto de sistema métrico a sistema inglés:

$$
q_{STB/d} = q_{m^3/d}(6.28981)
$$

Conversión de presión de sistema inglés a sistema métrico:

$$
P_{kg/cm^2} = \frac{P_{psi}}{14.2233}
$$

Conversión de gasto de sistema inglés a sistema métrico:

$$
q_{m^3/d} = \frac{q_{STB/d}}{6.28981}
$$

## Flujo general de la aplicación

1. El usuario selecciona el sistema de unidades.
2. Ingresa los datos de la prueba presión-producción.
3. Presiona el botón **Calcular IPR**.
4. La aplicación valida los datos de entrada.
5. Se calculan las curvas IPR y los gastos máximos.
6. Se muestran los resultados en la tabla.
7. Se grafican las curvas comparativas en la ventana principal.
8. El usuario puede cambiar el sistema de unidades para visualizar los resultados convertidos.


## Requisitos

- MATLAB.
- App Designer.
- Archivo principal de la aplicación: `CurvadeAfluencia.mlapp`.

## Nota

Esta aplicación tiene fines académicos y de apoyo al análisis de comportamiento de afluencia en pozos petroleros.
