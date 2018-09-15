---
title: Практическое руководство. Безопасное приведение с помощью сопоставления шаблонов и операторы is и as
description: Узнайте, как использовать сопоставление шаблонов для безопасного приведения переменных в другой тип. Вы можете использовать сопоставление шаблонов, а также операторы as и is для безопасного преобразования типов.
ms.date: 09/05/2018
helpviewer_keywords:
- cast operators [C#], as and is operators
- as operator [C#]
- is operator [C#]
ms.openlocfilehash: 88289099864293b3b19da62155d58ba4797948bd
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2018
ms.locfileid: "44216181"
---
# <a name="how-to-safely-cast-by-using-pattern-matching-is-and-as-operators"></a><span data-ttu-id="253af-104">Практическое руководство. Безопасное приведение с помощью сопоставления шаблонов и операторы is и as</span><span class="sxs-lookup"><span data-stu-id="253af-104">How to: safely cast by using pattern matching is and as operators</span></span>

<span data-ttu-id="253af-105">В связи с полиморфизмом объектов переменная типа базового класса может содержать производный [тип](../programming-guide/types/index.md).</span><span class="sxs-lookup"><span data-stu-id="253af-105">Because objects are polymorphic, it's possible for a variable of a base class type to hold a derived [type](../programming-guide/types/index.md).</span></span> <span data-ttu-id="253af-106">Для доступа к членам экземпляра производного типа необходимо [привести](../programming-guide/types/casting-and-type-conversions.md) значение обратно к производному типу.</span><span class="sxs-lookup"><span data-stu-id="253af-106">To access the derived type's instance members, it's necessary to [cast](../programming-guide/types/casting-and-type-conversions.md) the value back to the derived type.</span></span> <span data-ttu-id="253af-107">Однако приведение создает риск возникновения исключения <xref:System.InvalidCastException>.</span><span class="sxs-lookup"><span data-stu-id="253af-107">However, a cast creates the risk of throwing an <xref:System.InvalidCastException>.</span></span> <span data-ttu-id="253af-108">C# предоставляет операторы [сопоставления шаблонов](../pattern-matching.md), которые выполняют приведение условно только в случае успеха.</span><span class="sxs-lookup"><span data-stu-id="253af-108">C# provides [pattern matching](../pattern-matching.md) statements that perform a cast conditionally only when it will succeed.</span></span> <span data-ttu-id="253af-109">C# также предоставляет операторы [is](../language-reference/keywords/is.md) и [as](../language-reference/keywords/as.md) для проверки определенного типа значения.</span><span class="sxs-lookup"><span data-stu-id="253af-109">C# also provides the [is](../language-reference/keywords/is.md) and [as](../language-reference/keywords/as.md) operators to test if a value is of a certain type.</span></span>

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

<span data-ttu-id="253af-110">В следующем коде показан оператор сопоставления шаблонов `is`.</span><span class="sxs-lookup"><span data-stu-id="253af-110">The following code demonstrates the pattern matching `is` statement.</span></span> <span data-ttu-id="253af-111">Он содержит методы, которые проверяют аргумент метода, чтобы определить, является ли он одним из возможных наборов производных типов.</span><span class="sxs-lookup"><span data-stu-id="253af-111">It contains methods that test a method argument to determine if it is one of a possible set of derived types:</span></span>

[!code-csharp-interactive[Pattern matching is statement](../../../samples/snippets/csharp/how-to/safelycast/patternmatching/Program.cs#PatternMatchingIs)]

<span data-ttu-id="253af-112">В предыдущем примере показано несколько возможностей синтаксиса сопоставления шаблонов.</span><span class="sxs-lookup"><span data-stu-id="253af-112">The preceding sample demonstrates a few features of pattern matching syntax.</span></span> <span data-ttu-id="253af-113">Операторы `if (a is Mammal m)` и `if (o is Mammal m)` объединяют проверку с назначением инициализации.</span><span class="sxs-lookup"><span data-stu-id="253af-113">The `if (a is Mammal m)` and `if (o is Mammal m)` statements combine the test with an initialization assignment.</span></span> <span data-ttu-id="253af-114">Назначение происходит, только если проверка пройдет успешно.</span><span class="sxs-lookup"><span data-stu-id="253af-114">TThe assignment occurs only when the test succeeds.</span></span> <span data-ttu-id="253af-115">Переменная `m` действует только во внедренном операторе `if`, где она назначена.</span><span class="sxs-lookup"><span data-stu-id="253af-115">The variable `m` is only in scope in the embedded `if` statement where it has been assigned.</span></span> <span data-ttu-id="253af-116">Вы не сможете получить доступ к `m` позже в этом же методе.</span><span class="sxs-lookup"><span data-stu-id="253af-116">You cannot access `m` later in the same method.</span></span> <span data-ttu-id="253af-117">Попробуйте сделать это в интерактивном окне.</span><span class="sxs-lookup"><span data-stu-id="253af-117">Try it in the interactive window.</span></span>

<span data-ttu-id="253af-118">Вы можете использовать тот же синтаксис для проверки наличия значения у [типа, допускающего значение null](../programming-guide/nullable-types/index.md), как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="253af-118">You can also use the same syntax for testing if a [nullable type](../programming-guide/nullable-types/index.md) has a value, as shown in the following sample code:</span></span>

[!code-csharp-interactive[Pattern matching with nullable types](../../../samples/snippets/csharp/how-to/safelycast/nullablepatternmatching/Program.cs#PatternMatchingNullable)]

<span data-ttu-id="253af-119">В предыдущем примере показаны другие возможности сопоставления шаблонов для использования с преобразованиями.</span><span class="sxs-lookup"><span data-stu-id="253af-119">The preceding sample demonstrates other features of pattern matching to use with conversions.</span></span> <span data-ttu-id="253af-120">Вы можете проверить переменную для шаблона со значением NULL путем проверки конкретно значения `null`.</span><span class="sxs-lookup"><span data-stu-id="253af-120">You can test a variable for the null pattern by checking specifically for the `null` value.</span></span> <span data-ttu-id="253af-121">Если значение переменной в среде выполнения равно `null`, оператор `is`, проверяющий тип, всегда возвращает `false`.</span><span class="sxs-lookup"><span data-stu-id="253af-121">When the runtime value of the variable is `null`, an `is` statement checking for a type always returns `false`.</span></span> <span data-ttu-id="253af-122">Оператор сопоставления шаблонов `is` не принимает тип, допускающий значение NULL, например `int?` или `Nullable<int>`, но вы можете выполнить проверку для любого другого типа значения.</span><span class="sxs-lookup"><span data-stu-id="253af-122">The pattern matching `is` statement doesn't allow a nullable value type, such as `int?` or `Nullable<int>`, but you can test for any other value type.</span></span>

<span data-ttu-id="253af-123">Предыдущий пример также показывает, как использовать выражение сопоставления шаблонов `is` в операторе `switch`, где переменная может принимать один из множества различных типов.</span><span class="sxs-lookup"><span data-stu-id="253af-123">The preceding sample also shows how you use the pattern matching `is` expression in a `switch` statement where the variable may be one of many different types.</span></span>

<span data-ttu-id="253af-124">Если вы хотите проверить, принадлежит ли переменная определенному типу, но не хотите назначать новую переменную, используйте операторы `is` и `as` для ссылочных типов и типов, допускающих значение NULL.</span><span class="sxs-lookup"><span data-stu-id="253af-124">If you want to test if a variable is a given type, but not assign it to a new variable, you can use the `is` and `as` operators for reference types and nullable types.</span></span> <span data-ttu-id="253af-125">Ниже показано, как использовать операторы `is` и `as`, которые были частью языка C# до того, как было введено сопоставление шаблонов для проверки принадлежности переменной к определенному типу.</span><span class="sxs-lookup"><span data-stu-id="253af-125">The following code shows how to use the `is` and `as` statements that were part of the C# language before pattern matching was introduced to test if a variable is of a given type:</span></span>

[!code-csharp-interactive[testing variable types with the is and as statements](../../../samples/snippets/csharp/how-to/safelycast/asandis/Program.cs#IsAndAs)]

<span data-ttu-id="253af-126">Как видно при сравнении этого кода с кодом сопоставления шаблонов, синтаксис сопоставления шаблонов предоставляет более надежные функции, поскольку сочетает в себе проверку и назначение в одном операторе.</span><span class="sxs-lookup"><span data-stu-id="253af-126">As you can see by comparing this code with the pattern matching code, the pattern matching syntax provides more robust features by combining the test and the assignment in a single statement.</span></span> <span data-ttu-id="253af-127">Используйте синтаксис сопоставления шаблонов во всех подходящих случаях.</span><span class="sxs-lookup"><span data-stu-id="253af-127">Use the pattern matching syntax whenever possible.</span></span>

<span data-ttu-id="253af-128">Вы можете оценить эти примеры, просмотрев код в нашем [репозитории GitHub](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/safelycast).</span><span class="sxs-lookup"><span data-stu-id="253af-128">You can try these samples by looking at the code in our [GitHub repository](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/safelycast).</span></span> <span data-ttu-id="253af-129">Или можете загрузить образцы [в ZIP-файле](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/safelycast.zip).</span><span class="sxs-lookup"><span data-stu-id="253af-129">Or you can download the samples [as a zip file](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/safelycast.zip).</span></span>