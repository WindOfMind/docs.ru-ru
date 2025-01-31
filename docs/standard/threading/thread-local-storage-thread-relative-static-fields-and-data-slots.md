---
title: Локальное хранилище потока. Статические поля потока и области данных
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], local storage
- threading [.NET Framework], thread-relative static fields
- local thread storage
- TLS
ms.assetid: c633a4dc-a790-4ed1-96b5-f72bd968b284
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 681a9e71dcfb139c364d750383f13cdabbf33366
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64644894"
---
# <a name="thread-local-storage-thread-relative-static-fields-and-data-slots"></a>Локальное хранилище потока. Статические поля потока и области данных
Вы можете использовать управляемую локальную память потока для хранения данных, которые являются уникальными для потока и домена приложения. Платформа .NET Framework предоставляет два способа работы с локальной памятью: статические поля потоков и ячейки данных.  
  
- Статические поля потоков (поля потоков `Shared` в Visual Basic) можно применять, если вы можете точно прогнозировать потребности во время компиляции. Статические поля потоков обеспечивают более высокую производительность. Они также позволяют выполнять проверки типов во время компиляции.  
  
- Если фактические требования могут определяться только во время выполнения, используйте области данных. Области данных работают медленнее и менее удобны в использовании, чем статические поля потоков. Данные в них хранятся в качестве типа <xref:System.Object>, поэтому перед использованием необходимо привести их к правильному типу.  
  
 В неуправляемом коде C++ используются `TlsAlloc` для динамического выделения областей данных и `__declspec(thread)` для объявления переменных, которые нужно выделять в хранилище потока. Статические поля потоков и области данных реализуют такое же поведение для управляемого кода.  
  
 В [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] вы можете использовать класс <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> для создания объектов локального потока с отложенной инициализацией (при первом использовании объекта). Дополнительные сведения см. в статье [Отложенная инициализация](../../../docs/framework/performance/lazy-initialization.md).  
  
## <a name="uniqueness-of-data-in-managed-tls"></a>Уникальность данных в управляемой локальной памяти потока  
 Независимо от того, что вы используете — статические поля потоков или области данных — данные в управляемой локальной памяти потока являются уникальными для определенной комбинации потока и домена приложения.  
  
- Любой поток в домене приложения не может изменять данные другого потока, даже если оба потока используют одинаковые поля или области памяти.  
  
- Если поток обращается к одному полю или области через разные домены приложений, в каждом домене приложения для него хранится отдельное значение.  
  
 Таким образом, если поток устанавливает значение для статического поля потока, затем переходит в другой домен приложения и извлекает значение этого поля, он получит во втором домене приложения другое значение, отличное от значения в первом домене приложения. Сохранение нового значения для поля во втором домене приложения никак не влияет на значение этого поля в первом домене приложения.  
  
 Аналогичным образом, если поток получает одинаковую именованную область данных в двух разных доменах приложений, данные в первом домене не будут зависеть от данных во втором домене приложения.  
  
## <a name="thread-relative-static-fields"></a>Статические поля потоков  
 Если вы твердо уверены, что некоторые данные всегда уникальны для потока и домена приложения, примените для статического поля атрибут <xref:System.ThreadStaticAttribute>. Используйте это поле так же, как любое обычное статическое поле. Данные в этом поле всегда будут уникальными для каждого потока, который его использует.  
  
 Статические поля потоков обеспечивают более высокую производительность, чем области данных, и позволяют выполнять проверку типов во время компиляции.  
  
 Имейте в виду, что любой код конструктора класса будет выполняться в первом потоке в первом контексте, где происходит обращение к полю. Во всех других потоках и (или) контекстах в том же домене приложения эти поля получают значения `null` (`Nothing` в Visual Basic), а если они являются ссылочными типами, — значения по умолчанию для соответствующих типов. Таким образом, вы не можете инициализировать статические поля потоков через конструктор класса. Старайтесь не применять инициализацию для статических полей потоков, и всегда предполагайте, что они имеют значение `null` (`Nothing`) или значение по умолчанию для типа.  
  
## <a name="data-slots"></a>Области данных  
 Платформа .NET Framework предоставляет динамически выделяемые ячейки данных, которые являются уникальными для каждой комбинации потока и домена приложения. Есть два типа областей данных: именованные и безымянные. Оба типа реализуются с помощью структуры <xref:System.LocalDataStoreSlot>.  
  
- Чтобы создать именованную область данных, используйте метод <xref:System.Threading.Thread.AllocateNamedDataSlot%2A?displayProperty=nameWithType> или <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=nameWithType>. Чтобы получить ссылку на существующую именованную область, передайте ее имя в метод <xref:System.Threading.Thread.GetNamedDataSlot%2A>.  
  
- Чтобы создать неименованную область данных, используйте метод <xref:System.Threading.Thread.AllocateDataSlot%2A?displayProperty=nameWithType>.  
  
 Как для именованных, так и для неименованных областей данных можно применять методы <xref:System.Threading.Thread.SetData%2A?displayProperty=nameWithType> и <xref:System.Threading.Thread.GetData%2A?displayProperty=nameWithType> для сохранения и получения данных. Это статические методы, которые всегда работают с данными того потока, который их выполняет.  
  
 Именованные области особенно удобны, так как позволяют в любой момент получить нужную область, передав ее имя в метод <xref:System.Threading.Thread.GetNamedDataSlot%2A>, вместо того чтобы хранить ссылку на безымянную область. Но если другой компонент использует то же имя в своем хранилище потока, при выполнении в одном потоке кода из обоих этих компонентов они могут повредить данные друг друга. (Здесь предполагается, что оба компонента работают в одном домене приложения и не рассчитаны на совместное использование данных.)  
  
## <a name="see-also"></a>См. также

- <xref:System.ContextStaticAttribute>
- <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=nameWithType>
- <xref:System.ThreadStaticAttribute>
- <xref:System.Runtime.Remoting.Messaging.CallContext>
- [Работа с потоками](../../../docs/standard/threading/index.md)
