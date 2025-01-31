---
title: Защита распределенных приложений
ms.date: 03/30/2017
helpviewer_keywords:
- distributed application security [WCF]
- security [WCF], transfer
ms.assetid: 53928a10-e474-46d0-ab90-5f98f8d7b668
ms.openlocfilehash: 70ed0fe9191c18e88198871319b3c3ee3c0b4ab4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64626971"
---
# <a name="distributed-application-security"></a>Защита распределенных приложений
Безопасность Windows Communication Foundation (WCF) делится на три основные функциональные области: безопасность передачи, управление доступом и аудита. Безопасность передачи обеспечивает целостность, конфиденциальность и проверку подлинности. Безопасность передачи обеспечивается одним из следующих способов: безопасность транспорта, безопасность сообщений или `TransportWithMessageCredential`.  
  
 Общие сведения о защите сообщений WCF, см. в разделе [Общие сведения о безопасности](../../../../docs/framework/wcf/feature-details/security-overview.md). Дополнительные сведения о двух других способах безопасности WCF, см. в разделе [авторизации](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md) и [аудит](../../../../docs/framework/wcf/feature-details/auditing-security-events.md).  
  
## <a name="transfer-security-scenarios"></a>Сценарии безопасности передачи  
 Ниже приведены типичные сценарии, использующие безопасность передачи WCF:  
  
- Безопасная передача с помощью Windows. Клиентом WCF и службы развертываются в домене Windows (или в лесу Windows). Сообщения содержат личные данные, поэтому требуется взаимная проверка подлинности клиента и службы, целостность сообщений и конфиденциальность сообщений. Кроме того, требуется подтверждение проведения конкретной транзакции, например, получатель сообщения должен записать информацию о сигнатуры.  
  
- Безопасная передача с использованием `UserName` и HTTPS. WCF-клиент и служба должны быть разработаны для работы в Интернете. Подлинность учетных данных клиента проверяется по базе данных, содержащих пары "имя пользователя-пароль". Служба разворачивается по адресу HTTPS с использованием доверенного SSL-сертификата. Так как сообщения передаются по Интернету, необходима взаимная проверка подлинности клиента и службы, и во время передачи необходимо сохранение конфиденциальности и целостности сообщений.  
  
- Безопасная передача с помощью сертификатов. WCF-клиент и служба должны быть разработаны для работы через общедоступный Интернет. Как клиент, так и служба имеют сертификаты, которые можно использовать для обеспечения безопасности сообщений. Клиент и служба используют Интернет для взаимодействия друг с другом и для выполнения ценных транзакций, требующих целостности и конфиденциальности сообщений, а также взаимной проверки подлинности.  
  
## <a name="integrity-confidentiality-and-authentication"></a>Целостность, конфиденциальность и проверка подлинности  
 Эти функции (целостность, конфиденциальность и проверка подлинности) совместно называются безопасностью передачи. Безопасность передачи обеспечивает функции, позволяющие устранить угрозы для распределенных приложений. В приведенной ниже таблице кратко описаны три функции, составляющие безопасность передачи.  
  
|Функция|Описание|  
|--------------|-----------------|  
|Целостность|*Целостность* это гарантия того, что данные являются полные и точные, особенно после передачи из одной точки в другую и возможно, считывания несколькими агентами. Целостность, необходимая для предотвращения подделки данных, обычно обеспечивается цифровой подписью сообщения.|  
|Конфиденциальность|*Конфиденциальность* является гарантией того, что сообщение не было прочитано кем-либо, кроме предполагаемого читателя. Например, при передаче по Интернету необходимо сохранить в секрете номер кредитной карты. Конфиденциальность часто обеспечивается путем шифрования данных с использованием схемы "открытый ключ/закрытый ключ".|  
|Проверка подлинности|*Проверка подлинности* — это проверка заявленной идентификации. Например, при использовании банковского счета абсолютно необходимо, чтобы снятие средств могло быть выполнено только действительным владельцем счета. Проверка подлинности может обеспечиваться различными средствами. Одним из обычных способов является система пользователь/пароль. Вторым способом является использование сертификата X.509, предоставляемого третьей стороной.|  
  
