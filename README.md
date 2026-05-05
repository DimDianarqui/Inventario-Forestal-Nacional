# 🌿 Inventario Forestal Nacional — Herramienta de Captura de Datos

Herramienta interactiva desarrollada en Python (Jupyter/Google Colab) para el registro estructurado de datos de campo del **Inventario Forestal Nacional (IFN)**. Permite capturar, editar, eliminar y exportar información sobre especies vegetales y animales por brigada y conglomerado.

---

## 📋 Descripción

Este script genera formularios interactivos dentro de un notebook de Jupyter o Google Colab, facilitando el ingreso de datos de campo sin necesidad de editar código. Los datos se almacenan en memoria durante la sesión y pueden exportarse como archivo `.csv` al finalizar el registro.

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
3. Ingresa el número de grupos de datos (brigadas) que deseas registrar.
4. Por cada grupo se desplegará un formulario con los siguientes campos:

### 📝 Campos del formulario

| Campo | Descripción |
|---|---|
| **Brigada #** | Número identificador de la brigada |
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
| `guardar/editar` | 🟢 Verde | Guarda o actualiza los datos del grupo |
| `eliminar` | 🔴 Rojo | Marca el grupo como eliminado |
| `agregar grupo` | 🟠 Naranja | Añade un nuevo formulario de datos |
| `guardar como CSV` | 🟣 Morado | Exporta todos los datos a `IFN_Datos.csv` |

---

## 📁 Salida de datos

Al hacer clic en **"guardar como CSV"**, se genera (o actualiza) el archivo:

```
IFN_Datos.csv
```

El archivo contiene las siguientes columnas:

```
Fecha Registro, Brigada #, Conglomerado, Nombre Común Vegetal,
Tipo Especie Vegetal, Uso de Especie Vegetal, ID Vegetal,
Nombre Común Animal, Tipo Animal, ID Animal
```

> Si el archivo ya existe, los nuevos registros se **agregan** al final sin sobreescribir los anteriores.

---

## 🗂️ Estructura del código

```
inventarioforestalnacional_dim.py
│
├── save_data()         — Guarda datos de un grupo en la lista principal
├── remove_data()       — Marca un registro como eliminado
├── createNewDataset()  — Genera el formulario interactivo para un grupo
├── listToDict()        — Convierte la lista de datos a formato diccionario
├── saveCSV()           — Exporta los datos al archivo CSV
│
└── Flujo principal
    ├── Solicita número de grupos iniciales
    ├── Renderiza formularios por grupo
    ├── Botón para agregar grupos adicionales
    └── Botón para exportar a CSV
```

---

## ⚠️ Limitaciones conocidas

- Los datos **no persisten** entre sesiones; deben exportarse antes de cerrar el notebook.
- El campo **"Brigada #"** es un texto libre; se recomienda estandarizar la nomenclatura entre el equipo.
- El archivo CSV se guarda en el **directorio de trabajo actual** del notebook.

---

## 🛠️ Posibles mejoras (To-do)

- [ ] Registro formal de brigadas en lista desplegable
- [ ] Validación de campos obligatorios antes de guardar
- [ ] Exportación a formato Excel (`.xlsx`)
- [ ] Visualización previa de los datos registrados en tabla

---

## 📄 Licencia

Uso interno — Inventario Forestal Nacional de Colombia.
