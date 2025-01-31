---
title: Введение в расширяемость
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], extensibility
- Windows Communication Foundation [WCF], extensibility
- extensibility [WCF]
ms.assetid: ef56c251-d63c-4b3f-944f-b0c67bfb0f68
ms.openlocfilehash: 8ac605b562531329333b5f05e081d89de55d8cd2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645426"
---
# <a name="introduction-to-extensibility"></a>Введение в расширяемость
Модель приложения Windows Communication Foundation (WCF) призвана решить большей части связанных с обменом данных потребностей любого распределенного приложения. Однако всегда существуют сценарии, которые модель приложений по умолчанию и предоставленные системой реализации не поддерживают. Модель расширяемости WCF предназначен для поддержки пользовательских сценариев, предоставляя возможность изменять поведение системы на всех уровнях, вплоть до замены модели приложений целиком. В этом разделе кратко рассматриваются различные области расширения и даются ссылки на дополнительные сведения о каждой из них.  
  
## <a name="areas-to-extend"></a>Области расширения  
 Можно расширять следующее.  
  
- Среду выполнения приложения. При этом расширяются диспетчеризация и обработка сообщений для приложения. Сюда входит также расширение системы безопасности, системы метаданных, системы сериализации, а также привязок и элементов привязки, соединяющих приложение с системой базовых каналов.  
  
- Канал и среду выполнения канала. При этом расширяется система, функционирующая на уровне сообщения, и обеспечивается поддержка протоколов, транспорта и кодирования.  
  
- Среду выполнения узла. При этом расширяется связь домена приложения размещения с каналом и средой выполнения приложения.  
  
### <a name="extending-the-application-runtime"></a>Расширение среды выполнения приложения  
 В случае приложений WCF имеется различие между сообщениями, предназначенными для соответствующего канала и сообщения, предназначенные для самого приложения. Сообщения канала поддерживают некоторую связанную с каналами функциональность, такую как установление защищенного взаимодействия или установление безопасного сеанса. Эти сообщения недоступны среде выполнения приложения; они обрабатываются до задействования уровня приложения.  
  
 Сообщения приложения содержат данные, предназначенные для операции службы или клиента, созданной разработчиком или его заказчиком. Эти сообщения доступны системе расширения уровня приложения в виде сообщений или в виде объектов, в зависимости от конкретных потребностей.  
  
 Все сообщения проходят через систему каналов; только сообщения приложения передаются из системы каналов в приложение. Для создания новой функциональности уровня канала необходимо расширить систему каналов. Для создания новой функциональности уровня приложения необходимо расширить среду выполнения службы или клиента (соответственно диспетчеры и фабрики каналов). Дополнительные сведения о расширении среды выполнения приложения см. в разделе [расширение ServiceHost и уровень модели службы](../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md).  
  
#### <a name="extending-security"></a>Расширение безопасности  
 Для построения пользовательских механизмов безопасности, таких как маркеры и учетные данные, необходимо расширить систему безопасности. Дополнительные сведения см. в разделе [расширение безопасности](../../../docs/framework/wcf/extending/extending-security.md).  
  
#### <a name="extending-metadata"></a>Расширение системы метаданных  
 Чтобы предоставлять метаданные способом, отличным от предусмотренного по умолчанию, необходимо расширить систему метаданных. Дополнительные сведения см. в разделе [расширении системы метаданных](../../../docs/framework/wcf/extending/extending-the-metadata-system.md).  
  
#### <a name="extending-serialization"></a>Расширение системы сериализации  
 Для построения пользовательских кодировщиков, создания суррогатов данных или выполнения какой-либо иной обработки, подразумевающей настройку передаваемых данных, необходимо расширить систему сериализации. Дополнительные сведения см. в разделе [расширение кодировщиков и сериализаторов](../../../docs/framework/wcf/extending/extending-encoders-and-serializers.md).  
  
#### <a name="extending-bindings"></a>Расширение привязок  
 Для связывания каналов транспорта или протокола с уровнем приложения необходимо расширить систему привязок. Дополнительные сведения см. в разделе [расширение привязок](../../../docs/framework/wcf/extending/extending-bindings.md).  
  
### <a name="extending-the-channel-system"></a>Расширение системы каналов  
 Для создания каналов, которые поддерживают пользовательский транспорт или функциональности протокола, см. в разделе [расширение уровня каналов](../../../docs/framework/wcf/extending/extending-the-channel-layer.md).  
  
### <a name="extending-the-service-hosting-system"></a>Расширение системы размещения службы  
 Для изменения модели приложений в масштабе всей службы необходимо расширить класс <xref:System.ServiceModel.ServiceHostBase?displayProperty=nameWithType>. Дополнительные сведения см. в разделе [расширение ServiceHost и уровень модели службы](../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md).  
  
 Для изменения связи между доменом приложения размещения и узлом службы необходимо расширить класс <xref:System.ServiceModel.Activation.ServiceHostFactory?displayProperty=nameWithType>. Дополнительные сведения см. в разделе [расширение ServiceHostFactory размещение с помощью](../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md).  
  
## <a name="see-also"></a>См. также

- [Расширение WCF](../../../docs/framework/wcf/extending/index.md)
