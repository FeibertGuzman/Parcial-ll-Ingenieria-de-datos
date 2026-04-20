# 🎓 Tutorial: Construcción de un Data Warehouse y Dashboard Interactivo

Este tutorial te guiará paso a paso a través de la creación del proyecto **Parcial II - Ingeniería de Datos**, desde la concepción del modelo de datos hasta el despliegue de una landing page premium.

---

## 🚀 1. Fundamentos: El Modelo Estrella (Star Schema)

Antes de programar, debemos entender la arquitectura. Un **Modelo Estrella** organiza los datos en:
- **Tabla de Hechos (`ventas.csv`)**: Contiene las métricas cuantitativas (precio, cantidad, total) y claves foráneas.
- **Tablas de Dimensiones (`clientes.csv`, `productos.csv`, `fechas.csv`)**: Contienen los atributos descriptivos para filtrar y agrupar los datos.

---

## 🛠️ 2. Preparación del Entorno

Para ejecutar este proyecto, necesitas:

1.  **Instalar Python 3.12+**.
2.  **Clonar el repositorio**:
    ```bash
    git clone https://github.com/FeibertGuzman/Parcial-ll-Ingenieria-de-datos.git
    cd Parcial-ll-Ingenieria-de-datos
    ```
3.  **Instalar dependencias**:
    ```bash
    pip install -r requirements.txt
    ```

---

## 🔄 3. El Pipeline ETL (Extract, Transform, Load)

El proceso mas importante ocurre en `app.py` y el notebook `DW_EST.ipynb`.

### Paso A: Extracción (Extract)
Cargamos los datos desde archivos CSV en la carpeta `data/`.
```python
import pandas as pd
ventas = pd.read_csv('data/ventas.csv')
clientes = pd.read_csv('data/clientes.csv')
```

### Paso B: Transformación (Transform)
Unimos las tablas para crear el Data Warehouse (JOIN) y limpiamos los datos.
```python
# Unir ventas con clientes
dw = ventas.merge(clientes, on='id_cliente')
# Limpiar nulos y duplicados
dw = dw.dropna().drop_duplicates()
```

### Paso C: Carga (Load)
Guardamos el resultado para su uso en otras herramientas.
```python
dw.to_csv('cleaned_dataset.csv', index=False)
```

---

## 📊 4. Dashboard Interactivo con Streamlit

El dashboard permite interactuar con los datos del Data Warehouse en tiempo real.

**Cómo ejecutarlo:**
```bash
streamlit run app.py
```

**Funcionalidades clave:**
- **Filtros Dinámicos**: Por región, categoría y año.
- **Métricas**: Visualización instantánea de KPIs.
- **Gráficos**: Histogramas de ventas y mapas de distribución geográfica.
- **Análisis Predictivo**: Estimaciones de ventas futuras basadas en el histórico.

---

## 🎨 5. Presentación: La Landing Page Premium

Hemos creado una **Landing Page (`index.html`)** para presentar el proyecto de forma profesional.

- **Diseño**: Modo oscuro, glassmorphism y orbes animados.
- **Contenido**: Resumen técnico del pipeline y visualización del DAG (Grafo Acíclico Dirigido).
- **Cómo verla**: Solo abre `index.html` en tu navegador favorito.

---

## 🤝 6. Colaboración: Git y Pull Request

Para trabajar en equipo y entregar el parcial:

1.  **Hacer un Fork**: Copia el repositorio original a tu propia cuenta de GitHub.
2.  **Crear una Rama**: `git checkout -b feature/mi-mejora`.
3.  **Hacer Push**: `git push origin feature/mi-mejora`.
4.  **Pull Request (PR)**: Solicita integrar tus cambios en el repositorio de la profesora (Daniela) desde la interfaz de GitHub.

---

## 📝 Resumen de Archivos Principales

| Archivo | Propósito |
| :--- | :--- |
| `app.py` | Código principal del Dashboard y Pipeline ETL. |
| `index.html` | Página de aterrizaje premium del proyecto. |
| `data/` | Datos fuente en formato CSV. |
| `DW_EST.ipynb` | Notebook con el análisis y construcción del DW. |
| `dag.svg` | Diagrama del flujo de tareas del pipeline. |

---
*Tutorial creado con ❤️ para el equipo de Ingeniería de Datos.*
