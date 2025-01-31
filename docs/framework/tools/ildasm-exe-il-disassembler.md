---
title: Ildasm.exe (дизассемблер IL)
ms.date: 03/30/2017
helpviewer_keywords:
- PE files, MSIL Disassembler
- portable executable files, MSIL Disassembler
- Ildasm.exe
- MSIL Disassembler
- text files produced by MSIL Disassembler
- disassembling file for MSIL Assembler input
ms.assetid: db27f6b2-f1ec-499e-be3a-7eecf95ca42b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dfc55bcd97a6c1d68d4ce900b19ace7356d6ee92
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/30/2019
ms.locfileid: "66378572"
---
# <a name="ildasmexe-il-disassembler"></a>Ildasm.exe (дизассемблер IL)

Дизассемблер IL является сопутствующим инструментом ассемблера IL (*Ilasm.exe*). *Ildasm.exe* принимает переносимый исполняемый файл (PE-файл), содержащий код на промежуточном языке (IL), и создает на его основе текстовый файл, который может служить входным файлом для *Ilasm.exe*.

Эта программа автоматически устанавливается вместе с Visual Studio. Чтобы применить этот инструмент, воспользуйтесь командной строкой разработчика для Visual Studio (или командной строкой Visual Studio в Windows 7). Дополнительные сведения см. в разделе [Командные строки](../../../docs/framework/tools/developer-command-prompt-for-vs.md).

В командной строке введите следующее.

## <a name="syntax"></a>Синтаксис

```
ildasm [options] [PEfilename] [options]
```

## <a name="parameters"></a>Параметры

Перечисленные ниже параметры допустимы для файлов *EXE*, *DLL*, *OBJ*, *LIB* и *WINMD*.

| Параметр | Описание |
| ------ | ----------- |
|**/out=** `filename`|Создает выходной файл с заданным параметром `filename` вместо вывода результатов в графический пользовательский интерфейс.|
|**/rtf**|Выводит данные в формате RTF. Не может использоваться с параметром **/text**.|
|**/text**|Отображает результаты в окне консоли вместо вывода в графический пользовательский интерфейс или выходной файл.|
|**/html**|Выводит данные в формате HTML. Может использоваться только с параметром **/output**.|
|**/?**|Отображает синтаксис команд и параметров для средства.|

Перечисленные ниже дополнительные параметры допустимы для файлов *EXE*, *DLL* и *WINMD*.

| Параметр | Описание |
| ------ | ----------- |
|**/bytes**|Отображает фактические байты в шестнадцатеричном формате в виде комментариев к инструкциям.|
|**/caverbal**|Создает большие двоичные объекты настраиваемых атрибутов в текстовом виде. По умолчанию задана двоичная форма.|
|**/linenum**|Включает ссылки на строки исходного файла.|
|**/nobar**|Подавляет вывод всплывающего окна с индикатором хода выполнения дизассемблирования.|
|**/noca**|Подавляет вывод настраиваемых атрибутов.|
|**/project**|Отображает метаданные в представлении для управляемого кода, вместо того как их представляет [!INCLUDE[wrt](../../../includes/wrt-md.md)] в машинном коде. Если параметр `PEfilename` не является файлом метаданных Windows (*WINMD*-файлом), этот параметр не учитывается. См. раздел [Поддержка приложений для Магазина Windows и среды выполнения Windows в .NET Framework](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md).|
|**/pubonly**|Дизассемблирует только открытые типы и члены. Эквивалентен **/visibility:PUB**.|
|**/quoteallnames**|Заключает все имена в одинарные кавычки.|
|**/raweh**|Отображает предложения обработки исключений в исходном виде.|
|**/source**|Отображает строки исходного кода в виде комментариев.|
|**/tokens**|Отображает токены метаданных классов и членов.|
|**/visibility:** `vis`[+`vis`...]|Дизассемблирует только типы и члены с заданной областью видимости. Допустимы следующие значения аргумента `vis`:<br /><br /> **PUB** — открытый;<br /><br /> **PRI** — закрытый;<br /><br /> **FAM** — семейство;<br /><br /> **ASM** — сборка;<br /><br /> **FAA** — семейство и сборка;<br /><br /> **FOA** — семейство или сборка;<br /><br /> **PSC** — закрытая область.<br /><br /> Определения модификаторов видимости см. в описании <xref:System.Reflection.MethodAttributes> и <xref:System.Reflection.TypeAttributes>.|

Перечисленные ниже параметры допустимы для файлов *EXE*, *DLL* и *WINMD* только при выводе в файл или окно консоли.

