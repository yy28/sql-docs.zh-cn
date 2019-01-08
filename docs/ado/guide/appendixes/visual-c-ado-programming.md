---
title: Visual c + + ADO 编程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1b34c2b88c8e1906438f706143fcf6ec966026d
ms.sourcegitcommit: fa2f85b6deeceadc0f32aa7f5f4e2b6e4d99541c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2019
ms.locfileid: "53997589"
---
# <a name="visual-c-ado-programming"></a>Visual C++ ADO 编程
ADO API 参考介绍 ADO 应用程序编程接口 (API) 使用 Microsoft Visual Basic 类似的语法的功能。 ADO 程序员的目标的受众是所有用户，但采用不同语言，例如 Visual Basic、 Visual c + + (带和不带 **#import**指令)，和 Visual J + + 中 （与 ADO/WFC 类包）。  

> [!NOTE]
> Microsoft 在 2004 年结束支持 Visual J + +。

 以适应这种多样性[的 ADO for Visual c + + 语法索引](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)Visual c + + 特定于语言的语法提供的功能、 参数、 异常行为和等等，API 中的常见描述链接引用。  
  
 ADO 使用 COM （组件对象模型） 接口实现。 但是，它是更易于编程人员使用比其他某些编程语言中的 COM。 例如，使用 COM 的几乎所有详细信息是隐式 for 处理 Visual Basic 编程人员，而 Visual c + + 程序员必须参加到这些本身的详细信息。  
  
 以下部分概述详细信息的 C 和 c + + 程序员使用 ADO 和 **#import**指令。 它重点介绍特定于 COM 数据类型 (**Variant**， **BSTR**，并**SafeArray**)，和错误处理 (_com_error)。  
  
## <a name="using-the-import-compiler-directive"></a>使用 #import 编译器指令  
 **#Import** Visual c + + 编译器指令可以简化使用 ADO 方法和属性。 指令将包含类型库，如 ADO.dll (Msado15.dll) 的文件的名称，并生成包含 typedef 声明、 接口和枚举的常量的智能指针的标头文件。 每个接口封装，或将其包装在类中。  
  
 类 （即，方法或属性调用） 中的每个操作，对于没有声明来调用此操作直接 （即，"原始"窗体的操作），并声明调用原始操作并引发 COM 错误，如果该操作无法执行 successfully。 如果该操作是一个属性，则通常创建的语法与 Visual Basic 语法的操作的可选语法的编译器指令。  
  
 检索属性值的操作具有名称的窗体中，**获取**_属性_。 设置属性的值的操作具有名称的窗体中，**放**_属性_。 将具有一个指针的属性的值设置为 ADO 对象的操作具有名称的窗体中， **PutRef**_属性_。  
  
 你可以获取或设置具有以下形式的调用的属性：  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>使用属性指令  
 **__Declspec(property...)** 编译器指令是一个特定于 Microsoft 的 C 语言扩展，声明一个函数，用于为属性具有的可选语法。 因此，可以设置或获取属性的值的方式类似于 Visual Basic。 例如，您可以设置和获取这种方式的属性：  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 请注意，目前没有对代码：  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 编译器将生成的相应**获取**_-_，**放**-，或**PutRef**_属性_调用基于声明哪些替代语法，并且是否正在属性读取或写入。  
  
 **__Declspec(property...)** 编译器指令可以仅声明**获取**，**放**，或**获取**并**放**函数的替代语法。 只读操作只有**获取**声明; 只写操作只有**放置**声明; 操作的同时读取和写入同时具有**获取**和**放置**声明。  
  
 只有两个声明都可能包含此指令;但是，每个属性可能有三个属性函数：**获取**_属性_，**放**_属性_，并且**PutRef**_属性_。 在这种情况下，只有两个窗体的属性具有可选的语法。  
  
 例如，**命令**对象**ActiveConnection**属性声明与为的可选语法**获取**_ActiveConnection_并**PutRef**_ActiveConnection_。 **PutRef**的语法是一个不错的选择，因为在实践中，通常需要将一种开放**连接**对象 (即**连接**对象指针) 在此属性。 但是，**记录集**对象具有**获取**-，**放**-，和**PutRef**_ActiveConnection_操作，但没有替代语法。  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>集合、 GetItem 方法和项属性  
 ADO 定义了多个集合，包括**字段**，**参数**，**属性**，以及**错误**。 在 Visual c + + **GetItem (_索引_)** 方法返回集合的成员。 *索引*是**变体**，其值是数字索引的集合中的成员或包含的成员的名称的字符串。  
  
 **__Declspec(property...)** 编译器指令声明**项**属性设置为每个集合的可选语法的基本**GetItem()** 方法。 替代语法使用方括号括起来，看起来类似于数组引用。 一般情况下，两种形式如以下所示：  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 例如，将值分配到的字段**记录集**对象，名为 **_rs_** 派生自**作者**表**pubs**数据库。 使用**Item()** 属性来访问第三个**字段**的**记录集**对象**字段**（集合编制索引从集合零;假设第三个字段的名称为 **_au\_fname_**)。 然后调用**value （)** 方法**字段**对象来将一个字符串值。  
  
 这可以用来表示在 Visual Basic 中以下四种方法 （最后两个窗体是唯一的 Visual Basic; 其他语言不具有等效项）：  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 在 Visual c + + 更高版本的前两个窗体的等效项是：  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 -(的替代语法**值**属性还会显示)  
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 有关循环访问集合的示例，请参阅"ADO 参考"的"ADO 集合"部分。  
  
