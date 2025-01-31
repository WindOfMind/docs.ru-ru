---
title: Рекомендации по разработке элементов управления с возможностью использования стилей
ms.date: 03/30/2017
helpviewer_keywords:
- style design for controls [WPF]
- controls [WPF], style design
ms.assetid: c52dde45-a311-4531-af4c-853371c4d5f4
ms.openlocfilehash: 99644be4a275c1de7f4b89ca23368a26a8b76f5b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614543"
---
# <a name="guidelines-for-designing-stylable-controls"></a>Рекомендации по разработке элементов управления с возможностью использования стилей
В этом документе содержатся рекомендации по разработке элементов управления, стили и шаблоны которых можно с легкостью изменять. Эти рекомендации являются результатом продолжительного периода проб и ошибок при работе над стилями тем оформления для встроенного набора элементов управления [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Было выяснено, что успешное изменение стилей зависит как от хорошо спроектированной объектной модели, так и самого стиля. Данный документ предназначен именно для разработчиков элементов управления, а не для разработчиков стилей.  
  
  <a name="Terminology"></a>   
## <a name="terminology"></a>Терминология  
 Термин "использование стилей и шаблонов" относится к набору технологий, позволяющих разработчику элементов управления отложить разработку визуальных характеристик элемента управления на этап разработки стилей и шаблонов элемента управления. Такой набор технологий включает следующее:  
  
- стили (включая методы задания свойств, триггеры и раскадровки);  
  
- ресурсы;  
  
- шаблоны элементов управления;  
  
- шаблоны данных.  
  
 Вводная информация, касающаяся стилей и шаблонов, представлена в разделе [Стилизация и использование шаблонов](styling-and-templating.md).  
  
<a name="Before_You_Start__Understanding_Your_Control"></a>   
## <a name="before-you-start-understanding-your-control"></a>Перед началом работы: Основные сведения о элемент управления  
 Прежде чем перейти к рекомендациям, важно понять и определить типичные способы использования элементов управления. Зачастую стили предоставляют неуправляемый набор возможностей. Проблема элементов управления, написанных для широкого применения (многими разработчиками, во многих приложениях), состоит в том, что стили можно использовать для масштабных изменений внешнего вида элементов управления. На самом же деле элемент управления, к которому применен стиль, может не соответствовать замыслу разработчика. Поскольку стили по сути представляют безграничную гибкость, можно использовать подход, подразумевающий типичные способы их использования, чтобы ограничить область их применения.  
  
 Чтобы понять, какие существуют типичные способы использования элементов управления, можно рассмотреть область значений, предоставляемых элементом управления. Какие специфические свойства отличают конкретный элемент управления от всех остальных? Типичные способы использования не подразумевают какой-либо определенный внешний вид, они подразумевают концепцию элемента управления и соответствующий набор ожидаемых функций. В этом свете можно сделать некоторые предположения о структурной модели и поведении элемента управления в соответствии с примененным стилем в общем случае. В случае использования <xref:System.Windows.Controls.ComboBox>, например, основные сведения о типичных способов использования не даст представления о ли конкретный <xref:System.Windows.Controls.ComboBox> имеет скругленные углы, но она даст вам представление о тот факт, <xref:System.Windows.Controls.ComboBox> скорее всего, необходимы всплывающее окно и способ переключения при открытии.  
  
<a name="General_Guidelines"></a>   
## <a name="general-guidelines"></a>Общие рекомендации  
  
- **Не вводите строгие контракты шаблонов.** Контракт шаблона элемента управления может состоять из элементов, команд, привязок, триггеров или даже параметров свойств, которые требуются или ожидаются для правильного функционирования элемента управления.  
  
    - Минимизируйте контракты, насколько возможно.  
  
    - При разработке основывайтесь на факте, что во время разработки (то есть при использовании средства разработки) для шаблона элемента управления естественным является состояние незавершенности. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] не поддерживает инфраструктуру состояния составления, поэтому элементы управления нужно создавать, предполагая, что такое состояние может допускаться.  
  
    - Не следует генерировать исключения, если не выполняется какой-либо аспект контракта шаблона. Согласно этому, панели не должны вызывать исключения, если у них слишком много или слишком мало дочерних элементов.  
  
