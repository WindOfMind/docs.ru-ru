---
title: Преимущества приложений, созданных для облака
description: Модернизация существующих приложений .NET с помощью облака Azure и Windows контейнерах | Как насчет облачных приложений?
ms.date: 04/28/2018
ms.openlocfilehash: 2d459b4ab3e015bb328699aa1d53159593e06da0
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65643661"
---
# <a name="what-about-cloud-native-applications"></a>Преимущества приложений, созданных для облака

Несмотря на то что [облака](https://azure.microsoft.com/overview/cloudnative/) приложения не служит главной темой этого руководства, полезно иметь представление о этого уровня зрелости модернизации и отличать его от оптимизированную для облачных приложений.

Рис. 4-3 помещает облачных приложений по уровням зрелости модернизации приложений:

![Позиционирование облачных приложений](./media/image3.png)

> **Рис. 4-3.** Позиционирование облачных приложений

Уровня зрелости модернизации облака обычно требуется новый вложений в развитие. Перемещение на уровень облака - машинный код обычно определяется потребность в модернизация приложений, насколько возможно, чтобы радикально улучшить масштабирование в больших приложениях, создав автономные подсистемы (микрослужб), которые могут быть развернуты и масштабирования независимо друг от друга из других областей приложения при снижении расходов в длинный термин и увеличение гибкости развитие части этих автономного приложения, которые предоставляют значительные преимущества конкурируют.

Основные принципы облачных приложений основаны на подходы к архитектуре микрослужб, которые могут развиваться с гибкостью и масштабирование до ограничения, которые будет трудно достичь в монолитных архитектуре, развертывании в локальной или облачной Среда.

Рис. 4-4 показаны основные характеристики модели облака.

> ![Характеристики облака, Микрослужб, гибкие, оркестраторов контейнеров и без сервера](./media/image4.png)
>
> **Рис. 4-4.** Характеристики облака

Кроме того вы можете расширить базовые современных веб-приложений и облачными приложениями, добавив другие службы, например искусственного интеллекта (ИИ), машинного обучения (ML) и Интернета вещей. Можно использовать любой из этих служб для расширения любого из возможных подходов, оптимизированными для облака.

Фундаментальное различие в приложениях на уровне облака — в архитектуре приложения. Облачные приложения, по определению приложений, основанных на микрослужбах. Облачные приложения требуют специальных архитектур, технологий и платформ, по сравнению с монолитных веб-приложения или традиционных N-уровневого приложения.

## <a name="cloud-native-applications-details"></a>Сведения об облачных приложений

Облака — это более расширенную или зрелой состояние для больших и критически важных приложений. Облачные приложения обычно требуют архитектура и проектирование, которая была создана с нуля, а не модернизация существующих приложений. Основное различие между приложением облака и проще, оптимизированными для облака веб-приложения — это рекомендации по использованию архитектуры микрослужб в рамках подхода облака. Оптимизированная для облачных приложений также может быть монолитных веб-приложений или N-уровневых приложений.

[-Факторного приложения](https://12factor.net/) (коллекция шаблонов, которые тесно связаны с подходами микрослужб) также считается обязательным для архитектуры облачных приложений.

[Cloud собственного Foundation вычислений (CNCF)](https://www.cncf.io/) является основной диспетчера принципов облака. Корпорация Майкрософт считает [членом CNCF](https://azure.microsoft.com/blog/announcing-cncf/).

Пример определения и Дополнительные сведения о характеристиках облачных приложений, см. в статье Gartner [о разработке архитектуры и проектирование приложений для облака](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications). Конкретные рекомендации от корпорации Майкрософт о том, как реализовать приложение, облака, см. в разделе [микрослужбы .NET: Архитектура контейнерных приложений .NET](https://aka.ms/microservicesebook).

Наиболее важным фактором, которые следует учитывать при переносе полноценное приложение с моделью облака — что необходимо перепроектирование архитектуры на базе микрослужб. Это требует значительных инвестиций для разработки из-за больших рефакторинга процесс. Обычно этот параметр выбирается для критически важных приложений, требующих новых уровней масштабируемости и долгосрочной перспективе. Однако можно начать перемещение к облака, добавив микрослужб для всего несколько новых сценариев и в конечном итоге рефакторинга приложения полностью как микрослужбы. Это добавочное подход, который является наилучшим вариантом для некоторых сценариев.

## <a name="what-about-microservices"></a>Как насчет микрослужб?

Важно понимать микрослужбы и как они работают, когда вы рассматриваете облачных приложений для вашей организации.

Архитектура микрослужб является усовершенствованный подход, который можно использовать для приложений, созданных с нуля, или по мере развития существующих приложений к облачных приложений. Можно запустить, добавив несколько микрослужб в существующие приложения, чтобы узнать о новых парадигм микрослужб. Но, очевидно, необходимо архитектор и кодом, особенно для таких архитектурный подход.

Тем не менее не являются обязательными для любого нового или современные приложения микрослужб. Микрослужбы не «bullet magic», и они не лучший способ создания каждое приложение. Как и когда вы используете микрослужбы зависит от типа приложения, которое необходимо создать.

Архитектура микрослужб становится предпочтительным подходом для распределенных и крупных или сложных критически важных приложений, основанных на нескольких независимых подсистемах в виде автономных служб. В архитектуре на базе микрослужб приложения на базе коллекции служб, которые можно независимо разрабатывать, тестировать, обновлять, развертывать и масштабировать. Это могут быть любые связанные автономной базы данных каждой микрослужбы.

Подробный обзор архитектуры микрослужб, который можно реализовать с помощью .NET Core, см. в разделе PDF электронная книга [микрослужбы .NET: Архитектура контейнерных приложений .NET](https://aka.ms/microservicesebook). Это руководство также доступно [online](../../microservices-architecture/index.md).

Но даже в сценариях, в которых микрослужбы открывают мощные возможности независимый развертывание, строгие границы подсистем и техническое разнообразие — они создают много новых задач. Проблемы относятся к разработке распределенных приложений, например моделей фрагментации и не зависят от данных; Достижение устойчивой связью между микрослужбами; потребность в итоговую согласованность; и сложность эксплуатации. Микрослужбы представлена более высокий уровень сложности, по сравнению с традиционной монолитных приложений.

Из-за сложности архитектуры микрослужб только для конкретных сценариев и определенных типах приложения подходят для приложений на основе микрослужб. К ним относятся большие и сложные приложения с несколькими развивается подсистем. В таких случаях разумно инвестировать в более сложная архитектура программного обеспечения, повысить гибкость долгосрочное и более эффективное обслуживание приложения. Но для более сложных сценариев, это будет лучшим решением для продолжения подход монолитного приложения или приближается к проще N-уровневых.

И последнее замечание, несмотря на риск повторяющихся о трудностях, из которых не следует взглянуть на использование микрослужб в приложениях как «файловый или ничего вообще.» Можно расширять и развивать имеющиеся монолитные приложения путем добавления новых, небольших сценариях на основе микрослужб. Не нужно начинать с нуля, чтобы приступить к работе с использованием архитектуры микрослужб. На самом деле мы рекомендуем, что вы переходите от с помощью существующего монолитных или N-уровневого приложения, добавив новые сценарии. В конце концов вы можете разбить приложение в автономные компоненты или микрослужб. Вы можете начать развивается монолитных приложений в направлении микрослужб, шаг за шагом.

В любом случае остальной части этого настоящем руководстве основное внимание уделяется самое главное в «нет на базе микрослужб приложений», так как это руководство предназначено главным образом модернизации существующих приложений, которые обычно имеют монолитных или N-уровневых архитектур.

> [!div class="step-by-step"]
> [Назад](microsoft-technologies-in-cloud-optimized-applications.md)
> [Вперед](deploy-existing-net-apps-as-windows-containers.md)
