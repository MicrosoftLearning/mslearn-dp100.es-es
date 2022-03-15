---
lab:
  title: Entrenamiento de modelos
ms.openlocfilehash: dffa9edda34c599dfbd372fe898ddcf955f6f200
ms.sourcegitcommit: 66d8872bc3d24c2121e225be132b56f4df7920ac
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2022
ms.locfileid: "138597265"
---
# <a name="train-models"></a>Entrenar modelos

Machine Learning trata principalmente sobre el entrenamiento de modelos, que puede usar para proporcionar servicios predictivos a las aplicaciones. En este ejercicio, verá cómo puede usar los experimentos de Azure Machine Learning para ejecutar scripts de entrenamiento y cómo registrar los modelos entrenados resultantes.

## <a name="before-you-start"></a>Antes de empezar

Si todavía no lo ha hecho, complete el ejercicio *[Creación de un área de trabajo de Azure Machine Learning](01-create-a-workspace.md)* para crear un área de trabajo y una instancia de proceso de Azure Machine Learning y clone los cuadernos necesarios para completarlo.

## <a name="open-jupyter"></a>Abrir Jupyter

Aunque puede usar la página **Cuadernos** de Azure Machine Learning Studio para ejecutar cuadernos, a menudo es más productivo usar un entorno de desarrollo de cuadernos más completo como *Jupyter*.

1. En [Azure Machine Learning Studio](https://ml.azure.com), consulte la página **Proceso** del área de trabajo y, en la pestaña **Instancias de proceso**, inicie la instancia de proceso si aún no se está ejecutando.
2. Cuando se esté ejecutando la instancia de proceso, haga clic en el vinculo de **Jupyter** para abrir la página principal de Jupyter en una nueva pestaña del explorador.

> **Sugerencia**: ¿Es la primera vez que usa Python? Use la [hoja de referencia rápida de Python](cheat-sheets/dp100-cheat-sheet-python.pdf) para entender el código. ¿Es la primera vez que trabaja con aprendizaje automático? En la [introducción al aprendizaje automático](cheat-sheets/dp100-cheat-sheet-machine-learning.pdf) obtendrá información sobre el proceso de aprendizaje automático en Azure Machine Learning.

## <a name="train-models-using-the-azure-machine-learning-sdk"></a>Entrenar modelos con el SDK de Azure Machine Learning

En este ejercicio, el código para entrenar modelos se proporciona en un cuaderno.

1. En la página principal de Jupyter, vaya a la carpeta **/users/*su-nombre-de-usuario*/mslearn-dp100** donde clonó el repositorio de cuadernos y abra el cuaderno **Entrenar modelos**.
2. A continuación, lea las notas del cuaderno y ejecute todas las celdas de código de una en una.
3. Cuando haya terminado de ejecutar el código en el cuaderno, en el menú **Archivo**, haga clic en **Cerrar y detener** para cerrarlo y apagar su kernel de Python. A continuación, cierre todas las pestañas del explorador de Jupyter.

## <a name="clean-up"></a>Limpieza

Si ha terminado de trabajar con Azure Machine Learning por ahora, en Azure Machine Learning Studio, en la pestaña **Instancias de proceso** de la página **Proceso**, seleccione la instancia de proceso y haga clic en **Detener** para cerrarlo. De lo contrario, déjelo en ejecución para el siguiente laboratorio.

> **Nota**: Al detener el proceso, garantiza que no se cobren los recursos de proceso en la suscripción. Sin embargo, se le cobrará un importe reducido por el almacenamiento de datos, siempre que el área de trabajo de Azure Machine Learning exista en la suscripción. Si ha terminado de explorar Azure Machine Learning, puede eliminar el área de trabajo de Azure Machine Learning y los recursos asociados. Sin embargo, si planea completar cualquier otro laboratorio de esta serie, deberá repetir el ejercicio *[Crear un área de trabajo de Azure Machine Learning](01-create-a-workspace.md)* para crear el área de trabajo y preparar primero el entorno.