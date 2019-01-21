---
title: Метод DacpGetModuleAddress::Request
ms.date: 01/16/2019
api.name:
- DacpGetModuleAddress::Request Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpGetModuleAddress::Request Method
helpviewer.keywords:
- DacpGetModuleAddress::Request Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 86a51605ad8ea8b394c5b8a5961f32e96baf9e58
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2019
ms.locfileid: "54416617"
---
# <a name="dacpgetmoduleaddressrequest-method"></a><span data-ttu-id="93b1e-102">Метод DacpGetModuleAddress::Request</span><span class="sxs-lookup"><span data-stu-id="93b1e-102">DacpGetModuleAddress::Request Method</span></span>

<span data-ttu-id="93b1e-103">Выполняет запрос для заполнения структуры из структуры данной среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="93b1e-103">Performs a request to populate the structure from the given runtime structure.</span></span>

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a><span data-ttu-id="93b1e-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="93b1e-104">Syntax</span></span>

```
HRESULT Request(
    [in] IXCLRDataModule* pDataModule
);
```

### <a name="parameters"></a><span data-ttu-id="93b1e-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="93b1e-105">Parameters</span></span>

<span data-ttu-id="93b1e-106">`pDataModule` [in] Указатель на модуль начальное значение данных.</span><span class="sxs-lookup"><span data-stu-id="93b1e-106">`pDataModule` [in] A pointer to the seed data module.</span></span>

## <a name="remarks"></a><span data-ttu-id="93b1e-107">Примечания</span><span class="sxs-lookup"><span data-stu-id="93b1e-107">Remarks</span></span>

<span data-ttu-id="93b1e-108">Эта структура находится внутри среды выполнения и не предоставляется через любой заголовков или библиотек.</span><span class="sxs-lookup"><span data-stu-id="93b1e-108">This structure lives inside the runtime and is not exposed through any headers or library files.</span></span> <span data-ttu-id="93b1e-109">Чтобы использовать его, проще всего имитируют реализации:</span><span class="sxs-lookup"><span data-stu-id="93b1e-109">To use it, the easiest way is to mimic the implementation:</span></span>

- <span data-ttu-id="93b1e-110">Возвращает значение, полученное от вызова `Request` метод `IXCLRDataModule*` параметра со следующими параметрами: `((uint32) 0xf0000000, 0, 0, (uint32) sizeof(*this), (uint8*) this)`</span><span class="sxs-lookup"><span data-stu-id="93b1e-110">Return the value obtained from calling the `Request` method on the `IXCLRDataModule*` parameter with the following parameters: `((uint32) 0xf0000000, 0, 0, (uint32) sizeof(*this), (uint8*) this)`</span></span>


## <a name="requirements"></a><span data-ttu-id="93b1e-111">Требования</span><span class="sxs-lookup"><span data-stu-id="93b1e-111">Requirements</span></span>

<span data-ttu-id="93b1e-112">**Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="93b1e-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
<span data-ttu-id="93b1e-113">**Заголовок.** Нет</span><span class="sxs-lookup"><span data-stu-id="93b1e-113">**Header:** None</span></span>     
<span data-ttu-id="93b1e-114">**Библиотека:** Нет</span><span class="sxs-lookup"><span data-stu-id="93b1e-114">**Library:** None</span></span>  
<span data-ttu-id="93b1e-115">**Версии платформы .NET Framework:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span><span class="sxs-lookup"><span data-stu-id="93b1e-115">**.NET Framework Versions:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span></span>  

## <a name="see-also"></a><span data-ttu-id="93b1e-116">См. также</span><span class="sxs-lookup"><span data-stu-id="93b1e-116">See Also</span></span>

- [<span data-ttu-id="93b1e-117">Отладка</span><span class="sxs-lookup"><span data-stu-id="93b1e-117">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [<span data-ttu-id="93b1e-118">Интерфейс DacpGetModuleAddress</span><span class="sxs-lookup"><span data-stu-id="93b1e-118">DacpGetModuleAddress Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/dacpgetmoduleaddress-structure.md)