---
title: "Análisis Epidemiológico ENSSEX"
author: "Felipe Carrasco"
date: "2024-12-09"
output:
  html_document:
    theme: cosmo
    highlight: tango
    toc: true
    toc_float:
      collapsed: false
      smooth_scroll: true
    code_folding: show
    df_print: paged
    fig_width: 10
    fig_height: 6
    fig_caption: true
    number_sections: true
    self_contained: true
---





## 0. Verificación de Paquetes y Datos


``` r
# Verificar la existencia del archivo de datos
archivo_datos <- "20240516_enssex_data.rdata"
if (!file.exists(archivo_datos)) {
  stop("Error: No se encuentra el archivo de datos '", archivo_datos, 
       "' en el directorio de trabajo actual: ", getwd())
}

# Mostrar información del entorno
cat("\nDirectorio de trabajo actual:", getwd(), "\n")
```

```
## 
## Directorio de trabajo actual: /Users/felipecarrasco/Library/Mobile Documents/com~apple~CloudDocs/Magíster/MAGISTER/ASIGNATURAS/II SEMESTRE/EPIDEMiOLOGIA II/Clases_profesor_Amaru_aguero/Trabajo/Proyecto_trabajo
```

``` r
cat("Archivo de datos encontrado:", archivo_datos, "\n")
```

```
## Archivo de datos encontrado: 20240516_enssex_data.rdata
```

## 1. Definición de Variables


``` r
# Definir la variable dependiente
var_dependiente <- c("depresion")

# Definir las variables independientes a utilizar
vars_categoricas <- c("sexo_al_nacer", "nivel_educacional", "bienestar_emocional", 
                     "calidad_vida_percibida", "satisfaccion_aspecto_fisico",
                     "consumo_tranquilizantes", "consumo_alcohol")
vars_numericas <- c("edad", "peso", "talla")

# Descripción de la variable dependiente
cat("\nDescripción de la variable dependiente:\n")
```

```
## 
## Descripción de la variable dependiente:
```

``` r
cat("\n1. ¿Alguna vez un doctor o médico le ha dicho que tiene o que padece de depresión?")
```

```
## 
## 1. ¿Alguna vez un doctor o médico le ha dicho que tiene o que padece de depresión?
```

``` r
cat("\n   - SI")
```

```
## 
##    - SI
```

``` r
cat("\n   - NO\n")
```

```
## 
##    - NO
```

``` r
# Descripción de las variables independientes categóricas
cat("\nDescripción de Variables Independientes Categóricas:\n")
```

```
## 
## Descripción de Variables Independientes Categóricas:
```

``` r
cat("\n1. Sexo al nacer:")
```

```
## 
## 1. Sexo al nacer:
```

``` r
cat("\n   - Hombre (1)")
```

```
## 
##    - Hombre (1)
```

``` r
cat("\n   - Mujer (2)")
```

```
## 
##    - Mujer (2)
```

``` r
cat("\n\n2. Nivel educacional:")
```

```
## 
## 
## 2. Nivel educacional:
```

``` r
cat("\n   - 1: Nunca asistió")
```

```
## 
##    - 1: Nunca asistió
```

``` r
cat("\n   - 2: Sala cuna")
```

```
## 
##    - 2: Sala cuna
```

``` r
cat("\n   - 3: Jardín Infantil (medio menor y medio mayor)")
```

```
## 
##    - 3: Jardín Infantil (medio menor y medio mayor)
```

``` r
cat("\n   - 4: Pre-kinder /Kinder (Transición Menor y Transición Mayor)")
```

```
## 
##    - 4: Pre-kinder /Kinder (Transición Menor y Transición Mayor)
```

``` r
cat("\n   - 5: Educación Especial (Diferencial)")
```

```
## 
##    - 5: Educación Especial (Diferencial)
```

``` r
cat("\n   - 6: Primario o Preparatoria (Sistema antiguo)")
```

```
## 
##    - 6: Primario o Preparatoria (Sistema antiguo)
```

``` r
cat("\n   - 7: Educación Básica")
```

```
## 
##    - 7: Educación Básica
```

``` r
cat("\n   - 8: Humanidades (Sistema Antiguo)")
```

```
## 
##    - 8: Humanidades (Sistema Antiguo)
```

``` r
cat("\n   - 9: Educación Media Científico-Humanista")
```

```
## 
##    - 9: Educación Media Científico-Humanista
```

``` r
cat("\n   - 10: Técnica Comercial, Industrial o Normalista (Sistema Antiguo)")
```

```
## 
##    - 10: Técnica Comercial, Industrial o Normalista (Sistema Antiguo)
```

``` r
cat("\n   - 11: Educación Media Técnica Profesional")
```

```
## 
##    - 11: Educación Media Técnica Profesional
```

``` r
cat("\n   - 12: Técnico Nivel Superior Incompleto (carreras de 1 a 3 años)")
```

```
## 
##    - 12: Técnico Nivel Superior Incompleto (carreras de 1 a 3 años)
```

``` r
cat("\n   - 13: Técnico Nivel Superior Completo (carreras de 1 a 3 años)")
```

```
## 
##    - 13: Técnico Nivel Superior Completo (carreras de 1 a 3 años)
```

``` r
cat("\n   - 14: Profesional Incompleto (carreras de 4 o más años)")
```

```
## 
##    - 14: Profesional Incompleto (carreras de 4 o más años)
```

``` r
cat("\n   - 15: Profesional Completo (carreras de 4 o más años)")
```

```
## 
##    - 15: Profesional Completo (carreras de 4 o más años)
```

``` r
cat("\n   - 16: Postgrado incompleto")
```

```
## 
##    - 16: Postgrado incompleto
```

``` r
cat("\n   - 17: Postgrado completo")
```

```
## 
##    - 17: Postgrado completo
```

``` r
cat("\n\n3. Bienestar emocional:")
```

```
## 
## 
## 3. Bienestar emocional:
```

``` r
cat("\n   - 1: Muy mal")
```

```
## 
##    - 1: Muy mal
```

``` r
cat("\n   - 2-6: Niveles intermedios")
```

```
## 
##    - 2-6: Niveles intermedios
```

