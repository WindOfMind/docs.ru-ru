---
title: Метод ICLRMetaHost::RequestRuntimeLoadedNotification
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.RequestRuntimeLoadedNotification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::RequestRuntimeLoadedNotification
helpviewer_keywords:
- RequestRuntimeLoadedNotification method [.NET Framework hosting]
- ICLRMetaHost::RequestRuntimeLoadedNotification method [.NET Framework hosting]
ms.assetid: 0d5ccc4d-0193-41f5-af54-45d7b70d5321
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 87afb19736a484d24bde56cc34854dcd26c6b53b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64755699"
---
# <a name="iclrmetahostrequestruntimeloadednotification-method"></a>Метод ICLRMetaHost::RequestRuntimeLoadedNotification
Предоставляет функцию обратного вызова, которая гарантированно вызывается при первой загрузке версия CLR (CLR), но еще не запущен. Этот метод заменяет [LockClrVersion](../../../../docs/framework/unmanaged-api/hosting/lockclrversion-function.md) функции.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT RequestRuntimeLoadedNotification (  
    [in] RuntimeLoadedCallbackFnPtr pCallbackFunction);  
```  
  
## <a name="parameters"></a>Параметры  
 `pCallbackFunction`  
 [in] Функция обратного вызова, который вызывается при загрузке новой среды выполнения.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Этот метод возвращает следующие конкретные результаты HRESULT, а также ошибки HRESULT, которые указывают на сбой метода.  
  
|HRESULT|Описание|  
|-------------|-----------------|  
|S_OK|Метод завершился успешно.|  
|E_POINTER|Параметр `pCallbackFunction` имеет значение null.|  
  
## <a name="remarks"></a>Примечания  
 Функция обратного вызова работает следующим образом:  
  
- Функция обратного вызова вызывается только в том случае, когда среда выполнения загружается в первый раз.  
  
- Функция обратного вызова не вызывается для реентерабельных загрузок ту же среду выполнения.  
  
- Для загрузки среды выполнения не допускающий повторные входы сериализуются вызовы функции обратного вызова.  
  
 Функция обратного вызова имеет следующий прототип:  
  
```  
typedef void (__stdcall *RuntimeLoadedCallbackFnPtr)(  
                     ICLRRuntimeInfo *pRuntimeInfo,  
                     CallbackThreadSetFnPtr pfnCallbackThreadSet,  
                     CallbackThreadUnsetFnPtr pfnCallbackThreadUnset);  
```  
  
 Прототипы функции обратного вызова, следующим образом:  
  
- `pfnCallbackThreadSet`:  
  
    ```  
    typedef HRESULT (__stdcall *CallbackThreadSetFnPtr)();  
    ```  
  
- `pfnCallbackThreadUnset`:  
  
    ```  
    typedef HRESULT (__stdcall *CallbackThreadUnsetFnPtr)();  
    ```  
  
 Если основное приложение намеревается загрузить или вызывать другой среды выполнения должен быть загружен в виде реентерабельным, `pfnCallbackThreadSet` и `pfnCallbackThreadUnset` параметры, предоставляемые в обратном вызове, необходимо использовать функцию следующим образом:  
  
- `pfnCallbackThreadSet` должен вызываться потоком, который может вызвать загрузку среды выполнения, до попытки такой загрузки.  
  
- `pfnCallbackThreadUnset` должен вызываться, когда поток больше не вызывает загрузку среды выполнения (и перед возвратом из начальной обратного вызова).  
  
- `pfnCallbackThreadSet` и `pfnCallbackThreadUnset` оба являются не допускающий повторные входы.  
  
> [!NOTE]
>  Ведущие приложения не должны вызывать `pfnCallbackThreadSet` и `pfnCallbackThreadUnset` выходит за рамки `pCallbackFunction` параметра.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** MetaHost.h  
  
 **Библиотека:** Включена как ресурс в MSCorEE.dll  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICLRMetaHost](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-interface.md)
- [Размещение](../../../../docs/framework/unmanaged-api/hosting/index.md)
