---
title: 'Исключения: функция raise'
description: Узнайте, как F# «raise» функция используется для указания, что произошло ошибку или исключительную ситуацию.
ms.date: 05/16/2016
ms.openlocfilehash: 9e2515ad7b85c1025bc3aa0aa2a6929a8d35436d
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641967"
---
# <a name="exceptions-the-raise-function"></a>Исключения: функция raise

`raise` Функция используется для указания, что произошло ошибку или исключительную ситуацию. Сведения об ошибке записывается в объект исключения.

## <a name="syntax"></a>Синтаксис

```fsharp
raise (expression)
```

## <a name="remarks"></a>Примечания

`raise` Функция создает объект исключения и инициирует процесс освобождения стека. Процесс освобождения стека управляет среда CLR (CLR), поэтому этот процесс происходит так же, как в любом другом языке .NET. Процесс освобождения стека заключается в поиске обработчик исключений, который соответствует порожденное исключение. Поиск начинается в текущем `try...with` выражения, если таковой имеется. Каждый шаблон `with` блока установлен, в порядке. При обнаружении соответствующего обработчика исключений, исключение считается обработанным; в противном случае стек освобождается и `with` блоков в цепочке вызовов проверяются, пока не будет найден соответствующий обработчик. Любой `finally` блоки, которые встречаются в цепочке вызовов, также выполняются в последовательности раскрутки стека.

`raise` Функция является эквивалентом `throw` в C# или C++. Используйте `reraise` в обработчике catch для распространения вверх по цепи вызова одно и то же исключение.

В следующих примерах кода показано использование `raise` функция создает исключение.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5801.fs)]

`raise` Функция также может использоваться для создания исключений .NET, как показано в следующем примере.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5802.fs)]

## <a name="see-also"></a>См. также

- [Обработка исключений](index.md)
- [Типы исключения](exception-types.md)
- [Исключения. `try...with` Выражение](the-try-with-expression.md)
- [Исключения. `try...finally` Выражение](the-try-finally-expression.md)
- [Исключения. `failwith` Функции](the-failwith-function.md)
- [Исключения. `invalidArg` Функции](the-invalidArg-function.md)