``` r
cat("\n   - 7: Muy bien")
```

```
## 
##    - 7: Muy bien
```

``` r
cat("\n\n4. Calidad de vida percibida:")
```

```
## 
## 
## 4. Calidad de vida percibida:
```

``` r
cat("\n   - 1: Muy mala")
```

```
## 
##    - 1: Muy mala
```

``` r
cat("\n   - 2: Mala")
```

```
## 
##    - 2: Mala
```

``` r
cat("\n   - 3: Ni buena ni mala")
```

```
## 
##    - 3: Ni buena ni mala
```

``` r
cat("\n   - 4: Buena")
```

```
## 
##    - 4: Buena
```

``` r
cat("\n   - 5: Muy buena")
```

```
## 
##    - 5: Muy buena
```

``` r
cat("\n   - 8: No sabe")
```

```
## 
##    - 8: No sabe
```

``` r
cat("\n   - 9: No responde")
```

```
## 
##    - 9: No responde
```

``` r
cat("\n\n5. Satisfacción aspecto físico:")
```

```
## 
## 
## 5. Satisfacción aspecto físico:
```

``` r
cat("\n   - 1: Muy en desacuerdo")
```

```
## 
##    - 1: Muy en desacuerdo
```

``` r
cat("\n   - 2: En desacuerdo")
```

```
## 
##    - 2: En desacuerdo
```

``` r
cat("\n   - 3: Ni de acuerdo, ni en desacuerdo")
```

```
## 
##    - 3: Ni de acuerdo, ni en desacuerdo
```

``` r
cat("\n   - 4: De acuerdo")
```

```
## 
##    - 4: De acuerdo
```

``` r
cat("\n   - 5: Muy de acuerdo")
```

```
## 
##    - 5: Muy de acuerdo
```

``` r
cat("\n   - 8: NS")
```

```
## 
##    - 8: NS
```

``` r
cat("\n   - 9: NR")
```

```
## 
##    - 9: NR
```

``` r
cat("\n\n6. Consumo de alcohol:")
```

```
## 
## 
## 6. Consumo de alcohol:
```

``` r
cat("\n   - 1: Durante los últimos 30 días")
```

```
## 
##    - 1: Durante los últimos 30 días
```

``` r
cat("\n   - 2: Hace más de un mes, pero menos de un año")
```

```
## 
##    - 2: Hace más de un mes, pero menos de un año
```

``` r
cat("\n   - 3: Hace más de un año")
```

```
## 
##    - 3: Hace más de un año
```

``` r
cat("\n   - 9: NS/NR")
```

```
## 
##    - 9: NS/NR
```

``` r
cat("\n\n7. Consumo de tranquilizantes:")
```

```
## 
## 
## 7. Consumo de tranquilizantes:
```

``` r
cat("\n   - Si (1)")
```

```
## 
##    - Si (1)
```

``` r
cat("\n   - No (2)")
```

```
## 
##    - No (2)
```

``` r
# Descripción de las variables independientes numéricas
cat("\n\nDescripción de Variables Independientes Numéricas:\n")
```

```
## 
## 
## Descripción de Variables Independientes Numéricas:
```

``` r
cat("\n1. Edad (años)")
```

```
## 
## 1. Edad (años)
```

``` r
cat("\n2. Peso (kg)")
```

```
## 
## 2. Peso (kg)
```

``` r
cat("\n3. Talla (cm)\n")
```

```
## 
## 3. Talla (cm)
```

## 2. Preparación y Análisis Descriptivo de los Datos

### 2.1 Análisis de Variable Dependiente


``` r
# Cargar datos
load('20240516_enssex_data.rdata')

# Función para limpiar valores numéricos
limpiar_numerico <- function(x) {
  x <- as.numeric(x)
  x[!is.finite(x)] <- NA
  return(x)
}

# Crear variables necesarias
datos <- enssex4 %>%
  mutate(
    # Variable dependiente
    depresion = factor(as.numeric(i_1_p18a2), levels = c(1, 2), labels = c("Si", "No")),
    
    # Variables categóricas independientes
    sexo_al_nacer = factor(as.numeric(p1), levels = c(1, 2), labels = c("Hombre", "Mujer")),
    nivel_educacional = factor(as.numeric(p5)),
    bienestar_emocional = factor(as.numeric(i_2_p9)),
    calidad_vida_percibida = factor(as.numeric(p8)),
    satisfaccion_aspecto_fisico = factor(as.numeric(i_1_p24)),
    consumo_tranquilizantes = factor(as.numeric(i_4_p25), levels = c(1, 2), labels = c("Si", "No")),
    consumo_alcohol = factor(as.numeric(i_5_p26)),
    
    # Variables numéricas independientes
    edad = limpiar_numerico(p4),
    peso = limpiar_numerico(p22),
    talla = limpiar_numerico(p23)
  )

# Análisis descriptivo de la variable dependiente
cat("\n### Análisis de Variable Dependiente (Depresión):\n")
```

```
## 
## ### Análisis de Variable Dependiente (Depresión):
```

``` r
tabla_depresion <- table(datos$depresion, useNA = "ifany")
prop_depresion <- prop.table(tabla_depresion) * 100

# Crear tabla de depresión
knitr::kable(
  data.frame(
    Categoría = names(tabla_depresion),
    Frecuencia = as.numeric(tabla_depresion),
    Porcentaje = round(as.numeric(prop_depresion), 2)
  ),
  caption = "Distribución de Depresión",
  col.names = c("Categoría", "Frecuencia", "Porcentaje (%)"),
  align = c("l", "r", "r")
)
```



Table: Distribución de Depresión

|Categoría | Frecuencia| Porcentaje (%)|
|:---------|----------:|--------------:|
|Si        |       3829|          18.78|
|No        |      16365|          80.25|
|NA        |        198|           0.97|

