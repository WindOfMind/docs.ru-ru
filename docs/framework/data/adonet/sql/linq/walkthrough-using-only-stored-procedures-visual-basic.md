---
title: Пошаговое руководство. Применение только хранимых процедур (Visual Basic)
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 5a736a30-ba66-4adb-b87c-57d19476e862
ms.openlocfilehash: 22db347afb45b981602d5a92516271f75b8e4359
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648677"
---
# <a name="walkthrough-using-only-stored-procedures-visual-basic"></a>Пошаговое руководство. Применение только хранимых процедур (Visual Basic)
В данном пошаговом руководстве представлен основной полный сценарий [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] для получения доступа к данным с использованием только хранимых процедур. Этот метод часто используется администраторами баз данных для ограничения способов получения доступа к хранилищам данных.  
  
> [!NOTE]
>  Хранимые процедуры можно также использовать в приложениях [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] для переопределения поведения по умолчанию, особенно для процессов `Create`, `Update` и `Delete`. Дополнительные сведения см. в разделе [Настройка операций вставки, обновления и удалить](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md).  
  
 Для целей данного пошагового руководства будут использованы два метода, которые были сопоставлены с хранимыми процедурами в образце базы данных Northwind: CustOrdersDetail и CustOrderHist. Сопоставление осуществляется при запуске средства командной строки SqlMetal для создания файла Visual Basic. Дополнительные сведения см. в разделе "Предварительные требования" далее в этом руководстве.  
  
 В пошаговом руководстве не используется [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]. Разработчики, использующие Visual Studio можно также использовать [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] для реализации функций хранимых процедур. См. в разделе [средства LINQ to SQL в Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2).  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Это пошаговое руководство было написано с помощью параметров разработки Visual Basic.  
  
## <a name="prerequisites"></a>Предварительные требования  
 Необходимо выполнить следующие требования.  
  
- Для хранения файлов используется выделенная папка ("c:\linqtest3"). Прежде чем приступить к выполнению задач, создайте такую папку.  
  
- Наличие учебной базы данных Northwind.  
  
     Если база данных не установлена на компьютере разработчика, загрузите ее с веб-узла Центра загрузки Майкрософт. Инструкции см. в разделе [Загрузка примеров баз данных](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md). После загрузки базы данных скопируйте файл northwnd.mdf в папку c:\linqtest3.  
  