## <a name="com-specific-data-types"></a>特定于 COM 的数据类型  
 一般情况下，ADO API 参考中查找任何 Visual Basic 数据类型具有一个返回 Visual c + + 等效。 这些包括标准的数据类型，如下所述**unsigned char**适用于 Visual Basic**字节**，**短**有关**整数**，和**长**有关**长**。 查找范围语法 Indexesto 看到所需的特定的方法或属性的操作数的内容。  
  
 此规则的例外是特定于 COM 的数据类型：**变体**， **BSTR**，和**SafeArray**。  
  
### <a name="variant"></a>Variant  
 一个**变体**是包含值成员和数据类型成员的结构化的数据类型。 一个**变体**可能包含各种其他数据类型，包括另一个变体、 BSTR、 布尔值、 IDispatch 或 IUnknown 指针、 货币、 日期和等等。 COM 还提供了方法，可以轻松快速地转换到另一种数据类型。  
  
 **_Variant_t**类封装并管理**变体**数据类型。  
  
 当 ADO API 参考说一种方法或属性操作数采用一个值时，这通常意味着中传递的值 **_variant_t**。  
  
 此规则为 true; 显式**参数**ADO API 参考主题中的部分显示操作数**变体**。 一个例外情况是当文档中明确指出操作数采用标准数据类型，如**长**或**字节**，或枚举。 另一个例外情况是当操作数采用**字符串**。  
  
### <a name="bstr"></a>BSTR  
 一个**BSTR** (**B**asic **STR**ing) 是结构化的数据类型，其中包含一个字符字符串和字符串的长度。 COM 提供方法来分配、 操作和释放**BSTR**。  
  
 **_Bstr_t**类封装并管理**BSTR**数据类型。  
  
 ADO API 参考时显示的方法或属性采用**字符串**值，它表示形式的值是 **_bstr_t**。  
  
### <a name="casting-variantt-and-bstrt-classes"></a>强制转换 _variant_t 和 _bstr_t 类  
 通常没有必要显式代码 **_variant_t**或 **_bstr_t**中操作的参数。 如果 **_variant_t**或 **_bstr_t**类具有匹配参数的数据类型的构造函数，编译器将生成相应 **_variant_t**或 **_bstr_t**。  
  
 但是，如果参数是不明确，即，参数的数据类型匹配多个构造函数，必须使用相应的数据类型来调用正确的构造函数转换参数。  
  
 例如，声明**Recordset::Open**方法是：  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 `ActiveConnection`自变量将引用 **_variant_t**，这可能会为连接字符串或指向一个打开的代码**连接**对象。  
  
 正确 **_variant_t**如果你将传递一个字符串，例如将隐式构造"`DSN=pubs;uid=MyUserName;pwd=MyPassword;`"，或如指针"`(IDispatch *) pConn`"。  
  