``` r
# Gráfico de depresión
ggplot(data = datos, aes(x = depresion, fill = depresion)) +
  geom_bar() +
  labs(
    title = "Distribución de Depresión en la Población",
    subtitle = "Basado en diagnóstico médico reportado",
    x = "Diagnóstico de Depresión",
    y = "Número de Personas",
    caption = "Fuente: Encuesta Nacional de Salud Sexual (ENSSEX)"
  ) +
  theme_minimal() +
  scale_fill_brewer(palette = "Set2") +
  theme(
    plot.title = element_text(hjust = 0.5, size = 14, face = "bold"),
    plot.subtitle = element_text(hjust = 0.5, size = 12),
    axis.title = element_text(size = 11),
    legend.title = element_text(size = 10),
    legend.position = "bottom"
  )
```

<img src="trabajo_final_files/figure-html/analisis_dependiente-1.png" width="100%" style="display: block; margin: auto;" />

### 2.2 Análisis de Variables Categóricas


``` r
# Análisis de variables categóricas
cat("\n### Análisis de Variables Categóricas:\n")
```

```
## 
## ### Análisis de Variables Categóricas:
```

``` r
# Función para crear tabla y gráfico de variable categórica
analizar_categorica <- function(datos, variable, titulo) {
  # Tabla
  tabla <- table(datos[[variable]], useNA = "ifany")
  prop <- prop.table(tabla) * 100
  
  cat(paste("\n#### ", titulo, ":\n"))
  
  # Crear tabla
  knitr::kable(
    data.frame(
      Categoría = names(tabla),
      Frecuencia = as.numeric(tabla),
      Porcentaje = round(as.numeric(prop), 2)
    ),
    caption = paste("Distribución de", titulo),
    col.names = c("Categoría", "Frecuencia", "Porcentaje (%)"),
    align = c("l", "r", "r")
  )
  
  # Gráfico
  print(
    ggplot(data = datos, aes_string(x = variable, fill = variable)) +
      geom_bar() +
      labs(
        title = paste("Distribución de", titulo),
        subtitle = "Análisis de frecuencias por categoría",
        x = titulo,
        y = "Número de Personas",
        caption = "Fuente: ENSSEX"
      ) +
      theme_minimal() +
      theme(
        axis.text.x = element_text(angle = 45, hjust = 1),
        plot.title = element_text(hjust = 0.5, size = 14, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, size = 12),
        axis.title = element_text(size = 11),
        legend.position = "none"
      ) +
      scale_fill_brewer(palette = "Set3")
  )
}

# Analizar cada variable categórica
vars_cat <- c("sexo_al_nacer", "nivel_educacional", "bienestar_emocional",
              "calidad_vida_percibida", "satisfaccion_aspecto_fisico",
              "consumo_tranquilizantes", "consumo_alcohol")

titulos_cat <- c("Sexo al Nacer", "Nivel Educacional", "Bienestar Emocional",
                 "Calidad de Vida Percibida", "Satisfacción Aspecto Físico",
                 "Consumo de Tranquilizantes", "Consumo de Alcohol")

for(i in seq_along(vars_cat)) {
  analizar_categorica(datos, vars_cat[i], titulos_cat[i])
}
```

```
## 
## ####  Sexo al Nacer :
```

<img src="trabajo_final_files/figure-html/analisis_categoricas-1.png" width="100%" style="display: block; margin: auto;" />

```
## 
## ####  Nivel Educacional :
```

<img src="trabajo_final_files/figure-html/analisis_categoricas-2.png" width="100%" style="display: block; margin: auto;" />

```
## 
## ####  Bienestar Emocional :
```

<img src="trabajo_final_files/figure-html/analisis_categoricas-3.png" width="100%" style="display: block; margin: auto;" />

```
## 
## ####  Calidad de Vida Percibida :
```

<img src="trabajo_final_files/figure-html/analisis_categoricas-4.png" width="100%" style="display: block; margin: auto;" />

```
## 
## ####  Satisfacción Aspecto Físico :
```

<img src="trabajo_final_files/figure-html/analisis_categoricas-5.png" width="100%" style="display: block; margin: auto;" />

```
## 
## ####  Consumo de Tranquilizantes :
```

<img src="trabajo_final_files/figure-html/analisis_categoricas-6.png" width="100%" style="display: block; margin: auto;" />

```
## 
## ####  Consumo de Alcohol :
```

<img src="trabajo_final_files/figure-html/analisis_categoricas-7.png" width="100%" style="display: block; margin: auto;" />

### 2.3 Análisis de Variables Numéricas


``` r
# Análisis de variables numéricas
cat("\n### Análisis de Variables Numéricas:\n")
```

```
## 
## ### Análisis de Variables Numéricas:
```

``` r
# Función para crear resumen y gráfico de variable numérica
analizar_numerica <- function(datos, variable, titulo) {
  # Resumen estadístico
  resumen <- summary(datos[[variable]])
  sd_val <- sd(datos[[variable]], na.rm = TRUE)
  
  cat(paste("\n#### ", titulo, ":\n"))
  
  # Crear tabla de resumen
  knitr::kable(
    data.frame(
      Estadístico = c("Mínimo", "1er Cuartil", "Mediana", "Media", "3er Cuartil", "Máximo", "Desv. Est."),
      Valor = c(as.numeric(resumen), round(sd_val, 2))
    ),
    caption = paste("Resumen estadístico de", titulo),
    align = c("l", "r")
  )
  
  # Histograma
  print(
    ggplot(data = datos, aes_string(x = variable)) +
      geom_histogram(aes(y = ..density..), bins = 30, fill = "skyblue", color = "black") +
      geom_density(color = "red", size = 1) +
      labs(
        title = paste("Distribución de", titulo),
        subtitle = "Histograma y curva de densidad",
        x = titulo,
        y = "Densidad",
        caption = "La línea roja representa la curva de densidad"
      ) +
      theme_minimal() +
      theme(
        plot.title = element_text(hjust = 0.5, size = 14, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, size = 12),
        axis.title = element_text(size = 11)
      )
  )
  
  # Boxplot
  print(
    ggplot(data = datos, aes_string(y = variable)) +
      geom_boxplot(fill = "skyblue") +
      labs(
        title = paste("Diagrama de Caja de", titulo),
        subtitle = "Visualización de la distribución y valores atípicos",
        y = titulo,
        caption = "Los puntos representan valores atípicos"
      ) +
      theme_minimal() +
      theme(
        plot.title = element_text(hjust = 0.5, size = 14, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, size = 12),
        axis.title = element_text(size = 11)
      )
  )
}

# Analizar cada variable numérica
vars_num <- c("edad", "peso", "talla")
titulos_num <- c("Edad (años)", "Peso (kg)", "Talla (cm)")

for(i in seq_along(vars_num)) {
  analizar_numerica(datos, vars_num[i], titulos_num[i])
}
```

