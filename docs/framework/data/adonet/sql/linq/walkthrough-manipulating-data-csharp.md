---
title: Пошаговое руководство. Обработка данных (C#)
ms.date: 03/30/2017
ms.assetid: 24adfbe0-0ad6-449f-997d-8808e0770d2e
ms.openlocfilehash: 7bac370ae8dc260ca4b665fd51680a80fd9846fd
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64618039"
---
# <a name="walkthrough-manipulating-data-c"></a>Пошаговое руководство. Обработка данных (C#)
В данном руководстве представлен основной и полный сценарий [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] по добавлению, изменению и удалению данных в базе данных. Для добавления клиента, изменения его имени и удаления заказа следует использовать копию учебной базы данных Northwind.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Это пошаговое руководство было написано с использованием параметров разработки Visual C#.  
  
## <a name="prerequisites"></a>Предварительные требования  
 Необходимо выполнить следующие требования.  
  
- Для хранения файлов используется выделенная папка ("c:\linqtest6"). Прежде чем приступить к выполнению задач, создайте такую папку.  
  
- Наличие учебной базы данных Northwind.  
  
     Если база данных не установлена на компьютере разработчика, загрузите ее с веб-узла Центра загрузки Майкрософт. Инструкции см. в разделе [Загрузка примеров баз данных](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md). После загрузки базы данных скопируйте файл northwnd.mdf в папку c:\linqtest6.  
  
- Наличие файла кода C#, созданного из базы данных Northwind.  
  
     Его можно создать либо помощью оператора [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)], либо с помощью средства SQLMetal. Данное пошаговое руководство было написано с использованием средства SQLMetal со следующей командной строкой:  
  
     **sqlmetal /code:"c:\linqtest6\northwind.cs" /language:csharp "C:\linqtest6\northwnd.mdf" /pluralize**  
  
     Дополнительные сведения см. в разделе [SQLMetal.exe (средство создания кода)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## <a name="overview"></a>Обзор  
 Данное пошаговое руководство состоит из шести основных задач.  
  
- Создание [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] решения в Visual Studio.  
  
- Добавление файла кода базы данных в проект.  
  
- Создание нового объекта клиента.  
  
- Изменение контактного имени клиента.  
  
- Удаление заказа.  
  
- Отправка внесенных изменений в базу данных Northwind.  
  
## <a name="creating-a-linq-to-sql-solution"></a>Создание решения LINQ to SQL  
 В первой задаче создается решение Visual Studio, содержащее ссылки, необходимые для построения и запуска [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] проекта.  
  
#### <a name="to-create-a-linq-to-sql-solution"></a>Создание решения LINQ to SQL  
  
1. В Visual Studio **файл** последовательно выберите пункты **New**, а затем нажмите кнопку **проекта**.  
  
2. В **типы проектов** области в **новый проект** диалоговом окне щелкните **Visual C#** .  
  
3. В области **Шаблоны** щелкните **Консольное приложение**.  
  
4. В **имя** введите **LinqDataManipulationApp**.  
  
5. В **расположение** убедитесь в том, где будут храниться файлы проекта.  
  
6. Нажмите кнопку **ОК**.  
  
## <a name="adding-linq-references-and-directives"></a>Добавление ссылок и директив LINQ  
 В этом пошаговом руководстве используются сборки, которые могут быть не установлены по умолчанию в проект. Если System.Data.Linq не входит в список ссылок проекта, добавьте ее, как описано в следующих действиях.  
  
#### <a name="to-add-systemdatalinq"></a>Добавление сборки System.Data.Linq  
  
1. В **обозревателе решений**, щелкните правой кнопкой мыши **ссылки**, а затем нажмите кнопку **добавить ссылку**.  
  
2. В **добавить ссылку** диалоговом окне щелкните **.NET**, выберите сборку System.Data.Linq, затем нажмите кнопку **ОК**.  
  
     Сборка будет добавлена в проект.  
  
3. Добавьте следующие директивы в начало Program.cs.  
  
     [!code-csharp[DLinqWalk3CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#1)]  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a>Добавление файла кода Northwind в проект  
 При выполнении этих действий подразумевается, что для создания файла кода из учебной базы данных Northwind использовалось средство SQLMetal. Дополнительные сведения см. в разделе "Предварительные требования" ранее в этом руководстве.  
  
#### <a name="to-add-the-northwind-code-file-to-the-project"></a>Добавление файла кода northwind в проект  
  
1. На **проекта** меню, щелкните **добавить существующий элемент**.  
  
2. В **добавить существующий элемент** диалоговом окне перейдите к c:\linqtest6\northwind.cs и нажмите кнопку **добавить**.  
  
     Файл northwind.cs будет добавлен в проект.  
  
## <a name="setting-up-the-database-connection"></a>Настройка подключения к базе данных  
 Сначала проверьте подключение к базе данных. Обратите особое внимание, что в имени базы данных - Northwnd - отсутствует буква "i". Если при выполнении следующих действий возникают ошибки, просмотрите файл northwind.cs, чтобы определить написание разделяемого класса Northwind.  
  
#### <a name="to-set-up-and-test-the-database-connection"></a>Настройка и проверка подключения к базе данных  
  
1. Введите или вставьте следующий код в метод `Main` в классе Program.  
  
     [!code-csharp[DLinqWalk3CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#2)]  
  
2. Чтобы проверить приложение на этом этапе, нажмите клавишу F5.  
  
     Объект **консоли** откроется окно.  
  
     Можно закрыть приложение, нажав клавишу ВВОД в **консоли** окна, или щелкнув **остановить отладку** на Visual Studio **Отладка** меню.  
  
## <a name="creating-a-new-entity"></a>Создание новой сущности  
 Создание новой сущности не представляет особых проблем. Для создания объектов (например, `Customer`) можно использовать ключевое слово `new`.  
  
 В этом и следующих разделах выполняются изменения только локального кэша. Изменения не будут отправлены в базу данных до тех пор, пока ближе к концу данного руководства не будет вызван <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  
  
#### <a name="to-add-a-new-customer-entity-object"></a>Добавление нового объекта сущностей Customer  
  
1. Создайте новый `Customer`, добавив перед `Console.ReadLine();`в методе `Main` следующий код.  
  
     [!code-csharp[DLinqWalk3CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#3)]  
  
2. Нажмите клавишу F5 для отладки решения.  
  
3. Нажмите клавишу ВВОД в **консоли** окно, чтобы остановить отладку и продолжить выполнение других действий.  
  
## <a name="updating-an-entity"></a>Обновление сущности  
 При выполнении следующих действий будет извлечен объект `Customer` и изменено одно из его свойств.  
  
#### <a name="to-change-the-name-of-a-customer"></a>Изменение имени клиента  
  
- Добавьте следующий код перед `Console.ReadLine();`:  
  
     [!code-csharp[DLinqWalk3CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#4)]  
  
## <a name="deleting-an-entity"></a>Удаление сущности  
 Используя тот же самый объект клиента, можно удалить первый заказ.  
  
 В следующем коде показано, как разорвать связь между строками и удалить строку из базы данных. Чтобы удаление объектов, добавьте следующий код перед `Console.ReadLine`.  
  
#### <a name="to-delete-a-row"></a>Удаление строки  
  
- Добавьте следующий код перед `Console.ReadLine();`.  
  
     [!code-csharp[DLinqWalk3CS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#5)]  
  
## <a name="submitting-changes-to-the-database"></a>Отправка изменений в базу данных  
 Последнее действие, необходимое для создания, обновления и удаления объектов, заключается в фактической отправке изменений в базу данных. Без него изменения останутся на локальном уровне и не появятся в результатах запроса.  
  
#### <a name="to-submit-changes-to-the-database"></a>Отправка изменений в базу данных  
  
1. Вставьте следующий код перед `Console.ReadLine`.  
  
     [!code-csharp[DLinqWalk3CS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#6)]  
  
2. Вставьте следующий код (после `SubmitChanges`), чтобы показать результаты до и после отправки изменений.  
  
     [!code-csharp[DLinqWalk3CS#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#7)]  
  
3. Нажмите клавишу F5 для отладки решения.  
  
4. Нажмите клавишу ВВОД в **консоли** окна, чтобы закрыть приложение.  
  
> [!NOTE]
>  После добавления нового клиента путем отправки изменений это решение нельзя повторно выполнить в исходном виде. Для повторного выполнения решения измените имя клиента и значение идентификатора добавляемого клиента.  
  
## <a name="see-also"></a>См. также

- [Обучение с использованием пошаговых руководств](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)