> [!NOTE]
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码在连接字符串中的信息。  
  
 或者也可能会显式 **_variant_t**包含一个指针，如"`_variant_t((IDispatch *) pConn, true)`"。 强制转换、 `(IDispatch *)`，解析含糊歧义采用的 IUnknown 接口指针的另一个构造函数。  
  
 尽管很少提及这一事实，ADO 的 IDispatch 接口是至关重要的。 每当必须作为传递到 ADO 对象的指针**变体**，该指针必须可强制转换为指向的 IDispatch 接口的指针。  
  
 最后一种情况，显式地编写构造函数的第二个布尔型参数，其可选的默认值为`true`。 此参数会导致**Variant**构造函数来调用其**AddRef**（） 方法，ADO 自动调用的补偿 **_variant_t::Release**（） 方法ADO 方法或属性调用何时完成。  
  
### <a name="safearray"></a>SafeArray  
 一个**SafeArray**是包含其他数据类型的数组的结构化的数据类型。 一个**SafeArray**称为*安全*因为它包含的每个数组维度的界限的信息，并限制对这些边界内的数组元素的访问。  
  
 当 ADO API 参考说一种方法或属性接受或返回一个数组，意味着该方法或属性接受或返回**SafeArray**，不本机 C/c + + 数组。  
  
 例如，第二个参数的**连接**对象**OpenSchema**方法需要一个数组**变体**值。 那些**变体**值必须作为元素传递**SafeArray**，并且**SafeArray**设置为另一个值，必须**变体**. 它是其他**Variant**作为第二个参数传递**OpenSchema**。  
  
 为进一步示例、 的第一个参数**查找**方法是**变体**其值是一个一维**SafeArray**; 每个的可选的第一个和第二个参数**AddNew**是一维**SafeArray**; 和返回值的**GetRows**方法是**变体**其值是一个二维**SafeArray**。  
  
## <a name="missing-and-default-parameters"></a>缺少和默认参数  
 Visual Basic 允许缺少中方法的参数。 例如，**记录集**对象**打开**方法具有五个参数，但你可以跳过中间参数并将保持关闭状态的尾随参数。 默认值**BSTR**或**变体**将替换具体取决于缺少操作数的数据类型。  
  
 在 C/c + + 中，必须指定所有操作数。 如果你想要指定缺少的参数的数据类型为字符串，指定 **_bstr_t**包含空字符串。 如果想要指定缺少的参数的数据类型是**Variant**，指定 **_variant_t** DISP_E_PARAMNOTFOUND 和 VT_ERROR 类型的值。 或者，指定等效 **_variant_t**常量， **vtMissing**，它们由提供 **#import**指令。  
  
 三种方法是例外情况的典型用法**vtMissing**。 这些是**Execute**方法的**连接**并**命令**对象，并**NextRecordset** 方法**记录集**对象。 它们的签名如下：  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 参数， *RecordsAffected*并*参数*，都是指向**变体**。 *参数*是一个输入的参数指定的地址**变体**包含单个参数或将修改正在执行的命令的参数的数组。 *RecordsAffected*是一个输出参数，指定的地址**变体**，其中返回受影响的方法的行数。  
  
 在中**命令**对象**Execute**方法，指示通过设置未指定任何参数*参数*为`&vtMissing`（这推荐的） 或null 指针 (即**NULL**或零 (0))。 如果*参数*设置为 null 指针，该方法在内部替换的等效项**vtMissing**，然后完成该操作。  
  
 所有方法中指示受影响的记录数不应返回通过设置*RecordsAffected*到 null 指针。 在这种情况下，null 指针不太是缺少参数用于指示方法应丢弃受影响的记录数。  
  
 因此，对于这三种方法是有效如下代码：  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>错误处理  
 在 COM 中，大多数操作返回一个 HRESULT 返回代码，指示函数是否已成功完成。 **#Import**指令生成每个"原始"方法或属性周围的包装代码，并检查返回的 HRESULT。 如果 HRESULT 表示失败，包装器代码将 COM 错误的 HRESULT 返回代码的调用 _com_issue_errorex() 引发作为参数。 COM 错误对象可以陷入**尝试**-**捕获**块。 (为提高效率的起见，捕获的引用 **_com_error**对象。)  
  
 请记住，这些是 ADO 错误： 可疑 ADO 操作失败。 基础提供程序返回的错误显示为**错误**中的对象**连接**对象**错误**集合。  
  
 **#Import**指令创建唯一的错误处理例程的方法和 ADO.dll 中声明的属性。 但是，您可以利用此相同的错误处理机制，通过编写自己的错误检查宏或内联函数。 请参阅主题[Visual c + + 扩展](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md)，或有关示例的以下部分中的代码。  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual c + + 的 Visual Basic 约定的等效项  
 下面是在 ADO 文档中，编码在 Visual Basic 和 Visual c + + 中的等效项的多个约定的摘要。  
  
