---
title: Монолитные приложения
description: Изучить основные понятия для контейнеризация монолитных приложений.
ms.date: 02/15/2019
ms.openlocfilehash: e577f9a8d9ce4f9d2c8180318b1df181db730e2f
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641299"
---
# <a name="monolithic-applications"></a>Монолитные приложения

В этом случае при создании в единый и монолитных веб-приложение или службу и развернуть его в качестве контейнера. В приложении структуре не может быть монолитных; он может состоять из нескольких библиотек, компонентов или даже уровней (уровень приложений, уровень предметной области, уровень доступа к данным, и т.д.). Внешне оно будет представлять собой единый контейнер, одного процесса, единое веб-приложение или единую службу.

Для управления этой моделью вы развертываете один контейнер, представляющий собой приложение. Для его масштабирования, просто добавьте несколько дополнительные копии с подсистемой балансировки нагрузки спереди. Гораздо проще управлять одним развертыванием в одном контейнере или виртуальной машины (VM).

После основного сервера контейнер делает только одну вещь что делает это в рамках одного процесса монолитный шаблон находится в конфликт. Как показано на рисунке 4-1, может включать несколько компонентов, библиотек или внутренних слоев в каждом контейнере.

![Такие приложения масштабируются имеет всего или большей части его функциональность в одном процессе или контейнере, и он состоит из отдельных компонентов в внутренних слоев или библиотеки.](./media/image1.png)

**Рис. 4-1.** Пример архитектуры монолитного приложения

Недостаток этого подхода, определяется Если или когда приложение разрастается и его необходимо масштабировать. Если масштабируется приложение целиком, все получится. Однако в большинстве случаев несколько частей приложения являются нормально, которые требуют масштабирования, в то время как менее используются другими компонентами.

Используя пример типичных электронной коммерции, скорее всего, необходим для масштабирования сведения компонента продукта. Клиенты чаще просматривают товары, чем приобретают их. Клиенты чаще складывают товары в корзину, чем оплачивают их. Не так много клиентов пишут комментарии или просматривают историю покупок. И, скорее всего у вас есть лишь небольшое число сотрудников в одном регионе, которые управляют содержимым и маркетинговыми кампаниями. При масштабировании монолитных решений весь код развертывается многократно.

В дополнение к «масштабирования-все» проблему, изменения в одном компоненте требуют полного повторного тестирования всего приложения, а также полного повторного развертывания всех экземпляров.

Применить Монолитный подход широкое распространение и многими организациями при разработке с помощью этого метода архитектуры. Многие наслаждайтесь хорошо результатов, тогда как другие возникнуть ограничения. Многие строились в этой модели, так как средства и инфраструктура были слишком сложно создать SOA, и они не видят необходимость, пока его размер увеличивается.

С точки зрения инфраструктуры каждый сервер может выполнять множество приложений в том же узле и применять допустимое соотношение эффективности вашего использования ресурсов, как показано на рисунке 4-2.

![Один узел может выполняться несколько приложений в отдельных контейнерах.](./media/image2.png)

**Рис. 4-2.** На узел под управлением нескольких приложений или контейнеров

Наконец с точки зрения доступности монолитного приложения должны быть развернуты в целом; Это означает, что в случае, если необходимо *остановить и запустить*, все функциональные возможности, а также все пользователи будут применяться во время развертывания окна. В некоторых случаях использование Azure и контейнеров можно свести к минимуму эти ситуации и снижают вероятность простоя для вашего приложения, как показано на рисунке 4-3.