## <a name="security-modes"></a>Режимы безопасности  
 WCF предусмотрены несколько режимов безопасности передачи, которые описаны в следующей таблице.  
  
|Mode|Описание|  
|----------|-----------------|  
|Нет|Безопасность на уровне транспорта или на уровне сообщений не обеспечивается. Используйте этот режим, ни один из предопределенных привязок по умолчанию, за исключением [ \<basicHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) элемент или, при использовании кода, <xref:System.ServiceModel.BasicHttpBinding> класса.|  
|Transport|Для обеспечения целостности, конфиденциальности и взаимной проверки подлинности используется безопасный транспорт, такой как HTTPS.|  
|Сообщение|Для обеспечения целостности, конфиденциальности и для взаимной проверки подлинности используется безопасность SOAP-сообщений. Защита SOAP-сообщений обеспечивается в соответствии со стандартами WS-Security.|  
|Смешанный режим|Целостность, конфиденциальность и проверка подлинности сервера обеспечиваются с помощью средств безопасности транспорта. Для проверки подлинности клиента используются средства безопасности сообщений (WS-Security и другие стандарты).<br /><br /> (В перечислении этому режиму соответствует значение `TransportWithMessageCredential`.)|  
|Оба|Защита и проверка подлинности выполняется на обоих уровнях. Этот режим доступен только в [ \<netMsmqBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md) элемент.|  
  
## <a name="credentials-and-transfer-security"></a>Учетные данные и безопасность передачи  
 Объект *учетных данных* — это данные, предоставляемые для подтверждения заявленной идентификации или возможностей. При предоставлении учетных данных требуется предоставить как сами данные, так и доказательство обладания ими. WCF поддерживает различные типы учетных данных на уровнях безопасности транспорта и сообщений. Можно указать тип учетных данных для привязки WCF.  
  
 Во многих странах или регионах примером учетных данных могут служить водительские права. Водительские права содержат данные о личности и возможностях их обладателя. Они содержат доказательство владения в виде фотографии владельца. Водительские права выданы доверенной организацией, обычно государственным органом. Водительские права ламинированы и могут содержать голограмму, подтверждающую, что права не изменены или подделаны.  
  
 Например, рассмотрим два типа учетных данных, поддерживаемые в WCF: имя пользователя и сертификат (X.509) учетные данные.  
  
 В учетных данных с именем пользователя имя пользователя представляет заявленную идентификацию, а пароль является доказательством прав обладания. Центром авторизации в данном случае является система, проверяющая имя пользователя и пароль.  
  
 В учетных данных с сертификатом имя субъекта, альтернативное имя субъекта или определенные поля сертификата могут использоваться для представления заявленной идентификации и/или возможностей. Обладание данными, приведенными в учетных данных, доказывается с помощью соответствующего закрытого ключа, использованного для создания сигнатуры.  
  
 Дополнительные сведения о программировании безопасность передачи, и указания учетных данных, см. в разделе [привязки и безопасность](../../../../docs/framework/wcf/feature-details/bindings-and-security.md) и [поведения безопасности](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md).  
  
### <a name="transport-client-credential-types"></a>Типы учетных данных клиента с безопасностью транспорта  
 В следующей таблице приведены возможные значения, применимые при создании приложения, использующего безопасность транспорта. Эти значения можно использовать либо в коде, либо в параметрах привязки.  
  
|Параметр|Описание|  
|-------------|-----------------|  
|Нет|Указывает, что клиенту не требуется предоставлять учетные данные. Это означает, что клиент является анонимным.|  
|Basic|Задает обычную проверку подлинности.  Дополнительные сведения см. в документе RFC2617, "[проверки подлинности HTTP: Основные и дайджест-проверка подлинности](https://go.microsoft.com/fwlink/?LinkId=88313).»|  
|Digest|Задает дайджест-проверку подлинности.  Дополнительные сведения см. в документе RFC2617, "[проверки подлинности HTTP: Основные и дайджест-проверка подлинности](https://go.microsoft.com/fwlink/?LinkId=88313).»|  
|Ntlm|Задает проверку подлинности Windows с использованием согласования SSPI с домене Windows.<br /><br /> При согласовании SSPI выбирается либо протокол Kerberos, либо протокол NT LanMan (NTLM).|  
|Windows|Задает проверку подлинности Windows с использованием согласования SSPI с домене Windows. В качестве службы проверки подлинности SSPI выбирает либо протокол Kerberos, либо протокол NT LanMan (NTLM).<br /><br /> Сначала SSPI пытается использовать протокол Kerberos; если это не удается, используется NTLM.|  
|Сертификат|Выполняет проверку подлинности клиента с использованием сертификата, обычно X.509.|  
  