- Наличие файла кода Visual Basic, созданного из базы данных "Борей".  
  
     Данное пошаговое руководство было написано с использованием средства SqlMetal со следующей командной строкой:  
  
     **sqlmetal /code:"c:\linqtest3\northwind.vb" /language:vb "c:\linqtest3\northwnd.mdf" /sprocs /functions /pluralize**  
  
     Дополнительные сведения см. в разделе [SQLMetal.exe (средство создания кода)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## <a name="overview"></a>Обзор  
 Данное пошаговое руководство состоит из шести основных задач.  
  
- Настройка [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] решения в Visual Studio.  
  
- Добавление сборки System.Data.Linq в проект.  
  
- Добавление файла кода базы данных в проект.  
  
- Создание подключения к базе данных.  
  
- Настройка пользовательского интерфейса.  
  
- Запуск и тестирование приложения.  
  
## <a name="creating-a-linq-to-sql-solution"></a>Создание решения LINQ to SQL  
 В первой задаче создается решение Visual Studio, содержащее ссылки, необходимые для построения и запуска [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] проекта.  
  
#### <a name="to-create-a-linq-to-sql-solution"></a>Создание решения LINQ to SQL  
  
1. В меню **Файл** Visual Studio выберите команду **Создать проект**.  
  
2. В области **Типы проектов** диалогового окна **Создать проект** разверните узел **Visual Basic**, а затем щелкните **Windows**.  
  
3. Выберите **Приложение Windows Forms** в области **Шаблоны**.  
  
4. В **имя** введите **SprocOnlyApp**.  
  
5. Нажмите кнопку **ОК**.  
  
     Откроется конструктор Windows Forms.  
  
## <a name="adding-the-linq-to-sql-assembly-reference"></a>Добавление ссылки на сборку LINQ to SQL  
 Сборка [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] не включается в стандартный шаблон приложения Windows Forms. Сборку необходимо добавить самостоятельно, выполнив приведенные ниже действия.  
  
#### <a name="to-add-systemdatalinqdll"></a>Добавление сборки System.Data.Linq.dll  
  
1. В **обозревателе решений**, нажмите кнопку **Показать все файлы**.  
  
2. В **обозревателе решений**, щелкните правой кнопкой мыши **ссылки**, а затем нажмите кнопку **добавить ссылку**.  
  
3. В **добавить ссылку** диалоговом окне щелкните **.NET**, выберите сборку System.Data.Linq, затем нажмите кнопку **ОК**.  
  
     Сборка будет добавлена в проект.  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a>Добавление файла кода Northwind в проект  
 При выполнении действий этого шага предполагается, что для создания файла кода из учебной базы данных Northwind использовалась программа SQLMetal. Дополнительные сведения см. в разделе "Предварительные требования" ранее в этом руководстве.  
  
#### <a name="to-add-the-northwind-code-file-to-the-project"></a>Добавление файла кода northwind в проект  
  
1. На **проекта** меню, щелкните **добавить существующий элемент**.  
  
2. В **добавить существующий элемент** переместить c:\linqtest3\northwind.vb диалоговом окне и нажмите кнопку **добавить**.  
  
     Файл northwind.vb будет добавлен в проект.  
  
## <a name="creating-a-database-connection"></a>Создание подключения к базе данных  
 На этом этапе определяется подключение к учебной базе данных Northwind. В качестве пути используется "c:\linqtest3\northwnd.mdf".  
  
#### <a name="to-create-the-database-connection"></a>Создание подключения к базе данных  
  
1. В **обозревателе решений**, щелкните правой кнопкой мыши **Form1.vb**, а затем нажмите кнопку **Просмотр кода**.  
  
     В редакторе кода откроется `Class Form1`.  
  
2. В блок кода `Form1` введите следующий код.  
  
     [!code-vb[DLinqWalk4VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#1)]  
  
## <a name="setting-up-the-user-interface"></a>Настройка пользовательского интерфейса  
 В этой задаче создается интерфейс, с помощью которого пользователи могут выполнять хранимые процедуры для получения доступа к данным в базе данных. В приложении, разрабатываемом с помощью настоящего пошагового руководства, пользователи могут получать доступ к данным в базе данных только с помощью хранимых процедур, внедренных в приложение.  
  
#### <a name="to-set-up-the-user-interface"></a>Настройка пользовательского интерфейса  
  
1. Конструктор вернуться в Windows Forms (**Form1.vb[Design]**).  
  
2. В меню **Вид** выберите пункт **Панель элементов**.  
  
     Откроется панель элементов.  
  
    > [!NOTE]
    >  Нажмите кнопку **Автоскрытие** вешку, чтобы не закрывайте панели элементов при выполнении оставшихся действий данного раздела.  
  
3. Перетащите две кнопки, два текстовых поля и две метки из панели элементов на **Form1**.  
  
     Расположите элементы управления в соответствии с показанным здесь рисунком. Разверните **Form1** , чтобы разместить все элементы управления.  
  
4. Щелкните правой кнопкой мыши **Label1**, а затем нажмите кнопку **свойства**.  
  
5. Изменение **текст** свойства из **Label1** для **введите код заказа:**.  
  
6. Таким же образом для **Label2**, изменить **текст** свойства из **Label2** для **введите код клиента:**.  
  
7. Таким же образом, изменить **текст** свойство для **Button1** для **Order Details**.  
  
8. Изменение **текст** свойство для **Button2** для **История заказа**.  
  
     Расширьте элементы управления "Кнопка", чтобы отображался весь текст.  
  
#### <a name="to-handle-button-clicks"></a>Обработка нажатий кнопки  
  
1. Дважды щелкните **Order Details** на **Form1** для создания `Button1` обработчик событий и открыть редактор кода.  
  
2. Введите в обработчик кнопки `Button1` следующий код:  
  
     [!code-vb[DLinqWalk4VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#2)]  
  
3. Теперь дважды щелкните **Button2** на форме Form1, чтобы создать `Button2` обработчик событий и открыть редактор кода.  
  
4. Введите в обработчик кнопки `Button2` следующий код:  
  
     [!code-vb[DLinqWalk4VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#3)]  
  
## <a name="testing-the-application"></a>Тестирование приложения  
 Теперь необходимо протестировать приложение. Обратите внимание, что все обращения к хранилищу данных ограничены теми действиями, которые могут выполняться двумя хранимыми процедурами. Эти действия заключаются в возвращении продуктов, включенных в заказ с введенным кодом, или истории продуктов, заказанных клиентом с введенным кодом.  
  
#### <a name="to-test-the-application"></a>Тестирование приложения  
  
1. Нажмите клавишу F5, чтобы начать отладку.  
  
     Откроется форма "Form1".  
  
2. В **введите код заказа** введите **10249** и нажмите кнопку **Order Details**.  
  
     В окне сообщения будет отображен список продуктов, включенных в заказ 10249.  
  
     Нажмите кнопку **ОК** чтобы закрыть окно сообщения.  
  
3. В **введите код клиента** введите `ALFKI`, а затем нажмите кнопку **История заказа**.  
  
     Откроется окно сообщения, в котором отображается история заказа для клиента ALFKI.  
  
     Нажмите кнопку **ОК** чтобы закрыть окно сообщения.  
  
4. В **введите код заказа** введите `123`, а затем нажмите кнопку **Order Details**.  
  
     Откроется окно сообщения, в котором отображается текст "Нет результатов".  
  
     Нажмите кнопку **ОК** чтобы закрыть окно сообщения.  
  
5. На **Отладка** меню, щелкните **остановить отладку**.  
  
     Сеанс отладки закрывается.  
  
6. Если проверка завершена, вы можете щелкнуть **закрыть проект** на **файл** меню и сохранить проект при появлении запроса.  
  
## <a name="next-steps"></a>Следующие шаги  
 Этот проект можно улучшить, выполнив некоторые изменения. Например, можно создать поле со списком доступных хранимых процедур и разрешить пользователю выбирать процедуру для выполнения. Можно также записывать выходные данных отчетов в текстовый файл.  
  
## <a name="see-also"></a>См. также

- [Обучение с использованием пошаговых руководств](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)
- [Хранимые процедуры](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)
