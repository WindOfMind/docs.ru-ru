---
title: Моделирование и сопоставление
ms.date: 03/30/2017
ms.assetid: ec8a9515-3708-4cde-a688-4d8e6975f150
ms.openlocfilehash: 55fea170d98c737197d1e3e26c8d25fd97760ddd
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65583580"
---
# <a name="modeling-and-mapping"></a>Моделирование и сопоставление
Платформа [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] позволяет определить концептуальную модель, модель хранения и сопоставление между ними, которые оптимальным образом подходят для приложения. Средств модели EDM в Visual Studio позволяют создавать. [EDMX-файла](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100)) из базы данных или графической модели и затем обновлять его при изменении модели или базы данных.  
  
 Начиная с версии 4.1 платформы Entity Framework модель можно также создавать программно с помощью шаблона разработки Code First. Шаблон разработки Code First имеет два различных сценария. В обоих случаях разработчик определяет модель, задавая в коде определения классов .NET Framework, а затем выборочно определяет дополнительные сопоставления или конфигурации с помощью заметок к данным или fluent API.  
  
 Дополнительные сведения см. в разделе [Создание и сопоставление концептуальной модели](https://go.microsoft.com/fwlink/?LinkId=235016).  
  
 Можно также использовать генератор модели EDM, который входит в состав .NET Framework. Программа EdmGen.exe формирует файлы языка CSDL, SSDL и MSL на основе существующего источника данных. Можно также вручную создать содержимое модели и сопоставления. Дополнительные сведения см. в разделе [генератор модели EDM (EdmGen.exe)](../../../../../docs/framework/data/adonet/ef/edm-generator-edmgen-exe.md).
