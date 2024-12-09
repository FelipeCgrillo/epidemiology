# Análisis Epidemiológico de Factores Asociados al Consumo de Tranquilizantes

Este repositorio contiene el análisis de la Encuesta Nacional de Salud Sexual (ENSSEX) para estudiar los factores asociados al consumo de tranquilizantes.

## Contenido

- `trabajo_final.Rmd`: Código R Markdown con el análisis completo
- `trabajo_final.html`: [Ver análisis interactivo en línea](https://felipecgrillo.github.io/epidemiology/trabajo_final.html)
- `trabajo_final.pdf`: Resultados del análisis en formato PDF

## Visualización en Línea

Puedes ver el análisis completo de forma interactiva [aquí](https://felipecgrillo.github.io/epidemiology/trabajo_final.html). La versión HTML incluye:
- Navegación interactiva con tabla de contenidos
- Código R desplegable
- Gráficos interactivos
- Mejor visualización de tablas

## Variables Analizadas

### Variable Dependiente
- Consumo de tranquilizantes

### Variables Independientes
#### Variables Categóricas:
1. Sexo al nacer
2. Nivel educacional
3. Bienestar emocional
4. Calidad de vida percibida
5. Satisfacción aspecto físico
6. Consumo de alcohol

#### Variables Numéricas:
1. Edad
2. IMC

## Metodología

1. Análisis descriptivo de variables
2. Modelado predictivo usando:
   - Random Forest
   - Regresión Logística
3. Evaluación de modelos mediante:
   - Sensibilidad
   - Especificidad
   - Valor predictivo positivo
   - Exactitud
4. Visualización mediante curvas ROC y cálculo de AUC

## Requisitos

Paquetes de R necesarios:
- dplyr
- caret
- randomForest
- pROC
- tidyverse
- haven

## Instalación

```R
# Instalar paquetes necesarios
install.packages(c("dplyr", "caret", "randomForest", "pROC", "tidyverse", "haven"))
```

## Uso

1. Clonar el repositorio
```bash
git clone https://github.com/FelipeCgrillo/epidemiology.git
```

2. Abrir `trabajo_final.Rmd` en RStudio

3. Ejecutar el análisis usando:
   - "Knit to HTML" para versión interactiva
   - "Knit to PDF" para versión PDF

## Resultados

Los resultados están disponibles en dos formatos:

### Versión HTML Interactiva
- [Ver análisis en línea](https://felipecgrillo.github.io/epidemiology/trabajo_final.html)
- Incluye navegación interactiva
- Código R desplegable
- Gráficos interactivos

### Versión PDF
- Disponible en `trabajo_final.pdf`
- Formato ideal para impresión
- Incluye:
  - Análisis descriptivo de todas las variables
  - Resultados de los modelos predictivos
  - Comparación de desempeño entre modelos
  - Visualizaciones y métricas de evaluación 