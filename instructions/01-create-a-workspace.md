---
lab:
  title: Creación de un área de trabajo de Azure Machine Learning
ms.openlocfilehash: c2f33973281221da1a4871f19fbaff8f127d028f
ms.sourcegitcommit: 8601551af6c32a4c75fd9ecffce750583c2ab4b8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/01/2022
ms.locfileid: "141346682"
---
# <a name="create-and-explore-an-azure-machine-learning-workspace"></a>Creación y exploración de un área de trabajo de Azure Machine Learning

En este ejercicio, creará y explorará un área de trabajo de Azure Machine Learning.

## <a name="create-an-azure-machine-learning-workspace"></a>Creación de un área de trabajo de Azure Machine Learning

Como sugiere su nombre, un área de trabajo es un lugar centralizado para administrar todos los recursos de Azure ML que necesita para trabajar en un proyecto de aprendizaje automático.

1. En [Azure Portal](https://portal.azure.com), cree un nuevo recurso de **Machine Learning** y especifique la siguiente configuración:

    - **Suscripción**: *suscripción de Azure*
    - **Grupo de recursos**: *cree o seleccione un grupo de recursos*.
    - **Nombre del área de trabajo**: *escriba un nombre único para el área de trabajo*.
    - **Región**: *seleccione la región geográfica más cercana*.
    - **Cuenta de almacenamiento**: *tenga en cuenta la nueva cuenta de almacenamiento predeterminada que se creará para el área de trabajo*.
    - **Almacén de claves**: *tenga en cuenta el nuevo almacén de claves predeterminado que se creará para el área de trabajo*.
    - **Application Insights**: *tenga en cuenta el nuevo recurso de Application Insights predeterminado que se creará para el área de trabajo*.
    - **Registro de contenedor**: ninguno (*se creará uno automáticamente la primera vez que implemente un modelo en un contenedor*).

    > **Nota**: Al crear un área de trabajo de Azure Machine Learning, puede usar algunas opciones avanzadas para restringir el acceso a través de un *punto de conexión privado* y especificar claves personalizadas para el cifrado de datos. No usaremos estas opciones en este ejercicio, pero debe tenerlas en cuenta.

2. Cuando se hayan creado el área de trabajo y sus recursos asociados, vea el área de trabajo en el portal.

## <a name="explore-azure-machine-learning-studio"></a>Exploración de Azure Machine Learning Studio

Puede administrar algunos recursos de área de trabajo en Azure Portal, aunque para los científicos de datos esta herramienta contiene mucha información y vínculos irrelevantes relacionados con la administración de recursos generales de Azure. *Azure Machine Learning Studio* proporciona un portal web dedicado para trabajar con el área de trabajo.

1. En la hoja de Azure Portal del área de trabajo de Azure Machine Learning, haga clic en el vínculo para iniciar Studio; o bien, en una nueva pestaña del explorador, abra [https://ml.azure.com](https://ml.azure.com). Si se le solicita, inicie sesión con la cuenta Microsoft que usó en la tarea anterior y seleccione la suscripción y el área de trabajo de Azure.

    > **Sugerencia** Si tiene varias suscripciones de Azure, debe elegir el *directorio* de Azure en el que está definida la suscripción. A continuación, elija la suscripción y, por último, el área de trabajo.

2. Consulte la interfaz de Azure Machine Learning Studio para su área de trabajo: puede administrar todos los recursos del área de trabajo desde aquí.
3. En Azure Machine Learning Studio, alterne el icono &#9776; en la parte superior izquierda para mostrar y ocultar las distintas páginas de la interfaz. Puede usar estas páginas para administrar los recursos en el área de trabajo.

## <a name="create-a-compute-instance"></a>Creación de una instancia de proceso

Una de las ventajas de Azure Machine Learning es la capacidad de crear un proceso basado en la nube en el que pueda ejecutar experimentos y scripts de entrenamiento a gran escala.

1. En Azure Machine Learning Studio, vaya a la página **Proceso**. Aquí es donde administrará los recursos de proceso para las actividades de ciencia de datos. Puede crear cuatro tipos de recursos de proceso:
    - **Instancias de proceso**: estaciones de trabajo de desarrollo que los científicos de datos pueden usar para trabajar con datos y modelos.
    - **Clústeres de proceso**: clústeres escalables de máquinas virtuales para el procesamiento a petición de código de experimento.
    - **Clústeres de inferencia**: destinos de implementación para servicios predictivos que usan los modelos entrenados.
    - **Proceso asociado**: vínculos a otros recursos de proceso de Azure, como clústeres de Azure Virtual Machines o Azure Databricks.

    Para este ejercicio, creará una instancia de proceso para poder ejecutar algo de código en el área de trabajo.

2. En la pestaña **Instancias de proceso**, agregue una nueva instancia de proceso con los valores siguientes. La usará como estación de trabajo para ejecutar código en los cuadernos.
    - **Nombre del proceso**: *escriba un nombre único*.
    - **Ubicación**: *la misma que la del área de trabajo*
    - **Tipo de máquina virtual**: CPU
    - **Tamaño de máquina virtual**: Standard_DS11_v2
    - **Total de cuotas disponibles**: muestra los núcleos dedicados disponibles.
    - **Mostrar la configuración avanzada**: tenga en cuenta la siguiente configuración, pero no la seleccione. 
        - **Enable SSH access** (Habilitar acceso SSH): no seleccionada *(se puede usar para habilitar el acceso directo a la máquina virtual mediante un cliente SSH).*
        - **Enable virtual network** (Habilitar red virtual): no seleccionada *(normalmente se usaría en un entorno empresarial para mejorar la seguridad de red).*
        - **Asignar a otro usuario**: no seleccionada *(puede usarla para asignar una instancia de proceso a un científico de datos).* 3. Espere a que se inicie la instancia de proceso y su estado cambie a **En ejecución**.

> **Nota**: Las instancias de proceso y los clústeres se basan en imágenes de máquina virtual de Azure estándar. Para este ejercicio, se recomienda la imagen *Standard_DS11_v2* para lograr el equilibrio óptimo entre el costo y el rendimiento. Si la suscripción tiene una cuota que no incluye esta imagen, elija una imagen alternativa, pero tenga en cuenta que una imagen más grande puede incurrir en un costo mayor y una imagen más pequeña puede no ser suficiente para completar las tareas. Como alternativa, pida al administrador de Azure que amplíe la cuota.

## <a name="clone-and-run-a-notebook"></a>Clonación y ejecución de un cuaderno

Al ejecutar código en *cuadernos* se realiza una gran cantidad de experimentación de ciencia de datos y aprendizaje automático. La instancia de proceso incluye entornos de cuadernos de Python con todas las características *(Jupyter* y *JuypyterLab)* , que puede usar para un amplio trabajo. No obstante, para la edición básica de cuadernos, puede usar la página **Cuadernos** integrada en Azure Machine Learning Studio.

1. En Azure Machine Learning Studio, vaya a la página **Cuadernos**.
2. Si se muestra un mensaje que describe las nuevas características, ciérrelo.
3. Seleccione **Terminal** o el icono para **abrir el terminal** y asegúrese de que el **Proceso** correspondiente está establecido en su instancia de proceso y de que la ruta de acceso actual es la carpeta **/users/su-nombre-de-usuario**.
4. Escriba el siguiente comando para clonar un repositorio de Git que contenga cuadernos, datos y otros archivos en su área de trabajo:

    ```bash
    git clone https://github.com/MicrosoftLearning/mslearn-dp100 mslearn-dp100
    ```

4. Una vez completado el comando, en el panel **Archivos**, haga clic en **&#8635;** para actualizar la vista y compruebe que se ha creado la carpeta **/users/*su-nombre-de-usuario*/mslearn-dp100**. Esta carpeta contiene varios archivos de cuaderno **.ipynb**.
5. Cierre el panel del terminal y finalice la sesión.
6. En la carpeta **/users/*su-nombre-de-usuario*/mslearn-dp100**, abra el cuaderno **Introducción a Notebooks**. A continuación, lea las notas y siga las instrucciones que contiene.

> **Sugerencia**: Para ejecutar una celda de código, seleccione la celda que desea ejecutar y, a continuación, use el botón **&#9655;** para ejecutarla. 

> **¿Es la primera vez que usa Python?** Use la [hoja de referencia rápida de Python](cheat-sheets/dp100-cheat-sheet-python.pdf) para entender el código.

> **¿Es la primera vez que trabaja con aprendizaje automático?** En la [introducción al aprendizaje automático](cheat-sheets/dp100-cheat-sheet-machine-learning.pdf) obtendrá información sobre el proceso de aprendizaje automático en Azure Machine Learning.

## <a name="stop-your-compute-instance"></a>Detención de la instancia de proceso

Si ha terminado de explorar Azure Machine Learning, debe apagar la instancia de proceso para evitar incurrir en cargos innecesarios en la suscripción de Azure.

1. En Azure Machine Learning Studio, en la página **Proceso**, seleccione su instancia de proceso.
2. Haga clic en **Detener** para detenerla. Una vez apagada, su estado cambiará a **Detenido**.

> **Nota**: Al detener el proceso, garantiza que no se cobren los recursos de proceso en la suscripción. Sin embargo, se le cobrará un importe reducido por el almacenamiento de datos, siempre que el área de trabajo de Azure Machine Learning exista en la suscripción. Si ha terminado de explorar Azure Machine Learning, puede eliminar el área de trabajo de Azure Machine Learning y los recursos asociados. Sin embargo, si planea completar cualquier otro laboratorio de esta serie, deberá repetir este laboratorio para crear el área de trabajo y preparar el entorno primero.
