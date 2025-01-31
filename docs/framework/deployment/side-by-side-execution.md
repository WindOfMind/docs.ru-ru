---
title: Параллельное выполнение в .NET Framework
ms.date: 03/30/2017
helpviewer_keywords:
- side-by-side execution
ms.assetid: 649f1342-766b-49e6-a90d-5b019a751e11
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7c500b9343bdfa3481e8e5d9b938ebec8a323bdb
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64641040"
---
# <a name="side-by-side-execution-in-the-net-framework"></a>Параллельное выполнение в .NET Framework
Параллельное выполнение представляет собой возможность запускать несколько версий приложения или компонента с одного и того же компьютера. В одно и то же время на одном компьютере можно запускать несколько версий среды CLR, а также несколько версий приложений и компонентов, использующих одну из версий среды выполнения.  
  
 На следующем рисунке показаны несколько приложений, которые используют две разные версии среды выполнения на одном компьютере. Приложения A, B и C используют среду выполнения версии 1.0, а приложение D использует версию 1.1.  
  
 ![Параллельное выполнение разных версий среды выполнения,](./media/side-by-side-execution/side-by-side-runtime-execution.gif)  
  
 .NET Framework состоит из среды CLR и набора сборок, содержащих типы API. Версии среды выполнения и сборок платформы .NET Framework устанавливаются раздельно. Например, версия среды выполнения 4.0 на самом деле является версией 4.0.319, в то время как версия 1.0 сборок платформы .NET Framework — версией 1.0.3300.0.  
  
 На следующем рисунке показаны несколько приложений, которые используют две разных версии компонента на одном компьютере. Приложения A и B используют компонент версии 1.0, а приложение C использует версию 2.0 того же компонента.  
  
 ![Схема, показывающая параллельное выполнение компонента.](./media/side-by-side-execution/side-by-side-component-execution.gif)  
  
 Параллельное выполнение позволяет более строго контролировать, к каким версиям компонента привязывается приложение и какую версию среды выполнения оно использует.  
  
## <a name="benefits-of-side-by-side-execution"></a>Преимущества параллельного выполнения  
 До появления Microsoft Windows XP и платформы .NET Framework возникали конфликты библиотек DLL, поскольку приложения были не в состоянии различить несовместимые между собой версии одного и того же кода. Сведения о типах, содержавшиеся в библиотеках DLL, были ограничены именем файла. Приложение не могло различить, были ли типы в библиотеке DLL теми же, что применялись в приложении. В результате новая версия компонента могла перезаписать старую и привести к сбою в работе приложений.  
  
 Следующие возможности параллельного выполнения и платформы .NET Framework исключают конфликты библиотек DLL:  
  
- Сборки со строгими именами.  
  
     Параллельное выполнение использует сборки со строгими именами, чтобы привязать сведения о типе к определенной версии сборки. Это исключает возможность того, что приложение или компонент будут привязаны к неправильной версии сборки. Сборки со строгими именами также позволяют нескольким версиям файла располагаться на одном компьютере и использоваться приложениями. Подробнее см. в статье [Сборки со строгими именами](../../../docs/framework/app-domains/strong-named-assemblies.md).  
  
- Хранилище, следящее за версией кода.  
  
     Платформа .NET Framework предоставляет хранилище, следящее за версией кода, в глобальном кэше сборок. Глобальный кэш сборок — это кэш, в котором хранится используемый всеми приложениями на компьютере код. Подобный кэш есть на всех компьютерах, где установлена платформа .NET Framework. Он хранит сборки на основании версии, языка и региональных параметров и сведений об издателе, а также поддерживает одновременное хранение разных версий одного и того же компонента или приложения. Дополнительные сведения см. в разделе [Глобальный кэш сборок](../../../docs/framework/app-domains/gac.md).  
  
- Изоляция.  
  
     С помощью платформы .NET Framework можно создавать приложения и компоненты, которые работают изолированно. Изоляция является неотъемлемой частью параллельного выполнения. Изоляция предполагает сбор сведений о задействованных ресурсах и безопасное совместное использование ресурсов несколькими версиями приложения или компонента. Изоляция также предполагает сохранение файла с указанием версии. Дополнительные сведения об изоляции см. в разделе [Рекомендации по созданию компонентов для параллельного выполнения](../../../docs/framework/deployment/guidelines-for-creating-components-for-side-by-side-execution.md).  
  
