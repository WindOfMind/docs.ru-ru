---
ms.openlocfilehash: cbe1b32fa40e509f620845866c7a584e37f49a80
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774224"
---
### <a name="targetframeworkname-for-default-app-domain-no-longer-defaults-to-null-if-not-set"></a>TargetFrameworkName для домена приложения по умолчанию больше не принимает значение NULL по умолчанию, если оно не задано

|   |   |
|---|---|
|Подробные сведения|Свойство <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=name> имело ранее значение NULL в домене приложения по умолчанию, если оно не было задано явно. Начиная с версии 4.6, свойство <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=name> для домена приложения по умолчанию будет иметь значение по умолчанию, полученное из свойства TargetFrameworkAttribute (если оно доступно). Домены приложений не по умолчанию будут по-прежнему наследовать свойство <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=name> от домена приложения по умолчанию (который не будет по умолчанию иметь значение NULL в 4.6), если оно явно не переопределено.|
|Предложение|Следует обновить код так, чтобы он не зависел от <xref:System.AppDomainSetup.TargetFrameworkName>, принимающего п умолчанию значение NULL. Если требуется, чтобы свойство продолжало принимать значение NULL, ему можно явно присвоить это значение.|
|Область|Пограничный случай|
|Версия|4.6|
|Тип|Среда выполнения|
|Затронутые API|<ul><li><xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=nameWithType></li></ul>|
