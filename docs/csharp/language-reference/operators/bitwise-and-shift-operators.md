---
title: Побитовые операторы и операторы сдвига — справочник по C#
description: Дополнительные сведения об операторах C#, которые выполняют побитовые логические операции или операции сдвига с операндами целочисленного типа.
ms.date: 04/18/2019
author: pkulikov
f1_keywords:
- ~_CSharpKeyword
- <<_CSharpKeyword
- '>>_CSharpKeyword'
- '&_CSharpKeyword'
- ^_CSharpKeyword
- '|_CSharpKeyword'
helpviewer_keywords:
- bitwise logical operators [C#]
- shift operators [C#]
- tilde operator [C#]
- one's complement operator [C#]
- bitwise complement operator [C#]
- ~ operator [C#]
- left shift operator [C#]
- << operator [C#]
- right shift operator [C#]
- '>> operator [C#]'
- bitwise logical AND operator [C#]
- ampersand operator [C#]
- '& operator [C#]'
- bitwise logical exclusive OR operator [C#]
- bitwise logical XOR operator [C#]
- ^ operator [C#]
- bitwise logical OR operator [C#]
- '| operator [C#]'
ms.openlocfilehash: bf42a53a89676f457d3d2df8d193a83299c3e4cc
ms.sourcegitcommit: 904b98d8d706f0e2d5ceaa00ce17ffbd92adfb88
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66758374"
---
# <a name="bitwise-and-shift-operators-c-reference"></a>Побитовые операторы и операторы сдвига (справочник по C#)

Следующие операторы выполняют побитовые операции или операции сдвига с операндами [целочисленных типов](../keywords/integral-types-table.md):

- Унарный оператор [`~` (побитовое дополнение)](#bitwise-complement-operator-)
- Бинарные операторы сдвига [`<<` (сдвиг влево)](#left-shift-operator-) и [`>>` (сдвиг вправо)](#right-shift-operator-)
- Бинарные операторы [`&` (логическое и)](#logical-and-operator-), [`|` (логическое или)](#logical-or-operator-) и [`^` (логическое исключающее или)](#logical-exclusive-or-operator-)

Эти операторы определены для типов `int`, `uint`, `long` и `ulong`. Если оба операнда имеют другие целочисленные типы (`sbyte`, `byte`, `short`, `ushort` или `char`), их значения преобразуются в тип `int`, который также является типом результата операции. Если операнды имеют разные целочисленные типы, их значения преобразуются в ближайший содержащий целочисленный тип. Дополнительные сведения см. в разделе [Числовые повышения уровня](~/_csharplang/spec/expressions.md#numeric-promotions) в статье [Спецификации языка C#](~/_csharplang/spec/introduction.md).

Операторы `&`, `|` и `^` также определяются для операндов типа `bool`. Дополнительные сведения см. в разделе [Логические операторы](boolean-logical-operators.md).

Побитовые операции и операции сдвига никогда не вызывают переполнение и дают одинаковые результаты в [проверенных и непроверенных](../keywords/checked-and-unchecked.md) контекстах.

## <a name="bitwise-complement-operator-"></a>Оператор побитового дополнения ~

Оператор `~` создает побитовое дополнение своего операнда путем инвертирования каждого бита:

[!code-csharp-interactive[bitwise NOT](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseComplement)]

Можно также использовать символ `~` для объявления методов завершения. Дополнительные сведения см. в разделе [Методы завершения](../../programming-guide/classes-and-structs/destructors.md).

## <a name="left-shift-operator-"></a>Оператор сдвига влево \<\<

Оператор `<<` сдвигает первый операнд влево на количество битов, определенное вторым операндом.

Операция сдвига влево отбрасывает старшие биты, которые находятся за пределами диапазона типа результата, и задает позиции пустых битов низкого порядка, равные нулю, как показано в следующем примере:

[!code-csharp-interactive[left shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#LeftShift)]

Поскольку операторы сдвига определены только для типов `int`, `uint`, `long` и `ulong`, результат операции всегда содержит по крайней мере 32 бита. Если первый операнд имеет другой целочисленный тип (`sbyte`, `byte`, `short`, `ushort` или `char`), его значение преобразуется в тип `int`, как показано в следующем примере:

[!code-csharp-interactive[left shift with promotion](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#LeftShiftPromoted)]

Сведения о том, как второй операнд оператора `<<` определяет величину сдвига, см. в разделе [Величина смещения операторов сдвига](#shift-count-of-the-shift-operators).

## <a name="right-shift-operator-"></a>Оператор сдвига вправо >>

Оператор `>>` сдвигает первый операнд вправо на количество битов, определенное вторым операндом.

Операция сдвига вправо удаляет младшие разряды, как показано в следующем примере:

[!code-csharp-interactive[right shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#RightShift)]

Позиции пустых битов высокого порядка задаются с учетом типа первого операнда следующим образом.

- Если первый операнд имеет тип [int](../keywords/int.md) или [long](../keywords/long.md), оператор сдвига вправо выполняет *арифметический* сдвиг. Значение старшего значимого бита (знаковый бит) первого операнда распространяется на пустые битовые позиции высокого разряда. То есть пустые битовые позиции высокого порядка разряда устанавливаются на ноль, если первый операнд неотрицательный, и устанавливаются на единицу, если он отрицательный.

  [!code-csharp-interactive[arithmetic right shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#ArithmeticRightShift)]

- Если первый операнд имеет тип [uint](../keywords/uint.md) или [ulong](../keywords/ulong.md), оператор сдвига вправо выполняет *логический* сдвиг. Пустым битовым позициям высокого порядка всегда присваивается нулевое значение.

  [!code-csharp-interactive[logical right shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#LogicalRightShift)]

Сведения о том, как второй операнд оператора `>>` определяет величину сдвига, см. в разделе [Величина смещения операторов сдвига](#shift-count-of-the-shift-operators).

## <a name="logical-and-operator-amp"></a>Оператор логического И &amp;

Оператор `&` вычисляет побитовое логическое И своих операндов:

[!code-csharp-interactive[bitwise AND](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseAnd)]

Для операндов типа `bool` оператор `&` вычисляет [логическое И](boolean-logical-operators.md#logical-and-operator-) своих операндов. Унарный оператор `&` является оператором [AddressOf](pointer-related-operators.md#address-of-operator-).

## <a name="logical-exclusive-or-operator-"></a>Оператор логического исключения ИЛИ ^

Оператор `^` вычисляет побитовое логическое исключающее ИЛИ, также известное как побитовое логическое XOR, своих операндов:

[!code-csharp-interactive[bitwise XOR](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseXor)]

Для операндов типа `bool` оператор `^` вычисляет [логическое исключающее ИЛИ](boolean-logical-operators.md#logical-exclusive-or-operator-) своих операндов.

## <a name="logical-or-operator-"></a>Оператор логического ИЛИ |

Оператор `|` вычисляет побитовое логическое ИЛИ своих операндов:

[!code-csharp-interactive[bitwise OR](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseOr)]

Для операндов типа `bool` оператор `|` вычисляет [логическое ИЛИ](boolean-logical-operators.md#logical-or-operator-) своих операндов.

## <a name="compound-assignment"></a>Составное присваивание

Для бинарного оператора `op` выражение составного присваивания в форме

```csharp
x op= y
```

эквивалентно

```csharp
x = x op y
```

за исключением того, что `x` вычисляется только один раз.

В следующем примере показано использование составного присваивания с побитовыми операторами и операторами сдвига:

[!code-csharp-interactive[compound assignment](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#CompoundAssignment)]

Из-за [числовых повышений уровня](~/_csharplang/spec/expressions.md#numeric-promotions) результат операции `op` может не быть явно преобразуемым в тип `T` `x`. В этом случае, если `op` является предопределенным оператором, и результат операции является явно преобразуемым в тип `T` `x`, выражение составного присваивания формы `x op= y` эквивалентно `x = (T)(x op y)`, за исключением того, что `x` вычисляется только один раз. В следующем примере продемонстрировано такое поведение.

[!code-csharp-interactive[compound assignment with cast](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#CompoundAssignmentWithCast)]

## <a name="operator-precedence"></a>Приоритет операторов

Следующий список упорядочивает побитовые операторы и операторы сдвига по приоритету, от высокого до низкого:

- Оператор побитового дополнения `~`
- Операторы сдвига `<<` и `>>`
- Оператор логического И `&`
- Оператор логического исключающего ИЛИ `^`
- Оператор логического ИЛИ `|`

Порядок вычисления, определяемый приоритетом операторов, можно изменить с помощью скобок (`()`).

[!code-csharp-interactive[operator precedence](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#Precedence)]

Полный список операторов C#, упорядоченных по уровню приоритета, см. в статье [Операторы C#](index.md).

## <a name="shift-count-of-the-shift-operators"></a>Величина смещения операторов сдвига

Для операторов сдвига `<<` и `>>` тип второго операнда должен быть [int](../keywords/int.md) или типом, имеющим [предопределенное неявное числовое преобразование](../keywords/implicit-numeric-conversions-table.md) в `int`.

Для выражений `x << count` и `x >> count` фактическая величина сдвига зависит от типа `x` следующим образом:

- Если тип `x` — [int](../keywords/int.md) или [uint](../keywords/uint.md), величина сдвига определяется младшими *пятью* битами второго операнда. То есть величина сдвига вычисляется на основе `count & 0x1F` (или `count & 0b_1_1111`).

- Если тип `x` — [long](../keywords/long.md) или [ulong](../keywords/ulong.md), величина сдвига определяется младшими *шестью* битами второго операнда. То есть величина сдвига вычисляется на основе `count & 0x3F` (или `count & 0b_11_1111`).

В следующем примере продемонстрировано такое поведение.

[!code-csharp-interactive[shift count example](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#ShiftCount)]

## <a name="enumeration-logical-operators"></a>Логические операторы перечисления

Операторы `~`, `&`, `|` и `^` также определены для любого типа [перечисления](../keywords/enum.md). Для операндов одного типа перечисления логическая операция выполняется для соответствующих значений базового целочисленного типа. Например, для любого `x` и `y` типа перечисления `T` с базовым типом `U` выражение `x & y` дает тот же результат, что и выражение `(T)((U)x & (U)y)`.

Побитовые логические операторы обычно используются с типом перечисления, который определяется с помощью атрибута [Flags](xref:System.FlagsAttribute). Дополнительные сведения см. в разделе [Типы перечислений как битовые флаги](../../programming-guide/enumeration-types.md#enumeration-types-as-bit-flags) в статье [Типы перечислений](../../programming-guide/enumeration-types.md).

## <a name="operator-overloadability"></a>Возможность перегрузки оператора

Определяемый пользователем тип может [перегружать](../keywords/operator.md) операторы `~`, `<<`, `>>`, `&`, `|` и `^`. При перегрузке бинарного оператора соответствующий оператор составного присваивания также неявно перегружается. Определяемый пользователем тип не может перегружать оператор составного присваивания явным образом.

Если определяемый пользователем тип `T` перегружает оператор `<<` или `>>`, тип первого операнда должен быть `T`, а тип второго — `int`.

## <a name="c-language-specification"></a>Спецификация языка C#

Дополнительные сведения см. в следующих разделах статьи [Спецификация языка C#](~/_csharplang/spec/introduction.md):

- [Оператор побитового дополнения](~/_csharplang/spec/expressions.md#bitwise-complement-operator)
- [Операторы сдвига](~/_csharplang/spec/expressions.md#shift-operators)
- [Логические операторы](~/_csharplang/spec/expressions.md#logical-operators)
- [Составное присваивание](~/_csharplang/spec/expressions.md#compound-assignment)
- [Числовые повышения уровня](~/_csharplang/spec/expressions.md#numeric-promotions)

## <a name="see-also"></a>См. также

- [Справочник по C#](../index.md)
- [Руководство по программированию на C#](../../programming-guide/index.md)
- [Операторы в C#](index.md)
- [Логические операторы](boolean-logical-operators.md)
