---
title: Контейнеры как основа для совместной работы DevOps
description: Понять ключевую роль контейнеров для упрощения DevOps.
ms.date: 02/15/2019
ms.openlocfilehash: 37faf00f270414df363f36894317f31f81a2937e
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641317"
---
# <a name="containers-as-the-foundation-for-devops-collaboration"></a>Контейнеры как основа для совместной работы DevOps

По самой природе технологии Docker и контейнеры разработчики могут совместно использовать программного обеспечения и его зависимости легко с ИТ-операций и рабочих средах устраняя типичный оправдание «это работает на моем компьютере». Контейнеры решить конфликты приложений одной среды в другую. Косвенно, контейнеры и Docker объединяют разработчиков и ИТ-операций ближе, упрощая их эффективной совместной работы. Внедрение рабочего процесса контейнера предоставляет многие клиенты с непрерывности DevOps, они поиск, но ранее приходилось реализовывать более сложные конфигурации для выпуска и сборки конвейеров. Контейнеры упрощают конвейеры сборки, тестирования и развертывания в DevOps.

![Docker позволяет мостов между разработчиков и архитекторов рабочей нагрузки разработки и проектирования и ИТ-операций в рабочей нагрузке выполнения/наблюдение и управление](./media/image1.png)

**Рис. 2-1.** Основных рабочих нагрузок на «лица» жизненного цикла контейнерных приложений Docker

С помощью контейнеров Docker, разработчикам собственных что находится в пределах контейнера (приложения и службы и зависимости для платформы и компонентов) и как контейнеры и службы, ведут себя вместе как приложение, состоящее в коллекцию служб. Определенные взаимозависимости из нескольких контейнеров в `docker-compose.yml` файла или сути *манифест развертывания*. В то же время команд ИТ-специалистов (специалистов по ИТ и управление) можно сосредоточиться на управлении производственные среды; инфраструктуры; масштабируемость; мониторинг; и, в конечном счете, гарантируя, что приложения обеспечивают должным образом для конечных пользователей без необходимости знать содержание различные контейнеры. Таким образом имя «контейнера,» отзыв проносить на реальных контейнеры. Таким образом Владельцы содержимого контейнера требуется не относятся к себе в том, как будут отправлены контейнера доставки компании транспорты и контейнера из исходной точки в место назначения без знания или проявлением заботы о содержимом. Аналогичным образом разработчики могут создавать и владельцем содержимого в контейнере Docker, без необходимости вынужденными обращаться с механизмами «транспорт».

В принцип, в левой части из рис. 2-1 разработчиков, записи и выполнения кода локально в контейнерах Docker с помощью Docker для Windows или Mac. Они определяют операционной среде для кода, используя файл Dockerfile, который указывает базовый операционную систему для запуска, а также действия построения для создания кода в образ Docker. Разработчики определяют, как один или несколько образов может взаимодействовать с помощью упомянутых выше `docker-compose.yml` файл манифеста развертывания. По завершении их локальной разработки, они сближают код приложений, а также файлы конфигурации Docker в репозитории кода по своему выбору (то есть репозиторий Git).

Принцип DevOps определяет конвейеры сборки — постоянная интеграции (CI), с помощью Dockerfile, предоставленные в репозитории кода. Интеграция CI-системы извлекает базовых образов контейнеров из выбранного реестра Docker и построения пользовательских образов Docker для приложения. Образы затем проверяются и отправлялся в реестр Docker, используемых для развертываний в нескольких средах.

В опорный справа операции, которые команды управлять развернутых приложений и инфраструктуры в рабочей среде при наблюдении за среды и приложений, таким образом, они могут предоставить отзыв и подробные сведения для разработчиков о том, как приложение может быть улучшена. Приложения-контейнеры обычно выполняются в рабочей среде с помощью оркестраторов контейнеров.

Две команды работаете совместно с другими через базовая платформа (контейнерах Docker), которая обеспечивает разделение областей ответственности как контракт, то же время значительно улучшает совместную работу двух группах в жизненном цикле приложения. Разработчики владельцем содержимого контейнера, его операционной среды и взаимозависимости контейнера, тогда как проектные занять готовые образы, а также манифест и выполняет их в системы оркестрации.

## <a name="challenges-in-application-life-cycle-when-using-docker"></a>Задач в приложение жизненного цикла при использовании Docker.

Есть много причин, которые будет увеличить количество контейнерных приложений в предстоящие годы и одной из следующих причин заключается в создании приложений на основе микрослужб.

В течение 15 лет, использование веб-службы была базой для тысяч приложений и, возможно, после нескольких лет, очень скоро найдется та же ситуация с приложениями на базе микрослужб, работающими в контейнерах Docker.

Также стоит, можно также использовать контейнеры Docker для монолитных приложений, а вы по-прежнему получить большую часть преимущества Docker. Контейнеры не будут выполняться только микрослужб.

Использование Docker использование контейнеров и микрослужб причины новые трудности в процессе разработки вашей организации, и таким образом, вы должны хорошо продуманная стратегия для поддержания множества контейнеров и микрослужб, выполняющихся в рабочих системах. В конечном счете корпоративные приложения будет иметь сотни или тысячи контейнеров или экземпляров, работающих в рабочей среде.