| Параметр | Описание |
| ------ | ----------- |
|**/all**|Задает сочетание параметров **/header**, **/bytes**, **/stats**, **/classlist** и **/tokens**.|
|**/classlist**|Включает список классов, определенных в этом модуле.|
|**/forward**|Использует прямое объявление класса.|
|**/headers**|Включает сведения заголовка файла в выходные данные.|
|**/item:** `class`[ **::** `member`[`(sig`]]|В зависимости от заданных аргументов выполняет дизассемблирование:<br /><br /> дизассемблируется указанный `class`;<br />дизассемблируется указанный член `member` этого класса `class`;<br />дизассемблируется член `member` класса `class` с указанной сигнатурой `sig`. Формат `sig` выглядит следующим образом:<br />     [`instance`] `returnType`(`parameterType1`, `parameterType2`, …, `parameterTypeN`)<br />     **Примечание.** В .NET Framework версий 1.0 и 1.1 за атрибутом `sig` должна следовать закрывающая скобка: `(sig)`. В .NET Framework 2.0 и последующих версиях закрывающая скобка должна быть опущена: `(sig`.|
|**/noil**|Подавляет вывод кода сборки IL.|
|**/stats**|Включает статистику по образу.|
|**/typelist**|Создает полный список типов, чтобы сохранить упорядочение типов в круговом пути.|
|**/unicode**|Использует для выходных данных кодировку Юникод.|
|**/utf8**|Использует для выходных данных кодировку UTF-8. ANSI является значением по умолчанию.|

Перечисленные ниже параметры допустимы для файлов *EXE*, *DLL*, *OBJ*, *LIB* и *WINMD* только при выводе в файл или окно консоли.

| Параметр | Описание |
| ------ | ----------- |
|**/metadata**[=`specifier`]|Отображает метаданные, при этом параметр `specifier` может принимать следующие значения:<br /><br /> **MDHEADER** — показывать сведения и размеры заголовка метаданных;<br /><br /> **HEX** — показывать сведения в шестнадцатеричном и текстовом формате;<br /><br /> **CSV** — показывать количество записей и размеры кучи;<br /><br /> **UNREX** — показывать неразрешенные внешние элементы;<br /><br /> **SCHEMA** — показывать сведения о заголовке и схеме метаданных;<br /><br /> **RAW** — показывать необработанные таблицы метаданных;<br /><br /> **HEAPS** — показывать необработанные кучи;<br /><br /> **VALIDATE** — проверять согласованность метаданных.<br /><br /> Параметр **/metadata** можно задать несколько раз с различными значениями аргумента `specifier`.|

Перечисленные ниже параметры допустимы для *LIB*-файлов только при выводе в файл или окно консоли.

| Параметр | Описание |
| ------ | ----------- |
|**/objectfile**=`filename`|Вывод метаданных отдельного объектного файла из заданной библиотеки.|

> [!NOTE]
> Параметры программы *Ildasm.exe* не учитывают регистр и распознаются по первым трем буквам. Например, команда **/quo** эквивалентна команде **/quoteallnames**. Разделителем параметра и его аргумента может служить двоеточие (:) или знак равенства (=). Например, команда **/output:** *filename* эквивалентна команде **/output=** *filename*.

## <a name="remarks"></a>Примечания

Программа *Ildasm.exe* работает только с PE-файлами, расположенными на жестком диске. Программа не обрабатывает файлы, установленные в глобальном кэше сборок.

Текстовый файл, созданный программой *Ildasm.exe*, можно передавать в качестве входных данных в ассемблер IL (*Ilasm.exe*). Это полезно, к примеру, при компиляции кода на языке программирования, не поддерживающем все атрибуты метаданных среды выполнения. После компиляции кода и обработки результатов с помощью *Ildasm.exe* можно вручную добавить недостающие атрибуты в полученный текстовый файл IL. Чтобы создать окончательный исполняемый файл, следует обработать этот текстовый файл ассемблером IL.

> [!NOTE]
> На данный момент такая технология не применяется к PE-файлам, содержащим встроенный машинный код (например, к PE-файлам, созданным компилятором Microsoft Visual C++).  

Для просмотра метаданных и дизассемблированного кода PE-файлов в иерархическом представлении в виде дерева применяется графический пользовательский интерфейс по умолчанию дизассемблера IL. Чтобы запустить графический пользовательский интерфейс, введите в командной строке команду **ildasm** без аргумента *имя_PE-файла* и без параметров. В меню **Файл** можно перейти к PE-файлу, который требуется загрузить в программу *Ildasm.exe*. Чтобы сохранить метаданные и дизассемблированный код, отображаемый для выбранного PE-файла, выберите в меню **Файл** команду **Дамп**. Чтобы сохранить только иерархическое представление в виде дерева, выберите в меню **Файл** команду **Дерево дампа**. Дополнительные инструкции по загрузке файла в программу *Ildasm.exe* и интерпретации выходных данных см. в учебнике по *Ildasm.exe*, расположенном в папке Samples, входящей в комплект поставки [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].

Если программе *Ildasm.exe* задан аргумент *имя_PE-файла*, содержащий внедренные ресурсы, будет создано несколько выходных файлов: текстовый файл с IL-кодом и RESOURCES-файл для каждого внедренного управляемого ресурса (название файла соответствует названию ресурса в метаданных). Если в аргумент *имя_PE-файла* внедрены неуправляемые ресурсы, будет создан RES-файл с именем, указанным для IL-вывода в параметре **/output**.

