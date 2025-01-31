---
title: Начало работы с F# в Visual Studio
description: Сведения об использовании F# с помощью Visual Studio.
ms.date: 07/03/2018
ms.openlocfilehash: 9b02a5d295f982b1911dab567213fa9a2b6c4304
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754863"
---
# <a name="get-started-with-f-in-visual-studio"></a>Начало работы с F# в Visual Studio

F#и визуальный F# инструментарий поддерживаются в Интегрированной среде разработки Visual Studio.

Чтобы начать, убедитесь, что у вас есть [установлена среда Visual Studio с F# ](install-fsharp.md#install-f-with-visual-studio).

## <a name="creating-a-console-application"></a>Создание консольного приложения

Одним из основных проектов в Visual Studio — это консольное приложение.  Вот как это делается.  После открытия Visual Studio:

1. На **файл** последовательно выберите пункты **New**, а затем выберите **проекта**.

2. В New Project диалоговое окно, в разделе **шаблоны**, вы должны увидеть **Visual F#** .  Выберите для отображения F# шаблонов.

3. Выберите либо **.NET Core, консольное приложение** или **консольное приложение**.

4. Выберите **хорошо** кнопку, чтобы создать F# проекта!  Теперь вы увидите F# проекта в обозревателе решений.

## <a name="writing-your-code"></a>Написание кода

Давайте начнем сначала пишет некоторый код.  Убедитесь, что `Program.fs` файл открыт и замените его содержимое следующим:

[!code-fsharp[HelloSquare](../../../samples/snippets/fsharp/getting-started/hello-square.fs)]

В предыдущем примере кода, функция `square` был определен который принимает ввод с именем `x` и умножает его самостоятельно.  Так как F# использует [вывод типа](../language-reference/type-inference.md), тип `x` не должны быть указаны.  F# Компилятор распознает типы, где умножение является допустимым, а также будет назначать тип для `x` зависит `square` вызывается.  Если навести `square`, вы должны увидеть следующее:

```fsharp
val square: x:int -> int
```

Это связано с так называемой сигнатура типа функции.  Может быть прочитан следующим образом: «Квадрата является функция, которая принимает целое число с именем x и создает целое число».  Обратите внимание, что компилятор обеспечивал `square` `int` тип сейчас - это обусловлено умножения, не является универсальным через *все* типы, но довольно универсален через набор закрытых типов.  F# Компилятора выбраны `int` это точка, но он настроит сигнатуре типа при вызове метода `square` с другим ввода типа, например `float`.

Другую функцию, `main`, определяется, который дополняется `EntryPoint` атрибут, чтобы сообщить F# компилятора, выполнение программы следует начать с этого.  Его следует тому же образцу что и другие [языков программирования в стиле C](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B), где эту функцию можно передать аргументы командной строки и возвращается код целого числа (обычно `0`).

В этой функции, мы вызываем `square` функцию с аргументом `12`.  F# Компилятор затем назначает тип `square` быть `int -> int` (то есть функция, которая принимает `int` и создает `int`).  Вызов `printfn` является форматированный печати функция, которая использует строку формата, аналогичную языков программирования C-стиля, параметры, которые соответствуют заданным в строке формата, а затем распечатывает результат и новую строку.

## <a name="running-your-code"></a>Выполнение кода

Можно выполнить код и увидеть результаты, нажав клавишу **Ctrl**+**F5**.  Это запускает программу без отладки и дает возможность видеть результаты.  Кроме того, вы можете **Отладка** меню верхнего уровня элемент в Visual Studio, выбрав **Запуск без отладки**.

Теперь вы увидите напечатаны в окне консоли, Visual Studio появилось следующее:

```
12 squared is 144!
```

Поздравляем!  Вы создали свое первое F# проект в Visual Studio, написанные F# функция печати результаты вызова метода, функции и запустите проект, чтобы увидеть некоторые результаты.

## <a name="next-steps"></a>Следующие шаги

Если это еще не сделано, см. статью [примером F# ](../tour.md), где приведены некоторые основные функции F# языка.  Она даст вам Общие сведения о некоторых возможностях F#и приводятся примеры кода можно в полной мере, которые можно скопировать в Visual Studio и запустить.  Существуют также некоторые полезные внешние ресурсы, которые можно использовать, показывавшие в [ F# руководство](../index.md).

## <a name="see-also"></a>См. также

- [Обзор языка F#](../tour.md)
- [F#Справочник по языку](../language-reference/index.md)
- [Вывод типа](../language-reference/type-inference.md)
- [Справочник символов и оператор](../language-reference/symbol-and-operator-reference/index.md)
