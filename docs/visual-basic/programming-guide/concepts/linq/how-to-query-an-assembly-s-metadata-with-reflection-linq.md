---
title: Практическое руководство. Запрос к метаданным сборки при помощи отражения (LINQ) (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 53caa336-ab83-4181-b0f6-5c87c5f9e4ee
ms.openlocfilehash: cea1469e6f0acc9c958be9247d7d3d750d881afe
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65586344"
---
# <a name="how-to-query-an-assemblys-metadata-with-reflection-linq-visual-basic"></a>Практическое руководство. Запрос к метаданным сборки при помощи отражения (LINQ) (Visual Basic)
В следующем примере показано использование LINQ с отражением для извлечения определенных метаданных о методах, соответствующих условиям поиска. В этом примере запрос будет искать имена всех методов в сборке, которые возвращают перечислимые типы, такие как массивы.  
  
## <a name="example"></a>Пример  
  
```vb  
Imports System.Reflection  
Imports System.IO  
Imports System.Linq  
Module Module1  
  
    Sub Main()  
        Dim asmbly As Assembly =   
            Assembly.Load("System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken= b77a5c561934e089")  
  
        Dim pubTypesQuery = From type In asmbly.GetTypes()   
                            Where type.IsPublic   
                            From method In type.GetMethods()   
                            Where method.ReturnType.IsArray = True   
                            Let name = method.ToString()   
                            Let typeName = type.ToString()   
                            Group name By typeName Into methodNames = Group  
  
        Console.WriteLine("Getting ready to iterate")  
        For Each item In pubTypesQuery  
            Console.WriteLine(item.methodNames)  
  
            For Each type In item.methodNames  
                Console.WriteLine(" " & type)  
            Next  
        Next  
        Console.ReadKey()  
    End Sub  
  
End Module  
```  
  
 В примере используется метод <xref:System.Reflection.Assembly.GetTypes%2A> для возвращения массива типов в указанной сборке. [Предложение Where](../../../../visual-basic/language-reference/queries/where-clause.md) применяется фильтр, чтобы возвращались только открытые типы. Для каждого открытого типа создается вложенный запрос с использованием массива <xref:System.Reflection.MethodInfo>, который возвращается из вызова <xref:System.Type.GetMethods%2A>. Эти результаты фильтруются для возвращения только тех методов, возвращаемый тип которых является массивом или типом, который реализует <xref:System.Collections.Generic.IEnumerable%601>. Наконец, эти результаты группируются с помощью имени типа в качестве ключа.  
  
## <a name="compiling-the-code"></a>Компиляция кода  
Создайте проект консольного приложения VB.NET, с помощью `Imports` оператор для пространства имен System.Linq.
  
## <a name="see-also"></a>См. также

- [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
