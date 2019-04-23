---
title: элемент < Crst_DisableSpinWait >
ms.date: 04/18/2019
f1_keywords:
- Crst_DisableSpinWait
helpviewer_keywords:
- Crst_DisableSpinWait element
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6cde26250db0b3d11c51a18b7ebd378953ae0958
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59981258"
---
# <a name="crstdisablespinwait-element"></a><span data-ttu-id="30f6f-102">\<Crst_DisableSpinWait > элемент</span><span class="sxs-lookup"><span data-stu-id="30f6f-102">\<Crst_DisableSpinWait> element</span></span>

<span data-ttu-id="30f6f-103">Указывает, следует ли отключить спин ожидает критический раздел, если состязаний.</span><span class="sxs-lookup"><span data-stu-id="30f6f-103">Specifies whether to disable spin-waiting for a critical section when contended.</span></span> \ 
  
 <span data-ttu-id="30f6f-104">\<configuration></span><span class="sxs-lookup"><span data-stu-id="30f6f-104">\<configuration></span></span>  
<span data-ttu-id="30f6f-105">\<Среда выполнения ></span><span class="sxs-lookup"><span data-stu-id="30f6f-105">\<runtime></span></span>  
<span data-ttu-id="30f6f-106">\<Crst_DisableSpinWait ></span><span class="sxs-lookup"><span data-stu-id="30f6f-106">\<Crst_DisableSpinWait></span></span>  
  
## <a name="syntax"></a><span data-ttu-id="30f6f-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="30f6f-107">Syntax</span></span>  
  
```xml  
<Crst_DisableSpinWait enabled="true | false"/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="30f6f-108">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="30f6f-108">Attributes and Elements</span></span>

<span data-ttu-id="30f6f-109">В следующих разделах описаны атрибуты, дочерние и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="30f6f-109">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="30f6f-110">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="30f6f-110">Attributes</span></span>  
  
|<span data-ttu-id="30f6f-111">Атрибут</span><span class="sxs-lookup"><span data-stu-id="30f6f-111">Attribute</span></span>|<span data-ttu-id="30f6f-112">Описание</span><span class="sxs-lookup"><span data-stu-id="30f6f-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="30f6f-113">**включен**</span><span class="sxs-lookup"><span data-stu-id="30f6f-113">**enabled**</span></span>|<span data-ttu-id="30f6f-114">Указывает, включена ли спин ожидание критических секций, когда они являются состязаний.</span><span class="sxs-lookup"><span data-stu-id="30f6f-114">Specifies whether spin-waiting for critical sections is enabled when they are contended.</span></span>|  
  
## <a name="enabled-attribute"></a><span data-ttu-id="30f6f-115">Атрибут enabled</span><span class="sxs-lookup"><span data-stu-id="30f6f-115">enabled Attribute</span></span>  
  
|<span data-ttu-id="30f6f-116">Значение</span><span class="sxs-lookup"><span data-stu-id="30f6f-116">Value</span></span>|<span data-ttu-id="30f6f-117">Описание</span><span class="sxs-lookup"><span data-stu-id="30f6f-117">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="30f6f-118">1</span><span class="sxs-lookup"><span data-stu-id="30f6f-118">1</span></span>|<span data-ttu-id="30f6f-119">Ожидание управления "Счетчик" включен.</span><span class="sxs-lookup"><span data-stu-id="30f6f-119">Spin-waiting is enabled.</span></span>|  
|<span data-ttu-id="30f6f-120">0</span><span class="sxs-lookup"><span data-stu-id="30f6f-120">0</span></span>|<span data-ttu-id="30f6f-121">Ожидание управления "Счетчик" отключено.</span><span class="sxs-lookup"><span data-stu-id="30f6f-121">Spin-waiting is disabled.</span></span> <span data-ttu-id="30f6f-122">Это значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="30f6f-122">This is the default</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="30f6f-123">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="30f6f-123">Child Elements</span></span>  
 <span data-ttu-id="30f6f-124">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="30f6f-124">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="30f6f-125">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="30f6f-125">Parent Elements</span></span>  
  
|<span data-ttu-id="30f6f-126">Элемент</span><span class="sxs-lookup"><span data-stu-id="30f6f-126">Element</span></span>|<span data-ttu-id="30f6f-127">Описание</span><span class="sxs-lookup"><span data-stu-id="30f6f-127">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="30f6f-128">Корневой элемент в любом файле конфигурации, используемом средой CLR и приложениями .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="30f6f-128">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`runtime`|<span data-ttu-id="30f6f-129">Содержит сведения о различных параметров конфигурации среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="30f6f-129">Contains information about various runtime configuration settings.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="30f6f-130">Пример</span><span class="sxs-lookup"><span data-stu-id="30f6f-130">Example</span></span>  

<span data-ttu-id="30f6f-131">В следующем примере отключается спин ожидания в критических разделах при состязаний.</span><span class="sxs-lookup"><span data-stu-id="30f6f-131">The following example disables spin-waiting in critical sections when contended.</span></span>  
  
```xml  
<configuration>  
   <runtime>  
      <Crst_DisableSpinWait enabled="1"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="30f6f-132">См. также</span><span class="sxs-lookup"><span data-stu-id="30f6f-132">See also</span></span>

- [<span data-ttu-id="30f6f-133">Схема параметров среды выполнения</span><span class="sxs-lookup"><span data-stu-id="30f6f-133">Runtime Settings Schema</span></span>](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [<span data-ttu-id="30f6f-134">Схема файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="30f6f-134">Configuration File Schema</span></span>](../../../../../docs/framework/configure-apps/file-schema/index.md)