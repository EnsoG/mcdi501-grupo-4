# Reproducibilidad - Sumativa 1

Este repositorio contiene el notebook de la Sumativa 1 del curso de Estadistica Computacional.
Este README documenta un flujo reproducible de punta a punta: entorno, datos, ejecucion y verificaciones.

## 1. Alcance

- Notebook principal: `notebooks/analisis_sumativa1.ipynb`
- Dataset esperado: `data/raw/data.csv`
- Salida de figuras: `docs/sumativa1/`

## 2. Requisitos del sistema

- Sistema operativo: Windows 10/11 (tambien deberia funcionar en Linux/macOS con ajustes menores en comandos de entorno)
- Python: 3.11 recomendado
- `pip` disponible
- Jupyter Notebook/JupyterLab

## 3. Estructura esperada del proyecto

```text
sumativa 1/
|- README.md
|- requirements.txt
|- data/
|  |- raw/
|- docs/
|  |- sumativa1/
|- notebooks/
	|- analisis_sumativa1.ipynb
```

## 4. Dependencias Python

Instaladas desde `requirements.txt`:

- pandas==2.2.2
- numpy==2.2.6
- matplotlib==3.9.4
- jupyter==1.0.0
- seaborn==0.13.2
- scipy==1.11.3

## 5. Configuracion reproducible del entorno

Ejecutar desde la raiz del proyecto.

### Opcion A: venv (recomendada)

```powershell
python -m venv venv
venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### Opcion B: conda

```powershell
conda create -n sumativa1 python=3.11 -y
conda activate sumativa1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## 6. Variables de entorno (opcional, recomendado)

El notebook ya trae rutas por defecto correctas:

- `DATA_PATH = ../data/raw/data.csv`
- `FIG_DIR = ../docs/sumativa1`

Si quieres parametrizar sin tocar el notebook, puedes declarar variables de entorno y usarlas en futuras versiones.
Actualmente no son obligatorias para ejecutar el notebook tal como esta.

Sugerencia de estandarizacion:

- `SUMATIVA1_DATA_PATH`
- `SUMATIVA1_FIG_DIR`

Ejemplo en PowerShell (solo sesion actual):

```powershell
$env:SUMATIVA1_DATA_PATH = "data/raw/data.csv"
$env:SUMATIVA1_FIG_DIR = "docs/sumativa1"
```

Persistente para usuario (nuevas terminales):

```powershell
setx SUMATIVA1_DATA_PATH "data/raw/data.csv"
setx SUMATIVA1_FIG_DIR "docs/sumativa1"
```

## 7. Preparacion de datos

Debe existir el archivo:

- `data/raw/data.csv`

Si no existe, copiar o descargar el dataset en esa ruta antes de correr el notebook.

## 8. Ejecucion del notebook

1. Activar entorno virtual.
2. Abrir VS Code en la raiz del proyecto.
3. Abrir `notebooks/analisis_sumativa1.ipynb`.
4. Seleccionar el kernel del entorno creado.
5. Ejecutar todas las celdas en orden (Run All).

Comando alternativo por terminal con Jupyter:

```powershell
jupyter notebook
```

## 9. Resultados esperados

Al finalizar, deberian existir estos archivos en `docs/sumativa1/`:

- `fig1_boxplots.png`
- `fig2_histogramas.png`
- `fig3_categoricas.png`
- `fig4_correlacion.png`
- `fig5_intervalos.png`

Y en salida de celdas, entre otros:

- Carga correcta del dataset (4424 filas x 37 columnas)
- Binarizacion de target (3630 filas)
- Pruebas de hipotesis con p-valores significativos en los contrastes reportados

## 10. Verificacion rapida (checklist)

- [ ] Entorno Python activo
- [ ] Dependencias instaladas sin error
- [ ] `data/raw/data.csv` existe
- [ ] Notebook ejecuta de la celda 1 a la final sin errores
- [ ] Se generan 5 figuras en `docs/sumativa1/`

## 11. Problemas comunes

### Error: `ModuleNotFoundError`

Instalar dependencias:

```powershell
pip install -r requirements.txt
```

### Error: `FileNotFoundError: data/raw/data.csv`

Verificar ruta y nombre exacto del archivo CSV en `data/raw/data.csv`.

### Kernel incorrecto en VS Code

Seleccionar explicitamente el interprete del entorno (`venv` o `conda`) desde el selector de kernel del notebook.

## 12. Congelamiento del entorno (opcional)

Para auditoria de reproducibilidad:

```powershell
pip freeze > requirements-lock.txt
python --version
```

Guardar tambien:

- version de VS Code
- version de extension Jupyter
- fecha de ejecucion

## 13. Notas de reproducibilidad estadistica

- Se utiliza semilla global: `np.random.seed(42)`.
- La inyeccion de faltantes MCAR usa 12% con semilla fija, por lo que los resultados son replicables bajo el mismo entorno.

