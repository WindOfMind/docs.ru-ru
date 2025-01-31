---
title: Оптимизация производительности с помощью механизмов уведомления об однофазной фиксации и повышаемого однофазного присоединения
ms.date: 03/30/2017
ms.assetid: 57beaf1a-fb4d-441a-ab1d-bc0c14ce7899
ms.openlocfilehash: 73340f5f65de1d743e046cf669258ab5f6c66298
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61793631"
---
# <a name="optimization-using-single-phase-commit-and-promotable-single-phase-notification"></a>Оптимизация производительности с помощью механизмов уведомления об однофазной фиксации и повышаемого однофазного присоединения

В этом разделе описываются предоставляемые инфраструктурой <xref:System.Transactions> механизмы для оптимизации производительности.

## <a name="promotable-single-phase-enlistment"></a>Повышаемое однофазное зачисление

Инфраструктура <xref:System.Transactions> управляет транзакцией в пределах одного домена приложения, включающего по крайней мере один устойчивый ресурс или несколько неустойчивых ресурсов. Поскольку инфраструктура <xref:System.Transactions> использует только вызовы внутри домена приложения, она обеспечивает оптимальную производительность.

Однако при предоставлении транзакции другому объекту в другом домене приложения (а также в другом процессе или компьютере) на том же самом компьютере или зачислении другого диспетчера устойчивых ресурсов инфраструктура <xref:System.Transactions> автоматически передает управление транзакцией координатору MSDTC. Производительность транзакции, управляемой координатором MSDTC, является более низкой по сравнению с производительностью транзакции, управляемой инфраструктурой <xref:System.Transactions>.

Для оптимизации производительности в инфраструктуре <xref:System.Transactions> предусмотрен механизм повышаемого однофазного зачисления (PSPE), который позволяет одному удаленному устойчивому ресурсу, расположенному в другом домене приложения, процессе или компьютере, участвовать в транзакции <xref:System.Transactions>, не вызывая ее повышения до транзакции MSDTC. Этот диспетчер ресурсов может "владеть" и управлять транзакцией, которая затем при необходимости может быть повышена до распределенной транзакции (или транзакции MSDTC). Это уменьшает вероятность использования координатора MSDTC.

У данного диспетчера ресурсов, как правило, существуют собственные внутренние нераспределенные транзакции, и он должен поддерживать преобразование этих транзакций в распределенные транзакции во время выполнения. Например, в качестве такого диспетчера ресурсов может выступать SQL Server 2005. В этом случае инфраструктура <xref:System.Transactions> принимает пассивное участие в управлении транзакцией, выполняя только мониторинг транзакции с целью определения необходимости ее передачи на следующий уровень иерархии. Для поддержки взаимодействия между инфраструктурой <xref:System.Transactions> и диспетчером ресурсов последнему необходимо реализовать интерфейс <xref:System.Transactions.IPromotableSinglePhaseNotification>.

Метод <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> используется для зачисления одного устойчивого ресурса, который затем может быть повышен. Этот метод обеспечивает возможность повышения зачисления по мере необходимости. В случае успешного зачисления диспетчер ресурсов создает собственную внутреннюю транзакцию и связывает ее с транзакцией <xref:System.Transactions>. Если PSPE-зачисление выполнить не удается, диспетчеру ресурсов следует выполнить зачисление с помощью метода <xref:System.Transactions.Transaction.EnlistDurable%2A>. PSPE-зачисление может оказаться невозможным, если транзакция уже является распределенной или другой диспетчер ресурсов уже выполнил PSPE-зачисление.

После зачисления клиентские вызовы, предназначенные для фиксации или прерывания транзакции <xref:System.Transactions>, преобразуются в вызовы диспетчера ресурсов посредством вызова метода <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> или <xref:System.Transactions.IPromotableSinglePhaseNotification.Rollback%2A> соответственно.

Если передача транзакции <xref:System.Transactions> на следующий уровень иерархии не требуется, после фиксации транзакции диспетчер ресурсов получает уведомление <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A>. После этого он может зафиксировать изначально созданную внутреннюю транзакцию.

Если транзакцию <xref:System.Transactions> требуется передать на следующий уровень иерархии (например, для поддержки нескольких диспетчеров ресурсов), инфраструктура <xref:System.Transactions> информирует об этом диспетчер ресурсов путем вызова метода <xref:System.Transactions.ITransactionPromoter.Promote%2A> интерфейса <xref:System.Transactions.ITransactionPromoter>, от которого наследуется интерфейс <xref:System.Transactions.IPromotableSinglePhaseNotification>. После этого диспетчер ресурсов осуществляет внутреннее преобразование локальной транзакции (для которой не требуется ведение журнала) в объект транзакции, способный участвовать в транзакции DTC, и связывает этот объект с уже выполненными действиями. В случае запроса фиксации транзакции диспетчер транзакций отправляет уведомление <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> диспетчеру ресурсов, который фиксирует распределенную транзакцию, созданную во время передачи на следующий уровень иерархии.

> [!NOTE]
> **TransactionCommitted** трассировок (создаваемых при вызове фиксации над повышенной транзакцией) содержится идентификатор действия транзакции DTC.