## <a name="version-compatibility"></a>Совместимость версий  
 Версии платформы .NET Framework 1.0 и 1.1 совместимы. Приложение, разработанное с помощью платформы .NET Framework версии 1.0, работает с версией 1.1, и наоборот. Однако следует отметить, что функции API, добавленные в платформу .NET Framework версии 1.1, не будут работать в платформе .NET Framework версии 1.0. Приложения, созданные с помощью версии 2.0, будут выполняться только в версии 2.0. Приложения версии 2.0 не будут выполняться в версии 1.1 или в более ранней версии.  
  
 В платформе .NET Framework версии рассматриваются как единые блоки, состоящие из среды выполнения и связанных с ней сборок платформы .NET Framework (концепция, называемая "унификацией сборок"). Можно перенаправлять привязку сборок, чтобы включить другие версии сборок платформы .NET Framework, но переопределение привязки по умолчанию рискованно и должно быть тщательно протестировано до развертывания.  
  
## <a name="locating-runtime-version-information"></a>Обнаружение сведений о версии среды выполнения  
 Сведения о том, в какой версии среды выполнения было скомпилировано приложение или компонент, а также о том, какие версии среды выполнения необходимы для запуска приложения, хранятся в двух местах. После компиляции приложения или компонента сведения о версии среды выполнения, использованной для этой компиляции, хранятся в управляемом исполняемом файле. Сведения о версиях среды выполнения, необходимых для приложения или компонента, хранятся в файле конфигурации приложения.  
  
### <a name="runtime-version-information-in-the-managed-executable"></a>Сведения о версии среды выполнения в управляемом исполняемом файле  
 Заголовок переносимого исполняемого (PE) файла каждого управляемого приложения и компонента содержит сведения о версии среды выполнения, в которой он был создан. Среда CLR использует эти сведения, чтобы определить наиболее вероятную версию среды выполнения, необходимую для запуска приложения.  
  
### <a name="runtime-version-information-in-the-application-configuration-file"></a>Сведения о версии среды выполнения в файле конфигурации приложения  
 Кроме сведений в заголовке PE-файла приложение можно развернуть с использованием файла конфигурации приложения, в котором содержатся сведения о версии среды выполнения. Файл конфигурации приложения — это XML-файл, который создается разработчиком приложения и поставляется вместе с приложением. [Элемент \<requiredRuntime>](../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md) [раздела \<startup>](../../../docs/framework/configure-apps/file-schema/startup/startup-element.md), если таковой присутствует в этом файле, указывает, какие версии среды выполнения и какие версии компонента поддерживает приложение. Его также можно использовать для тестирования совместимости приложения с разными версиями среды выполнения.  
  
 Неуправляемый код (включая приложения COM и COM+) может иметь файлы конфигурации приложения, используемые средой выполнения для взаимодействия с управляемым кодом. Файл конфигурации приложения влияет на любой управляемый код, активированный через COM. В файле можно указать, какие версии среды выполнения он поддерживает, а также какие сборки перенаправляет. По умолчанию приложения COM-взаимодействия, вызывающие управляемый код, используют последнюю версию среды выполнения, установленную на компьютере.  
  
 Подробнее о файлах конфигурации приложений см. в разделе [Настройка приложений](../../../docs/framework/configure-apps/index.md).  
  
## <a name="determining-which-version-of-the-runtime-to-load"></a>Определение загружаемой версии среды выполнения  
 Среда CLR использует следующие сведения, чтобы определить, какую версию среды выполнения необходимо загрузить для приложения:  
  
- доступные версии среды выполнения;  
  
- версии среды выполнения, поддерживаемые приложением.  
  
### <a name="supported-runtime-versions"></a>Поддерживаемые версии среды выполнения  
 Для определения версии среды выполнения, поддерживаемой приложением, среда выполнения использует файл конфигурации приложения и заголовок переносимого исполняемого (PE) файла. Если файл конфигурации приложения отсутствует, среда выполнения загружает версию, указанную в заголовке PE-файла приложения, при ее наличии.  
  
 Если файл конфигурации приложения имеется, среда выполнения определяет подходящую версию для загрузки с помощью описанной ниже процедуры.  
  
1. Среда выполнения проверяет элемент [\<supportedRuntime>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) в файле конфигурации приложения. Если в элементе **\<supportedRuntime>** указана одна поддерживаемая версия или несколько, среда выполнения загружает версию, указанную в первом элементе **\<supportedRuntime>**. Если эта версия недоступна, среда выполнения проверяет следующий элемент **\<supportedRuntime>** и предпринимает попытку загрузить указанную версию. Если эта версия среды выполнения недоступна, проверяются следующие элементы **\<supportedRuntime>**. Если ни одна из поддерживаемых версий среды выполнения недоступна, среде выполнения не удается загрузить версию, и она выводит соответствующее сообщение (см. шаг 3).  
  