- **Периферийная функциональность в шаблонных вспомогательных элементах по категориям.** Каждый элемент управления должен концентрироваться на функциональных возможностях его ядра и на верном представлении ценности и определяться общим использованием элемента управления. Для этого используйте в шаблоне композицию и вспомогательные элементы, чтобы предоставить периферийные проявления и визуализации, т. е. модели поведения и визуализации, которые не относятся к основной функциональности элемента управления. Вспомогательные элементы делятся на три категории.  
  
    - **Изолированные** вспомогательные элементы — это повторно используемые общедоступные элементы управления или примитивы, используемые в шаблоне "анонимно", в том смысле что ни вспомогательный элемент, ни элемент управления с примененным стилем не знают друг о друге. С технической точки зрения любой элемент может быть анонимного типа, но в данном контексте этот термин описывает типы, которые инкапсулируют специализированные функции для выполнения целевых сценариев.  
  
    - **Основанные на типах** вспомогательные элементы — это новые типы, инкапсулирующие специализированные функции. Эти элементы обычно разрабатываются с более узким диапазоном функциональных возможностей, чем стандартные элементы управления и примитивы. В отличие от изолированных вспомогательных элементов основанные на типах вспомогательные элементы имеют сведения о контексте, в котором используются, и обычно должны использовать общие данные с элементом управления, к шаблону которого они относятся.  
  
    - **Именованные вспомогательные элементы** являются общими элементами управления или примитивами, которые элемент управления ожидает найти в своем шаблоне по имени. Таким элементам присваиваются известные имена в шаблоне, что дает элементу управления возможность найти элемент и взаимодействовать с ним программным способом. Имена всех элементов в шаблоне уникальные.  
  
     В таблице ниже иллюстрируется современное использование вспомогательных элементов в стилях элементов управления (данный список не является полным).  
  
    |Элемент|Тип|Где используется|  
    |-------------|----------|-------------|  
    |<xref:System.Windows.Controls.ContentPresenter>|Основанные на типе|<xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.CheckBox>, <xref:System.Windows.Controls.RadioButton>, <xref:System.Windows.Controls.Frame>, и так далее (все <xref:System.Windows.Controls.ContentControl> типы)|  
    |<xref:System.Windows.Controls.ItemsPresenter>|Основанные на типе|<xref:System.Windows.Controls.ListBox>, <xref:System.Windows.Controls.ComboBox>, <xref:System.Windows.Controls.Menu>, и так далее (все <xref:System.Windows.Controls.ItemsControl> типы)|  
    |<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|Именованные|<xref:System.Windows.Controls.ToolBar>|  
    |<xref:System.Windows.Controls.Primitives.Popup>|Автономные|<xref:System.Windows.Controls.ComboBox>, <xref:System.Windows.Controls.ToolBar>, <xref:System.Windows.Controls.Menu>, <xref:System.Windows.Controls.ToolTip>, и так далее|  
    |<xref:System.Windows.Controls.Primitives.RepeatButton>|Именованные|<xref:System.Windows.Controls.Slider>, <xref:System.Windows.Controls.Primitives.ScrollBar>, и так далее|  
    |<xref:System.Windows.Controls.Primitives.ScrollBar>|Именованные|<xref:System.Windows.Controls.ScrollViewer>|  
    |<xref:System.Windows.Controls.ScrollViewer>|Автономные|<xref:System.Windows.Controls.ListBox>, <xref:System.Windows.Controls.ComboBox>, <xref:System.Windows.Controls.Menu>, <xref:System.Windows.Controls.Frame>, и так далее|  
    |<xref:System.Windows.Controls.Primitives.TabPanel>|Автономные|<xref:System.Windows.Controls.TabControl>|  
    |<xref:System.Windows.Controls.TextBox>|Именованные|<xref:System.Windows.Controls.ComboBox>|  
    |<xref:System.Windows.Controls.Primitives.TickBar>|Основанные на типе|<xref:System.Windows.Controls.Slider>|  
  