```
## 
## ####  Edad (años) :
```

<img src="trabajo_final_files/figure-html/analisis_numericas-1.png" width="100%" style="display: block; margin: auto;" /><img src="trabajo_final_files/figure-html/analisis_numericas-2.png" width="100%" style="display: block; margin: auto;" />

```
## 
## ####  Peso (kg) :
```

<img src="trabajo_final_files/figure-html/analisis_numericas-3.png" width="100%" style="display: block; margin: auto;" /><img src="trabajo_final_files/figure-html/analisis_numericas-4.png" width="100%" style="display: block; margin: auto;" />

```
## 
## ####  Talla (cm) :
```

<img src="trabajo_final_files/figure-html/analisis_numericas-5.png" width="100%" style="display: block; margin: auto;" /><img src="trabajo_final_files/figure-html/analisis_numericas-6.png" width="100%" style="display: block; margin: auto;" />

### 2.4 Análisis Bivariado


``` r
# Análisis bivariado con la variable dependiente
cat("\n### Análisis Bivariado con Depresión:\n")
```

```
## 
## ### Análisis Bivariado con Depresión:
```

``` r
# Para variables categóricas
for(i in seq_along(vars_cat)) {
  cat(paste("\n#### Depresión vs", titulos_cat[i], ":\n"))
  
  # Tabla de contingencia
  tabla_cont <- table(datos$depresion, datos[[vars_cat[i]]])
  print(knitr::kable(tabla_cont, 
                     caption = paste("Tabla de contingencia: Depresión vs", titulos_cat[i])))
  
  # Test Chi-cuadrado
  chi_test <- chisq.test(tabla_cont)
  cat("\nTest Chi-cuadrado:\n")
  print(chi_test)
  
  # Gráfico de barras apiladas
  print(
    ggplot(datos, aes_string(x = vars_cat[i], fill = "depresion")) +
      geom_bar(position = "fill") +
      labs(
        title = paste("Relación entre Depresión y", titulos_cat[i]),
        subtitle = "Proporción de casos por categoría",
        x = titulos_cat[i],
        y = "Proporción",
        fill = "Diagnóstico de Depresión",
        caption = "Fuente: ENSSEX"
      ) +
      theme_minimal() +
      theme(
        axis.text.x = element_text(angle = 45, hjust = 1),
        plot.title = element_text(hjust = 0.5, size = 14, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, size = 12),
        axis.title = element_text(size = 11),
        legend.position = "bottom"
      )
  )
}
```

```
## 
## #### Depresión vs Sexo al Nacer :
## 
## 
## Table: Tabla de contingencia: Depresión vs Sexo al Nacer
## 
## |   | Hombre| Mujer|
## |:--|------:|-----:|
## |Si |    657|  3172|
## |No |   6107| 10258|
## 
## Test Chi-cuadrado:
## 
## 	Pearson's Chi-squared test with Yates' continuity correction
## 
## data:  tabla_cont
## X-squared = 565.18, df = 1, p-value < 2.2e-16
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-1.png" width="100%" style="display: block; margin: auto;" />

```
## 
## #### Depresión vs Nivel Educacional :
## 
## 
## Table: Tabla de contingencia: Depresión vs Nivel Educacional
## 
## |   |   1|  3|  5|   6|    7|   8|    9|  10|   11|  12|   13|   14|   15| 16|  17|
## |:--|---:|--:|--:|---:|----:|---:|----:|---:|----:|---:|----:|----:|----:|--:|---:|
## |Si |  48|  0|  1| 126|  775| 130| 1176|  84|  287| 153|  323|  249|  424| 16|  37|
## |No | 145|  1|  9| 390| 2363| 706| 5657| 437| 1387| 677| 1476| 1083| 1869| 42| 123|
## 
## Test Chi-cuadrado:
## 
## 	Pearson's Chi-squared test
## 
## data:  tabla_cont
## X-squared = 114.96, df = 14, p-value < 2.2e-16
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-2.png" width="100%" style="display: block; margin: auto;" />

```
## 
## #### Depresión vs Bienestar Emocional :
## 
## 
## Table: Tabla de contingencia: Depresión vs Bienestar Emocional
## 
## |   |   1|   2|   3|    4|    5|    6|    7|  9|
## |:--|---:|---:|---:|----:|----:|----:|----:|--:|
## |Si | 187| 145| 331|  721| 1077|  823|  542|  3|
## |No | 131| 144| 475| 1660| 3919| 5192| 4816| 28|
## 
## Test Chi-cuadrado:
## 
## 	Pearson's Chi-squared test
## 
## data:  tabla_cont
## X-squared = 1372.2, df = 7, p-value < 2.2e-16
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-3.png" width="100%" style="display: block; margin: auto;" />

```
## 
## #### Depresión vs Calidad de Vida Percibida :
## 
## 
## Table: Tabla de contingencia: Depresión vs Calidad de Vida Percibida
## 
## |   |   1|   2|    3|    4|    5|  8|  9|
## |:--|---:|---:|----:|----:|----:|--:|--:|
## |Si |  46| 199| 1264| 2011|  300|  6|  3|
## |No | 123| 324| 3512| 9880| 2493| 23| 10|
## 
## Test Chi-cuadrado:
## 
## 	Pearson's Chi-squared test
## 
## data:  tabla_cont
## X-squared = 462.08, df = 6, p-value < 2.2e-16
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-4.png" width="100%" style="display: block; margin: auto;" />