Монолитные приложения в Azure можно развернуть с помощью выделенных виртуальных машин для каждого экземпляра. С помощью [масштабируемых наборов виртуальных Машин Azure](https://docs.microsoft.com/azure/virtual-machine-scale-sets/), вы можете легко масштабировать виртуальные машины.

Можно также использовать [службы приложений](https://azure.microsoft.com/services/app-service/) выполнять монолитные приложения и легко масштабировать экземпляры без необходимости управлять виртуальными машинами. Службы приложений Azure могут выполнять отдельные экземпляры контейнеров Docker, а также, упрощая развертывание.

Можно развернуть несколько виртуальных машин в качестве узлов Docker и запустить любое количество контейнеров на каждой виртуальной Машине. Затем с помощью Azure Load Balancer, как показано на рисунке 4-3, можно управлять масштабированием.

![Такие приложения масштабируются может быть горизонтальным масштабированием на разных узлах, где каждый из них запуск приложения в контейнеры.](./media/image3.png)

**Рис. 4-3**. Несколько узлов масштабирование одного приложения приложений или контейнеров Docker

Вы можете управлять развертыванием самих узлов с помощью традиционных методов развертывания.

Контейнеры Docker можно управлять из командной строки с помощью команд, таких как `docker run` и `docker-compose up`, и можно также автоматизировать его в конвейерах непрерывной поставки (CD) и развертывания узлов Docker из служб Azure DevOps, например.

## <a name="monolithic-application-deployed-as-a-container"></a>Развертывание монолитного приложения в контейнере

Существуют преимущества использования контейнеров для управления развертываниями монолитных. Масштабировать экземпляры контейнера гораздо быстрее и проще, чем развертывать дополнительные виртуальные машины.

Развертывание обновлений в виде образов Docker выполняется гораздо быстрее и эффективнее с точки зрения использования сети. Контейнеры docker обычно запускаются за считанные секунды, что позволяет ускорить выпуск. Закрытие контейнера Docker так же просто, что и вызов `docker stop` команды, обычно Завершение менее чем за секунду.

Поскольку контейнеры неизменны по своей природе, по своей природе, не придется беспокоиться о поврежденных виртуальных машинах, так как забыли скрипт обновления учесть определенную конфигурацию или файл на диске.

Несмотря на то, что монолитные приложения могут использовать преимущества Docker, мы прервать только советами преимущества по. Увеличить преимущества управлении контейнерами открываются благодаря развертыванию с оркестраторами контейнеров, которые управляют различными экземплярами и жизненным циклом каждого экземпляра контейнера. Когда вы разбиваете монолитное приложение на подсистемы, которые затем можно масштабировать, разрабатывать и развертывать по отдельности, вы переходите на уровень микрослужб.

Дополнительные сведения о том, как «lift- and -shift монолитных приложений с контейнерами и как можно модернизировать приложения, можно прочитать это дополнительные руководство Microsoft [модернизация существующих приложений .NET с помощью облака Azure и контейнеров Windows ](../../modernize-with-azure-and-containers/index.md), который вы также можете скачать как PDF-ФАЙЛ из <https://aka.ms/LiftAndShiftWithContainersEbook>.

## <a name="publish-a-single-docker-container-app-to-azure-app-service"></a>Публикация одного приложения контейнера Docker в службе приложений Azure

Либо так, как вы хотите получить быстрой проверки контейнер, развернутый в Azure или приложение просто, одном контейнере приложения службы приложений Azure предоставляет отличный способ предоставления масштабируемых служб в одном контейнере.

С помощью службы приложений Azure интуитивно понятный и можно начать и выполняется быстро, поскольку он предоставляет отличный Git интеграции кода, сборки в Microsoft Visual Studio, а также развернуть его непосредственно в Azure. Но, традиционно (с помощью нет Docker), при необходимости другие возможности, платформы или зависимости, которые не поддерживаются в службах приложений, необходимые для дождитесь пока не команда Azure обновит эти зависимости в службе приложений или переключается на другие службы, например Service Fabric, облачных служб или даже просто виртуальные машины, для которых есть дополнительные элемента управления и можно установить необходимый компонент или платформу для вашего приложения.

Теперь, как показано на рисунке 4-4 при использовании Visual Studio 2017, поддержка контейнеров в службе приложений Azure дает возможность включать угодно в вашей среде приложений. Если вы добавили зависимость в приложение, так как он выполняется в контейнере, вы получаете возможность, в том числе эти зависимости в образ Dockerfile или Docker.

![Представление Visual Studio мастер должен опубликовать службу приложений Azure, выделение селектор для реестра контейнеров.](./media/image4.png)

**Рис. 4-4**. Публикация контейнера в службе приложений Azure из приложений Visual Studio/контейнеры

Рис. 4-4 также показано, что поток публикации отправляет образ через реестр контейнеров, который может быть реестр контейнеров Azure (реестр практически к вашим развертываниям в Azure и защищенных с помощью групп Azure Active Directory и учетных записей) или другой реестр Docker как и реестры Docker Hub или локально.

>[!div class="step-by-step"]
>[Назад](common-container-design-principles.md)
>[Вперед](state-and-data-in-docker-applications.md)
