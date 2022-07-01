---
lab:
  title: Uso del aprendizaje automático automatizado
ms.openlocfilehash: a4908c0de74edb6c2fdf7b1a7288014d1ab86b94
ms.sourcegitcommit: 48bc4227570b0817702d195aa06fa4dabe1bbdd7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2022
ms.locfileid: "146733071"
---
# <a name="use-automated-machine-learning"></a>Uso del aprendizaje automático automatizado

Azure Machine Learning incluye una funcionalidad de *aprendizaje automático automatizado* que aprovecha la escalabilidad del proceso en la nube para probar automáticamente varias técnicas de preprocesamiento y algoritmos de entrenamiento de modelos en paralelo a fin de encontrar el modelo de Machine Learning de mejor rendimiento para sus datos.

En este ejercicio, usará la interfaz visual para el aprendizaje automático automatizado en Azure Machine Learning Studio.

> **Nota**: También puede usar el aprendizaje automático automatizado a través del SDK de Azure Machine Learning.

## <a name="before-you-start"></a>Antes de comenzar

Si todavía no lo ha hecho, complete el ejercicio *[Creación de un área de trabajo de Azure Machine Learning](01-create-a-workspace.md)* para crear un área de trabajo y una instancia de proceso de Azure Machine Learning y clone los cuadernos necesarios para completarlo.

## <a name="configure-compute-resources"></a>Configurar recursos de proceso

Para usar el aprendizaje automático automatizado, necesita un proceso en el que ejecutar el experimento de entrenamiento del modelo.