```
## 
## #### Depresión vs Satisfacción Aspecto Físico :
## 
## 
## Table: Tabla de contingencia: Depresión vs Satisfacción Aspecto Físico
## 
## |   |   1|    2|    3|    4|    5|  8|  9|
## |:--|---:|----:|----:|----:|----:|--:|--:|
## |Si | 151|  742|  717| 1843|  370|  5|  1|
## |No | 359| 1534| 3042| 9277| 2104| 37| 12|
## 
## Test Chi-cuadrado:
## 
## 	Pearson's Chi-squared test
## 
## data:  tabla_cont
## X-squared = 382.74, df = 6, p-value < 2.2e-16
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-5.png" width="100%" style="display: block; margin: auto;" />

```
## 
## #### Depresión vs Consumo de Tranquilizantes :
## 
## 
## Table: Tabla de contingencia: Depresión vs Consumo de Tranquilizantes
## 
## |   |   Si|    No|
## |:--|----:|-----:|
## |Si | 1751|  2056|
## |No |  952| 15264|
## 
## Test Chi-cuadrado:
## 
## 	Pearson's Chi-squared test with Yates' continuity correction
## 
## data:  tabla_cont
## X-squared = 4247.2, df = 1, p-value < 2.2e-16
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-6.png" width="100%" style="display: block; margin: auto;" />

```
## 
## #### Depresión vs Consumo de Alcohol :
## 
## 
## Table: Tabla de contingencia: Depresión vs Consumo de Alcohol
## 
## |   |    1|    2|    3|  9|
## |:--|----:|----:|----:|--:|
## |Si | 1725|  498|  470|  3|
## |No | 7340| 1913| 1262| 15|
## 
## Test Chi-cuadrado:
## 
## 	Pearson's Chi-squared test
## 
## data:  tabla_cont
## X-squared = 59.173, df = 3, p-value = 8.831e-13
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-7.png" width="100%" style="display: block; margin: auto;" />

``` r
# Para variables numéricas
for(i in seq_along(vars_num)) {
  cat(paste("\n#### Depresión vs", titulos_num[i], ":\n"))
  
  # Test t
  t_test <- t.test(datos[[vars_num[i]]] ~ datos$depresion)
  cat("\nTest t:\n")
  print(t_test)
  
  # Boxplot
  print(
    ggplot(datos, aes_string(x = "depresion", y = vars_num[i], fill = "depresion")) +
      geom_boxplot() +
      labs(
        title = paste("Comparación de", titulos_num[i], "según Diagnóstico de Depresión"),
        subtitle = "Distribución y valores atípicos por grupo",
        x = "Diagnóstico de Depresión",
        y = titulos_num[i],
        caption = "Los puntos representan valores atípicos"
      ) +
      theme_minimal() +
      theme(
        plot.title = element_text(hjust = 0.5, size = 14, face = "bold"),
        plot.subtitle = element_text(hjust = 0.5, size = 12),
        axis.title = element_text(size = 11),
        legend.position = "none"
      )
  )
}
```

```
## 
## #### Depresión vs Edad (años) :
## 
## Test t:
## 
## 	Welch Two Sample t-test
## 
## data:  datos[[vars_num[i]]] by datos$depresion
## t = 12.458, df = 5912.1, p-value < 2.2e-16
## alternative hypothesis: true difference in means between group Si and group No is not equal to 0
## 95 percent confidence interval:
##  3.324843 4.566644
## sample estimates:
## mean in group Si mean in group No 
##         48.19169         44.24595
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-8.png" width="100%" style="display: block; margin: auto;" />

```
## 
## #### Depresión vs Peso (kg) :
## 
## Test t:
## 
## 	Welch Two Sample t-test
## 
## data:  datos[[vars_num[i]]] by datos$depresion
## t = 0.96198, df = 5622.4, p-value = 0.3361
## alternative hypothesis: true difference in means between group Si and group No is not equal to 0
## 95 percent confidence interval:
##  -0.3599752  1.0536571
## sample estimates:
## mean in group Si mean in group No 
##         71.74171         71.39487
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-9.png" width="100%" style="display: block; margin: auto;" />

```
## 
## #### Depresión vs Talla (cm) :
## 
## Test t:
## 
## 	Welch Two Sample t-test
## 
## data:  datos[[vars_num[i]]] by datos$depresion
## t = -8.2629, df = 5530.1, p-value < 2.2e-16
## alternative hypothesis: true difference in means between group Si and group No is not equal to 0
## 95 percent confidence interval:
##  -4.996640 -3.080358
## sample estimates:
## mean in group Si mean in group No 
##         155.4928         159.5313
```

<img src="trabajo_final_files/figure-html/analisis_bivariado-10.png" width="100%" style="display: block; margin: auto;" />

## 3. Preparación para Modelado

### 3.1 Selección de Variables


``` r
# Seleccionar solo las variables necesarias para el modelo
variables_modelo <- c(
  "depresion", "sexo_al_nacer", "nivel_educacional", "bienestar_emocional",
  "calidad_vida_percibida", "satisfaccion_aspecto_fisico", "consumo_tranquilizantes",
  "consumo_alcohol", "edad", "peso", "talla"
)

# Crear conjunto de datos para modelado
datos_modelo <- datos[, variables_modelo]

# Manejar valores faltantes
cat("\n### Análisis de valores faltantes:\n")
```

```
## 
## ### Análisis de valores faltantes:
```

``` r
na_summary <- colSums(is.na(datos_modelo))
knitr::kable(
  data.frame(
    Variable = names(na_summary),
    Valores_Faltantes = as.numeric(na_summary),
    Porcentaje = round(as.numeric(na_summary) / nrow(datos_modelo) * 100, 2)
  ),
  caption = "Resumen de valores faltantes por variable",
  col.names = c("Variable", "Valores Faltantes", "Porcentaje (%)"),
  align = c("l", "r", "r")
)
```



Table: Resumen de valores faltantes por variable

|Variable                    | Valores Faltantes| Porcentaje (%)|
|:---------------------------|-----------------:|--------------:|
|depresion                   |               198|           0.97|
|sexo_al_nacer               |                 0|           0.00|
|nivel_educacional           |                 0|           0.00|
|bienestar_emocional         |                 0|           0.00|
|calidad_vida_percibida      |                 0|           0.00|
|satisfaccion_aspecto_fisico |                 0|           0.00|
|consumo_tranquilizantes     |               183|           0.90|
|consumo_alcohol             |              7068|          34.66|
|edad                        |                 0|           0.00|
|peso                        |                 0|           0.00|
|talla                       |                 0|           0.00|

``` r
# Eliminar filas con valores faltantes
datos_modelo <- na.omit(datos_modelo)

