---
title: Перечисление CorDebugExceptionCallbackType
ms.date: 03/30/2017
api_name:
- CorDebugExceptionCallbackType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugExceptionCallbackType
helpviewer_keywords:
- CorDebugExceptionCallbackType enumeration [.NET Framework debugging]
ms.assetid: 4d946ad4-3c19-42cb-bec9-8633325ba769
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 91b09be04499396a2229962fd592f29cb8bc8d04
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61609040"
---
# <a name="cordebugexceptioncallbacktype-enumeration"></a>Перечисление CorDebugExceptionCallbackType
Указывает тип обратного вызова, состоящее из [ICorDebugManagedCallback2::Exception](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-exception-method.md) событий.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
typedef enum CorDebugExceptionCallbackType {  
    DEBUG_EXCEPTION_FIRST_CHANCE         = 1,  
    DEBUG_EXCEPTION_USER_FIRST_CHANCE    = 2,  
    DEBUG_EXCEPTION_CATCH_HANDLER_FOUND  = 3,  
    DEBUG_EXCEPTION_UNHANDLED            = 4  
} CorDebugExceptionCallbackType;  
```  
  
## <a name="members"></a>Участники  
  
|Член|Описание|  
|------------|-----------------|  
|`DEBUG_EXCEPTION_FIRST_CHANCE`|Возникло исключение.|  
|`DEBUG_EXCEPTION_USER_FIRST_CHANCE`|В процессе очистки исключения ввода пользовательского кода.|  
|`DEBUG_EXCEPTION_CATCH_HANDLER_FOUND`|В процессе очистки исключения найден `catch` блока в пользовательском коде.|  
|`DEBUG_EXCEPTION_UNHANDLED`|Исключение не обработано.|  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Перечисления отладки](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
