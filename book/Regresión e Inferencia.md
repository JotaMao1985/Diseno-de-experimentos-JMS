---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---


# **Aspectos Estadísticos de la Regresión Lineal: Distribuciones, Inferencia y Métricas**

En esta sección, centraremos nuestra atención en los aspectos estadísticos clave de la regresión lineal, incluyendo las distribuciones de los estimadores, pruebas de hipótesis, intervalos de confianza y métricas como $R^2$ y $R^2_{adj}$.

---

## **1. Distribuciones de los Estimadores**

### **1.1. Distribución de los Estimadores de Coeficientes**

Los estimadores de los coeficientes en la regresión lineal, obtenidos mediante el método de mínimos cuadrados ordinarios (OLS), siguen distribuciones normales bajo ciertos supuestos:

- **Distribución del Intercepto ($\hat{\beta}_0$):**

  $$\hat{\beta}_0 \sim N\left(\beta_0, \sigma^2 \left( \frac{1}{n} + \frac{\bar{x}^2}{\sum (x_i - \bar{x})^2} \right) \right)$$

- **Distribución de la Pendiente ($\hat{\beta}_1$):**
  
  $$\hat{\beta}_1 \sim N\left(\beta_1, \frac{\sigma^2}{\sum (x_i - \bar{x})^2} \right)$$

Donde:
- $\sigma^2$ es la varianza del error.
- $\bar{x}$ es la media de la variable independiente $x$.

Estas distribuciones son útiles para realizar inferencia estadística sobre los coeficientes.

### **1.2. Distribución de los Residuos**

Los residuos en la regresión lineal, definidos como $e_i = y_i - \hat{y}_i$, siguen una distribución normal con media cero y varianza $\sigma^2$:

$$e_i \sim N(0, \sigma^2)$$

Esto implica que los residuos son independientes y idénticamente distribuidos (i.i.d.).

---

## **2. Pruebas de Hipótesis**

### **2.1. Prueba para el Intercepto ($\beta_0$)**

Hipótesis nula:

$$H_0: \beta_0 = 0 \quad \text{vs} \quad H_a: \beta_0 \neq 0$$

El estadístico t para esta prueba es:

$$t = \frac{\hat{\beta}_0}{\text{SE}(\hat{\beta}_0)}$$

Donde:

- $\text{SE}(\hat{\beta}_0)$ es la desviación estándar del estimador $\hat{\beta}_0$.

Si $|t| > t_{\alpha/2, n-2}$, rechazamos $H_0$.

### **2.2. Prueba para la Pendiente ($\beta_1$)**

Hipótesis nula:

$$H_0: \beta_1 = 0 \quad \text{vs} \quad H_a: \beta_1 \neq 0$$

El estadístico $t$ para esta prueba es:

$$t = \frac{\hat{\beta}_1}{\text{SE}(\hat{\beta}_1)}$$

Donde:
- $\text{SE}(\hat{\beta}_1)$ es la desviación estándar del estimador $\hat{\beta}_1$.

Si $|t| > t_{\alpha/2, n-2}$, rechazamos $H_0$.

### **2.3. Prueba F para el Modelo Completo**

Hipótesis nula:
$$H_0: \beta_1 = \beta_2 = \cdots = \beta_p = 0 \quad \text{vs} \quad H_a: \text{Al menos un } \beta_j \neq 0$$

El estadístico F para esta prueba es:

$$F = \frac{\text{MSR}}{\text{MSE}}$$

Donde:

- MSR (Mean Square Regression) es la suma de cuadrados de regresión dividida por el número de grados de libertad de regresión.
- MSE (Mean Square Error) es la suma de cuadrados residual dividida por el número de grados de libertad residual.

Si $F > F_{\alpha, p, n-p-1}$, rechazamos $H_0$.

---

## **3. Intervalos de Confianza**

### **3.1. Intervalo de Confianza para el Intercepto ($\beta_0$)**

El intervalo de confianza al $(1-\alpha)\%$ para el intercepto es:

$$\hat{\beta}_0 \pm t_{\alpha/2, n-2} \cdot \text{SE}(\hat{\beta}_0)$$

### **3.2. Intervalo de Confianza para la Pendiente ($\beta_1$)**

El intervalo de confianza al $(1-\alpha)\%$ para la pendiente es:

$$\hat{\beta}_1 \pm t_{\alpha/2, n-2} \cdot \text{SE}(\hat{\beta}_1)$$

---

## **4. Métricas de Ajuste del Modelo**

### **4.1. Coeficiente de Determinación ($R^2$)**

El **coeficiente de determinación ($R^2$)** mide la proporción de la varianza de la variable dependiente que se explica por el modelo:

$$R^2 = 1 - \frac{\text{SSE}}{\text{SST}}$$

Donde:

- $\text{SSE}$ es la suma de cuadrados residual.
- $\text{SST}$ es la suma de cuadrados total.

Un $R^2$ cercano a 1 indica que el modelo explica una gran parte de la variabilidad de la variable dependiente.

### **4.2. Coeficiente de Determinación Ajustado ($R^2_{adj}$)**

El **coeficiente de determinación ajustado ($R^2_{adj}$)** corrige el $R^2$ para tener en cuenta el número de variables independientes en el modelo:

$$R^2_{adj} = 1 - \left( \frac{n-1}{n-p-1} \right) (1 - R^2)$$

Donde:

- $n$ es el número de observaciones.
- $p$ es el número de variables independientes.

El $R^2_{adj}$ es útil para comparar modelos con diferentes números de variables independientes, ya que penaliza el uso de demasiadas variables.

### **4.3. Desventajas de $R^2$ y $R^2_{adj}$**

- **$R^2$ siempre aumenta con el número de variables independientes**, incluso si estas no son significativas.
- **$R^2_{adj}$** es más conservador, pero aún puede subestimar el ajuste real del modelo si hay demasiadas variables irrelevantes.

---

## **5. Distribución de $R^2$**

La distribución de $R^2$ sigue una distribución beta ajustada, pero para fines prácticos, podemos usar tablas de distribución $F$ para realizar inferencia sobre $R^2$.

### **5.1. Prueba para $R^2$**

Podemos realizar una prueba para verificar si el $R^2$ es significativamente diferente de cero. Esta prueba se basa en la distribución $F$:

$$F = \frac{R^2 / p}{(1 - R^2) / (n - p - 1)}$$

Donde:

- $p$ es el número de variables independientes.
- $n$ es el número de observaciones.

Si $F > F_{\alpha, p, n-p-1}$, rechazamos la hipótesis nula de que $R^2 = 0$.


