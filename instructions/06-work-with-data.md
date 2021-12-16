---
lab:
  title: Trabajar con datos
ms.openlocfilehash: 6db1dd05ed150a1428ee355c932edc1082c1e3ba
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2021
ms.locfileid: "132832664"
---
# <a name="work-with-data"></a>Trabajo con datos

Aunque es bastante habitual trabajar con datos en su sistema de archivos local, en un entorno empresarial puede ser más eficaz almacenar los datos en una ubicación central donde varios científicos de datos e ingenieros de aprendizaje automático puedan acceder a ellos.

En este ejercicio, explorará *almacenes de datos* y *conjuntos de datos*, que son los objetos principales que se usan para abstraer el acceso a los datos en Azure Machine Learning.

## <a name="before-you-start"></a>Antes de empezar

Si todavía no lo ha hecho, complete el ejercicio *[Creación de un área de trabajo de Azure Machine Learning](01-create-a-workspace.md)* para crear un área de trabajo y una instancia de proceso de Azure Machine Learning y clone los cuadernos necesarios para completarlo.

## <a name="open-jupyter"></a>Abrir Jupyter

Aunque puede usar la página **Cuadernos** de Azure Machine Learning Studio para ejecutar cuadernos, a menudo es más productivo usar un entorno de desarrollo de cuadernos más completo como *Jupyter*.

1. En [Azure Machine Learning Studio](https://ml.azure.com), consulte la página **Proceso** del área de trabajo y, en la pestaña **Instancias de proceso**, inicie la instancia de proceso si aún no se está ejecutando.
2. Cuando se esté ejecutando la instancia de proceso, haga clic en el vinculo de **Jupyter** para abrir la página principal de Jupyter en una nueva pestaña del explorador.

## <a name="work-with-datastores-and-datasets"></a>Trabajar con almacenes de datos y conjuntos de datos

En este ejercicio, el código para trabajar con los datos se proporciona en un cuaderno.

1. En la página principal de Jupyter, vaya a la carpeta **/users/*su-nombre-de-usuario*/mslearn-dp100** donde clonó el repositorio de cuadernos y abra el cuaderno **Trabajar con datos**.
2. A continuación, lea las notas del cuaderno y ejecute todas las celdas de código de una en una.
3. Cuando haya terminado de ejecutar el código en el cuaderno, en el menú **Archivo**, haga clic en **Cerrar y detener** para cerrarlo y apagar su kernel de Python. A continuación, cierre todas las pestañas del explorador de Jupyter.

## <a name="clean-up"></a>Limpieza

Si ha terminado de trabajar con Azure Machine Learning por ahora, en Azure Machine Learning Studio, en la pestaña **Instancias de proceso** de la página **Proceso**, seleccione la instancia de proceso y haga clic en **Detener** para cerrarlo. De lo contrario, déjelo en ejecución para el siguiente laboratorio.

> **Nota**: Al detener el proceso, garantiza que no se cobren los recursos de proceso en la suscripción. Sin embargo, se le cobrará un importe reducido por el almacenamiento de datos, siempre que el área de trabajo de Azure Machine Learning exista en la suscripción. Si ha terminado de explorar Azure Machine Learning, puede eliminar el área de trabajo de Azure Machine Learning y los recursos asociados. Sin embargo, si planea completar cualquier otro laboratorio de esta serie, deberá repetir el ejercicio *[Crear un área de trabajo de Azure Machine Learning](01-create-a-workspace.md)* para crear el área de trabajo y preparar primero el entorno.