cat("\n### Dimensiones del conjunto de datos después de eliminar valores faltantes:\n")
```

```
## 
## ### Dimensiones del conjunto de datos después de eliminar valores faltantes:
```

``` r
knitr::kable(
  data.frame(
    Métrica = c("Número de filas", "Número de columnas"),
    Valor = c(nrow(datos_modelo), ncol(datos_modelo))
  ),
  caption = "Dimensiones del conjunto de datos limpio",
  align = c("l", "r")
)
```



Table: Dimensiones del conjunto de datos limpio

|Métrica            | Valor|
|:------------------|-----:|
|Número de filas    | 13190|
|Número de columnas |    11|

``` r
# Dividir datos en entrenamiento y prueba
set.seed(123)
indices_train <- createDataPartition(datos_modelo$depresion, p = 0.7, list = FALSE)
datos_entrenamiento <- datos_modelo[indices_train,]
datos_prueba <- datos_modelo[-indices_train,]

# Verificar distribución de clases
cat("\n### Distribución de clases en conjuntos de entrenamiento y prueba:\n")
```

```
## 
## ### Distribución de clases en conjuntos de entrenamiento y prueba:
```

``` r
# Tabla para conjunto de entrenamiento
tabla_train <- table(datos_entrenamiento$depresion)
prop_train <- prop.table(tabla_train) * 100

knitr::kable(
  data.frame(
    Conjunto = "Entrenamiento",
    Categoría = names(tabla_train),
    Frecuencia = as.numeric(tabla_train),
    Porcentaje = round(as.numeric(prop_train), 2)
  ),
  caption = "Distribución de clases en conjunto de entrenamiento",
  col.names = c("Conjunto", "Categoría", "Frecuencia", "Porcentaje (%)"),
  align = c("l", "l", "r", "r")
)
```



Table: Distribución de clases en conjunto de entrenamiento

|Conjunto      |Categoría | Frecuencia| Porcentaje (%)|
|:-------------|:---------|----------:|--------------:|
|Entrenamiento |Si        |       1883|          20.39|
|Entrenamiento |No        |       7350|          79.61|

``` r
# Tabla para conjunto de prueba
tabla_test <- table(datos_prueba$depresion)
prop_test <- prop.table(tabla_test) * 100

knitr::kable(
  data.frame(
    Conjunto = "Prueba",
    Categoría = names(tabla_test),
    Frecuencia = as.numeric(tabla_test),
    Porcentaje = round(as.numeric(prop_test), 2)
  ),
  caption = "Distribución de clases en conjunto de prueba",
  col.names = c("Conjunto", "Categoría", "Frecuencia", "Porcentaje (%)"),
  align = c("l", "l", "r", "r")
)
```



Table: Distribución de clases en conjunto de prueba

|Conjunto |Categoría | Frecuencia| Porcentaje (%)|
|:--------|:---------|----------:|--------------:|
|Prueba   |Si        |        807|          20.39|
|Prueba   |No        |       3150|          79.61|

## 4. Modelado Predictivo

### 4.1 Random Forest


``` r
# Configuración de la validación cruzada con menos folds
set.seed(123)
control <- trainControl(
  method = "cv",
  number = 3,  # Reducido de 5 a 3 folds
  classProbs = TRUE,
  summaryFunction = twoClassSummary,
  verboseIter = TRUE  # Añadido para mostrar progreso
)

# Entrenamiento del modelo con menos árboles
rf_model <- train(
  depresion ~ .,
  data = datos_entrenamiento,
  method = "rf",
  metric = "ROC",
  trControl = control,
  ntree = 100,  # Reducido de 500 a 100 árboles
  importance = TRUE
)
```

```
## + Fold1: mtry= 2 
## - Fold1: mtry= 2 
## + Fold1: mtry=21 
## - Fold1: mtry=21 
## + Fold1: mtry=41 
## - Fold1: mtry=41 
## + Fold2: mtry= 2 
## - Fold2: mtry= 2 
## + Fold2: mtry=21 
## - Fold2: mtry=21 
## + Fold2: mtry=41 
## - Fold2: mtry=41 
## + Fold3: mtry= 2 
## - Fold3: mtry= 2 
## + Fold3: mtry=21 
## - Fold3: mtry=21 
## + Fold3: mtry=41 
## - Fold3: mtry=41 
## Aggregating results
## Selecting tuning parameters
## Fitting mtry = 21 on full training set
```

``` r
# Crear tabla con resultados de la validación cruzada
resultados_cv <- data.frame(
  Fold = 1:3,
  ROC = rf_model$resample$ROC,
  Sensibilidad = rf_model$resample$Sens,
  Especificidad = rf_model$resample$Spec
)

# Mostrar resultados en formato de tabla
cat("\n#### Resultados por Fold de Validación Cruzada:\n")
```

```
## 
## #### Resultados por Fold de Validación Cruzada:
```

``` r
knitr::kable(
  resultados_cv,
  digits = 3,
  col.names = c("Fold", "ROC", "Sensibilidad", "Especificidad"),
  caption = "Métricas por fold de validación cruzada (Random Forest)",
  align = c("c", "r", "r", "r")
)
```



Table: Métricas por fold de validación cruzada (Random Forest)

| Fold |   ROC| Sensibilidad| Especificidad|
|:----:|-----:|------------:|-------------:|
|  1   | 0.802|        0.440|         0.934|
|  2   | 0.770|        0.398|         0.933|
|  3   | 0.801|        0.417|         0.938|

``` r
# Mostrar promedio de resultados
cat("\n#### Promedio de Métricas:\n")
```

```
## 
## #### Promedio de Métricas:
```

``` r
resultados_promedio <- data.frame(
  Métrica = c("ROC", "Sensibilidad", "Especificidad"),
  Valor = c(
    mean(resultados_cv$ROC),
    mean(resultados_cv$Sensibilidad),
    mean(resultados_cv$Especificidad)
  )
)

