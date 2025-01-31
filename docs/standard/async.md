---
title: Обзор асинхронной модели
description: Сведения о том, что асинхронное программирование — это ключевая методика, которая упрощает обработку блокирующих операций ввода-вывода и параллельных операций на нескольких ядрах.
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.technology: dotnet-standard
ms.assetid: 1e38e9d9-8284-46ee-a15f-199adc4f26f4
ms.openlocfilehash: aa08389d896fa81dbed8a63bb22a97e151016392
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64628798"
---
# <a name="async-overview"></a>Обзор асинхронной модели

Не так давно ускорение работы приложений обеспечивалось простой покупкой нового ПК или сервера, однако со временем эта тенденция сошла на нет. Более того, она обернулась вспять. Появились мобильные телефоны с процессорами ARM с частотой каждого ядра 1 ГГц, а серверные рабочие нагрузки были перенесены в виртуальные машины. Пользователи по-прежнему хотят иметь быстрый и отзывчивый интерфейс, а деловые пользователи хотят, чтобы их серверы масштабировались с ростом их бизнеса. Переход на мобильные и облачные решения 3 миллиарда подключенных к Интернету пользователей привели к появлению нового набора шаблонов ПО. 

* Клиентские приложения должны быть постоянно доступны, всегда подключены к сети, мгновенно реагировать на действия пользователей (например, касания экрана) и иметь высокий рейтинг в магазинах приложений.
* Службы должны справляться со всплесками трафика, корректно выполняя масштабирование вверх и вниз. 

Асинхронное программирование — это ключевая методика, которая упрощает обработку блокирующих операций ввода-вывода и параллельных операций на нескольких ядрах. .NET позволяет приложениям и службам сохранять гибкость и оставаться эластичными благодаря простым моделям асинхронного программирования на уровне языка в C#, VB и F#.

## <a name="why-write-async-code"></a>Зачем писать асинхронный код?

Современные приложения активно используют файловые и сетевые операции ввода-вывода. API ввода-вывода обычно являются блокирующими по умолчанию, в результате чего возникают зависания пользовательского интерфейса и снижается эффективность использования оборудования. Избежать этого можно, только научившись пользоваться сложными шаблонами. Основанные на задачах асинхронные интерфейсы API и модель асинхронного программирования на уровне языка меняют эту диспозицию и делают асинхронное выполнение режимом по умолчанию, при этом для их использования требуется освоить совсем немного новых понятий.

Асинхронный код имеет следующие характеристики.

* Обрабатывает больше запросов сервера, предоставляя потокам возможность обрабатывать больше запросов во время ожидания результата от запросов ввода-вывода.
* Делает пользовательский интерфейс более быстрым, выделяя потоки для обработки действий в пользовательском интерфейсе во время ожидания запросов ввода-вывода и передавая затратные по времени операции другим ядрам ЦП.
* Многие новые API-интерфейсы .NET являются асинхронными.
* Писать асинхронный код в .NET очень просто.

## <a name="whats-next"></a>Что дальше?

Дополнительные сведения см. в статье [Подробный обзор асинхронного программирования](async-in-depth.md).

Статья [Шаблоны асинхронного программирования](asynchronous-programming-patterns/index.md) содержит общие сведения о трех шаблонах асинхронного программирования, поддерживаемых в .NET:  
  
- [Асинхронная модель программирования (APM)](asynchronous-programming-patterns/asynchronous-programming-model-apm.md) (устаревший)  
  
- [Асинхронная модель на основе событий (EAP)](asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md) (устаревший)  
  
- [Асинхронный шаблон, основанный на задачах (TAP)](asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) (рекомендуется для новых разработок)  

Дополнительные сведения о рекомендованных моделях программирования на основе задач см. в статье [Асинхронное программирование на основе задач](parallel-programming/task-based-asynchronous-programming.md).
