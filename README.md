# 🌿 Inventario Forestal Nacional — Herramienta de Captura de Datos

Herramienta interactiva desarrollada en Python (Jupyter/Google Colab) para el registro estructurado de datos de campo del **Inventario Forestal Nacional (IFN)**. Permite capturar, validar, exportar y filtrar información sobre especies vegetales y animales por brigada y conglomerado.

---

## 📋 Descripción

Este script genera un formulario interactivo dentro de un notebook de Jupyter o Google Colab, facilitando el ingreso de datos de campo sin necesidad de editar código. Incluye validación de campos obligatorios, IDs autocrecientes persistentes entre sesiones, y exportación directa a `.csv` con descarga automática al equipo.

---

## ⚙️ Requisitos

- Python 3.7+
- Jupyter Notebook o Google Colab
- Librerías:
  - `ipywidgets`
  - `csv` *(biblioteca estándar)*
  - `os` *(biblioteca estándar)*
  - `datetime` *(biblioteca estándar)*
  - `json` *(biblioteca estándar)*

### Instalación de dependencias

```bash
pip install ipywidgets
```

> En Google Colab, `ipywidgets` ya viene preinstalado.

---

## 🚀 Uso

1. Abre el archivo en **Google Colab**.
2. Ejecuta la celda principal.
3. Presiona **"Iniciar Registro"** para abrir el panel de captura.
4. Presiona **"Confirmar"** para cargar el formulario.
5. Llena los campos y presiona **"Revisar y guardar"** para validar y almacenar el registro.
6. El formulario se limpia automáticamente para ingresar el siguiente registro.

### 📝 Campos del formulario

| Campo | Tipo | Descripción |
|---|---|---|
| **Brigada #** | Desplegable | Número de brigada asignada |
| **Conglomerado (#)** | Numérico (1–999) | Número del conglomerado, no permite negativos |
| **Nombre Común (Vegetal)** | Texto | Nombre común de la especie vegetal |
| **Tipo de árbol** | Desplegable | Fustal / Latizal / Brinzal |
| **Uso del árbol** | Desplegable | Medicinal / Alimenticio / Maderable |
| **Cód. Vegetal** | Etiqueta (auto) | Asignado automáticamente, rango 1001–4999 |
| **Nombre Común (Animal)** | Texto | Nombre común de la especie animal |
| **Tipo de animal** | Desplegable | Pez / Mamífero / Reptil / Ave / Anfibio |
| **Cód. Animal** | Etiqueta (auto) | Asignado automáticamente, rango 5001+ |

### 🎛️ Botones disponibles

| Botón | Color | Función |
|---|---|---|
| `Iniciar Registro` | 🔵 Azul | Abre el panel y recrea los widgets desde cero |
| `Confirmar` | 🟣 Morado | Carga el formulario de captura |
| `Revisar y guardar` | 🟢 Verde | Valida los campos y guarda el registro en memoria |
| `🔄 Refrescar vista` | ⚫ Gris | Fuerza el re-render de la interfaz si se corta |
| `guardar como CSV` | 🟣 Morado | Exporta todos los registros y descarga el archivo |
| `Filtrar CSV` | 🩵 Teal | Filtra el CSV existente por brigada y lo descarga |

---

## ✅ Validación de campos

Al presionar **"Revisar y guardar"**, el sistema verifica que:

- La brigada seleccionada no sea `N/A`
- El nombre común de la especie vegetal no esté vacío
- El tipo y uso del árbol no sean `N/A`
- El nombre común de la especie animal no esté vacío
- El tipo de animal no sea `N/A`

Si algún campo es inválido, se muestra un mensaje en **rojo** indicando cuáles deben corregirse. El registro **no se guarda** hasta que todos los campos sean válidos.

---

## 🔢 IDs autocrecientes y persistentes

Los códigos de especie se asignan automáticamente y se guardan en `IFN_counters.json`:

- **Especie vegetal:** inicia en `1001`, incrementa con cada registro guardado
- **Especie animal:** inicia en `5001`, incrementa con cada registro guardado

Al cerrar y volver a abrir el notebook, los contadores retoman desde el último valor guardado, evitando que se reinicien a cero.

---

## 📁 Salida de datos

### Archivo general
Al hacer clic en **"guardar como CSV"**, se genera o actualiza el archivo y se descarga automáticamente:
```
IFN_Datos_General.csv
```

### Archivo filtrado por brigada
Al usar **"Filtrar CSV"** y seleccionar una brigada, se genera y descarga:
```
IFN_Brigada_<número>.csv
```

Ambos archivos contienen las siguientes columnas:

```
Fecha Registro, Brigada #, Conglomerado, Nombre Común Vegetal,
Tipo Especie Vegetal, Uso de Especie Vegetal, # Vegetal,
Nombre Común Animal, Tipo Animal, # Animal
```

> Los registros se **agregan** al final del archivo general sin sobreescribir los anteriores.

---

## 🗂️ Estructura del código

```
inventarioforestalnacional.py
│
├── loadCounters()      — Lee los últimos IDs desde IFN_counters.json
├── saveCounters()      — Guarda el estado de los contadores en JSON
│
├── showInputLogs()     — Inicializa la interfaz recreando los Output widgets
├── logInfo()           — Lógica principal; contiene las funciones internas:
│   ├── validateForm()      — Valida campos obligatorios y retorna lista de errores
│   ├── saveData()          — Valida, incrementa IDs y guarda el registro en memoria
│   ├── refreshOutput()     — Fuerza el re-render del Output widget (fix Colab)
│   ├── listToDict()        — Convierte la lista de registros a formato diccionario
│   ├── saveCSV()           — Exporta registros al CSV general y lo descarga
│   └── filterBrigade()     — Filtra el CSV por brigada y descarga el resultado
│
└── Flujo principal
    ├── "Iniciar Registro" → showInputLogs() → recrea widgets
    ├── "Confirmar"        → logInfo()       → carga formulario
    ├── "Revisar y guardar"→ saveData()      → valida y guarda
    ├── "guardar como CSV" → saveCSV()       → exporta y descarga
    └── "Filtrar CSV"      → filterBrigade() → filtra y descarga
```

---

## ⚠️ Limitaciones conocidas

- La lista de brigadas disponibles está fija en `["N/A", 1, 2, 3]`; debe ajustarse manualmente en el código si se requieren más.
- El filtro por brigada requiere que `IFN_Datos_General.csv` exista previamente.
- No hay verificación de registros duplicados al guardar en el CSV *(próxima actualización)*.
- Los archivos se guardan en el directorio de trabajo temporal de Colab; la descarga automática los lleva al equipo local.

---

## 🛠️ Próximas mejoras (To-do)

- [ ] Verificación de registros duplicados al exportar al CSV
- [ ] Registro dinámico de brigadas desde un CSV externo
- [ ] Botón para visualizar los registros guardados en tabla antes de exportar
- [ ] Exportación a formato Excel (`.xlsx`)

---

## 👥 Autores

| Nombre | Código |
|---|---|
| Diego Alejandro Durán Crispín | 01240372007 |
| Diego Andrés Ardila Quintero | 01240372038 |

---

## 📄 Licencia

Uso interno — Inventario Forestal Nacional de Colombia.