2. Среда выполнения считывает заголовок PE-файла исполняемого файла приложения. Если версия среды выполнения, указанная в этом заголовке, доступна, среда выполнения загружает ее. Если указанная версия недоступна, среда выполнения ищет версию, которая определена Майкрософт как совместимая с указанной в заголовке PE-файла. Если эту версию найти не удается, процедура переходит к шагу 3.  
  
3. Среда выполнения выводит сообщение о том, что версия среды выполнения, поддерживаемая приложением, недоступна. Среда выполнения не загружается.  
  
    > [!NOTE]
    >  Вы можете отключить вывод сообщения, используя параметр NoGuiFromShim в разделе реестра HKLM\Software\Microsoft\\.NETFramework или переменную среды COMPLUS_NoGuiFromShim. Например, можно отключить сообщение для приложений, которые обычно не взаимодействуют с пользователем, таких как автоматически устанавливаемые компоненты или службы Windows. Если вывод сообщения отключен, среда выполнения записывает сообщение в журнал событий.  Чтобы отключить это сообщение для всех приложений на компьютере, присвойте параметру реестра NoGuiFromShim значение 1. Аналогично присвойте переменной среды COMPLUS_NoGuiFromShim значение 1, чтобы отключить сообщение для приложений, выполняющихся в контексте определенного пользователя.  
  
> [!NOTE]
>  После загрузки версии среды выполнения перенаправления привязки сборок могут указывать, что будет загружена другая версия отдельной сборки .NET Framework. Такие перенаправления привязки влияют только на конкретную перенаправляемую сборку.  
  
## <a name="partially-qualified-assembly-names-and-side-by-side-execution"></a>Частичные имена сборок и параллельное выполнение  
 Так как частичные ссылки на сборки потенциально являются источником проблем при параллельном выполнении, их следует применять только для привязки к сборкам в пределах каталога приложения. Использовать частичные ссылки на сборки в коде не рекомендуется.  
  
 Чтобы снизить возможную опасность от частичных ссылок на сборки, при их применении в коде можно использовать элемент [\<qualifyAssembly>](../../../docs/framework/configure-apps/file-schema/runtime/qualifyassembly-element.md) в файле конфигурации приложения и дать полные определения частичных ссылок на сборки. При использовании элемента **\<qualifyAssembly>** следует указывать только те поля, которые не указаны в частичной ссылке. Идентификатор сборки, указанный в атрибуте **fullName**, должен содержать все сведения, необходимые для задания полного имени сборки: имя, открытый ключ, язык и региональные параметры и версию сборки.  
  
 В примере ниже показана запись в файле конфигурации приложения для задания полного имени сборки `myAssembly`.  
  
```xml  
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">   
<qualifyAssembly partialName="myAssembly"   
fullName="myAssembly,  
      version=1.0.0.0,   
publicKeyToken=...,   
      culture=neutral"/>   
</assemblyBinding>   
```  
  
 Если оператор загрузки сборки ссылается на `myAssembly`, эти параметры файла конфигурации заставляют среду выполнения автоматически преобразовывать частичную ссылку на `myAssembly` в полную ссылку. Например, Assembly.Load("myAssembly") преобразуется в Assembly.Load("myAssembly, version=1.0.0.0, publicKeyToken=..., culture=neutral").  
  
> [!NOTE]
>  С помощью метода **LoadWithPartialName** можно обойти ограничение среды CLR, которое запрещает загрузку сборок с частичными ссылками из глобального кэша сборок. Этот метод следует использовать только в сценариях удаленного взаимодействия, так как он может привести к проблемам, связанным с параллельным выполнением.  
  
## <a name="related-topics"></a>См. также  
  
|Заголовок|Описание|  
|-----------|-----------------|  
|[Практическое руководство. Включение и отключение автоматического перенаправления привязки](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)|Описание способов привязки приложения к определенной версии сборки.|  
|[Настройка перенаправления привязки сборок](../../../docs/framework/deployment/configuring-assembly-binding-redirection.md)|Рассматривается перенаправление ссылок на привязки сборок на определенную версию сборок .NET Framework.|  
|[Внутрипроцессное параллельное выполнение](../../../docs/framework/deployment/in-process-side-by-side-execution.md)|Описание порядка использования внутрипроцессной параллельной активации хост-приложения среды выполнения для запуска нескольких версий среды CLR в одном процессе.|  
|[Сборки в среде CLR](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)|Общие сведения о сборках.|  
|[Домены приложений](../../../docs/framework/app-domains/application-domains.md)|Общие сведения о доменах приложений.|  
  
## <a name="reference"></a>Ссылка  
 [\<Поддерживаемый элемент среды выполнения](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)
