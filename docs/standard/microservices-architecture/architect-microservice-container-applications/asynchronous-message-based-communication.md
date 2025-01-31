---
title: Асинхронное взаимодействие на основе сообщений
description: Архитектура микрослужб .NET для контейнерных приложений .NET | Асинхронная связь на основе сообщений является основным понятием в архитектуре микрослужб, так как это лучший способ обеспечить независимость микрослужб друг от друга и при этом синхронизировать их.
ms.date: 09/20/2018
ms.openlocfilehash: 65bd0cd2b316fe7011ad8e878852547ee5949f09
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641378"
---
# <a name="asynchronous-message-based-communication"></a>Асинхронное взаимодействие на основе сообщений

Асинхронный обмен сообщениями и взаимодействие, управляемое событиями, имеют важное значение при распространении изменений по многим микрослужбам и связанным с ними моделям доменов. Как упоминалось ранее в обсуждении микрослужб и ограниченных контекстов (BC), модели (пользователь, клиент, продукт, учетная запись и т. д.) могут иметь разное значение для разных микрослужб или BC. Это означает, что при внесении изменений необходимо найти способ согласовать эти изменения для разных моделей. Для решения этой проблемы необходимо обеспечить итоговую согласованность и взаимодействие, управляемое событиями, на основе асинхронного обмена сообщениями.

При использовании системы обмена сообщениями процессы взаимодействуют путем асинхронного обмена сообщениями. Клиент отправляет команду или запрос в службу при помощи сообщения. Если служба должна ответить, она отправляет ответное сообщение клиенту. Так как это взаимодействие на основе сообщений, клиент знает, что ответ может поступить не сразу, а возможно, что ответа не будет вообще.

Сообщение состоит из заголовка (метаданные, например, идентификатор или данные для обеспечения безопасности) и текста. Обычно сообщения отправляются с использованием асинхронного протокола, например AMQP.

Предпочтительной инфраструктурой для такого типа обмена данными в сообществе микрослужб является упрощенный брокер сообщений, который отличается от больших брокеров и оркестраторов, используемых в SOA. В случае упрощенного брокера сообщений задача инфраструктуры обычно сводится к выполнению функций брокера обмена сообщениями с использованием простой реализации, например RabbitMQ или масштабируемой служебной шины в облаке, такой как служебная шина Azure. При таком сценарии основная обработка данных выполняется в конечных точках, там, где создаются и используются сообщения, т. е. микрослужбами.

Есть еще правило, которого следует придерживаться, насколько это возможно. Между внутренними службами следует использовать только асинхронный обмен сообщениями, а синхронное взаимодействие (например, HTTP) использовать только для клиентских приложений, работающих со службами интерфейса (шлюзами API и микрослужбами первого уровня).

Существует два типа асинхронного обмена сообщениями: взаимодействие на основе сообщений с одним получателем и взаимодействие с несколькими получателями. В следующих разделах содержатся дополнительные сведения об этих типах обмена.

## <a name="single-receiver-message-based-communication"></a>Взаимодействие на основе сообщений с одним получателем

Асинхронное взаимодействие на основе сообщений с одним получателем — это передача данных от одного узла другому, когда единственный получатель считывает сообщение из канала и сообщение обрабатывается только один раз. Однако существуют особые случаи. Например, в облачной системе, когда предпринимаются попытки автоматического восстановления после сбоя, одно и то же сообщение может быть отправлено многократно. Чтобы быть устойчивым к сетевым и другим сбоям, клиент должен иметь возможность повторить отправку сообщения, а сервер должен обеспечить идемпотентность операции, чтобы обработать каждое конкретное сообщение только один раз.

Взаимодействие на основе сообщений с одним получателем особенно хорошо подходит в случаях отправки асинхронных команд из одной микрослужбы другую. На рис. 4-18 иллюстрируется этот метод.

После того как вы начнете взаимодействие на основе сообщений (с использованием команд или событий), вам не следует использовать этот тип взаимодействия вместе с синхронным обменом по протоколу HTTP.

![Одна микрослужба, получающая асинхронное сообщение](./media/image18.png)

**Рис. 4-18**. Одна микрослужба, получающая асинхронное сообщение

Обратите внимание, что когда команды поступают из клиентских приложений, они могут быть реализованы в виде синхронных команд HTTP. Команды на основе сообщений следует использовать в случае необходимости обеспечения высокой масштабируемости или тогда, когда уже запущен бизнес-процесс на основе сообщений.

