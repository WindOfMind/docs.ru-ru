---
title: Практическое руководство. Как разрешать конфликты путем переписывания значений базы данных
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fd6db0b8-c29c-48ff-b768-31d28e7a148c
ms.openlocfilehash: 7b8d7cf8ab2335c064062ed3ab4072d81e8042fe
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62033661"
---
# <a name="how-to-resolve-conflicts-by-overwriting-database-values"></a>Практическое руководство. Как разрешать конфликты путем переписывания значений базы данных
Чтобы выверить различия между ожидаемыми и фактическими значениями базы данных до повторной отправки изменений, можно воспользоваться <xref:System.Data.Linq.RefreshMode.KeepCurrentValues> для перезаписи значений базы данных. Дополнительные сведения см. в разделе [оптимистичный параллелизм: Общие сведения о](../../../../../../docs/framework/data/adonet/sql/linq/optimistic-concurrency-overview.md).  
  
> [!NOTE]
>  Во всех случаях запись на клиенте сначала обновляется путем извлечения обновленных данных из базы данных. Это действие гарантирует успешное выполнение следующей попытки обновления при тех же проверках параллелизма.  
  
## <a name="example"></a>Пример  
 В данном сценарии, когда Пользователь1 пытается отправить изменения, возникает исключение <xref:System.Data.Linq.ChangeConflictException>, поскольку Пользователь2 в это время изменил столбцы "Помощник" и "Отдел". Эта ситуация представлена в следующей таблице.  
  
||Руководитель|Помощник|Отдел|  
|------|-------------|---------------|----------------|  
|Исходное состояние базы данных при отправке запросов Пользователем1 и Пользователем2.|Алексеи|Мария|Продажи|  
|Пользователь1 готовится отправить изменения.|Алексей||Маркетинговый отдел|  
|Пользователь2 уже отправил изменения.||Инна|Служба|  
  
 Пользователь1 решает устранить этот конфликт путем перезаписи значений базы данных текущими значениями членов клиента.  
  
 При устранении Пользователем1 конфликта с помощью <xref:System.Data.Linq.RefreshMode.KeepCurrentValues> результат в базе данных будет соответствовать данным в следующей таблице.  
  
||Руководитель|Помощник|Отдел|  
|------|-------------|---------------|----------------|  
|Новое состояние после устранения конфликта.|Алексей<br /><br /> (от Пользователя1)|Мария<br /><br /> (исходное значение)|Маркетинговый отдел<br /><br /> (от Пользователя1)|  
  
 В следующем примере кода показано, как перезаписать значения базы данных текущими значениями членов клиента (проверка или пользовательская обработка конфликтов отдельных членов не выполняется).  
  
 [!code-csharp[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#2)]
 [!code-vb[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#2)]  
  
## <a name="see-also"></a>См. также

- [Практическое руководство. Управление конфликтами изменений](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)