### <a name="declaring-an-ado-object"></a>声明 ADO 对象  
 在 Visual Basic 中的 ADO 对象变量 (在本例中为**记录集**对象) 的声明方式如下：  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 该子句中，"`ADODB.Recordset`"，是的 ProgID**记录集**对象，如注册表中定义。 新实例**记录**对象声明，如下所示：  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 -或-  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 在 Visual c + + **#import**指令生成的所有 ADO 对象的智能指针类型声明。 例如，变量指向 **_Recordset**对象属于类型 **_RecordsetPtr**，并声明，如下所示：  
  
```cpp
_RecordsetPtr  rs;  
```
  
 变量指向的新实例 **_Recordset**对象声明，如下所示：  
  
```cpp
_RecordsetPtr  rs("ADODB.Recordset");  
```
  
 -或-  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```
  
 -或-  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```
  
 之后**CreateInstance**方法调用时，可以使用变量，如下所示：  
  
```cpp
rs->Open(...);  
```
  
 请注意，在一种情况下，"`.`"，像变量类的实例使用运算符 (`rs.CreateInstance`)，并在另一种情况下，"`->`"，像变量指向接口的指针使用运算符 (`rs->Open`)。  
  
 可以通过两种方式使用变量，因为"`->`"运算符将重载以允许进行的行为类似指向接口的类的实例。 实例变量的私有类成员包含一个指向 **_Recordset**接口;"`->`"运算符将返回该指针;，返回的指针访问成员的 **_Recordset**对象。  
  
### <a name="coding-a-missing-parameter---string"></a>缺少参数的字符串进行编码  
 当需要进行代码缺少**字符串**操作数在 Visual Basic 中，只是省略操作数。 在 Visual c + + 中，必须指定操作数。 代码 **_bstr_t**具有一个空字符串作为一个值。  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter---variant"></a>缺少参数的变体进行编码  
 当需要进行代码缺少**变体**操作数在 Visual Basic 中，只是省略操作数。 在 Visual c + + 中，必须指定所有操作数。 代码缺少**Variant**参数与 **_variant_t**设置为特殊值、 DISP_E_PARAMNOTFOUND 和类型，VT_ERROR。 或者，指定**vtMissing**，它们等效的预定义的常量由提供 **#import**指令。  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 -或使用-  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>声明一个变体  
 在 Visual Basic 中， **Variant**使用声明**Dim**语句，如下所示：  
  
```vb
Dim VariableName As Variant  
```
  
 在 Visual c + +，将变量声明为类型 **_variant_t**。 几个示意图 **_variant_t**声明如下所示。  
  
> [!NOTE]
>  这些声明只是为提供大致了解一下您在编写你自己的程序中。 有关详细信息，请参阅下面的示例和 Visual C + + 文档。  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>使用变体的数组  
 在 Visual Basic 中的数组**变体**编码**Dim**语句，或您可以使用**数组**函数，如下面的示例代码所示：  
  
