---
title: 'Managed Extensibility Framework для .NET: приложения из магазина Windows Store'
ms.date: 03/30/2017
ms.assetid: 7667770e-d163-4ad6-a303-085cf73db2f2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b2b62e6fea6da46e6307b35dd1c3372420dced80
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648512"
---
# <a name="mef-for-net-for-windows-store-apps"></a>Managed Extensibility Framework для .NET: приложения из магазина Windows Store
Пространство имен <xref:System.Composition?displayProperty=nameWithType> и его дочерние пространства содержат типы для разработки расширяемых приложений для [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] с использованием Managed Extensibility Framework (MEF). Эти пространства имен являются частью подмножества [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] для операционной системы [!INCLUDE[win8](../../../includes/win8-md.md)].  
  
 Они не входят в состав основной библиотеки классов, распространяемой с платформой .NET Framework. Чтобы установить эти пространства имен, откройте проект в Visual Studio, выберите пункт **Управление пакетами NuGet** в меню **Проект** и найдите в Интернете пакет Microsoft.Composition.  
  
- <xref:System.Composition?displayProperty=nameWithType> предоставляет классы, которые составляют ядро MEF для приложений [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  
  
- <xref:System.Composition.Convention?displayProperty=nameWithType> предоставляет типы, поддерживающие использование MEF с моделью конфигурации на основе соглашений.  
  
- <xref:System.Composition.Hosting?displayProperty=nameWithType> предоставляет типы MEF, которые могут пригодиться разработчикам ведущих приложений.  
  
- <xref:System.Composition.Hosting.Core?displayProperty=nameWithType> предоставляет типы MEF, которые использует обработчик композиции.  
  
 Дополнительные сведения о платформе [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] и список входящих в нее пространств имен и типов см. в статье [Обзор приложений .NET для Магазина Windows](https://go.microsoft.com/fwlink/p/?LinkID=238312) в Центре разработки для Windows.  
  
## <a name="see-also"></a>См. также

- [Общие сведения о платформе .NET для приложений Магазина Windows](https://go.microsoft.com/fwlink/p/?LinkID=238312)
- [Поддерживаемые API .NET для приложений Магазина Windows](https://go.microsoft.com/fwlink/p/?LinkID=247912)
- [Managed Extensibility Framework (MEF)](../../../docs/framework/mef/index.md)
