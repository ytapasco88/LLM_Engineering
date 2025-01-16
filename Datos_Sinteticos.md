# Generación de Datos Sintéticos con Python y R

## Introducción

### ¿Qué son los datos sintéticos?
- Datos generados artificialmente que imitan las propiedades de los datos reales.

### ¿Por qué usarlos?
- **Privacidad**: Evitan exponer datos sensibles.
- **Escalabilidad**: Ampliación de datasets pequeños.
- **Experimentación**: Pruebas sin depender de datos reales.

---

## Herramientas para la generación

### Python
- `Faker`: Generación de datos ficticios (nombres, direcciones, etc.).
- `SDV`: Modelos para datos tabulares y distribuciones.
- `scikit-learn`: Creación de datasets para aprendizaje automático.

### R
- `synthpop`: Generación de datos tabulares.
- `SimDesign`: Simulaciones estadísticas.
- `ggplot2`: Visualización de datos.

---

## Ejemplo Práctico con Python

### Generación de datos ficticios con Faker
```python
from faker import Faker
import pandas as pd

# Inicializar Faker
fake = Faker()

# Generar un dataset ficticio
data = {
    "Nombre": [fake.name() for _ in range(100)],
    "Correo": [fake.email() for _ in range(100)],
    "Dirección": [fake.address() for _ in range(100)],
    "Teléfono": [fake.phone_number() for _ in range(100)],
    "Fecha de nacimiento": [fake.date_of_birth(minimum_age=18, maximum_age=90) for _ in range(100)]
}

# Convertir a DataFrame
df = pd.DataFrame(data)

# Mostrar las primeras filas
print(df.head())

# Guardar el dataset en un archivo CSV
df.to_csv("datos_ficticios.csv", index=False)
```

### Generación de datos tabulares con SDV
```python
from sdv.tabular import GaussianCopula
import pandas as pd

# Cargar un dataset real
real_data = pd.DataFrame({
    "Edad": [23, 45, 31, 27, 29],
    "Salario": [40000, 80000, 50000, 45000, 47000],
    "Puntuación de crédito": [650, 720, 680, 640, 690]
})

# Modelo de SDV para datos sintéticos
model = GaussianCopula()
model.fit(real_data)

# Generar datos sintéticos
synthetic_data = model.sample(100)

# Mostrar los datos generados
print(synthetic_data)
```

---

## Ejemplo Práctico con R

### Uso de synthpop para datos tabulares
```R
# Instalar synthpop si no está instalado
if (!requireNamespace("synthpop", quietly = TRUE)) {
  install.packages("synthpop")
}

library(synthpop)

# Dataset de ejemplo
data("iris")
real_data <- iris

# Generar datos sintéticos
synthetic_data <- syn(real_data)

# Comparar datos reales vs sintéticos
summary(real_data)
summary(synthetic_data$syn)

# Guardar los datos generados
write.csv(synthetic_data$syn, "datos_sinteticos.csv", row.names = FALSE)
```

### Simulación estadística con SimDesign
```R
# Instalar SimDesign si no está instalado
if (!requireNamespace("SimDesign", quietly = TRUE)) {
  install.packages("SimDesign")
}

library(SimDesign)

# Simulación de una muestra normal
set.seed(123)
sim_data <- rnorm(100, mean = 50, sd = 10)

# Visualización
hist(sim_data, main = "Simulación de una distribución normal",
     xlab = "Valores", col = "skyblue", border = "white")
```

---

## Beneficios y Desafíos

### Beneficios
- **Privacidad**: Protección de datos sensibles.
- **Flexibilidad**: Ampliación y manipulación de datasets.
- **Pruebas**: Ideal para validación de modelos.

### Desafíos
- **Realismo**: Asegurar que los datos reflejen patrones reales.
- **Complejidad**: Configuración de distribuciones.

---

## Conclusión
- Los datos sintéticos ofrecen una solución poderosa para proteger la privacidad y escalar experimentos.
- Las herramientas en Python y R facilitan su generación para diferentes escenarios.
- Adoptar estas prácticas puede optimizar procesos en diversos dominios como e-commerce, salud y finanzas.