> [!NOTE]
> Для входных файлов *OBJ* и *LIB* программа *Ildasm.exe* отображает только описания метаданных. IL-код для файлов этих типов не дизассемблируется.

Чтобы определить, является ли файл EXE или *DLL* управляемым, обработайте его программой *Ildasm.exe*. Если файл не является управляемым, программа выдаст сообщение, что у файла отсутствует допустимый заголовок среды CLR и он не может быть дизассемблирован. Если файл является управляемым, программа будет выполнена без ошибок.

## <a name="version-information"></a>Сведения о версии

Начиная с .NET Framework 4.5 программа *Ildasm.exe* обрабатывает нераспознанный маршалинговый объект BLOB (большой двоичный объект), отображая необработанное двоичное содержимое. В следующем примере показано, как отображается маршалинговый объект BLOB, созданный программой C#:

```csharp
public void Test([MarshalAs((short)70)] int test) { }
```

```
// IL from Ildasm.exe output
.method public hidebysig instance void Test(int32  marshal({ 46 }) test) cil managed
```

Начиная с .NET Framework 4.5 программа *Ildasm.exe* отображает атрибуты, применяемые к реализации интерфейса, как показано в следующем фрагменте выходных данных *Ildasm.exe*:

```
.class public auto ansi beforefieldinit MyClass
  extends [mscorlib]System.Object
  implements IMyInterface
  {
    .interfaceimpl type IMyInterface
    .custom instance void
      [mscorlib]System.Diagnostics.DebuggerNonUserCodeAttribute::.ctor() = ( 01 00 00 00 )
      …
```

## <a name="examples"></a>Примеры

Следующая команда выводит метаданные и дизассемблированный код PE-файла `MyHello.exe` в стандартный графический пользовательский интерфейс программы *Ildasm.exe*.

```console
ildasm myHello.exe
```

Следующая команда дизассемблирует файл `MyFile.exe` и сохраняет выходной текст ассемблера IL в файле *MyFile.il*.

```console
ildasm MyFile.exe /output:MyFile.il
```

Следующая команда дизассемблирует файл `MyFile.exe` и выводит выходной текст ассемблера IL в окно консоли.

```console
ildasm MyFile.exe /text
```

Если файл `MyApp.exe` содержит внедренные управляемые и неуправляемые ресурсы, при выполнении следующей команды будет создано четыре файла: *MyApp.il*, *MyApp.res*, *Icons.resources* и *Message.resources*:

```console
ildasm MyApp.exe /output:MyApp.il
```

Следующая команда дизассемблирует метод `MyMethod` класса `MyClass` в файле `MyFile.exe` и выводит результат в окно консоли.

```console
ildasm /item:MyClass::MyMethod MyFile.exe /text
```

В предыдущем примере допустимо наличие нескольких методов с именем `MyMethod` и различными сигнатурами. Следующая команда дизассемблирует метод экземпляра `MyMethod` с типом возвращаемого значения **void** и типами параметров **int32** и **string**.

```console
ildasm /item:"MyClass::MyMethod(instance void(int32,string)" MyFile.exe /text
```

> [!NOTE]
> В .NET Framework версии 1.0 и 1.1 открывающей скобке, которая следует за именем метода, должна соответствовать закрывающая скобка после сигнатуры: `MyMethod(instance void(int32))`. В .NET Framework 2.0 и более поздних версий закрывающая скобка должна быть опущена: `MyMethod(instance void(int32)`.

Чтобы извлечь метод `static` (метод `Shared` в Visual Basic), следует опустить ключевое слово `instance`. Типы классов, которые не являются простыми типами (такими как `int32` и `string`), должны включать пространство имен и перед ними необходимо указывать ключевое слово `class`. Перед внешними типами должно быть указано имя соответствующей библиотеки в квадратных скобках. Следующая команда дизассемблирует статический метод с именем `MyMethod`, имеющий один параметр типа <xref:System.AppDomain>, и возвращает значение типа <xref:System.AppDomain>.

```console
ildasm /item:"MyClass::MyMethod(class [mscorlib]System.AppDomain(class [mscorlib]System.AppDomain)" MyFile.exe /text
```

Перед вложенным типом необходимо указывать содержащий его класс, отделенный косой чертой (/). Например, если класс `MyNamespace.MyClass` содержит вложенный класс с именем `NestedClass`, вложенный класс указывается следующим образом: `class MyNamespace.MyClass/NestedClass`.

## <a name="see-also"></a>См. также

- [Инструменты](../../../docs/framework/tools/index.md)
- [Ilasm.exe (ассемблер IL)](../../../docs/framework/tools/ilasm-exe-il-assembler.md)
- [Процесс управляемого выполнения](../../../docs/standard/managed-execution-process.md)
- [Командные строки](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