1. Inicie sesión en [Azure Machine Learning Studio](https://ml.azure.com?azure-portal=true) con las credenciales de Microsoft asociadas a su suscripción de Azure y seleccione su área de trabajo de Azure Machine Learning.
2. En Azure Machine Learning Studio, consulte la página **Proceso** y, en la pestaña **Instancias de proceso**, inicie la instancia de proceso si aún no se está ejecutando. Usará esta instancia de proceso para probar el modelo entrenado.
3. Mientras se inicia la instancia de proceso, cambie a la pestaña **Clústeres de proceso** y agregue un nuevo clúster de proceso con la configuración siguiente. Ejecutará el experimento de aprendizaje automático automatizado en este clúster para aprovechar la capacidad de distribuir las ejecuciones de entrenamiento en varios nodos de proceso:
    - **Ubicación**: *la misma que la del área de trabajo*
    - **Nivel de máquina virtual**: dedicado
    - **Tipo de máquina virtual**: CPU
    - **Tamaño de la máquina virtual**: Standard_DS11_v2
    - **Nombre del proceso**: *escriba un nombre único*
    - **Número mínimo de nodos**: 0
    - **Número máximo de nodos**: 2
    - **Segundos de inactividad antes de la reducción vertical**: 120
    - **Habilitar acceso SSH**: no seleccionado

## <a name="create-a-dataset"></a>Crear un conjunto de datos

Ahora que tiene algunos recursos de proceso que puede usar para procesar datos, necesitará una manera de almacenar e ingerir los datos que se van a procesar.

1. Vea los datos separados por comas en https://aka.ms/diabetes-data, en el explorador web. A continuación, guárdelos como un archivo local denominado **diabetes.csv** (no importa dónde lo guarde).
2. En Estudio de Azure Machine Learning, vea la página **Datos**. Los conjuntos de datos representan archivos de datos o tablas específicos con los que tiene previsto trabajar en Azure Machine Learning.
3. Cree un conjunto de datos a partir de archivos locales con los valores siguientes:
    * **Información básica**:
        * **Nombre**: conjunto de datos de diabetes
        * **Tipo de conjunto de datos**: tabular
        * **Descripción**: datos de diabetes
    * **Almacén de archivos y selección de archivos**:
        * **Seleccionar o crear un almacén de datos**: el almacén de datos seleccionado actualmente.
        * **Seleccionar archivos para el conjunto de datos**: busque el archivo **diabetes.csv** que descargó.
        * **Ruta de acceso de la carga**: *deje la selección predeterminada*.
        * **Omitir validación de datos**: no seleccionado.
    * **Configuración y vista previa**:
        * **Formato de archivo**: delimitado
        * **Delimitador**: coma
        * **Codificación**: UTF-8
        * **Encabezados de columna**: solo el primer archivo tiene encabezados
        * **Omitir filas**: ninguno
    * **Esquema**:
        * incluir todas las columnas que no sean **Ruta de acceso**
        * Revisar los tipos detectados automáticamente
    * **Confirmación de detalles**:
        * no generar perfil de este conjunto de datos después de su creación
4. Después de crear el conjunto de datos, ábralo y vea la página **Explorar** para obtener una muestra de los datos. Estos datos representan los detalles de los pacientes que se han sometido a pruebas de diabetes y los usará para entrenar un modelo que prediga la probabilidad de que un paciente resulte positivo de diabetes según las medidas clínicas.

    > **Nota**: De manera opcional, puede generar un *perfil* del conjunto de datos para ver más datos estadísticos.

## <a name="run-an-automated-machine-learning-experiment"></a>Ejecución de un experimento de aprendizaje automático automatizado

En Azure Machine Learning, las operaciones que se ejecutan se denominan *experimentos*. Siga los pasos que se indican a continuación para ejecutar un experimento que use el aprendizaje automático automatizado con el fin de entrenar un modelo de clasificación que prediga los diagnósticos de diabetes.

1. En Azure Machine Learning Studio, vea la página **ML automatizado** (en **Autor**).
2. Cree una nueva ejecución de ML automatizado con la configuración siguiente:
    - **Selección del conjunto de datos**:
        - **Conjunto de datos**: conjunto de datos de diabetes
    - **Configuración de la ejecución**:
        - **Nuevo nombre del experimento**: mslearn-automl-diabetes
        - **Columna de destino**: Diabético/a (*esta es la etiqueta que tendrá que predecir el modelo entrenado)* .
        - **Select compute type** (Seleccionar tipo de proceso): el clúster de proceso.
        - **Select Azure ML compute cluster** (Seleccionar el clúster de proceso de Azure ML): *el clúster de proceso que creó anteriormente.*
    - **Tipo de tarea y configuración**:
        - **Tipo de tarea**: clasificación
        - Seleccione **(Ver opciones de configuración adicionales)** (Ver opciones de configuración adicionales) para abrir **Configuraciones adicionales**:
            - **Métrica primaria**: seleccione **AUC ponderado** *(encontrará más información sobre esta métrica más adelante).*
            - **Explicación del mejor modelo**: seleccionada: *esta opción hace que el aprendizaje automático automatizado calcule la importancia de la característica para el mejor modelo, permitiendo determinar la influencia de cada característica en la etiqueta de predicción*.
            - **Usar todos los modelos admitidos**: <u>no</u>seleccionado: restringiremos el experimento para probar algunos algoritmos específicos.
            - **Modelos permitidos**: seleccione únicamente **LogisticRegression** and **RandomForest**. Estos son los únicos algoritmos que se probarán en el experimento.
            - **Criterio de salida**:
                - **Training job time (hours)** (Tiempo del trabajo de entrenamiento [horas]): 0,5: *esto hace que el experimento finalice después de un máximo de 30 minutos.*
                - **Umbral de puntuación de métrica**: 0,90 (*provoca que el experimento finalice si un modelo alcanza una métrica de AUC ponderada del 90 % o superior*).
        - Seleccione **View featurization settings** (Ver configuración de caracterización) para abrir **Caracterización**:
            - **Habilitar caracterización**: seleccionado: *hace que Azure Machine Learning preprocese automáticamente las características antes del entrenamiento*.
    - **Seleccione el tipo de validación y prueba**:
        - **Tipo de validación**: división entre entrenamiento y validación.
        - **Percentage validation of data** (Validación de porcentaje de datos): 30
        - **Test dataset** (Conjunto de datos de prueba): no se requiere ningún conjunto de datos de prueba.

3. Cuando termine de enviar los detalles de la ejecución de ML automatizado, se iniciará automáticamente. Puede observar el estado de la ejecución en el panel **Propiedades**.
4. Cuando el estado de ejecución cambia a *En ejecución*, vea la pestaña **Modelos** y observe que se prueba cada combinación posible de algoritmos de entrenamiento y pasos de preprocesamiento y se evalúa el rendimiento del modelo resultante. La página se actualizará frecuentemente de forma automática, pero también puede seleccionar **&#8635; Actualizar**. Los modelos pueden tardar unos 10 minutos en empezar a aparecer, ya que los nodos de clúster se deben inicializar y se debe completar el proceso de caracterización de datos para poder comenzar el entrenamiento. Ahora podría ser un buen momento para hacer una pausa.
5. Espere a que finalice el experimento.

## <a name="review-the-best-model"></a>Revisión del mejor modelo

Una vez finalizado el experimento, puede revisar el modelo de mejor rendimiento que se haya generado (tenga en cuenta que, en este caso, hemos usado los criterios de salida para detener el experimento, por lo que el "mejor" modelo que encuentra el experimento puede no ser el mejor modelo posible, sino el mejor encontrado en el tiempo y con las restricciones de métricas que se permiten para este ejercicio).

1. En la pestaña **Introducción** de la ejecución del aprendizaje automático automatizado, tenga en cuenta el resumen del mejor modelo.
2. Seleccione el **Nombre del algoritmo** para el mejor modelo a fin de ver la ejecución secundaria que lo ha producido.

    El mejor modelo se identifica en función de la métrica de evaluación que ha especificado (*AUC_Weighted*). Para calcular esta métrica, el proceso de entrenamiento ha usado algunos de los datos a fin de entrenar el modelo y ha aplicado una técnica llamada *validación cruzada* con el fin de probar de forma iterativa el modelo entrenado con datos con los que no se ha entrenado y comparar el valor previsto con el valor conocido real. A partir de estas comparaciones, se tabula una *matriz de confusión* de verdaderos positivos, falsos positivos, verdaderos negativos y falsos negativos y se calculan métricas de clasificación adicionales, incluido un gráfico de curva de operador receptor (ROC) que compara la tasa de Verdadero positivo y la tasa de Falso positivo. El área bajo esta curva (AUC) es una métrica común que se usa para evaluar el rendimiento de la clasificación.
3. Junto al valor de *AUC_Weighted*, seleccione **View all other metrics** (Ver el resto de métricas) a fin de ver los valores de otras métricas de evaluación posibles para un modelo de clasificación.
4. Seleccione la pestaña **Métricas** y revise las métricas de rendimiento que puede ver del modelo. Estos incluyen una visualización **confusion_matrix**, que muestra la matriz de confusión del modelo validado, y una visualización **accuracy_table**, que incluye el gráfico ROC.
5. Seleccione la pestaña **Explicaciones**, seleccione un **Id. de explicación** y, a continuación, vea la página **Aggregate Importance** (Importancia de agregado). Muestra el grado en que cada característica del conjunto de datos influye en la predicción de la etiqueta.

## <a name="deploy-a-predictive-service"></a>Implementación de un servicio predictivo

Después de usar el aprendizaje automático automatizado a fin de entrenar algunos modelos, puede implementar el modelo de mejor rendimiento como servicio para que lo usen las aplicaciones cliente.

> **Nota**: En Azure Machine Learning, puede implementar un servicio como una instancia de Azure Container Instances (ACI) o en un clúster de Azure Kubernetes Service (AKS). En escenarios de producción, se recomienda una implementación de AKS, para lo cual debe crear un destino de proceso de *clúster de inferencia*. En este ejercicio usará un servicio ACI, que es un destino de implementación adecuado para las pruebas y no requiere la creación de un clúster de inferencia.

1. Seleccione la pestaña **Introducción** de la ejecución que produjo el mejor modelo.
2. En la opción **Implementar**, use el botón **Deploy to web service** (Implementar en el servicio web) para implementar el modelo con la siguiente configuración:
    - **Nombre**: auto-predict-diabetes
    - **Descripción**: predicción de la diabetes
    - **Tipo de proceso**: instancia de Azure Container.
    - **Habilitar autenticación**: seleccionado
    - **Use custom deployment assets** (Usar recursos de implementación personalizados): no seleccionado.
3. Espere a que se inicie la implementación; esto puede tardar unos segundos. A continuación, en la pestaña **Modelo**, en la sección **Resumen de modelo**, observe el valor de **Estado de la implementación** para el servicio **auto-predict-diabetes**, que debería ser **En ejecución**. Espere a que este estado cambie a **Correcto**. Es posible que tenga que seleccionar **&#8635; Actualizar** frecuentemente.  **NOTA** La operación puede tardar un poco, espere.
4. En Azure Machine Learning Studio, vea la página **Puntos de conexión** y seleccione el punto de conexión en tiempo real **auto-predict-rentals**. Luego, seleccione la pestaña **Consumir** y tenga en cuenta la información siguiente. La necesitará para conectarse al servicio implementado desde una aplicación cliente.
    - El punto de conexión REST para el servicio
    - Clave principal para el servicio
5. Observe que puede usar el vínculo &#10697; situado junto a estos valores para copiarlos en el Portapapeles.

## <a name="test-the-deployed-service"></a>Prueba del modelo implementado

Ahora que ha implementado un servicio, puede probarlo con un código sencillo.

1. Con la página **Consumir** de la página del servicio **auto-predict-diabetes** abierta en el explorador, abra una nueva pestaña y una segunda instancia de Azure Machine Learning Studio. Después, en la pestaña nueva, vea la página **Notebooks**.
2. En la página **Cuadernos**, en **Mis archivos**, diríjase a la carpeta **/users/*su-nombre-de-usuario*/mslearn-dp100** donde clonó el repositorio de cuadernos y abra el cuaderno **Obtener predicción de AutoML**.
3. Cuando se abra el cuaderno, asegúrese de que la instancia de proceso que ha creado antes esté seleccionada en el cuadro **Proceso** y que tiene el estado **En ejecución**.
4. En el cuaderno, reemplace los marcadores de posición **ENDPOINT** y **PRIMARY_KEY** por los valores del servicio, que puede copiar de la pestaña **Consumir** de la página del punto de conexión.
5. Ejecute la celda de código y vea la salida devuelta por el servicio web.

## <a name="clean-up"></a>Limpieza

El servicio web que se ha creado se hospeda en una *instancia de Azure Container*. Si no tiene previsto experimentar con él, debe eliminar el punto de conexión para evitar el uso innecesario de Azure. También debe detener la instancia de proceso hasta que la vuelva a necesitar.

1. En Azure Machine Learning Studio, en la pestaña **Puntos de conexión**, seleccione el punto de conexión **auto-predict-diabetes**. Después, seleccione **Eliminar** (&#128465;) y confirme que quiere eliminar el punto de conexión.
2. En la página **Proceso**, en la pestaña **Instancias de proceso**, seleccione la instancia de proceso y, luego, **Detener**.

> **Nota**: Al detener el proceso, garantiza que no se cobren los recursos de proceso en la suscripción. Sin embargo, se le cobrará un importe reducido por el almacenamiento de datos, siempre que el área de trabajo de Azure Machine Learning exista en la suscripción. Si ha terminado de explorar Azure Machine Learning, puede eliminar el área de trabajo de Azure Machine Learning y los recursos asociados. Sin embargo, si planea completar cualquier otro laboratorio de esta serie, deberá repetir el ejercicio *[Crear un área de trabajo de Azure Machine Learning](01-create-a-workspace.md)* para crear el área de trabajo y preparar primero el entorno.