```vb
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```
  
 下面的 Visual c + + 示例演示了如何使用**SafeArray**用于 **_variant_t**。  
  
#### <a name="notes"></a>说明  
 以下说明对应于代码示例中的注释部分。  
  
1.  再次重申，TESTHR() 内联函数定义以充分利用现有的错误处理机制。  
  
2.  您只需一维数组，因此可以使用**SafeArrayCreateVector**，而不是常规用途**SAFEARRAYBOUND**声明并**SafeArrayCreate**函数。 下面是使用该代码将如下**SafeArrayCreate**:  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  由枚举常数，标识的架构**adSchemaColumns**，与四个约束列相关联：TABLE_CATALOG、 TABLE_SCHEMA、 TABLE_NAME 和 COLUMN_NAME。 因此，数组**变体**创建带有四个元素的值。 然后指定约束值与第三个列，TABLE_NAME 相对应。  
  
     **记录集**返回多个列，其中有一部分是约束列组成。 每个返回行的约束列的值必须与相应约束的值相同。  
  
4.  熟悉的那些**Safearray**可能会惊讶的**SafeArrayDestroy**退出之前未调用 （）。 实际上，调用**SafeArrayDestroy**（） 在这种情况下会导致运行时异常。 其原因在于的析构函数`vtCriteria`将调用**VariantClear**（) 时 **_variant_t**超出范围，可释放**SafeArray**。 调用**SafeArrayDestroy**，而无需手动清除 **_variant_t**，将导致析构函数尝试清除无效**SafeArray**指针。  
  
     如果**SafeArrayDestroy**已调用，代码将如下所示：  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     但是，它是要简单得多让 **_variant_t**管理**SafeArray**。  
  
```cpp
// Visual_CPP_ADO_Prog_1.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Note 1  
inline void TESTHR( HRESULT _hr ) {   
   if FAILED(_hr)   
      _com_issue_error(_hr);   
}  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      _ConnectionPtr pCn("ADODB.Connection");  
      _variant_t vtTableName("authors"), vtCriteria;  
      long ix[1];  
      SAFEARRAY *pSa = NULL;  
  
      pCn->Provider = "sqloledb";  
      pCn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
      // Note 2, Note 3  
      pSa = SafeArrayCreateVector(VT_VARIANT, 1, 4);  
      if (!pSa)   
         _com_issue_error(E_OUTOFMEMORY);  
  
      // Specify TABLE_NAME in the third array element (index of 2).   
      ix[0] = 2;        
      TESTHR(SafeArrayPutElement(pSa, ix, &vtTableName));  
  
      // There is no Variant constructor for a SafeArray, so manually set the   
      // type (SafeArray of Variant) and value (pointer to a SafeArray).  
  
      vtCriteria.vt = VT_ARRAY | VT_VARIANT;  
      vtCriteria.parray = pSa;  
  
      pRs = pCn->OpenSchema(adSchemaColumns, vtCriteria, vtMissing);  
  
      long limit = pRs->GetFields()->Count;  
      for ( long x = 0 ; x < limit ; x++ )  
         printf( "%d: %s\n", x + 1, ((char*) pRs->GetFields()->Item[x]->Name) );  
      // Note 4  
      pRs->Close();  
      pCn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Code meaning = %s\n", (char*) e.ErrorMessage());  
      printf("Source = %s\n", (char*) e.Source());  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   CoUninitialize();  
}  
```
  
### <a name="using-property-getputputref"></a>使用属性 Get/Put/替代语法  
 在 Visual Basic 中的属性名称不是无论它是检索、 分配，或分配一个引用限定的。  
  
```vb
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```
  
 此 Visual c + + 示例演示**获取**/**放**/**PutRef**_属性_。  
  
#### <a name="notes"></a>说明  
 以下说明对应于代码示例中的注释部分。  
  
1.  此示例使用两种形式的缺少字符串参数： 一个显式常量**strMissing**，和一个字符串，编译器将使用它来创建一个临时 **_bstr_t**将存在于的作用域**打开**方法。  
  
