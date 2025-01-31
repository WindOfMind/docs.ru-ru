---
title: Стилизация фокуса в элементах управления и FocusVisualStyle
ms.date: 03/30/2017
helpviewer_keywords:
- keyboard focus [WPF]
- focus [WPF], visual styling
- styles [WPF], focus visual style
ms.assetid: 786ac576-011b-4d72-913b-558deccb9b35
ms.openlocfilehash: 745c2174c54ed072f91a6d5eb3b43d5385e96b90
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053381"
---
# <a name="styling-for-focus-in-controls-and-focusvisualstyle"></a>Стилизация фокуса в элементах управления и FocusVisualStyle
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] предоставляет два параллельных механизма для изменения внешнего вида элемента управления при получении фокуса клавиатуры. Первый механизм — использование методов задания свойств для свойств, таких как <xref:System.Windows.UIElement.IsKeyboardFocused%2A> внутри стиля или шаблона, который применяется к элементу управления. Второй механизм представляет собой отдельный стиль в качестве значения <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> свойство; «стиль визуального отображения фокуса» создает отдельное визуальное дерево для декоративного элемента, который отображается поверх элемента управления, а не изменяет визуальное дерево элемента управления или другой пользовательский Интерфейс элемент путем ее замены. В данном разделе рассматриваются сценарии, для которых подходит любой из этих механизмов.  

<a name="Purpose"></a>   
## <a name="the-purpose-of-focus-visual-style"></a>Назначение визуального стиля фокуса  
 Функция визуального стиля фокуса предоставляет общую "объектную модель" для введения визуальной обратной связи с пользователем на основе навигации с помощью клавиатуры к любому элементу пользовательского интерфейса. Это можно сделать без применения нового шаблона к элементу управления или знания композиции определенного шаблона.  
  
 Но именно потому, что функция визуального стиля фокуса работает без знания шаблонов элементов управления, визуальная обратная связь, которая может отображаться для элемента управления с использованием визуального стиля фокуса, ограничена в обязательном порядке. Эта функция фактически накладывает другое визуальное дерево (декоративный элемент) поверх визуального дерева, созданного при отрисовке элемента управления с помощью его шаблона. Определить это отдельное визуальное дерево с использованием стиля, который заполняет <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> свойство.  
  
<a name="Default"></a>   
## <a name="default-focus-visual-style-behavior"></a>Поведение визуального стиля фокуса по умолчанию  
 Визуальные стили фокуса действуют только тогда, когда действие фокусировки было инициировано клавиатурой. Любое действие мыши или программное изменение фокуса отключает режим визуальных стилей фокуса. Дополнительные сведения о различиях между режимами фокуса см. в разделе [Общие сведения о фокусе](focus-overview.md).  
  
 Темы для элементов управления включают поведение визуального стиля фокуса по умолчанию, который становится визуальным стилем фокуса для всех элементов управления в теме. Этот стиль темы определяется значением статического ключа <xref:System.Windows.SystemParameters.FocusVisualStyleKey%2A>. При объявлении собственного визуального стиля фокуса на уровне приложения можно заменить это поведение стиля по умолчанию из темы. Кроме того, при определении целой темы необходимо использовать этот же ключ для определения стиля поведения по умолчанию для всей темы.  
  
 В темах визуальный стиль фокуса по умолчанию обычно очень прост. Ниже приводится приблизительная оценка.  
  
```xaml  
<Style x:Key="{x:Static SystemParameters.FocusVisualStyleKey}">  
  <Setter Property="Control.Template">  
    <Setter.Value>  
      <ControlTemplate>  
        <Rectangle StrokeThickness="1"  
          Stroke="Black"  
          StrokeDashArray="1 2"  
          SnapsToDevicePixels="true"/>  
      </ControlTemplate>  
    </Setter.Value>  
  </Setter>  
</Style>  
```  
  
<a name="When"></a>   
## <a name="when-to-use-focus-visual-styles"></a>Когда следует использовать визуальные стили фокуса  
 Концептуально внешний вид визуальных стилей фокуса, применяемых к элементам управления, должен быть согласованным в различных элементах. Одним из способов обеспечить такую согласованность является изменение визуального стиля фокуса только при составлении целой темы, в которой каждый элемент управления, определенный в теме, получает либо один и тот же визуальный стиль фокуса, либо некоторую вариацию стиля, визуально связанную с другими элементами управления. Кроме того, можно использовать один и тот же стиль (или аналогичные стили) для каждого элемента, фокусируемого с клавиатуры, на странице или в пользовательском интерфейсе.  
  
 Параметр <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> для отдельных стилей управления, которые не являются частью темы — фокус не предполагаемое использование стилей оформления. Это связано с тем, что несогласованность визуального поведения элементов управления может привести к путанице при использовании фокуса клавиатуры. Если планируется конкретное поведение для фокуса клавиатуры, которое намеренно не согласовано в теме, гораздо лучшим подходом является использование триггеры в стилях для отдельных свойств состояния ввода, таких как <xref:System.Windows.UIElement.IsFocused%2A> или <xref:System.Windows.UIElement.IsKeyboardFocused%2A>.  
  
 Визуальные стили фокуса действуют исключительно для фокуса клавиатуры. Таким образом, визуальные стили фокуса являются функцией специальных возможностей. Если требуется изменять пользовательский интерфейс для какого-либо типа фокуса с помощью мыши, клавиатуры или программными средствами, то не следует использовать визуальные стили фокуса. Вместо этого используйте методы задания и триггеры в стилях или шаблонах, которые работают на основе значения общих свойств фокуса, таких как <xref:System.Windows.UIElement.IsFocused%2A> или <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A>.  
  
