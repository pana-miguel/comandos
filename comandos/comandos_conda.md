# Guía Completa de Conda

## 📌 Introducción

Antes de usar conda se debe instalar anaconda que lo puedes buscar en google como anaconda download y por medio de un video ver como se instala y cual es su relacion con la terminal.

**Conda** es un gestor de entornos y paquetes que permite instalar diferentes versiones de **Python** y librerías de forma aislada este ambiente o entorno virtual esta mas enfocado a la parte de ciencia o ingenieria de datos donde se usa mas.  
A diferencia de `pip` o `venv`, conda gestiona tanto paquetes de Python como librerías de sistema, facilitando el trabajo en proyectos con dependencias diferentes.

### ¿Por qué usar conda?
- Puedes tener múltiples versiones de Python en el mismo equipo.
- Evita conflictos entre librerías.
- Es más fácil replicar entornos en otros equipos.
- Compatible con **Windows, Linux y macOS**.

### Concepto de "Entorno Madre"
En conda, puedes crear un **entorno madre** que tenga únicamente una versión específica de Python y unas librerías mínimas.  
Por ejemplo:
- `base` (Python 3.12, conda, jupyter)
- `py311` (Python 3.11 con librerías básicas)
- `py38` (Python 3.8 con librerías básicas)

Luego, para cada proyecto puedes:
1. Crear un entorno nuevo a partir del "madre".
2. Instalar solo las librerías necesarias.
3. Exportar un archivo `environment.yml` para recordar exactamente con qué entorno trabajaste.

### Uso de environment.yml
Este archivo guarda la información del entorno (nombre, versión de Python, librerías).  
Para exportar:
```bash
conda env export --from-history > environment.yml
```
Para recrear el entorno:
```bash
conda env create -f environment.yml
```

---

## 🔹 Comandos Básicos de Conda

### Información General
```bash
conda --version          # Ver versión de conda
conda info               # Información general de conda y rutas
conda list               # Listar librerías instaladas en el entorno actual
conda list -n NOMBRE     # Listar librerías de un entorno específico
```

### Manejo de Entornos
```bash
conda create -n NOMBRE python=VERSION   # Crear un entorno con cierta versión de Python
conda create -n NOMBRE paquete1 paquete2  # Crear un entorno e instalar paquetes
conda activate NOMBRE                   # Activar entorno
conda deactivate                        # Salir del entorno
conda env list                          # Listar entornos disponibles
conda remove -n NOMBRE --all            # Eliminar un entorno
conda rename -n viejo_nombre nuevo_nombre  # Renombrar un entorno
```

### Instalación y Actualización de Paquetes o librerias
```bash
conda install libreria                   # Instalar libreria
conda remove libreria                   # eliminar libreria
conda install libreria=VERSION           # Instalar una versión específica
conda install -c canal libreria           # Instalar desde un canal específico
conda update libreria                    # Actualizar libreria
conda update --all                      # Actualizar todos los paquetes
conda remove libreria                    # Eliminar un libreria
```

### Exportar y Reproducir Entornos
```bash
conda env export > environment.yml       # Exportar entorno completo
conda env export --from-history > environment.yml  # Solo paquetes instalados manualmente
conda env create -f environment.yml      # Crear entorno desde archivo
conda env update -f environment.yml      # Actualizar entorno desde archivo
```

### Limpieza
```bash
conda clean --all                        # Borrar caché y archivos temporales
conda clean --packages                   # Eliminar paquetes no usados
```

---

## 💡 Buenas Prácticas
1. Mantener el entorno `base` limpio (solo con Python y herramientas esenciales).
2. Crear entornos por versión de Python y proyectos.
3. Exportar siempre un `environment.yml` para cada proyecto.
4. Nombrar entornos de forma descriptiva (`py311-datascience`, `py38-ml`, etc.).
5. Usar `--from-history` para tener archivos `.yml` más limpios.

---

✍️ **Autor:** Miguel Sierra  
📅 **Última actualización:** Agosto 2025