## <a name="multiple-receivers-message-based-communication"></a>Взаимодействие на основе сообщений с несколькими получателями

Существует более гибкий подход. Это механизм публикации или подписки, позволяющий сделать сообщения от отправителя доступными дополнительным микрослужбам-подписчикам или внешним приложениям. Он позволяет реализовать [принцип "открыт — закрыт"](https://en.wikipedia.org/wiki/Open/closed_principle) в службе отправки. Таким образом, в будущем могут быть добавлены дополнительные подписчики без изменения службы отправителя.

При взаимодействии на основе публикаций и подписок вы, возможно, будете использовать интерфейс шины событий при публикации событий для всех подписчиков.

## <a name="asynchronous-event-driven-communication"></a>Асинхронное взаимодействие, управляемое событиями

При использовании асинхронного взаимодействия, управляемого событиями, одна микрослужба публикует событие интеграции, когда что-то происходит внутри ее домена, а другая микрослужба должна узнать об этом. Пример такого события — изменение цены в микрослужбе каталога продукции. Дополнительные микрослужбы подписываются на события, что позволяет им получать данные о них асинхронно. В этом случае получатели могут обновить свои собственные сущности домена, что может вызвать появление новых событий интеграции, которые будут опубликованы. Эта система публикаций и подписок обычно реализуется с помощью шины событий. Шина событий может быть разработана как абстракция или интерфейс с API, необходимым для подписки и отмены подписки на события и для публикации событий. Шина событий может иметь одну или несколько реализаций на основе любого межпроцессорного брокера или брокера обмена сообщениями как очередь сообщений или служебная шина, поддерживающая асинхронное взаимодействие и модель публикаций и подписок.

Если система использует итоговую согласованность, управляемую событиями интеграции, рекомендуется разъяснить этот подход конечным пользователям. Не следует использовать в системе подход, который имитирует события интеграции, как, например, в системе SignalR или системах опроса клиентов. Конечный пользователь и владелец компании должны открыто принимать использование в системе принципа итоговой согласованности и понимать, что в большинстве случаев у бизнеса не возникает проблем с этим подходом до тех пор, пока он является открытым. Это важно, поскольку пользователи ожидают увидеть некоторые результаты сразу, а с итоговой согласованностью их может не быть.

Как отмечалось ранее в разделе [Распределенное управление данными. Проблемы и решения](distributed-data-management.md), события интеграции можно использовать для реализации бизнес-задач, охватывающих многие микрослужбы. Таким образом, вы получите итоговую согласованность между этими службами. Согласованная по принципу итоговой согласованности транзакция состоит из коллекции распределенных действий. В каждом действии соответствующая микрослужба обновляет сущность домена и публикует другое событие интеграции, которое вызывает следующее действие в рамках той же конечной задачи.

Важно то, что вы можете передать сообщение сразу нескольким микрослужбам, которые подписаны на это событие. Чтобы сделать это, вы можете использовать систему обмена сообщениями о публикациях и подписках на основе взаимодействия, управляемого событиями, как показано на рис. 4-19. Этот механизм публикаций и подписок используется не только в архитектуре микрослужб. Он похож на способ, которым взаимодействуют [ограниченные контексты](https://martinfowler.com/bliki/BoundedContext.html) в DDD, или на способ распространения обновлений от баз данных записи к базам данных чтения в архитектурах типа [разделение команд и запросов (CQRS)](https://martinfowler.com/bliki/CQRS.html). Цель — получить итоговую согласованность между различными источниками данных в распределенной системе.

![В асинхронном взаимодействии на основе событий одна микрослужба публикует события в шине событий, и многие микрослужбы могут подписаться на него, чтобы получать уведомления и реагировать.](./media/image19.png)

**Рис. 4-19**. Асинхронное взаимодействие, управляемое сообщением о событиях

Протокол, используемый для взаимодействия на основе сообщений, управляемого событиями, зависит от вашей реализации. Протокол [AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol) позволяет добиться надежного взаимодействия с использованием очередей.

При использовании шины событий может возникнуть необходимость использования уровня абстракции (например, интерфейса шины событий) на основе соответствующей реализации в классах с кодом, использующим API из брокера сообщений, например [RabbitMQ](https://www.rabbitmq.com/) или служебной шины, такой как [служебная шина Azure с разделами](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions). Кроме того, можно использовать служебную шину более высокого уровня, например NServiceBus, MassTransit или Brighter, чтобы связать вашу шину событий и систему публикаций и подписок.

## <a name="a-note-about-messaging-technologies-for-production-systems"></a>Примечание о технологии обмена сообщениями для производственных систем

Технологии обмена сообщениями, с помощью которых можно реализовать абстрактную шину событий, находятся на разных уровнях. Например, такие продукты, как RabbitMQ (транспорт брокера обмена сообщениями) и служебная шина Azure находятся на более низком уровне, чем другие продукты, такие как NServiceBus, MassTransit и Brighter, которые могут работать, используя RabbitMQ и служебную шину Azure. Выбор зависит от того, насколько много сложных функций уровня приложения и готовых к использованию возможностей масштабирования необходимо для вашего приложения. Для реализации шины событий, предназначенной только для демонстрации принципа работы и используемой в среде разработки, как было показано на примере eShopOnContainers, будет достаточно простой реализации на основе системы RabbitMQ, работающей в контейнере Docker.

Для построения критически важных и производственных систем, требующих широких возможностей масштабирования, следует использовать служебную шину Azure. Для обеспечения высокого уровня абстракции и функций, облегчающих разработку распределенных приложений, рекомендуется использовать другие коммерческие служебные шины и служебные шины с открытым кодом, такие как NServiceBus, MassTransit и Brighter. Кроме того, вы можете создавать свои собственные функции служебной шины на основе низкоуровневых технологий, таких как RabbitMQ и Docker. Однако эта черная работа может оказаться слишком дорогим занятием при разработке корпоративного приложения.

## <a name="resiliently-publishing-to-the-event-bus"></a>Гибкая публикация в шине событий

Главной сложностью при реализации архитектуры, управляемой событиями, предназначенной для работы с несколькими микрослужбами, является обеспечение атомарного обновления состояния в исходной микрослужбе с одновременной гибкой публикацией соответствующего события интеграции в служебной шине, выполняемое с помощью транзакций. Далее описано несколько способов достижения этого. Возможны и другие подходы.

- Использование очереди транзакций (на основе DTC), подобной MSMQ. (Этот способ применялся в системах более ранних версий.)

- [Интеллектуальный анализ данных журнала транзакций](https://www.scoop.it/t/sql-server-transaction-log-mining).

- Использование полной модели [источников событий](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing).

- Использование [модели исходящих сообщений](http://gistlabs.com/2014/05/the-outbox/), таблицы базы данных транзакций как очереди сообщений, которая служит основой для компонента генерации событий, создающего и публикующего события.

При использовании асинхронного взаимодействия следует дополнительно рассмотреть вопросы идемпотентности и дедупликации сообщений. Эти вопросы рассматриваются в разделе [Реализация взаимодействия между микрослужбами на основе событий (события интеграции)](../multi-container-microservice-net-applications/integration-event-based-microservice-communications.md) далее в этом руководстве.

## <a name="additional-resources"></a>Дополнительные ресурсы

- **Обмен сообщениями на основе событий** \
  <http://soapatterns.org/design_patterns/event_driven_messaging>

- **Канал публикации или подписки** \
  <https://www.enterpriseintegrationpatterns.com/patterns/messaging/PublishSubscribeChannel.html>

- **Уди Дахан (Udi Dahan). Пояснения к CQRS** \
  <http://udidahan.com/2009/12/09/clarified-cqrs/>

- **Архитектура с разделением команд и запросов (CQRS)** \
  <https://docs.microsoft.com/azure/architecture/patterns/cqrs>

- **Взаимодействие между ограниченными контекстами** \
  <https://docs.microsoft.com/previous-versions/msp-n-p/jj591572(v=pandp.10)>

- **Итоговая согласованность** \
  <https://en.wikipedia.org/wiki/Eventual_consistency>

- **Джимми Богард (Jimmy Bogard). Рефакторинг для обеспечения отказоустойчивости: оценка взаимозависимости** \
  <https://jimmybogard.com/refactoring-towards-resilience-evaluating-coupling/>

> [!div class="step-by-step"]
> [Назад](communication-in-microservice-architecture.md)
> [Вперед](maintain-microservice-apis.md)