- **Минимизируйте необходимые во вспомогательных элементах определяемые пользователем привязки или параметры свойств**. Обычно для вспомогательного элемента необходимы некоторые привязки или параметры свойств, гарантирующие его правильную работу в шаблоне элемента управления. Вспомогательный элемент и элемент управления шаблон должны устанавливать эти параметры, насколько это возможно. При задании свойств или установке привязок следует соблюдать осторожность, чтобы не переопределить значения, установленные пользователем. Ниже приведены конкретные рекомендации.  
  
    - Именованные вспомогательные элементы должны идентифицироваться по родительскому элементу, который должен устанавливать все необходимые параметры вспомогательного элемента.  
  
    - Основанные на типах вспомогательные элементы должны непосредственно устанавливать себе все необходимые параметры. Это может потребовать запроса вспомогательным элементом информационного контекста, в котором он используется, включая его `TemplatedParent` (тип элемента управления для шаблона, в котором он используется). Например <xref:System.Windows.Controls.ContentPresenter> автоматически привязывает `Content` свойство его `TemplatedParent` для его <xref:System.Windows.Controls.ContentPresenter.Content%2A> свойства при использовании в <xref:System.Windows.Controls.ContentControl> производный тип.  
  
    - Изолированные вспомогательные элементы не могут быть оптимизированы таким образом, так как по определению ни вспомогательный элемент, ни родительский элемент не знают друг о друге.  
  
- **Используйте свойство Name, чтобы пометить элементы внутри шаблона**. Элемент управления, которому необходимо найти элемент в его стиле для программного доступа к нему, должен для этого использовать свойство `Name` и парадигму `FindName`. Элемент управления не должен вызывать исключение, когда элемент не найден, он должен без вмешательства пользователя корректно отключить функциональные возможности, которым требуется этот элемент.  
  
- **Используйте советы и рекомендации для задания состояния элемента управления и поведения в стиле**. Ниже приведен упорядоченный список советов и рекомендаций по заданию изменений состояния элемента управления и поведения в стиле. Следует использовать первый элемент в списке, который разрешает сценарий.  
  
    1. Привязка свойства. Пример: привязка <xref:System.Windows.Controls.ComboBox.IsDropDownOpen%2A?displayProperty=nameWithType> и <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A?displayProperty=nameWithType>.  
  
    2. Вызванные изменения свойств или анимация свойств. Пример: состояние наведения мыши <xref:System.Windows.Controls.Button>.  
  
    3. Команда. Пример: <xref:System.Windows.Controls.Primitives.ScrollBar.LineUpCommand>  /  <xref:System.Windows.Controls.Primitives.ScrollBar.LineDownCommand> в <xref:System.Windows.Controls.Primitives.ScrollBar>.  
  
    4. Изолированные вспомогательные элементы. Пример: <xref:System.Windows.Controls.Primitives.TabPanel> в <xref:System.Windows.Controls.TabControl>.  
  
    5. Вспомогательные типы, основанные на типах. Пример: <xref:System.Windows.Controls.ContentPresenter> в <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.Primitives.TickBar> в <xref:System.Windows.Controls.Slider>.  
  
    6. Именованные вспомогательные элементы. Пример: <xref:System.Windows.Controls.TextBox> в <xref:System.Windows.Controls.ComboBox>.  
  
    7. Передающиеся вверх события именованных вспомогательных типов. Если ожидать от элемента стиля передающихся вверх событий, следует потребовать, чтобы элемент, вызывающий событие, мог быть идентифицирован уникальным образом. Пример: <xref:System.Windows.Controls.Primitives.Thumb> в <xref:System.Windows.Controls.ToolBar>.  
  
    8. Настраиваемое поведение `OnRender`. Пример: <xref:Microsoft.Windows.Themes.ButtonChrome> в <xref:System.Windows.Controls.Button>.  
  
