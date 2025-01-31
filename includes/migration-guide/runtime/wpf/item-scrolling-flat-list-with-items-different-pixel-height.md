---
ms.openlocfilehash: 088ebad0f822f791d05a8a8dafb0f7fd74f5581a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774195"
---
### <a name="item-scrolling-a-flat-list-with-items-of-different-pixel-height"></a>Поэлементная прокрутка плоского списка с элементами, имеющими различную высоту в пикселях

|   |   |
|---|---|
|Подробные сведения|Когда <xref:System.Windows.Controls.ItemsControl?displayProperty=name> отображает коллекцию с помощью виртуализации (<code>IsVirtualizing=true</code>) и прокрутки элемента (<code>ScrollUnit=Item</code>) и когда элемент управления прокручивается для отображения элемента, высота которого в пикселях отличается о высоты соседних элементов, <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=name> выполняет итерацию по всем элементам в коллекции. При выполнении такой итерации для большой коллекции пользовательский интерфейс перестает отвечать, что воспринимается как зависание. Подобная итерация выполняется в других обстоятельствах даже в предыдущих выпусках .NET Framework. Например, она происходит при пиксельной прокрутке (<code>ScrollUnit=Pixel</code>) при обнаружении элемента другой высоты в пикселях, а также при поэлементной прокрутке иерархических данных (например, в элементе управления <xref:System.Windows.Controls.TreeView?displayProperty=name> или <xref:System.Windows.Controls.ItemsControl?displayProperty=name> с включенным группированием) при обнаружении элемента, число подчиненных элементов которого отличается от соседних элементов. Для поэлементной прокрутки элементов с разной высотой в пикселях эта итерация была представлена в .NET Framework 4.6.1, чтобы устранить ошибки, связанные с макетом иерархических данных.  Итерация не требуется, если данные не структурированы (без иерархии), и в этом случае .NET Framework 4.6.2 не выполняет ее.|
|Предложение|Если итерация выполняется в .NET Framework 4.6.1, но не в более ранних выпусках, т. е. если <xref:System.Windows.Controls.ItemsControl?displayProperty=name> прокручивает поэлементно плоский список с элементами разной высоты в пикселях, то существует два решения:<ol><li>Установите .NET Framework 4.6.2.</li><li>Установите исправление HR 1605 для .NET Framework 4.6.1.</li></ol>|
|Область|Дополнительный номер|
|Версия|4.6.1|
|Тип|Среда выполнения|
|Затронутые API|<ul><li><xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=nameWithType></li></ul>|