### <a name="message-client-credential-types"></a>Типы учетных данных клиента при использовании безопасности сообщений  
 В следующей таблице приведены возможные значения, применимые при создании приложения, использующего безопасность сообщений. Эти значения можно использовать либо в коде, либо в параметрах привязки.  
  
|Параметр|Описание|  
|-------------|-----------------|  
|Нет|Позволяет службе взаимодействовать с анонимными клиентами.|  
|Windows|Позволяет проводить обмен сообщениями SOAP, если выполнена проверка подлинности с помощью учетных данных Windows. Для выбора службы проверки подлинности (протокол Kerberos или протокол NTLM) используется механизм согласования SSPI.|  
|Имя пользователя|Позволяет службе запрашивать проверку подлинности клиента на основе учетных данных типа «имя пользователя». Обратите внимание на то, что WCF не позволяет выполнять криптографические операции с именем пользователя, таких как создание сигнатуры или шифрование данных. Таким образом WCF обеспечивает безопасность транспорта при использовании учетных данных имени пользователя.|  
|Сертификат|Позволяет службе требовать проверки подлинности клиента с помощью сертификата.|  
|[!INCLUDE[infocard](../../../../includes/infocard-md.md)]|Позволяет службе требовать проверку подлинности клиента с помощью [!INCLUDE[infocard](../../../../includes/infocard-md.md)].|  
  
### <a name="programming-credentials"></a>Программирование учетных данных  
 Для каждого из типов учетных данных клиента модель программирования WCF позволяет задать значения учетных данных и учетных данных проверяющих элементов управления с помощью поведения службы и канала.  
  
 Безопасность WCF имеет два типа учетных данных: поведения службы и поведения канала. Поведения учетных данных в WCF задают фактические данные, а именно, учетные данные, используемые в соответствии с требованиями безопасности, выраженных через привязки. В WCF класс клиента является компонент времени выполнения, который выполняет преобразование между вызовом операции и сообщениями. Все клиенты наследуют от класса <xref:System.ServiceModel.ClientBase%601>. Свойство <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> базового класса позволяет задавать различные значения учетных данных клиента.  
  
 В WCF поведения службы являются атрибутом, примененным к классу, реализующему контракт службы (интерфейс) для программного управления службой. Класс <xref:System.ServiceModel.Description.ServiceCredentials> позволяет указать сертификаты для учетных данных службы и параметры проверки клиента для различных типов учетных данных клиента.  
  
### <a name="negotiation-model-for-message-security"></a>Модель согласования для безопасности сообщений  
 Режим безопасности сообщений позволяет реализовать безопасность передачи таким образом, чтобы учетные данные службы задавались в клиенте по внештатному каналу. Например, если используется сертификат, хранящийся в хранилище сертификатов Windows, необходимо использовать такое средство, как оснастка консоли управления (MMC).  
  
 Режим безопасности сообщений также позволяет обеспечивать безопасность передачи таким образом, чтобы учетные данные службы передавались клиенту в процессе начального согласования. Для разрешения согласования задайте для свойства <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> значение `true`.  
  
## <a name="see-also"></a>См. также

- [Общие сведения о создании конечных точек](../../../../docs/framework/wcf/endpoint-creation-overview.md)
- [Привязки, предоставляемые системой](../../../../docs/framework/wcf/system-provided-bindings.md)
- [Общие сведения о безопасности](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [Модель безопасности для Windows Server App Fabric](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
