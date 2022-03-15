---
lab:
  title: Ejecución de los experimentos
ms.openlocfilehash: 62b6b79c99142d4311c2d9c0db4b02cfd710feb6
ms.sourcegitcommit: 66d8872bc3d24c2121e225be132b56f4df7920ac
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2022
ms.locfileid: "138597277"
---
# <a name="run-experiments"></a>Ejecución de los experimentos

Los experimentos son la esencia del trabajo de un científico de datos. En Azure Machine Learning, se usa un *experimento* para ejecutar un script o una canalización, y normalmente genera salidas y registra métricas. En este ejercicio, usará el SDK de Azure Machine Learning para ejecutar código de Python como experimentos.

## <a name="before-you-start"></a>Antes de empezar

Si todavía no lo ha hecho, complete el ejercicio *[Creación de un área de trabajo de Azure Machine Learning](01-create-a-workspace.md)* para crear un área de trabajo y una instancia de proceso de Azure Machine Learning y clone los cuadernos necesarios para completarlo.

## <a name="open-jupyter"></a>Abrir Jupyter

Aunque puede usar la página **Cuadernos** de Azure Machine Learning Studio para ejecutar cuadernos, a menudo es más productivo usar un entorno de desarrollo de cuadernos más completo como *Jupyter*. Afortunadamente, la instancia de proceso de Azure Machine Learning incluye una instalación de Jupyter.

> **Sugerencia**: Jupyter Notebook es una herramienta de código abierto que se usa con frecuencia para la ciencia de datos. Puede consultar la [documentación](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html) sino está familiarizado con ella.

1. En [Azure Machine Learning Studio](https://ml.azure.com), consulte la página **Proceso** del área de trabajo y, en la pestaña **Instancias de proceso**, inicie la instancia de proceso si aún no se está ejecutando.
2. Cuando se esté ejecutando la instancia de proceso, haga clic en el vinculo de **Jupyter** para abrir la página principal de Jupyter en una nueva pestaña del explorador. Asegúrese de abrir *Jupyter* y no *JupyterLab*.

> **Sugerencia**: ¿Es la primera vez que usa Python? Use la [hoja de referencia rápida de Python](cheat-sheets/dp100-cheat-sheet-python.pdf) para entender el código.

## <a name="verify-the-azure-machine-learning-sdk-is-installed"></a>Comprobar que el SDK de Azure Machine Learning está instalado

El SDK de Azure Machine Learning está instalado de forma predeterminada en la instancia de proceso. Siga estos pasos para comprobar la instalación.

1. En el entorno de Jupyter Notebook, cree un **terminal**. Se abrirá una nueva pestaña con un shell de comandos.
2. Escriba el siguiente comando para comprobar que el SDK de Azure ML está instalado:

    ```bash
    pip show azureml-sdk
    ```

    Observe que la versión del paquete del SDK está instalada.

3. El paquete del SDK **azureml-sdk** proporciona las bibliotecas más importantes necesarias para trabajar con Azure Machine Learning. Sin embargo, hay algunos paquetes adicionales que contienen otras bibliotecas útiles que no se incluyen en el paquete principal del SDK. Use el siguiente comando para comprobar que el paquete **azureml-widgets**, que contiene bibliotecas para mostrar información de Azure Machine Learning en cuadernos, también está instalado:

    ```bash
    pip show azureml-widgets
    ```

4. Cierre la pestaña **Terminal** y vuelva a la pestaña que contiene la página principal de Jupyter.

> **Más información**: para obtener más información sobre cómo instalar el SDK de Azure ML y sus componentes opcionales, consulte la [documentación del SDK de Azure ML](https://docs.microsoft.com/python/api/overview/azure/ml/install?view=azure-ml-py).

## <a name="run-experiments-in-a-notebook"></a>Ejecutar experimentos en un cuaderno

Los experimentos de Azure Machine Learning deben iniciarse desde algún tipo de capa de *control* (a menudo, un script o un programa). En este ejercicio, usará un cuaderno para controlar los experimentos.

1. En la página principal de Jupyter, vaya a la carpeta **/users/*su-nombre-de-usuario*/mslearn-dp100** donde clonó el repositorio de cuadernos y abra el cuaderno **Ejecutar experimentos**.
2. A continuación, lea las notas del cuaderno y ejecute todas las celdas de código de una en una.
3. Cuando haya terminado de ejecutar el código en el cuaderno, en el menú **Archivo**, haga clic en **Cerrar y detener** para cerrarlo y apagar su kernel de Python. A continuación, cierre todas las pestañas del explorador de Jupyter.

## <a name="clean-up"></a>Limpieza

Si ha terminado de trabajar con Azure Machine Learning por ahora, en Azure Machine Learning Studio, en la pestaña **Instancias de proceso** de la página **Proceso**, seleccione la instancia de proceso y haga clic en **Detener** para cerrarlo. De lo contrario, déjelo en ejecución para el siguiente laboratorio.

> **Nota**: Al detener el proceso, garantiza que no se cobren los recursos de proceso en la suscripción. Sin embargo, se le cobrará un importe reducido por el almacenamiento de datos, siempre que el área de trabajo de Azure Machine Learning exista en la suscripción. Si ha terminado de explorar Azure Machine Learning, puede eliminar el área de trabajo de Azure Machine Learning y los recursos asociados. Sin embargo, si planea completar cualquier otro laboratorio de esta serie, deberá repetir el ejercicio *[Crear un área de trabajo de Azure Machine Learning](01-create-a-workspace.md)* para crear el área de trabajo y preparar primero el entorno.