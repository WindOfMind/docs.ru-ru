---
title: объявляемая моделью функция
ms.date: 03/30/2017
ms.assetid: aba87f13-5685-4f6b-ad14-918e8a7d5c2a
ms.openlocfilehash: a0bea36693122c77d9c1abdf4484ee8e68627a0c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645875"
---
# <a name="model-declared-function"></a>объявляемая моделью функция
Объект *объявляемая моделью функция* является функцией, которая объявлена в концептуальной модели, но не определен в концептуальной модели. Функция может быть определена в среде размещения или хранения. Например, объявляемая моделью функция может быть сопоставлена функции, определенной в базе данных, экспонируя таким образом функцию в концептуальной модели на стороне сервера.  
  
 Объявление объявляемой моделью функции содержит следующую информацию.  
  
- Имя функции. (Обязательный атрибут).  
  
- Тип возвращаемого значения. (Необязательный параметр).  
  
    > [!NOTE]
    >  Если возвращаемое значение не задано, возвращаемого значения не будет.  
  
- Сведения о параметрах, включая имя и тип параметров. (Необязательный параметр).  
  
## <a name="example"></a>Пример  
 [ADO.NET Entity Framework](./ef/index.md) использует доменный язык (DSL), называемый языком определения концептуальной схемы ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) для определения концептуальных моделей. В языке CSDL, одна реализация объявляемой моделью функции является импорт функции (с помощью [элемент FunctionImport](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#functionimport-element-csdl)). Далее на языке CSDL определяется контейнер сущностей с определением импорта функции. Обратите внимание, что возвращаемый тип для функции отсутствует, поскольку возвращаемый тип не задан.  
  
 [!code-xml[EDM_Example_Model#FunctionImport](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#functionimport)]  
  
## <a name="see-also"></a>См. также

- [Основные понятия модели EDM](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)
- [Сущностная модель данных](../../../../docs/framework/data/adonet/entity-data-model.md)
