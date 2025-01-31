---
title: Практическое руководство. Добавление и удаление узлов с использованием элемента управления TreeView в формах Windows Forms с помощью конструктора
ms.date: 03/30/2017
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- TreeView control [Windows Forms], removing nodes
- tree nodes in TreeView control
- TreeView control [Windows Forms], adding nodes
ms.assetid: 35bf1750-045e-4ec5-97cb-b47b0dbdaa2c
ms.openlocfilehash: 71ada3235343aa7e014e12ebf5b367ec744b00d3
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959659"
---
# <a name="how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control-using-the-designer"></a>Практическое руководство. Добавление и удаление узлов с использованием элемента управления TreeView в формах Windows Forms с помощью конструктора

Так как Windows Forms <xref:System.Windows.Forms.TreeView> элемент управления отображает узлы в виде иерархии, при добавлении узла следует обращать внимание на является его родительским узлом.

Следующая процедура требуется **приложения Windows** проекта с формой, содержащей <xref:System.Windows.Forms.TreeView> элемента управления. Сведения о настройке такого проекта см. в разделе [как: Создайте проект приложения Windows Forms](/visualstudio/ide/step-1-create-a-windows-forms-application-project) и [как: Добавление элементов управления в Windows Forms](how-to-add-controls-to-windows-forms.md).

> [!NOTE]
> Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих параметров или выпуска. Чтобы изменить параметры, выберите в меню **Сервис** пункт **Импорт и экспорт параметров** . Дополнительные сведения см. в разделе [Персонализация интегрированной среды разработки Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).

### <a name="to-add-or-remove-nodes-in-the-designer"></a>Для добавления или удаления узлов в конструкторе

1. Выберите элемент управления <xref:System.Windows.Forms.TreeView>.

2. В **свойства** окно, нажмите кнопку **кнопку с многоточием** (![кнопку с многоточием (...) в окне свойств Visual Studio.](./media/visual-studio-ellipsis-button.png)) рядом с пунктом <xref:System.Windows.Forms.TreeView.Nodes%2A> свойство .

     **Редактор TreeNode** отображается.

3. Чтобы добавить узлы, необходимо наличие корневого узла; Если она отсутствует, вы должны сначала добавить его, нажав кнопку **Добавить корень** кнопки. После этого можно добавить дочерний узел, выделив корневой или любой другой узел и нажав кнопку **добавить дочерний элемент** кнопки.

4. Чтобы удалить узлы, выберите узел, чтобы удалить, а затем нажмите кнопку **удалить** кнопки.

## <a name="see-also"></a>См. также

- [Элемент управления TreeView](treeview-control-windows-forms.md)
- [Общие сведения об элементе управления TreeView](treeview-control-overview-windows-forms.md)
- [Практическое руководство. Определение значков для элемента управления TreeView в Windows Forms](how-to-set-icons-for-the-windows-forms-treeview-control.md)
- [Практическое руководство. Перебор узлов элемента управления TreeView в Windows Forms](how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)
- [Практическое руководство. Определить, какой узел элемента управления TreeView была нажата](how-to-determine-which-treeview-node-was-clicked-windows-forms.md)
- [Практическое руководство. Добавление пользовательских данных в элемент управления TreeView или элемент управления ListView (Windows Forms)](add-custom-information-to-a-treeview-or-listview-control-wf.md)