knitr::kable(
  resultados_promedio,
  digits = 3,
  col.names = c("Métrica", "Valor Promedio"),
  caption = "Promedio de métricas de validación cruzada (Random Forest)",
  align = c("l", "r")
)
```



Table: Promedio de métricas de validación cruzada (Random Forest)

|Métrica       | Valor Promedio|
|:-------------|--------------:|
|ROC           |          0.791|
|Sensibilidad  |          0.418|
|Especificidad |          0.935|

``` r
# Visualización de resultados
ggplot(resultados_cv, aes(x = factor(Fold))) +
  geom_point(aes(y = ROC, color = "ROC"), size = 3) +
  geom_point(aes(y = Sensibilidad, color = "Sensibilidad"), size = 3) +
  geom_point(aes(y = Especificidad, color = "Especificidad"), size = 3) +
  geom_hline(yintercept = mean(resultados_cv$ROC), linetype = "dashed", color = "red") +
  geom_hline(yintercept = mean(resultados_cv$Sensibilidad), linetype = "dashed", color = "green") +
  geom_hline(yintercept = mean(resultados_cv$Especificidad), linetype = "dashed", color = "blue") +
  labs(
    title = "Métricas por Fold de Validación Cruzada",
    subtitle = "Comparación de ROC, Sensibilidad y Especificidad",
    x = "Fold de Validación",
    y = "Valor de la Métrica",
    color = "Tipo de Métrica",
    caption = "Las líneas punteadas representan los valores promedio"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 14, face = "bold"),
    plot.subtitle = element_text(hjust = 0.5, size = 12),
    axis.title = element_text(size = 11),
    legend.position = "bottom"
  ) +
  scale_color_manual(values = c("ROC" = "red", "Sensibilidad" = "green", "Especificidad" = "blue"))
```

<img src="trabajo_final_files/figure-html/random_forest-1.png" width="100%" style="display: block; margin: auto;" />

``` r
# Importancia de variables
var_importance <- varImp(rf_model)
plot(var_importance, top = 10, main = "Top 10 Variables más Importantes")
```

<img src="trabajo_final_files/figure-html/random_forest-2.png" width="100%" style="display: block; margin: auto;" />

### 4.2 Regresión Logística


``` r
# Configuración de la validación cruzada
set.seed(123)
control_rl <- trainControl(
  method = "cv",
  number = 3,
  classProbs = TRUE,
  summaryFunction = twoClassSummary,
  verboseIter = TRUE
)

# Entrenamiento del modelo
rl_model <- train(
  depresion ~ .,
  data = datos_entrenamiento,
  method = "glm",
  family = "binomial",
  metric = "ROC",
  trControl = control_rl
)
```

```
## + Fold1: parameter=none 
## - Fold1: parameter=none 
## + Fold2: parameter=none 
## - Fold2: parameter=none 
## + Fold3: parameter=none 
## - Fold3: parameter=none 
## Aggregating results
## Fitting final model on full training set
```

``` r
# Mostrar resultados del modelo
print(rl_model)
```

```
## Generalized Linear Model 
## 
## 9233 samples
##   10 predictor
##    2 classes: 'Si', 'No' 
## 
## No pre-processing
## Resampling: Cross-Validated (3 fold) 
## Summary of sample sizes: 6156, 6155, 6155 
## Resampling results:
## 
##   ROC        Sens       Spec     
##   0.8093029  0.4237997  0.9453061
```

``` r
# Predicciones en conjunto de prueba
predicciones_rl <- predict(rl_model, datos_prueba)
predicciones_prob_rl <- predict(rl_model, datos_prueba, type = "prob")

# Calcular y mostrar matriz de confusión
tabla_confusion <- table(Predicho = predicciones_rl, Real = datos_prueba$depresion)
print("Matriz de Confusión:")
```

```
## [1] "Matriz de Confusión:"
```

``` r
print(tabla_confusion)
```

```
##         Real
## Predicho   Si   No
##       Si  360  163
##       No  447 2987
```

``` r
# Calcular métricas básicas
exactitud <- sum(diag(tabla_confusion)) / sum(tabla_confusion)
cat("\nExactitud:", round(exactitud, 3))
```

```
## 
## Exactitud: 0.846
```

``` r
# Calcular sensibilidad y especificidad manualmente
verdaderos_positivos <- sum(predicciones_rl == "Si" & datos_prueba$depresion == "Si")
falsos_positivos <- sum(predicciones_rl == "Si" & datos_prueba$depresion == "No")
verdaderos_negativos <- sum(predicciones_rl == "No" & datos_prueba$depresion == "No")
falsos_negativos <- sum(predicciones_rl == "No" & datos_prueba$depresion == "Si")

sensibilidad <- verdaderos_positivos / (verdaderos_positivos + falsos_negativos)
especificidad <- verdaderos_negativos / (verdaderos_negativos + falsos_positivos)

cat("\nSensibilidad:", round(sensibilidad, 3))
```

```
## 
## Sensibilidad: 0.446
```

``` r
cat("\nEspecificidad:", round(especificidad, 3))
```

```
## 
## Especificidad: 0.948
```

``` r
# Visualizar distribución de probabilidades predichas
hist(predicciones_prob_rl[,"Si"], 
     main = "Distribución de Probabilidades Predichas",
     xlab = "Probabilidad de Depresión",
     ylab = "Frecuencia",
     breaks = 20)
```

<img src="trabajo_final_files/figure-html/regresion_logistica-1.png" width="100%" style="display: block; margin: auto;" />

## 5. Comparación de Modelos

### 5.1 Métricas de Rendimiento


``` r
# Crear tabla comparativa con métricas básicas
comparacion <- data.frame(
  Modelo = c("Random Forest", "Regresión Logística"),
  Exactitud = c(
    sum(diag(table(predict(rf_model, datos_prueba), datos_prueba$depresion))) / nrow(datos_prueba),
    sensibilidad
  ),
  Especificidad = c(
    sum(predict(rf_model, datos_prueba) == "No" & datos_prueba$depresion == "No") / 
      sum(datos_prueba$depresion == "No"),
    especificidad
  )
)

