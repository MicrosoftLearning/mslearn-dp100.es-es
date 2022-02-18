---
title: Instrucciones hospedadas en línea
permalink: index.html
layout: home
ms.openlocfilehash: a2eb157b1d188655f4cfbcc575befec4a2e9c623
ms.sourcegitcommit: 18f734eeb1031a9cb69c3b294632efd2e69324ac
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2021
ms.locfileid: "137894586"
---
# <a name="azure-machine-learning-exercises"></a>Ejercicios de Azure Machine Learning

Este repositorio contiene los ejercicios de laboratorio práctico del curso de Microsoft [DP-100 *Diseño e implementación de una solución de ciencia de datos en Azure*](https://docs.microsoft.com/learn/certifications/courses/dp-100t01) y los [módulos autodirigidos equivalentes en Microsoft Learn](https://docs.microsoft.com/learn/paths/build-ai-solutions-with-azure-ml-service/). Los ejercicios están pensados para complementar los materiales de aprendizaje y permiten practicar el uso de las tecnologías descritas en estos materiales.

Para completar estos ejercicios, necesitará una suscripción a Microsoft Azure. Si su instructor no se la ha proporcionado, puede registrarse para obtener una evaluación gratuita en[https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| Ejercicios |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