Дополнительные сведения о расширении управления, см. в разделе [эскалации управления транзакцией](../../../../docs/framework/data/transactions/transaction-management-escalation.md).

## <a name="transaction-management-escalation-scenario"></a>Сценарий передачи управления транзакцией на следующий уровень иерархии

На примере приведенного ниже сценария показано, как повысить транзакцию до распределенной транзакции, используя пространство имен <xref:System.Data> как "посредника" для диспетчера ресурсов. В этом сценарии предполагается, что соединение <xref:System.Data>, CN1, с базой данных уже участвует в транзакции и приложению необходимо включить в транзакцию второе соединение <xref:System.Data>, CN2. Транзакция должна быть повышена до транзакции DTC, чтобы стать распределенной транзакцией с двухфазной фиксацией.

В этом сценарии:

1. Соединение CN1 вызывает метод <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> для зачисления в транзакцию. Поскольку транзакция по-прежнему является локальной и других повышаемых зачислений нет, вызов метода <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> является успешным.

2. Вызов метода <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> вторым соединением, CN2, заканчивается неудачей, поскольку в транзакции уже используется другое повышаемое зачисление. Поэтому соединению CN2 необходимо получить транзакцию DTC, чтобы выполнить передачу в SQL. Для этого соединение использует один из методов, предоставляемых классом <xref:System.Transactions.TransactionInterop>, чтобы представить транзакцию в формате, подходящем для передачи в SQL.

3. <xref:System.Transactions> вызывает метод <xref:System.Transactions.ITransactionPromoter.Promote%2A> интерфейса <xref:System.Transactions.ITransactionPromoter>, реализуемого соединением CN1.

4. На этом этапе соединение CN1 передает транзакцию на следующий уровень иерархии с помощью механизма, характерного для SQL 2005 и <xref:System.Data>.

5. Значение, возвращаемое методом <xref:System.Transactions.ITransactionPromoter.Promote%2A>, представляет массив байтов, который содержит токен распространения для транзакции. <xref:System.Transactions> использует этот маркер распространения для создания транзакции DTC, его можно включить в локальной транзакции.

6. На этом этапе соединение CN2 может использовать данные, полученные в результате вызова одного из методов объектом <xref:System.Transactions.TransactionInterop>, для передачи транзакции в SQL.

7. Теперь оба соединения зачислены в распределенную транзакцию DTC.

## <a name="single-phase-commit-optimization"></a>Оптимизация однофазной фиксации

Протокол однофазной фиксации наиболее эффективен при использовании во время выполнения, поскольку все изменения производятся без какой-либо явной координации. Чтобы использовать данную оптимизацию, необходимо реализовать диспетчер ресурсов с помощью интерфейса <xref:System.Transactions.ISinglePhaseNotification> и зачислить его в транзакцию с помощью метода <xref:System.Transactions.Transaction.EnlistDurable%2A> или <xref:System.Transactions.Transaction.EnlistVolatile%2A>. В частности *EnlistmentOptions* должно быть равно параметр <xref:System.Transactions.EnlistmentOptions.None> гарантирует, что будет выполнять однофазной фиксации.

Интерфейс <xref:System.Transactions.ISinglePhaseNotification> наследуется от интерфейса <xref:System.Transactions.IEnlistmentNotification>, поэтому если реализованный диспетчер ресурсов не подходит для однофазной фиксации, он, тем не менее, может получать уведомления о двухфазной фиксации. Если реализованный диспетчер ресурсов получает уведомление <xref:System.Transactions.ISinglePhaseNotification.SinglePhaseCommit%2A> от диспетчера транзакций, он должен попытаться выполнить действия, необходимые для фиксации транзакции, и сообщить диспетчеру транзакций о необходимости фиксации или отката транзакции путем вызова метода <xref:System.Transactions.SinglePhaseEnlistment.Committed%2A>, <xref:System.Transactions.SinglePhaseEnlistment.Aborted%2A> или <xref:System.Transactions.SinglePhaseEnlistment.InDoubt%2A> параметра <xref:System.Transactions.SinglePhaseEnlistment>. Ответ <xref:System.Transactions.Enlistment.Done%2A>, переданный зачисленному ресурсу на данном этапе, подразумевает семантику ReadOnly. Поэтому не следует передавать ответ <xref:System.Transactions.Enlistment.Done%2A> в дополнение к вызову любого из других методов.

Если имеется только один неустойчивый ресурс и не зачисление устойчивых ресурсов, неустойчивый ресурс получает уведомление о SPC. При возникновении любой зачислений неустойчивых ресурсов и только одно зачисление устойчивых ресурсов, зачисленные неустойчивые ресурсы получают 2PC. После этого зачисленный устойчивый ресурс получает уведомление об однофазной фиксации (SPC).

## <a name="see-also"></a>См. также

- [Зачисление ресурсов в транзакцию в качестве участников](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md)
- [Однофазная и многофазная фиксация транзакции](../../../../docs/framework/data/transactions/committing-a-transaction-in-single-phase-and-multi-phase.md)