<a name="How"></a>   
## <a name="how-to-create-a-focus-visual-style"></a>Создание визуального стиля фокуса  
 Стиль, создаваемые для визуального стиля фокуса, всегда должен иметь <xref:System.Windows.Style.TargetType%2A> из <xref:System.Windows.Controls.Control>. Стиль должен состоять в основном из <xref:System.Windows.Controls.ControlTemplate>. Не указан целевой тип как тип, в котором визуальный стиль фокуса назначен <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>.  
  
 Так как целевым типом всегда является <xref:System.Windows.Controls.Control>, нужно создать стиль, с помощью свойств, которые являются общими для всех элементов управления (с помощью свойств класса <xref:System.Windows.Controls.Control> класса и его базовых классов). Необходимо создать шаблон, который будет правильно функционировать как наложение для элемента пользовательского интерфейса и не будет скрывать функциональные области элемента управления. Как правило, это означает, что визуальная обратная связь должна появляться за пределами полей управления или в качестве временных или ненавязчивых эффектов, которые не будут блокировать проверку нажатий в элементе управления, к которому применен визуальный стиль фокуса. Свойства, которые можно использовать в привязке шаблона, которые можно использовать для определения размеров и расположения шаблона наложения включают <xref:System.Windows.FrameworkElement.ActualHeight%2A>, <xref:System.Windows.FrameworkElement.ActualWidth%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, и <xref:System.Windows.Controls.Control.Padding%2A>.  
  
<a name="Alternatives"></a>   
## <a name="alternatives-to-using-a-focus-visual-style"></a>Альтернативные варианты использования визуального стиля фокуса  
 В ситуациях, когда использование визуального стиля фокуса нецелесообразно (при стилизации только отдельных элементов управления или если необходим больший контроль над шаблоном элемента управления), существует множество других доступных свойств и методов, которые могут создавать визуальное поведение в ответ на изменения фокуса.  
  
 Триггеры, методы задания и методы задания событий рассматриваются подробно в разделе [Использование стилей и шаблонов](../controls/styling-and-templating.md). Обработка перенаправляемых событий рассматривается в разделе [Общие сведения о перенаправляемых событиях](routed-events-overview.md).  
  
### <a name="iskeyboardfocused"></a>IsKeyboardFocused  
 Если вас интересует именно фокус клавиатуры, <xref:System.Windows.UIElement.IsKeyboardFocused%2A> свойства зависимостей можно использовать для свойства <xref:System.Windows.Trigger>. Триггер свойства в стиле или шаблоне является более подходящим методом определения поведения фокуса клавиатуры, который применяется только для отдельного элемента управления и может визуально не соответствовать поведению фокуса клавиатуры других элементов управления.  
  
 Другим похожим свойством зависимостей является <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A>, который может быть можно использовать, чтобы визуально обнаружить, фокус клавиатуры находится где-то внутри структуры или в функциональной области элемента управления. Например, можно поместить <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> триггер таким образом, что панель, которая группирует несколько элементов управления будет отображаться по-разному, даже если фокус клавиатуры может более точно находиться на отдельном элементе этой панели.  
  
 Можно также использовать события <xref:System.Windows.UIElement.GotKeyboardFocus> и <xref:System.Windows.UIElement.LostKeyboardFocus> (а также их эквиваленты предварительного просмотра). Эти события можно использовать в качестве основы для <xref:System.Windows.EventSetter>, или можно написать обработчики событий в коде.  
  
### <a name="other-focus-properties"></a>Другие свойства фокуса  
 Если требуется, чтобы все возможные причины изменения фокуса для порождали визуальное поведение, следует установить метод доступа или триггер на <xref:System.Windows.UIElement.IsFocused%2A> свойства зависимостей, либо на <xref:System.Windows.UIElement.GotFocus> или <xref:System.Windows.UIElement.LostFocus> события, которые используются для <xref:System.Windows.EventSetter>.  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>
- [Стилизация и использование шаблонов](../controls/styling-and-templating.md)
- [Общие сведения о фокусе](focus-overview.md)
- [Общие сведения о входных данных](input-overview.md)
