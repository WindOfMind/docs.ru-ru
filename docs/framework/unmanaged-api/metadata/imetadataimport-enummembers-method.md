---
title: Метод IMetaDataImport::EnumMembers
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMembers
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMembers
helpviewer_keywords:
- IMetaDataImport::EnumMembers method [.NET Framework metadata]
- EnumMembers method [.NET Framework metadata]
ms.assetid: 3fb8e178-342b-4c89-9bcf-f7f834e6cb77
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e8d871f2ecbd96d5bda781b2ae11b94efd409442
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62049925"
---
# <a name="imetadataimportenummembers-method"></a>Метод IMetaDataImport::EnumMembers
Перечисляет токены MemberDef, представляющие члены указанного типа.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT EnumMembers (   
   [in, out]  HCORENUM    *phEnum,   
   [in]  mdTypeDef   cl,   
   [out] mdToken     rMembers[],   
   [in]  ULONG       cMax,   
   [out] ULONG       *pcTokens  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `phEnum`  
 [in, out] Указатель на перечислитель.  
  
 `cl`  
 [in] Токен TypeDef, представляющий тип, члены которого необходимо перечислить.  
  
 `rMembers`  
 [out] Массив, используемый для хранения токены MemberDef.  
  
 `cMax`  
 [in] Максимальный размер массива `rMembers`.  
  
 `pcTokens`  
 [out] Фактическое количество возвращаемых в токены MemberDef `rMembers`.  
  
## <a name="return-value"></a>Возвращаемое значение  
  
|HRESULT|Описание|  
|-------------|-----------------|  
|`S_OK`|`EnumMembers` успешно возвращен.|  
|`S_FALSE`|Существуют маркеры MemberDef для перечисления отсутствуют. В этом случае `pcTokens` равно нулю.|  
  
## <a name="remarks"></a>Примечания  
 При перечислении коллекций членов для класса, `EnumMembers` возвращает только члены (поля и методы, но **не** свойств или событий) определенные непосредственно в классе. Он не возвращает элементы, класс наследуется, даже если этот класс предоставляет реализацию для этих унаследованных членов. Чтобы перечислить унаследованные члены, вызывающий объект явным образом необходимо пройти по цепочке наследования. Обратите внимание, что правила для цепи наследования может меняться в зависимости от языка или компилятора, выдавшего исходные метаданные.
 
 Свойства и события не перечисляет `EnumMembers`. Чтобы перечислить их, используйте [EnumProperties](imetadataimport-enumproperties-method.md) или [EnumEvents](imetadataimport-enumevents-method.md).
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** Cor.h  
  
 **Библиотека:** Включена как ресурс в MsCorEE.dll  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [Интерфейс IMetaDataImport2](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
