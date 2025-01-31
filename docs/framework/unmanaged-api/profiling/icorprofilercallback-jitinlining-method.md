---
title: Метод ICorProfilerCallback::JITInlining
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITInlining
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITInlining
helpviewer_keywords:
- JITInlining method [.NET Framework profiling]
- ICorProfilerCallback::JITInlining method [.NET Framework profiling]
ms.assetid: c2f45801-dd38-4b78-b6b7-64397dc73f83
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 60183291fda551e328ee1def03c02240314a71e4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61598237"
---
# <a name="icorprofilercallbackjitinlining-method"></a>Метод ICorProfilerCallback::JITInlining
Уведомляет профилировщик, что компилятор just-in-time (JIT) сейчас вставить функцию в одну строку другой функции.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT JITInlining(  
    [in]  FunctionID callerId,  
    [in]  FunctionID calleeId,  
    [out] BOOL      *pfShouldInline);  
```  
  
## <a name="parameters"></a>Параметры  
 `callerId`  
 [in] Идентификатор функции, в которую `calleeId` функция будет вставлен.  
  
 `calleeId`  
 [in] Идентификатор функции для вставки.  
  
 `pfShouldInline`  
 [out] `true` для допускает вставку синхронизации; в противном случае `false`.  
  
## <a name="remarks"></a>Примечания  
 Профилировщик можно задать `pfShouldInline` для `false` во избежание `calleeId` функции из, вставляемого в `callerId` функции. Кроме того, профилировщик глобально можно отключить встроенные вставки с помощью значение COR_PRF_DISABLE_INLINING [COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md) перечисления.  
  
 Встроенные функции не вызывают событий входа или выхода. Таким образом, профилировщик должен установить `pfShouldInline` для `false` чтобы обеспечить точность графа. Установка `pfShouldInline` для `false` повлияет на производительность, так как встроенный вставки повышается скорость и сокращает количество отдельных событий JIT-компиляции для вставляемого метода.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
