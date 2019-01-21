---
title: Метод IXCLRDataProcess::GetAppDomainByUniqueId
ms.date: 01/16/2019
api.name:
- IXCLRDataProcess::GetAppDomainByUniqueId Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataProcess::GetAppDomainByUniqueId Method
helpviewer.keywords:
- IXCLRDataProcess::GetAppDomainByUniqueId Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 83e7d4e1a4ff3c2e6f573d6c097c7cdb9c5f3c54
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2019
ms.locfileid: "54416697"
---
# <a name="ixclrdataprocessgetappdomainbyuniqueid-method"></a><span data-ttu-id="244bb-102">Метод IXCLRDataProcess::GetAppDomainByUniqueId</span><span class="sxs-lookup"><span data-stu-id="244bb-102">IXCLRDataProcess::GetAppDomainByUniqueId Method</span></span>

<span data-ttu-id="244bb-103">Получает `AppDomain` в процесс, основанный на свой уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="244bb-103">Gets an `AppDomain` in a process based on its unique identifier.</span></span>

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a><span data-ttu-id="244bb-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="244bb-104">Syntax</span></span>
```
HRESULT GetAppDomainByUniqueID(
    [in] ULONG64               id,
    [out] IXCLRDataAppDomain **appDomain
);
```

### <a name="parameters"></a><span data-ttu-id="244bb-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="244bb-105">Parameters</span></span>
<span data-ttu-id="244bb-106">`id` [in] Уникальный идентификатор домена приложения</span><span class="sxs-lookup"><span data-stu-id="244bb-106">`id` [in] The unique identifier of the AppDomain</span></span>

<span data-ttu-id="244bb-107">`appDomain` [out] Домен приложения</span><span class="sxs-lookup"><span data-stu-id="244bb-107">`appDomain` [out] The AppDomain</span></span>

## <a name="remarks"></a><span data-ttu-id="244bb-108">Примечания</span><span class="sxs-lookup"><span data-stu-id="244bb-108">Remarks</span></span>

<span data-ttu-id="244bb-109">Указанный метод является частью `IXCLRDataProcess` интерфейса и соответствует 20 слот в таблице виртуального метода.</span><span class="sxs-lookup"><span data-stu-id="244bb-109">The provided method is part of the `IXCLRDataProcess` interface and corresponds to the 20th slot of the virtual method table.</span></span> <span data-ttu-id="244bb-110">`IXCLRDataAppDomain*` Возвращается используется для взаимодействия с другими интерфейсами API.</span><span class="sxs-lookup"><span data-stu-id="244bb-110">The `IXCLRDataAppDomain*` returned is used for interaction with other APIs.</span></span>

## <a name="requirements"></a><span data-ttu-id="244bb-111">Требования</span><span class="sxs-lookup"><span data-stu-id="244bb-111">Requirements</span></span>
<span data-ttu-id="244bb-112">**Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="244bb-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
<span data-ttu-id="244bb-113">**Заголовок.** Нет</span><span class="sxs-lookup"><span data-stu-id="244bb-113">**Header:** None</span></span>  
<span data-ttu-id="244bb-114">**Библиотека:** Нет</span><span class="sxs-lookup"><span data-stu-id="244bb-114">**Library:** None</span></span>  
<span data-ttu-id="244bb-115">**Версии платформы .NET Framework:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span><span class="sxs-lookup"><span data-stu-id="244bb-115">**.NET Framework Versions:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span></span>  

## <a name="see-also"></a><span data-ttu-id="244bb-116">См. также</span><span class="sxs-lookup"><span data-stu-id="244bb-116">See Also</span></span>
- [<span data-ttu-id="244bb-117">Отладка</span><span class="sxs-lookup"><span data-stu-id="244bb-117">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [<span data-ttu-id="244bb-118">Интерфейс IXCLRDataProcess</span><span class="sxs-lookup"><span data-stu-id="244bb-118">IXCLRDataProcess Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/ixclrdataprocess-interface.md)