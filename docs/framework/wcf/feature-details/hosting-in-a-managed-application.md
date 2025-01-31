---
title: Размещение в управляемом приложении
ms.date: 03/30/2017
ms.assetid: af70132d-e9e1-4f32-b20f-f0014629758a
ms.openlocfilehash: c1f4d91994ba44407ff5c93dbd34aa0bdef9332b
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591733"
---
# <a name="hosting-in-a-managed-application"></a>Размещение в управляемом приложении
Службы Windows Communication Foundation (WCF), могут размещаться в любом приложении .NET Framework. Резидентное размещение служб - самый гибкий вариант размещения, так как в этом случае требуется минимальное развертывание инфраструктуры. Тем не менее это наименее надежный вариант размещения, поскольку управляемые приложения не предоставляют расширенные размещения и функции управления другие варианты размещения в WCF, такими как службы Internet Information Services (IIS) и Windows.  
  
 Для создания резидентной службы необходимо создать и открыть экземпляр узла службы <xref:System.ServiceModel.ServiceHost>, который запускает службу, ожидающую сообщений. Дополнительные сведения см. в разделе [Практическое руководство. Размещение службы WCF в управляемом приложении](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md).  
  
 Полный пример о том, как определить контракт, реализация контракта и размещения службы внутри управляемого приложения см. в разделе [Приступая к работе](../../../../docs/framework/wcf/getting-started-tutorial.md) и [резидентного размещения](../../../../docs/framework/wcf/samples/self-host.md).  
  
 В следующих разделах описаны стандартные сценарии, использующие этот вариант размещения.  
  
## <a name="console-applications"></a>Консольные приложения  
 Распространенные сценарии, после чего размещение на собственном сервере, службы WCF, выполняющиеся внутри консольных приложений. Размещение службы WCF внутри консольного приложения обычно используется на этапе разработки службы. В этом случае приложение легко отлаживать, удобно получать данные трассировки, чтобы узнать, что происходит внутри приложения, и удобно копировать приложение в другие расположения.  
  
## <a name="rich-client-applications"></a>Функционально насыщенные клиентские приложения  
 Других стандартных сценариев, обеспечиваемых резидентным размещением полнофункциональных клиентских приложений, например тех, на основе Windows Presentation Foundation (WPF) или Windows Forms (WinForms). Кроме того, этот вариант размещения упрощает взаимодействие функционально насыщенных клиентских приложений, таких как приложения [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] и WinForms, с внешними системами. Например, клиент peer-to-peer совместной работы, использующий [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] для пользовательского интерфейса и также размещается служба WCF, позволяющую другим клиентам подключаться к нему и обмениваться информацией.  
  
## <a name="see-also"></a>См. также

- [Размещение служб](../../../../docs/framework/wcf/hosting-services.md)
- [Руководство по началу работы](../../../../docs/framework/wcf/getting-started-tutorial.md)
