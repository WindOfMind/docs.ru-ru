---
title: Вывод типа
description: Узнайте, как F# компилятор определяет типы значений, переменных, параметров и возвращаемых значений.
ms.date: 05/16/2016
ms.openlocfilehash: ab1a4aa8df4312287df749d5d6d0ea2858091152
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641679"
---
# <a name="type-inference"></a>Вывод типа

Здесь описывается, как F# компилятор определяет типы значений, переменных, параметров и возвращаемых значений.

## <a name="type-inference-in-general"></a>Определение типа в целом

Вывод типа суть в том, что у вас нет позволяет указать типы F# конструкции, за исключением случаев, когда компилятор не может определить тип. Пропуск явные сведения о типах не означает, что F# — динамически типизированный язык или значений в F# являются нестрого типизированными. F#— Это статически типизированный язык, это означает, что компилятор выводит тип точное, для каждой конструкции во время компиляции. Если имеется достаточно информации для компилятору команду выведения типов каждой конструкции, необходимо предоставить дополнительные сведения о типе, обычно путем добавления явные обозначения типов, где-нибудь в коде.

## <a name="inference-of-parameter-and-return-types"></a>Определение параметров и возвращаемых типов

В списке параметров у вас нет для указания типа каждого параметра. И еще, F# — это статически типизированный язык, и поэтому каждое значение и выражение имеет определенный тип во время компиляции. Для этих типов, которые явно не указан компилятор выводит тип на основе контекста. Если тип не указан, он определяется как универсальный. Если код использует значение несогласованно, так что нет единственного выведенного типа, который удовлетворяет все случаи использования значения, компилятор сообщает об ошибке.

Тип возвращаемого значения функции определяется типа последнего выражения в функции.

Например, в следующем коде, типы параметров `a` и `b` и тип возвращаемого значения определяется как `int` так как литерал `100` имеет тип `int`.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet301.fs)]

Вывод типа, можно изменить, изменив литералы. При внесении `100` `uint32` путем добавления суффикса `u`, типы `a`, `b`, и возвращаемое значение имеют тип `uint32`.

Может также повлиять на определение типа с помощью других конструкций, которые подразумевают ограничения на типы, такие как функции и методы, которые работают с определенным типом.

Кроме того можно применять явные обозначения типов для параметров функции или метода или для переменных в выражениях, как показано в следующих примерах. Если возникают конфликты между различными ограничениями возникать ошибки.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet302.fs)]

Можно явным образом указать возвращаемое значение функции, предоставляя аннотацию типа в конце концов параметры.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet303.fs)]

Распространенный случай, где аннотацию типа полезен для параметра, когда параметр не является типом объекта и вы хотите использовать член.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet304.fs)]

## <a name="automatic-generalization"></a>Автоматическое обобщение

Если код функции не зависит от типа параметра, компилятор считает, что параметр является универсальным. Это называется *Автоматическое обобщение*, и может быть помогать при написании универсального кода без повышения сложности.

Например следующая функция объединяет два параметра любого типа в кортеж.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet305.fs)]

Тип определяется как

```fsharp
'a -> 'b -> 'a * 'b
```

## <a name="additional-information"></a>Дополнительные сведения

Вывод типа описан более подробно в F# спецификации языка.

## <a name="see-also"></a>См. также

- [Автоматическое обобщение](generics/automatic-generalization.md)