2.  不需要强制转换的操作数`rs->PutRefActiveConnection(cn)`到`(IDispatch *)`因为操作数的类型已经`(IDispatch *)`。  
  
```cpp
// Visual_CPP_ado_prog_2.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _bstr_t strMissing(L"");  
      long oldPgSz = 0, newPgSz = 5;  
  
      // Note 1  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", strMissing, "", adConnectUnspecified);  
  
      oldPgSz = rs->GetPageSize();  
      // -or-  
      // oldPgSz = rs->PageSize;  
  
      rs->PutPageSize(newPgSz);  
      // -or-  
      // rs->PageSize = newPgSz;  
  
      // Note 2  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockReadOnly, adCmdTable);  
      printf("Original pagesize = %d, new pagesize = %d\n", oldPgSz, rs->GetPageSize());  
      rs->Close();  
      cn->Close();  
  
   }  
   catch (_com_error &e) {  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="using-getitemx-and-itemx"></a>使用 GetItem(x) 和项 [x]  
 此 Visual Basic 示例说明了标准和替代语法**项**（)。  
  
```vb
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```
  
 此 Visual c + + 示例演示**项**。  
  
> [!NOTE]
>  以下注释对应于代码示例中的注释部分：与访问集合时**项**，索引**2**，必须强制转换为**长**因此将调用相应的构造函数。  
  
```cpp
// Visual_CPP_ado_prog_3.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
void main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _variant_t vtFirstName;  
  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", "", "", adConnectUnspecified);  
  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockOptimistic, adCmdTable);  
      rs->MoveFirst();  
  
      // Note 1. Get a field.  
      vtFirstName = rs->Fields->GetItem((long)2)->GetValue();  
      // -or-  
      vtFirstName = rs->Fields->Item[(long)2]->Value;  
  
      printf( "First name = '%s'\n", (char*)( (_bstr_t)vtFirstName) );  
  
      rs->Fields->GetItem((long)2)->Value = L"TEST";  
      rs->Update(vtMissing, vtMissing);  
  
      // Restore name  
      rs->Fields->GetItem((long)2)->PutValue(vtFirstName);  
      // -or-  
      rs->Fields->GetItem((long)2)->Value = vtFirstName;  
      rs->Update(vtMissing, vtMissing);  
      rs->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>使用 ADO 对象指针强制转换 (IDispatch *)  
 下面的 Visual c + + 示例演示了如何使用 (IDispatch *) 的强制转换 ADO 对象指针。  
  
#### <a name="notes"></a>说明  
 以下说明对应于代码示例中的注释部分。  
  
1.  指定一种开放**连接**对象中显式编码**变体**。 将其与强制转换 (IDispatch \*) 以便将调用的正确构造函数。 此外，显式设置第二个 **_variant_t**参数的默认值为**true**，因此，对象引用计数将是正确时**Recordset::Open**操作将结束。  
  
2.  表达式中， `(_bstr_t)`，不是强制转换，但 **_variant_t**提取运算符 **_bstr_t**中的字符串**变体**返回**值**.  
  
 表达式中， `(char*)`，不是强制转换，但 **_bstr_t**提取到中的封装字符串指针的运算符 **_bstr_t**对象。  
  
 此部分的代码演示了一些有用的行为 **_variant_t**并 **_bstr_t**运算符。  
  
```cpp
// Visual_CPP_ado_prog_4.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr pConn("ADODB.Connection");  
      _RecordsetPtr pRst("ADODB.Recordset");  
  
      pConn->Provider = "sqloledb";  
      pConn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
  
      // Note 1.  
      pRst->Open("authors", _variant_t((IDispatch *) pConn, true), adOpenStatic, adLockReadOnly, adCmdTable);  
      pRst->MoveLast();  
  
      // Note 2.  
      printf("Last name is '%s %s'\n",   
         (char*) ((_bstr_t) pRst->GetFields()->GetItem("au_fname")->GetValue()),  
         (char*) ((_bstr_t) pRst->Fields->Item["au_lname"]->Value));  
  
      pRst->Close();  
      pConn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }     
   ::CoUninitialize();  
}  
```
