---
title: Использование средства привязки сериализации
ms.date: 03/30/2017
ms.assetid: ab46c087-200c-45bf-9c95-5a6cda6e8b98
ms.openlocfilehash: 677decebcf444fed95311bd02acf8a96e0a4eca9
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591775"
---
# <a name="usage-of-serialization-binder"></a>Использование средства привязки сериализации
В этом образце показано, как использовать <xref:System.Runtime.Serialization.SerializationBinder> для изменения версии универсального типа во время сериализации.  
  
## <a name="demonstrates"></a>Демонстрации  
 <xref:System.Runtime.Serialization.SerializationBinder>, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>  
  
## <a name="discussion"></a>Обсуждение  
 В этом примере показано, как две сущности, предназначенных для разных версий .NET Framework могут обмениваться данными с помощью двоичного форматировщика и средства привязки сериализации.  
  
 Разработка данного образца производилась с помощью .NET Remoting. Образец состоит из сервера, ориентированного на [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)], который реализует контракт с универсальными типами, и двух различных клиентов, один из которых ориентирован на [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)], а другой на [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)].  
  
 Сервер присоединяет средство привязки <xref:System.Runtime.Serialization.SerializationBinder> к двоичному форматировщику, чтобы иметь возможность соответствующим образом изменять версию типов при сериализации, в результате чего оба клиента смогут правильно десериализовать эти типы.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Настройка, построение и выполнение примера  
  
1. Чтобы запустить клиент, щелкните правой кнопкой мыши решение SBGenericsVTS (6 проектов), а затем выберите **свойства**.  
  
2. В **общие свойства**выберите **запускаемым проектом**, а затем выберите **несколько запускаемых проектов**.  
  
3. Выберите **Server** первой, затем **Client20** и затем **Client40**. Выберите **запустить** действие для трех этих проектов и оставьте остальные **None**.  
  
4. Нажмите кнопку **ОК** и нажмите клавишу F5 для запуска примера.
