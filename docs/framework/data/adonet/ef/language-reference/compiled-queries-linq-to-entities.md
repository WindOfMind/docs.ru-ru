---
title: Компилированные запросы (LINQ to Entities)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8025ba1d-29c7-4407-841b-d5a3bed40b7a
ms.openlocfilehash: f3ba6bfd0f83270bc6b9e980fe92f6630c90ad49
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61785350"
---
# <a name="compiled-queries--linq-to-entities"></a>Компилированные запросы (LINQ to Entities)
Если приложение многократно выполняет похожие по структуре запросы на платформе Entity Framework, во многих случаях можно повысить производительность, скомпилировав запрос один раз, а затем выполняя его несколько раз с разными параметрами. Например, приложению может понадобиться получить всех клиентов из определенного города; имя города указывается пользователем во время выполнения с помощью формы. Для этих целей технология LINQ to Entities поддерживает использование скомпилированных запросов.  
  
 Начиная с версии 4.5 платформы .NET Framework, запросы LINQ кэшируются автоматически. Тем не менее можно использовать скомпилированные запросы LINQ для снижения затрат при последующем выполнении, и скомпилированные запросы могут быть более эффективными, чем запросы LINQ, которые автоматически сохраняются в кэше. Обратите внимание, что запросы LINQ to Entities, которые применяют оператор `Enumerable.Contains` к коллекции в памяти, автоматически не кэшируются. Также в скомпилированных запросах LINQ не допускаются коллекции в памяти с параметрами.  
  
 Класс <xref:System.Data.Objects.CompiledQuery> обеспечивает компиляцию и кэширование запросов для повторного использования. Концептуально данный класс содержит метод <xref:System.Data.Objects.CompiledQuery>`Compile` с несколькими перегрузками. Вызовите метод `Compile`, чтобы создать новый делегат, для представления скомпилированного запроса. Метод `Compile`, которому предоставляют контекст <xref:System.Data.Objects.ObjectContext> и значения параметров, возвращает делегата, который формирует определенный результат (например, экземпляр <xref:System.Linq.IQueryable%601>). Компиляция запроса выполняется только один раз во время первого выполнения. Параметры слияния, которые заданы для запроса во время компиляции, далее не могут быть изменены. После компиляции запроса ему можно передавать только параметры примитивного типа, но нельзя заменять части запроса, которые изменят созданный код SQL. Дополнительные сведения см. в разделе [параметры объединения Entity Framework и компилированные запросы](https://go.microsoft.com/fwlink/?LinkId=199591)  
  
 [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] Выражение запроса, <xref:System.Data.Objects.CompiledQuery> `Compile` компилирует метод представляется одним из универсальных `Func` делегаты, такие как <xref:System.Func%605>. Выражение запроса может инкапсулировать не более одного параметра `ObjectContext`, одного возвращаемого параметра и 16 параметров запроса. Если нужно больше 16 параметров запроса, то можно создать структуру, свойства которой будут соответствовать параметрам запроса. После задания свойств ими можно будет воспользоваться в выражении запроса из структуры.  
  
## <a name="example"></a>Пример  
 В следующем примере компилируется и вызывается запрос, принимающий входной параметр типа <xref:System.Decimal> и возвращающий последовательность заказов, сумма заказа которых больше или равна 200 долларам США:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery2)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery2)]  
  
## <a name="example"></a>Пример  
 В следующем примере компилируется и вызывается запрос, возвращающий экземпляр элемента <xref:System.Data.Objects.ObjectQuery%601>:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery1_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery1_mq)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery1_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery1_mq)]  
  
## <a name="example"></a>Пример  
 В следующем примере компилируется и затем вызывается запрос, возвращающий среднее значение цен списка продуктов в виде значения <xref:System.Decimal>:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery3_mq)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery3_mq)]  
  
## <a name="example"></a>Пример  
 Следующий пример компилируется и вызывается запрос, который принимает <xref:System.String> входного параметра, а затем возвращает `Contact` , адрес электронной почты которого начинается с указанной строкой:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery4_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery4_mq)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery4_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery4_mq)]  
  
## <a name="example"></a>Пример  
 В следующем примере компилируется и вызывается запрос, который принимает входные параметры <xref:System.DateTime> и <xref:System.Decimal> и возвращает последовательность заказов с датой позднее 8 марта 2003 г. и суммой заказа менее 300 долларов:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery5)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery5)]  
  
## <a name="example"></a>Пример  
 В следующем примере компилируется и вызывается запрос, принимающий входной параметр типа <xref:System.DateTime> и возвращающий последовательность заказов с датой после 8 марта 2004 г. Этот запрос возвращает сведения о заказе в виде последовательности анонимных типов. Анонимные типы выводятся компилятором, поэтому параметры типа нельзя указать в методе <xref:System.Data.Objects.CompiledQuery>`Compile` и тип определяется в самом запросе.  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery6)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery6)]  
  
## <a name="example"></a>Пример  
 В следующем примере компилируется и вызывается запрос, принимающий входной параметр в виде пользовательской структуры и возвращающий последовательность заказов. В структуре определяются такие параметры запроса, как время начала, окончания и общая сумма заказа, а запрос возвращает заказы, поставленные с 3 по 8 марта 2003 г. общей суммой более 700 долларов США.  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery7)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery7)]  
  
 Структура, определяющая параметры запроса:  
  
 [!code-csharp[DP L2E Conceptual Examples#MyParamsStruct](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#myparamsstruct)]
 [!code-vb[DP L2E Conceptual Examples#MyParamsStruct](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#myparamsstruct)]  
  
## <a name="see-also"></a>См. также

- [ADO.NET Entity Framework](../../../../../../docs/framework/data/adonet/ef/index.md)
- [LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)
- [Параметры слияния Entity Framework и компилированные запросы](https://go.microsoft.com/fwlink/?LinkId=199591)
