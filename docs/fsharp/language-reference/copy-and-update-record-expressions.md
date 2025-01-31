---
title: Копирование и обновление выражений записей
description: Вы можете научиться писать «копировать и обновить записи выражение» копирует существующих записей, обновления полей и возвращает обновленной записи.
author: ChrSteinert
ms.date: 06/04/2016
ms.openlocfilehash: 7657b0295c9437890baea258295f9e9ab10073dd
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645583"
---
# <a name="copy-and-update-record-expressions"></a>Копирование и обновление выражений записей

Объект *копирование и обновление выражений записей* выражение, которое копирует существующую запись, затем обновляет указанные поля и возвращает обновленной записи.

## <a name="syntax"></a>Синтаксис

```fsharp
{ record-name with
    updated-member-definitions }
```

## <a name="remarks"></a>Примечания

Записи являются неизменяемыми по умолчанию, таким образом, возможна по существующей записи не обновляются. Для создания обновленной записи все поля записи придется задать снова. Для упрощения этой задачи *копирование и обновление выражений записей* может использоваться. Это выражение принимает существующую запись, создает новый того же типа, используя указанные поля из выражения и отсутствует поле, указанных с помощью выражения.
Это может быть полезно, если необходимо скопировать существующую запись и при необходимости измените некоторые значения поля.

Возьмем например созданной записи.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

Если пришлось обновлять только в поле этой записи можно использовать *копирование и обновление выражений записей* следующим образом:

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

## <a name="see-also"></a>См. также

- [Записи](records.md)
- [Справочник по языку F#](index.md)
