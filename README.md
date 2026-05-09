# 🌿 Inventario Forestal Nacional — Herramienta de Captura de Datos

Herramienta interactiva desarrollada en Python (Jupyter/Google Colab) para el registro estructurado de datos de campo del **Inventario Forestal Nacional (IFN)**. Permite capturar, editar, eliminar, exportar y filtrar información sobre especies vegetales y animales por brigada y conglomerado.

---

## 📋 Descripción

Este script genera formularios interactivos dentro de un notebook de Jupyter o Google Colab, facilitando el ingreso de datos de campo sin necesidad de editar código. Los datos se almacenan en memoria durante la sesión y pueden exportarse como archivo `.csv` al finalizar el registro. También es posible filtrar los registros exportados por número de brigada.

---

## ⚙️ Requisitos

- Python 3.7+
- Jupyter Notebook o Google Colab
- Librerías:
  - `ipywidgets`
  - `csv` *(incluida en la biblioteca estándar)*
  - `os` *(incluida en la biblioteca estándar)*
  - `datetime` *(incluida en la biblioteca estándar)*

### Instalación de dependencias

```bash
pip install ipywidgets
```

> En Google Colab, `ipywidgets` ya viene preinstalado.

---

## 🚀 Uso

1. Abre el archivo en **Jupyter Notebook** o **Google Colab**.
2. Ejecuta todas las celdas.
3. Presiona **"Iniciar Registro"** e ingresa el número de grupos de datos (brigadas) que deseas registrar.
4. Presiona **"Confirmar"** para generar los formularios.
5. Por cada grupo se desplegará un formulario con los siguientes campos:

### 📝 Campos del formulario

| Campo | Descripción |
|---|---|
| **Brigada #** | Número identificador de la brigada (desplegable) |
| **Conglomerado (#)** | Número del conglomerado asignado |
| **Nombre Común (Vegetal)** | Nombre común de la especie vegetal |
| **Tipo de árbol** | Fustal / Latizal / Brinzal |
| **Uso del árbol** | Medicinal / Alimenticio / Maderable |
| **Cod. ID (Vegetal)** | Código identificador de la especie vegetal |
| **Nombre Común (Animal)** | Nombre común de la especie animal |
| **Tipo de animal** | Pez / Mamífero / Reptil / Ave / Anfibio |
| **Cod. ID (Animal)** | Código identificador de la especie animal |

### 🎛️ Botones disponibles

| Botón | Color | Función |
|---|---|---|
| `Iniciar Registro` | 🔵 Azul | Abre el panel de configuración inicial |
| `Confirmar` | 🟣 Morado | Genera los formularios según el número indicado |
| `guardar/editar` | 🟢 Verde | Guarda o actualiza los datos del grupo |
| `eliminar` | 🔴 Rojo | Marca el grupo como eliminado |
| `agregar grupo` | 🟠 Naranja | Añade un nuevo formulario de datos |
| `guardar como CSV` | 🟣 Morado | Exporta todos los datos a `IFN_Datos_General.csv` |
| `Filtrar CSV` | 🩵 Teal | Filtra el CSV existente por brigada y lo exporta por separado |

---

## 📁 Salida de datos

### Archivo general
Al hacer clic en **"guardar como CSV"**, se genera o actualiza el archivo:
```
IFN_Datos_General.csv
```

### Archivo filtrado por brigada
Al usar **"Filtrar CSV"** y seleccionar una brigada, se genera:
```
IFN_Brigada_<número>.csv
```

Ambos archivos contienen las siguientes columnas:

```
Fecha Registro, Brigada #, Conglomerado, Nombre Común Vegetal,
Tipo Especie Vegetal, Uso de Especie Vegetal, ID Vegetal,
Nombre Común Animal, Tipo Animal, ID Animal
```

> Si el archivo general ya existe, los nuevos registros se **agregan** al final sin sobreescribir los anteriores.

---

## 🗂️ Estructura del código

```
inventarioforestalnacional_dim.py
│
├── showInputLogs()     — Inicializa la interfaz y recrea los Output widgets
├── logInfo()           — Lógica principal, contiene las funciones internas:
│   ├── saveData()          — Guarda datos de un grupo en la lista principal
│   ├── remove_data()       — Marca un registro como eliminado
│   ├── createNewDataset()  — Genera el formulario interactivo para un grupo
│   ├── listToDict()        — Convierte la lista de datos a formato diccionario
│   ├── saveCSV()           — Exporta los datos al archivo CSV general
│   └── filterBrigade()     — Filtra el CSV por brigada y genera archivo separado
│
└── Flujo principal
    ├── Botón "Iniciar Registro" → showInputLogs()
    ├── Botón "Confirmar" → logInfo()
    ├── Formularios por grupo de datos
    ├── Botón para agregar grupos adicionales
    ├── Botón para exportar a CSV general
    └── Botón para filtrar CSV por brigada
```

---

## ⚠️ Limitaciones conocidas

- Los datos **no persisten** entre sesiones; deben exportarse antes de cerrar el notebook.
- La lista de brigadas disponibles en el desplegable está fija en `["N/A", 1, 2, 3]`; debe ajustarse manualmente si se requieren más brigadas.
- El filtro por brigada requiere que el archivo `IFN_Datos_General.csv` exista previamente.
- Los archivos CSV se guardan en el **directorio de trabajo actual** del notebook.

---

## 🛠️ Posibles mejoras (To-do)

- [ ] Registro dinámico de brigadas en lista desplegable
- [ ] Validación de campos obligatorios antes de guardar
- [ ] Exportación a formato Excel (`.xlsx`)
- [ ] Visualización previa de los datos registrados en tabla
- [ ] Descarga directa del CSV desde la interfaz en Google Colab

---

## 👥 Autores

| Nombre | Código |
|---|---|
| Diego Alejandro Durán Crispín | 01240372007 |
| Diego Andrés Ardila Quintero | 01240372038 |

---

## 📄 Licencia

Uso interno — Inventario Forestal Nacional de Colombia.
