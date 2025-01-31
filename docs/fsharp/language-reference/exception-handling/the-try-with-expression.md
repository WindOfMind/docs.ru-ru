---
title: 'Исключения: Выражение try...with'
description: Сведения об использовании F# «try... with» выражение для обработки исключений.
ms.date: 05/16/2016
ms.openlocfilehash: 3ba13227ac55eff770ceb7631d3406ad80b6ea45
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641940"
---
# <a name="exceptions-the-trywith-expression"></a>Исключения: Выражение try...with

В этом разделе описывается `try...with` выражение, выражение, которое используется для обработки исключений в F# языка.

## <a name="syntax"></a>Синтаксис

```fsharp
try
    expression1
with
| pattern1 -> expression2
| pattern2 -> expression3
...
```

## <a name="remarks"></a>Примечания

`try...with` Выражение используется для обработки исключений в F#. Это похоже на `try...catch` инструкции на языке C#. Приведенный выше синтаксис кода в *expression1* может явиться источником исключения. `try...with` Выражение возвращает значение. Если исключение не создается, то все выражение возвращает значение *expression1*. Если создается исключение, каждый *шаблон* сравнивается в свою очередь, за исключением, а также для первый совпадающий шаблон, соответствующий *выражение*, которая называется *обработчик исключений*, для выполнения этой ветви, а общее выражение возвращает значение выражения в этом обработчике исключений. Если шаблон не совпадает, исключение передается вверх по стеку вызовов, пока не будет найден соответствующий обработчик. Типы значений, возвращаемых каждым из выражений в обработчиках исключений должен соответствовать типу, возвращаемому из выражения в `try` блока.

Как правило тот факт, что произошла ошибка также означает, что отсутствует допустимое значение, могут быть возвращены из выражений в каждый обработчик исключений. Часто является тип выражения быть типом параметра. В следующем примере кода показан этот шаблон.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5601.fs)]

Исключения могут вызываться исключения .NET, или они могут быть F# исключения. Вы можете определить F# исключения с помощью `exception` ключевое слово.

Другие шаблоны можно использовать для фильтрации по типу исключения и другие условия; в следующей таблице приведены параметры.

|Шаблон|Описание|
|-------|-----------|
|:? *Тип исключения*|Совпадает с указанным типом исключения .NET.|
|:? *Тип исключения* как *идентификатор*|Совпадает с указанным типом исключения .NET, но дает исключение именованное значение.|
|*имя исключения*(*аргументы*)|Совпадения F# тип исключения и привязывает аргументы.|
|*identifier*|Соответствует любому исключению и привязывает имя объекта исключения. Эквивалентно **:? System.Exception как**_идентификатор_|
|*Идентификатор* при *условие*|Соответствует любому исключению, если условие истинно.|

## <a name="examples"></a>Примеры

В следующих примерах кода показано использование различных шаблонов обработчиков исключений.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5602.fs)]

> [!NOTE]
> `try...with` Конструкция — отдельное выражение из `try...finally` выражение. Таким образом Если код требует оба `with` блока и `finally` блока, необходимо будет вкладывать друг в друга двух выражений.

> [!NOTE]
> Можно использовать `try...with` в асинхронные рабочие потоки и другие вычисления выражения, в котором случае настроенную версию `try...with` используется выражение. Дополнительные сведения см. в разделе [асинхронные рабочие потоки](../asynchronous-workflows.md), и [выражения вычисления](../computation-expressions.md).

## <a name="see-also"></a>См. также

- [Обработка исключений](index.md)
- [Типы исключения](exception-types.md)
- [Исключения. `try...finally` Выражение](the-try-finally-expression.md)
