---
title: Компиляция проекта, использующего взаимодействие
ms.date: 03/30/2017
helpviewer_keywords:
- interoperation with unmanaged code, compiling
- COM interop, compiling
- exposing COM components to .NET Framework
- compiling interop projects
- interoperation with unmanaged code, exposing COM components
- COM interop, exposing COM components
ms.assetid: 6fcf6588-5e25-41af-b4ae-780974f2c3df
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bf0244060d3c5dfa39c220fc2d699a5f2f1fef9e
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65636186"
---
# <a name="compiling-an-interop-project"></a>Компиляция проекта, использующего взаимодействие

Проекты, использующие COM-взаимодействие, в которых содержатся ссылки на одну или несколько сборок с импортированными типами COM, компилируются так же, как и любые другие управляемые проекты. Ссылки на сборки взаимодействия можно использовать как в среде разработки (например, Visual Studio), так при использовании компилятора командной строки. В обоих случаях для корректной компиляции сборка взаимодействия должна находиться в одном каталоге с другими файлами проекта.

 Ссылки на сборки взаимодействия можно использовать двумя способами:

- С помощью встроенных типов взаимодействия. Начиная с [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] и Visual Studio 2010 можно дать указание компилятору внедрять сведения о типах из сборки взаимодействия в исполняемый файл. Это рекомендуемая методика.

- Развертывание сборок взаимодействия. Можно создать стандартную ссылку на сборку взаимодействия. В этом случае сборки взаимодействия должны быть развернуты вместе с приложением.

 Различия между этими двумя способами более подробно описываются в разделе [Использование COM-типов в управляемом коде](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100)).

 Внедрение типов взаимодействия в Visual Studio демонстрируется в разделах [Пошаговое руководство. Внедрение типов из управляемых сборок в Visual Studio (C#)](/docs/csharp/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md) и [Пошаговое руководство. Внедрение типов из управляемых сборок в Visual Studio (Visual Basic)](/docs/visual-basic/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-vs.md).

 Чтобы задать ссылку на сборку взаимодействия в компиляторе командной строки и внедрить сведения о типах в исполняемые файлы, задайте параметр компилятора [/link (параметры компилятора C#)](../../csharp/language-reference/compiler-options/link-compiler-option.md) или [/link (Visual Basic)](../../visual-basic/reference/command-line-compiler/link.md) и укажите имя сборки взаимодействия.

> [!NOTE]
> Приложения Visual C++ не поддерживают внедрение сведений о типах, однако могут взаимодействовать с приложениями и надстройками, в которых такая возможность присутствует.

 Чтобы скомпилировать приложение, которое включает основную сборку взаимодействия при развертывании, задайте параметр компилятора **/reference** и укажите имя сборки взаимодействия.

## <a name="see-also"></a>См. также

- [Предоставление COM-компонентов платформе .NET Framework](exposing-com-components.md)
- [Независимость от языка и независимые от языка компоненты](../../standard/language-independence-and-language-independent-components.md)
- [Using COM Types in Managed Code](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100)) (Использование COM-типов в управляемом коде)
- [Пошаговое руководство: Внедрение типов из управляемых сборок в Visual Studio в C#](/docs/csharp/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md)
- [Пошаговое руководство: Внедрение типов из управляемых сборок в Visual Studio (Visual Basic)](/docs/visual-basic/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-vs.md)
- [Импорт библиотеки типов в виде сборки](importing-a-type-library-as-an-assembly.md)
