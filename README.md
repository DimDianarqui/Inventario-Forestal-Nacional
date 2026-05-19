# 📋 IFN — Sistema de Registro de Inventario Forestal Nacional

Sistema interactivo de captura de datos para brigadas de campo del Inventario Forestal Nacional (IFN), desarrollado en Python con `ipywidgets` para Google Colab.

---

## 📌 Descripción general

Este notebook permite registrar, validar, guardar y exportar información de campo recolectada por brigadas forestales. Cada registro asocia una brigada y conglomerado con una especie vegetal (árbol) y una especie animal observadas en la zona.

Los datos se persisten localmente en archivos CSV y los contadores de IDs se mantienen entre sesiones mediante un archivo JSON.

---

## 🗂️ Archivos generados

| Archivo | Descripción |
|---|---|
| `IFN_counters.json` | Persistencia de los últimos IDs asignados a vegetales y animales |
| `IFN_Brigadas.csv` | Registro de brigadas creadas (número, líder y guía local) |
| `IFN_Datos_General.csv` | Datos consolidados de todos los registros guardados |
| `IFN_Brigada_<N>.csv` | Exportación filtrada por número de brigada |

---

## ⚙️ Requisitos

- Python 3.x
- Google Colab (recomendado) o entorno Jupyter con soporte para `ipywidgets`
- Librerías estándar: `csv`, `os`, `json`, `datetime`
- Librería adicional: `ipywidgets`

```bash
pip install ipywidgets
```

> ⚠️ La función de descarga de archivos (`files.download`) depende de `google.colab` y solo funcionará en ese entorno.

---

## 🚀 Modo de uso

### 1. Iniciar el registro

Al ejecutar el notebook aparecerá el botón **"Iniciar Registro"**. Al pulsarlo se muestra el botón **"Confirmar"**, que carga el formulario principal.

### 2. Crear una brigada (obligatorio antes del primer registro)

Haz clic en el botón **"Crear brigada"** (naranja) e ingresa:
- **# Brigada** — número entero entre 1 y 999
- **Líder del equipo** — nombre del responsable
- **Guía local** — nombre del guía de campo

Pulsa **"Guardar brigada"** para registrarla en `IFN_Brigadas.csv`.

### 3. Completar el formulario de registro

Campos requeridos:

**Datos generales**
- `Brigada #` — seleccionar de la lista desplegable (no puede ser "N/A")
- `Conglomerado (#)` — número entero entre 1 y 999

**Especie vegetal (Árbol)**
- `Nombre común` — texto libre
- `Tipo de árbol` — Fustal / Latizal / Brinzal
- `Uso del árbol` — Medicinal / Alimenticio / Maderable
- `Cód. Vegetal asignado` — generado automáticamente (solo lectura)

**Especie animal**
- `Nombre común` — texto libre
- `Tipo de animal` — Pez / Mamífero / Reptil / Ave / Anfibio
- `Cód. Animal asignado` — generado automáticamente (solo lectura)

### 4. Guardar el registro

Pulsa **"Revisar y guardar"** (verde). El sistema valida todos los campos y, si son correctos, guarda el registro en memoria y limpia el formulario para el siguiente ingreso.

> Los IDs de vegetal y animal se incrementan automáticamente con cada guardado exitoso y se persisten en `IFN_counters.json`.

### 5. Exportar los datos

| Botón | Acción |
|---|---|
| **Guardar como CSV** (morado) | Agrega todos los registros de la sesión a `IFN_Datos_General.csv` y lo descarga |
| **Filtrar CSV** (teal) | Permite seleccionar una brigada y descargar solo sus registros |

### 6. Refrescar vista

El botón **"🔄 Refrescar vista"** (gris) imprime un mensaje de confirmación en la zona de formularios. Útil para forzar la actualización visual en Colab.

---

## 🔢 Sistema de IDs automáticos

Los códigos se asignan de forma secuencial y persistente:

| Tipo | ID inicial |
|---|---|
| Vegetal | 1001 (parte de 1000) |
| Animal | 5001 (parte de 5000) |

El archivo `IFN_counters.json` guarda el último ID utilizado. Si el archivo no existe, se inicializa con los valores base.

---

## ✅ Validaciones implementadas

### Registro de brigada
- El número de brigada no debe estar ya registrado en `IFN_Brigadas.csv`
- El nombre del líder no puede estar vacío
- El nombre del guía no puede estar vacío

### Registro de datos
- La brigada seleccionada no puede ser "N/A"
- El nombre común de la especie vegetal no puede estar vacío
- El tipo de árbol no puede ser "N/A"
- El uso del árbol no puede ser "N/A"
- El nombre común de la especie animal no puede estar vacío
- El tipo de animal no puede ser "N/A"

---

## 📐 Estructura del CSV principal (`IFN_Datos_General.csv`)

| Campo | Descripción |
|---|---|
| `Fecha Registro` | Fecha en que se guardó el registro (`YYYY-MM-DD`) |
| `Brigada #` | Número de brigada seleccionada |
| `Conglomerado` | Número del conglomerado |
| `Nombre Común Vegetal` | Nombre común de la especie vegetal |
| `Tipo Especie Vegetal` | Clasificación del árbol |
| `Uso de Especie Vegetal` | Uso principal del árbol |
| `# Vegetal` | Código único asignado a la especie vegetal |
| `Nombre Común Animal` | Nombre común de la especie animal |
| `Tipo Animal` | Clasificación del animal |
| `# Animal` | Código único asignado a la especie animal |

---

## 👥 Autores

| Nombre | Código |
|---|---|
| Diego Alejandro Durán Crispín | 01240372007 |
| Diego Andrés Ardila Quintero | 01240372038 |
