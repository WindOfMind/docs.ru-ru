---
title: Перечисление CorCallingConvention
ms.date: 03/30/2017
api_name:
- CorCallingConvention
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorCallingConvention
helpviewer_keywords:
- CorCallingConvention enumeration [.NET Framework metadata]
ms.assetid: 69156fbf-7219-43bf-b4b8-b13f1a2fcb86
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 44a4b5903cec2249eb1e176381fe3d8e600dd5e6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62046115"
---
# <a name="corcallingconvention-enumeration"></a>Перечисление CorCallingConvention
Содержит значения, описывающие типы соглашений о вызовах, выполняемых в управляемом коде.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
typedef enum CorCallingConvention  
{  
    IMAGE_CEE_CS_CALLCONV_DEFAULT       = 0x0,  
  
    IMAGE_CEE_CS_CALLCONV_VARARG        = 0x5,  
    IMAGE_CEE_CS_CALLCONV_FIELD         = 0x6,  
    IMAGE_CEE_CS_CALLCONV_LOCAL_SIG     = 0x7,  
    IMAGE_CEE_CS_CALLCONV_PROPERTY      = 0x8,  
    IMAGE_CEE_CS_CALLCONV_UNMGD         = 0x9,  
    IMAGE_CEE_CS_CALLCONV_GENERICINST   = 0xa,  
    IMAGE_CEE_CS_CALLCONV_NATIVEVARARG  = 0xb,  
    IMAGE_CEE_CS_CALLCONV_MAX           = 0xc,  
  
    IMAGE_CEE_CS_CALLCONV_MASK          = 0x0f,  
    IMAGE_CEE_CS_CALLCONV_HASTHIS       = 0x20,  
    IMAGE_CEE_CS_CALLCONV_EXPLICITTHIS  = 0x40,  
    IMAGE_CEE_CS_CALLCONV_GENERIC       = 0x10  
  
} CorCallingConvention;  
```  
  
## <a name="members"></a>Участники  
  
|Член|Описание|  
|------------|-----------------|  
|`IMAGE_CEE_CS_CALLCONV_DEFAULT`|Указывает соглашение о вызовах по умолчанию.|  
|`IMAGE_CEE_CS_CALLCONV_VARARG`|Указывает, что этот метод принимает переменное количество параметров.|  
|`IMAGE_CEE_CS_CALLCONV_FIELD`|Указывает, что вызов к полю.|  
|`IMAGE_CEE_CS_CALLCONV_LOCAL_SIG`|Указывает, что вызов предназначен для локального метода.|  
|`IMAGE_CEE_CS_CALLCONV_PROPERTY`|Указывает, что вызов к свойству.|  
|`IMAGE_CEE_CS_CALLCONV_UNMGD`|Указывает, что вызов является неуправляемым.|  
|`IMAGE_CEE_CS_CALLCONV_GENERICINST`|Показывает создание экземпляра универсального метода.|  
|`IMAGE_CEE_CS_CALLCONV_NATIVEVARARG`|Указывает метод, который принимает переменное количество параметров вызова PInvoke 64-разрядной.|  
|`IMAGE_CEE_CS_CALLCONV_MAX`|Описывает недопустимое 4-разрядное значение.|  
|`IMAGE_CEE_CS_CALLCONV_MASK`|Указывает, что соглашение о вызове описывается четырьмя младшими битами.|  
|`IMAGE_CEE_CS_CALLCONV_HASTHIS`|Указывает, что старшие биты описывают `this` параметра.|  
|`IMAGE_CEE_CS_CALLCONV_EXPLICITTHIS`|Указывает, что `this` параметра явно описан в сигнатуре.|  
|`IMAGE_CEE_CS_CALLCONV_GENERIC`|Указывает сигнатуру универсального метода с явной количество аргументов типа. Это предшествует обычное число параметров.|  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorHdr.h  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Перечисления метаданных](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