Эти задачи создают новые требования, при использовании инструментов DevOps, поэтому вам придется определить новые процессы в действиях DevOps, а также содержатся ответы на вопросы такого рода:

- Какие средства можно использовать для разработки, непрерывной Интеграции и Развертывания, управления и операций

- Как Моя компания управлять ошибок в контейнеры при выполнении в рабочей среде?

- Как изменить части нашего программного обеспечения в рабочей среде с минимальным временем простоя?

- Как выполнять масштабирование и как можно отслеживать производственную систему?

- Как мы выполнить тестирование и развертывание контейнеров на наш конвейер выпуска?

- Как можно использовать средства/платформ с открытым исходным для контейнеров в Microsoft Azure?

Если можно ответить на эти вопросы, вы будете лучше готовы переместить приложения (приложения для существующего или нового) для контейнеров Docker. 

## <a name="introduction-to-a-generic-end-to-end-docker-application-life-cycle-workflow"></a>Введение в универсальные приложения Docker end-to-end жизненного цикла рабочего процесса

Рис. 2-2 представляет более подробный рабочий процесс для жизненного цикла приложения Docker, уделяя основное внимание в данном экземпляре определенных действий DevOps и ресурсов.

![На этой диаграмме показаны «внешний цикл» DevOps. Когда код отправляется в репозиторий, конвейер непрерывной Интеграции запускается, а затем начинает конвейера компакт-диска, возвращает развернуто приложение. Метрики, собранные из развернутых приложений отправляются обратно рабочую нагрузку разработки, где происходит «внутреннем цикле», чтобы группы разработчиков имеют фактические данные реагировать на потребности пользователей и бизнес.](./media/image2.png)

**Рис. 2-2.** Высокоуровневый рабочий процесс для жизненного цикла контейнерного приложения Docker

Все начинается с разработчика, запускающий процесс написания кода в рабочий процесс внутреннего цикла. Этап внутреннего цикла является, где разработчикам определить все, что перед публикацией кода в репозитории кода (например, систему управления версиями например Git). После него зафиксирована, репозиторий триггеры непрерывной интеграции (CI) и остальная часть рабочего процесса.

Внутренний цикл, по сути состоит из типичные действия, такие как «код», «запустить», «test» и «отладка», а также дополнительные шаги, которые необходимы до локального запуска приложения. Это процесс разработчика для запуска и тестирования приложения в качестве контейнера Docker. Рабочий процесс внутреннего цикла будет рассматриваться в последующих разделах.

Рассмотрение рассмотрим конец окончания рабочего процесса, рабочий процесс DevOps больше, чем это технология или набор инструментов: это образ мышления, требующий региональные развитие. Его людей, процессы и соответствующие средства чтобы жизненного цикла приложения быстрее и более предсказуемой. Предприятия, которые обычно внедрить контейнерных рабочего процесса реструктуризации организациях для представления людей и процессы, которые соответствуют контейнерных рабочих процессов.

Практики DevOps может помочь группам реагировать быстрее вместе конкуренции, заменив ошибкам ручные процессы с помощью службы автоматизации, что приводит к возможность отслеживания и повторяемые рабочие процессы. Также организации можно более эффективно управлять средами и реализовать сэкономить с помощью сочетания локальных и облачных ресурсов, а также тесно интегрированных инструментов.

При реализации рабочего процесса DevOps для приложений Docker, вы увидите, что технологии Docker присутствуют в почти всех этапов рабочего процесса, в среде разработки при работе во внутреннем цикле (выполнения кода, отладки), на этапе сборки теста непрерывной Интеграции и, Наконец развертывание этих контейнеров в промежуточной и рабочей средах.

Для улучшения качества по помогает определить дефекты на ранних этапах цикла разработки, что сокращает затраты на их исправлении. Включая среды и зависимости в образ и внедрить принципы развертывания одного образа в нескольких средах, повышение уровня дисциплины извлечения конфигурации конкретной среды, надежность развертывания.

Форматированного данные, полученные через инструментарий действующие (мониторинг и диагностика) позволяет отслеживать проблемы с производительностью и поведения пользователей вспомогательными будущих приоритеты и инвестиций.

DevOps считается путешествие, а не место назначения. Он должен быть реализован постепенно посредством соответствующим образом области проектов, из которых можно продемонстрировать успех, Дополнительные сведения и развиваться.

## <a name="benefits-of-devops-for-containerized-applications"></a>Преимущества DevOps для контейнерных приложений

Ниже приведены некоторые из наиболее важных преимуществ, предоставляемых средой сплошной рабочего процесса DevOps.

- Доставка программного обеспечения более высокого качества, быстрее и лучше соответствует.

- Диск постоянного совершенствования и корректировки, более ранней версии и более выгодно.

- Повышение прозрачности и совместной работы между участниками, участвующих в доставке и эксплуатации программного обеспечения.

- Контроля затрат и более эффективно использовать подготовленные ресурсы, одновременно снижая риски безопасности.

- Plug and play с многие существующие инвестиции DevOps, включая вложения в открытым исходным кодом.

>[!div class="step-by-step"]
>[Назад](index.md)
>[Вперед](../Microsoft-platform-tools-containerized-apps/index.md)