# Mostrar tabla comparativa
print("Comparación de Modelos:")
```

```
## [1] "Comparación de Modelos:"
```

``` r
print(knitr::kable(
  comparacion,
  digits = 3,
  align = c("l", "r", "r", "r")
))
```

```
## 
## 
## |Modelo              | Exactitud| Especificidad|
## |:-------------------|---------:|-------------:|
## |Random Forest       |     0.836|         0.937|
## |Regresión Logística |     0.446|         0.948|
```

``` r
# Visualizar comparación de exactitud
barplot(
  comparacion$Exactitud,
  names.arg = comparacion$Modelo,
  main = "Comparación de Exactitud entre Modelos",
  ylab = "Exactitud",
  ylim = c(0, 1),
  col = c("skyblue", "lightgreen")
)
```

<img src="trabajo_final_files/figure-html/comparacion_modelos-1.png" width="100%" style="display: block; margin: auto;" />

### 5.2 Curvas ROC y AUC


``` r
library(pROC)

# Calcular ROC y AUC para ambos modelos
tryCatch({
  # Obtener predicciones de probabilidad para ambos modelos
  pred_prob_rf <- predict(rf_model, datos_prueba, type = "prob")
  pred_prob_log <- predict(rl_model, datos_prueba, type = "prob")
  
  # Para Random Forest
  roc_rf <- roc(datos_prueba$depresion, pred_prob_rf[,"Si"])
  auc_rf <- auc(roc_rf)
  
  # Para Regresión Logística
  roc_log <- roc(datos_prueba$depresion, pred_prob_log[,"Si"])
  auc_log <- auc(roc_log)
  
  # Graficar curvas ROC
  plot(roc_rf, main = "Curvas ROC", 
       col = "blue", 
       lwd = 2,
       legacy.axes = TRUE)
  lines(roc_log, col = "red", lwd = 2)
  
  # Agregar leyenda
  legend("bottomright", 
         legend = c(paste("Random Forest (AUC =", round(auc_rf, 3), ")"),
                   paste("Reg. Logística (AUC =", round(auc_log, 3), ")")),
         col = c("blue", "red"), 
         lwd = 2)
  
  # Agregar título y etiquetas
  title(main = "Comparación de Curvas ROC",
        sub = "Random Forest vs Regresión Logística",
        xlab = "Tasa de Falsos Positivos (1 - Especificidad)",
        ylab = "Tasa de Verdaderos Positivos (Sensibilidad)")
  
  # Imprimir valores de AUC
  cat("\nÁrea Bajo la Curva (AUC):\n")
  cat("Random Forest:", round(auc_rf, 3), "\n")
  cat("Regresión Logística:", round(auc_log, 3), "\n")
  
}, error = function(e) {
  cat("Error en el cálculo de ROC/AUC:\n")
  print(e)
  cat("\nVerificando objetos disponibles:\n")
  cat("Dimensiones datos_prueba:", dim(datos_prueba), "\n")
  cat("Clases en datos_prueba$depresion:", levels(datos_prueba$depresion), "\n")
})
```

```
## Error en el cálculo de ROC/AUC:
## <simpleError in binaryChecks(actual, "auc"): auc only works for binary outcomes at this time>
## 
## Verificando objetos disponibles:
## Dimensiones datos_prueba: 3957 11 
## Clases en datos_prueba$depresion: Si No
```

## 6. Interpretación de Resultados

### 6.1 Análisis de Sensibilidad y Especificidad

Los resultados muestran:

1. Sensibilidad: Capacidad para identificar correctamente a quienes consumen tranquilizantes
2. Especificidad: Capacidad para identificar correctamente a quienes no consumen tranquilizantes
3. Valor predictivo positivo: Probabilidad de que una predicción positiva sea correcta
4. Exactitud: Proporción total de predicciones correctas

Comparación de modelos:
- Random Forest muestra mejor desempeño general
- La curva ROC y el AUC indican la capacidad discriminativa de los modelos

### 6.2 Evaluación Final


``` r
# Calcular y mostrar métricas finales para ambos modelos
print("Métricas Finales en Conjunto de Prueba:")
```

```
## [1] "Métricas Finales en Conjunto de Prueba:"
```

``` r
# Random Forest
rf_pred <- predict(rf_model, datos_prueba)
rf_tabla <- table(Predicho = rf_pred, Real = datos_prueba$depresion)
rf_exactitud <- sum(diag(rf_tabla)) / sum(rf_tabla)

print("\nRandom Forest:")
```

```
## [1] "\nRandom Forest:"
```

``` r
print("Matriz de Confusión:")
```

```
## [1] "Matriz de Confusión:"
```

``` r
print(rf_tabla)
```

```
##         Real
## Predicho   Si   No
##       Si  357  200
##       No  450 2950
```

``` r
cat("\nExactitud:", round(rf_exactitud, 3))
```

```
## 
## Exactitud: 0.836
```

``` r
# Regresión Logística
print("\nRegresión Logística:")
```

```
## [1] "\nRegresión Logística:"
```

``` r
print("Matriz de Confusión:")
```

```
## [1] "Matriz de Confusión:"
```

``` r
print(tabla_confusion)
```

```
##         Real
## Predicho   Si   No
##       Si  360  163
##       No  447 2987
```

``` r
cat("\nExactitud:", round(exactitud, 3))
```

```
## 
## Exactitud: 0.846
```

``` r
# Visualizar comparación final
par(mfrow = c(1, 2))

# Gráfico para Random Forest
barplot(
  rf_tabla,
  beside = TRUE,
  main = "Predicciones Random Forest",
  legend.text = TRUE,
  args.legend = list(x = "topright"),
  col = c("skyblue", "lightgreen")
)

# Gráfico para Regresión Logística
barplot(
  tabla_confusion,
  beside = TRUE,
  main = "Predicciones Regresión Logística",
  legend.text = TRUE,
  args.legend = list(x = "topright"),
  col = c("skyblue", "lightgreen")
)
```

<img src="trabajo_final_files/figure-html/evaluacion_prueba-1.png" width="100%" style="display: block; margin: auto;" />