- **Как можно реже используйте триггеры стиля (в отличие от триггеров шаблона)**. Триггеры, которые влияют на свойства элементов в шаблоне, должны быть объявлены в шаблоне. Триггеры, которые влияют на свойства элемента управления (не `TargetName`), могут быть объявлены в стиле, если только не известно, что при изменении шаблона триггер уничтожится.  
  
- **Поддерживайте согласованность с существующими шаблонами стилей**. Зачастую существуют различные способы решения проблемы. Следите за шаблонами стилей элементов управления и, если возможно, обеспечивайте согласованность с существующими шаблонами стилей элементов управления. Это особенно важно для элементов управления, производных от одного базового типа (например, <xref:System.Windows.Controls.ContentControl>, <xref:System.Windows.Controls.ItemsControl>, <xref:System.Windows.Controls.Primitives.RangeBase>, и так далее).  
  
- **Предоставляйте свойства, чтобы разрешить выполнение общих сценариев настройки без создания новых шаблонов**. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] не поддерживает подключаемые/настраиваемые части, поэтому пользователю элемента управления доступны только два метода настройки: непосредственная установка свойств или установка свойств с использованием стилей. Исходя из этого, удобно предоставлять ограниченное количество свойств, нацеленных на очень общие, высокоприоритетные сценарии настройки, которые в противном случае потребуют создания новых шаблонов. Ниже приведены советы и рекомендации по тому, когда и как разрешать сценарии настройки.  
  
    - Самые общие настройки должны быть предоставлены как свойства элемента управления и использоваться шаблоном.  
  
    - Менее общие (хотя нередкие) настройки должны быть предоставлены как вложенные свойства зависимостей и использоваться шаблоном.  
  
    - Для известных, но редких настроек допустимо создание новых шаблонов.  
  
<a name="Theme_Considerations"></a>   
## <a name="theme-considerations"></a>Рекомендации касательно тем  
  
- **Стили тем должны стремиться к согласованной семантике свойств во всех темах, но ничего не гарантировать**. Элемент управления должен содержать в своей документации документ, описывающий семантику свойства элемента управления, то есть "значение" свойства для элемента управления. Например <xref:System.Windows.Controls.ComboBox> управления следует определить значение <xref:System.Windows.Controls.Control.Background%2A> свойство в пределах <xref:System.Windows.Controls.ComboBox>. Во всех темах стили по умолчанию для элемента управления должны стремиться следовать семантике, определенной в этом документе. С другой стороны, пользователи элемента управления должны знать, что семантика свойств может меняться от темы к теме. В некоторых случаях заданное свойство может оказаться неэффективным с учетом визуальных ограничений, накладываемых конкретной темой. (Например, для многих элементов управления в классической теме нет одинарной границы, к которой можно применить `Thickness`.)  
  
- **Для стилей тем не требуется согласованная для всех тем триггерная семантика**. Поведение, предоставляемое стилем элемента управления с помощью триггеров или анимации, может меняться от темы к теме. Пользователям элемента управления следует помнить, что элемент управления не обязательно будет использовать во всех темах один и тот же механизм для достижения определенного поведения. Например, для выражения поведения при наведении указателя мыши одна тема может использовать анимацию, а другая может использовать триггер. Это может привести к несогласованности в сохранении поведения настроенных элементов управления. (Например, изменение свойства фона может не повлиять на состояние нахождения элемента управления под наведенным указателем мыши, если это состояние обеспечивается с помощью триггера. Однако если такое состояние реализовано с использованием анимации, изменение фона может привести к неисправимым ошибкам анимации и, следовательно, к смене состояния.)  
  
- **Для стилей тем не требуется согласованной для всех тем семантики "макета"**. Например, стиль по умолчанию не должен гарантировать, что элемент управления будет иметь тот же размер во всех темах или что у него во всех темах будут те же границы/поля содержимого.  
  
## <a name="see-also"></a>См. также

- [Стилизация и использование шаблонов](styling-and-templating.md)
- [Общие сведения о разработке элементов управления](control-authoring-overview.md)
