---
title: 使用记录集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8e3c3c7ff7d623d3bec0adf60773266bb6e53571
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704440"
---
# <a name="working-with-recordsets"></a>使用记录集
**记录集**对象有内置功能，可用于重新排列结果集中的数据的顺序，根据你提供的条件的特定记录中搜索并且甚至优化那些使用索引的搜索操作。 可使用这些功能是否取决于提供程序以及在某些情况下-例如[索引](../../../ado/reference/ado-api/index-property.md)属性的数据源本身的结构。  
  
## <a name="arranging-data"></a>排列数据  
 通常情况下，最有效的方法中的对数据进行排序你**记录集**是用于将结果返回到其 SQL 命令中指定 ORDER BY 子句。 但是，您可能需要更改中的数据的顺序**记录集**已创建。 可以使用**排序**属性来建立的顺序中的哪些行**记录集**遍历。 此外，**筛选器**属性确定哪些行是遍历行时可以访问。  
  
 **排序**属性设置或返回**字符串**中的值，该值指示该字段名称**记录集**作为排序依据。 每个名称用逗号隔开，并可以选择后跟一个空格和关键字**ASC** （其中进行排序的字段按升序排序） 或**DESC** （排序降序排序的字段）。 默认情况下，如果不指定任何关键字，则该字段按升序顺序。  
  
 排序操作是有效的因为数据不以物理方式重新排列，但由索引指定的顺序访问。  
  
 **排序**属性需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。 对于每个字段中指定将创建一个临时索引**排序**如果索引不存在的属性。  
  
 设置**排序**属性为空字符串将行重置为其原始顺序并删除临时索引。 将删除现有的索引。  
  
 假设**记录集**包含名为三个字段*firstName*， *middleInitial*，以及*lastName*。 设置**排序**属性设置为字符串"`lastName DESC, firstName ASC`"，将顺序**记录集**按姓氏以降序，然后按升序排序的第一个名称。 中间名首字母将被忽略。  
  
 排序条件字符串中引用的任何字段可命名为"ASC"或"DESC"因为这些名称与关键字冲突**ASC**并**DESC**。 提供使用别名具有冲突名称的字段**AS**中返回的查询关键字**记录集**。  
  
 有关详细信息**记录集**筛选，参阅本主题的更高版本的"筛选结果"。  
  
## <a name="finding-a-specific-record"></a>查找特定记录  
 ADO 提供[查找](../../../ado/reference/ado-api/find-method-ado.md)并[Seek](../../../ado/reference/ado-api/seek-method.md)方法，用于查找中的特定记录**记录集**。 **查找**方法支持的各种提供程序，但仅限于单个搜索条件。 **Seek**方法支持多个条件进行搜索，但很多提供程序不支持。  
  
 字段的索引可以极大地提高的性能**查找**方法并**排序**并**筛选器**属性的**记录集**对象。 可以创建的内部索引**字段**对象通过设置其动态[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)属性。 此动态属性添加到**属性**系列**字段**对象设置时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**. 请记住，此索引是 ADO 的内部-不能对其进行访问，或将其用于任何其他用途。 此外，此索引是不同于[索引](../../../ado/reference/ado-api/index-property.md)的属性**记录集**对象。  
  
 **查找**方法可快速查找的列 （字段） 中的值**记录集**。 通常可以提高的速度**查找**使用的列方法**优化**属性以在其上创建索引。  
  
 **查找**方法将搜索限制为一个字段的内容。 **Seek**方法要求有索引，并且已以及其他限制。 如果必须在不是索引的基础的多个字段上搜索或如果您的提供程序不支持索引，您可以通过使用限制您的结果**筛选器**的属性**记录集**对象。  
  
### <a name="find"></a>查找  
 **查找**方法搜索**记录集**满足指定的条件的行。 （可选） 可以指定搜索、 起始行和偏移量开始的行的方向。 如果满足该条件，则在找到的记录; 上设置的当前行位置否则，将位置设置为的终点 （或起点）**记录集**，取决于搜索方向。  
  
 可以为条件指定仅包含单列的名称。 换而言之，此方法不支持多列搜索。  
  
 比较运算符中的条件可以是" **>** "（大于）、" **\<** "（小于）、"="（等于）"> ="（大于或等于）"< ="（小于或等于）、"<>"（不等于）、 或"LIKE"（模式匹配）。  
  
 条件值可以是字符串、 浮点数或日期。 字符串值是用单引号引起来或"#"（数字符号） 标记分隔 (例如，"状态 = WA"或"状态 = #WA #")。 日期值以"#"（数字符号） 标记 (例如，"start_date > #7/22/97 #")。  
  
 如果"like"比较运算符，字符串值可以包含一个星号 （*） 来找到的任何字符或子字符串的一个或多个匹配项。 例如，"等状态是\*"匹配 Maine 和马萨诸塞州。 前导和尾随星号还可用于查找的子字符串，包含的值内。 例如，"等状态\*作为\*"匹配阿拉斯加州、 阿肯色州和马萨诸塞州。  
  
 星号可以仅在条件字符串末尾或一起开头和末尾条件字符串，使用前面所示。 您不能使用星号作为前导通配符 (* str') 或嵌入式通配符 ('s\*r)。 这会导致错误。  
  
### <a name="seek-and-index"></a>查找并编制索引  
 使用**Seek**方法一起使用**索引**如果基础提供程序上支持索引属性**记录集**对象。 使用[支持](../../../ado/reference/ado-api/supports-method.md) **(adSeek)** 方法，以确定基础提供程序是否支持**搜寻**，以及**Supports(adIndex)** 若要确定该提供程序是否支持索引的方法。 (例如， [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)支持**Seek**并**索引**。)  
  
 如果**Seek**不找到所需的行中，没有错误发生，而且行位于末尾处**记录集**。 设置**索引**之前执行此方法所需索引的属性。  
  
 使用服务器端游标仅支持此方法。 查找时不支持[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性值为**记录集**对象**adUseClient**。  
  
 可以使用此方法时，才**记录集**以打开对象[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)的值**adCmdTableDirect**。  
  
## <a name="filtering-the-results"></a>筛选结果  
 **查找**方法将搜索限制为一个字段的内容。 **Seek**方法要求有索引，并且已以及其他限制。 如果必须在不是索引的基础的多个字段上搜索或如果您的提供程序不支持索引，您可以通过使用限制您的结果**筛选器**的属性**记录集**对象。  
  
 使用**筛选器**属性可有选择地筛选掉中的记录**记录集**对象。 筛选**记录集**变得不满足意味着记录的当前光标**筛选器**条件中均不提供**记录集**之前**筛选器**中删除。 返回基于当前游标值的其他属性受到影响，如**AbsolutePosition**， **AbsolutePage**， **RecordCount**，和**PageCount**。 这是因为设置**筛选器**为特定值的属性会将当前记录移到满足新值的第一个记录。  
  
 **筛选器**属性采用的变体的自变量。 此值表示使用三种方法之一**筛选器**属性： string 条件**FilterGroupEnum**常量或书签的数组。 有关详细信息，请参阅本主题后面的筛选条件字符串、 与常量、 筛选和用书签筛选。  
  
> [!NOTE]
>  当您知道您想要选择的数据时，是打开通常更高效**记录集**使用 SQL 语句有效地筛选结果集，而不是依靠**筛选器**属性。  
  
 若要删除筛选器从**记录集**，使用**adFilterNone**常量。 设置**筛选器**属性设置为零长度字符串 ("") 具有与使用相同的效果**adFilterNone**常量。  
  
### <a name="filtering-with-a-criteria-string"></a>使用条件字符串进行筛选  
 条件字符串包含窗体中的子句*FieldName 运算符值*(例如， `"LastName = 'Smith'"`)。 可以通过连接与多个子句来创建复合子句**AND** (例如， `"LastName = 'Smith' AND FirstName = 'John'"`) 和**或者**(例如， `"LastName = 'Smith' OR LastName = 'Jones'"`)。 条件字符串中使用以下准则：  
  
-   *FieldName*必须是有效的字段名称，从**记录集**。 如果字段名称包含空格，必须将名称括在方括号中。  
  
-   *运算符*必须是以下值之一： **\<** ， **>** ， **\< =** ， **>=** **<>** ， **=** ，或者**如**。  
  
-   *值*是将与之比较的字段值的值 (例如， `'Smith'`， `#8/24/95#`， `12.345`，或`$50.00`)。 使用字符串使用单引号 （'） 和井号 (`#`) 包含的日期。 对于数字，可以使用小数点、 美元符号和科学记数法。 如果*运算符*是**等**，*值*可以使用通配符。 仅星号 (\*) 和百分号 （%）允许使用通配符字符，并且它们必须是字符串中的最后一个字符。 *值*不能为 null。  
  
    > [!NOTE]
    >  若要在筛选器中包含单引号 （'）*值*，使用两个单引号来表示一个。 例如，对筛选*O'Malley*，则条件字符串应为`"col1 = 'O''Malley'"`。 若要包含在开头和筛选器值结束的单引号，请将字符串括在井号 （#）。 例如，对筛选 *'1'* ，则条件字符串应为`"col1 = #'1'#"`。  
  
 没有之间没有优先**AND**并**或**。 子句可以在括号内进行分组。 但是，也不能分组子句通过联接**或**然后将组加入到另一个带有一个 AND 子句，如下所示。  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 相反，将构造此筛选器，如下所示。  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 在**等**子句中，你可以使用通配符开头和末尾模式 (例如， `LastName Like '*mit*'`) 或仅在该模式末尾 (例如， `LastName Like 'Smit*'`)。  
  
### <a name="filtering-with-a-constant"></a>使用一个常量进行筛选  
 以下常量是可用于筛选**记录集**。  
  
|常量|Description|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|用于查看仅受影响的最后一个的记录的筛选器**删除**，**重新同步**， **UpdateBatch**，或者**CancelBatch**调用。|  
|**adFilterConflictingRecords**|用于查看失败的最后的批处理更新的记录的筛选器。|  
|**adFilterFetchedRecords**|筛选器用于查看当前的缓存-中的记录，即要从数据库中检索记录的最后一个调用的结果。|  
|**adFilterNone**|删除当前筛选器并还原所有记录以进行查看。|  
|**adFilterPendingRecords**|查看仅记录的筛选器的已更改但尚未发送到服务器。 仅适用于批更新模式。|  
  
 筛选器常量使其更轻松地解决个别记录冲突期间通过允许您查看，例如，只有这些记录的批更新模式下受影响在最后一个**UpdateBatch**方法调用，如中所示下面的示例。  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>使用书签进行筛选  
 最后，将传递到的书签的变体数组**筛选器**属性。 所得到的游标将包含只有那些其书签传递给该属性的记录。 下面的代码示例从记录中创建的书签数组**记录集**"B"在*ProductName*字段。 然后将传递到的数组**筛选器**有关生成筛选的属性和显示信息**记录集**。  
  
```  
'BeginFilterBkmk  
Dim vBkmkArray() As Variant  
Dim i As Integer  
  
'Recordset created using "SELECT * FROM Products" as command.  
'So, we will check to see if ProductName has a capital B, and  
'if so, add to the array.  
i = 0  
Do While Not objRs.EOF  
    If InStr(1, objRs("ProductName"), "B") Then  
        ReDim Preserve vBkmkArray(i)  
        vBkmkArray(i) = objRs.Bookmark  
        i = i + 1  
        Debug.Print objRs("ProductName")  
    End If  
    objRs.MoveNext  
Loop  
  
'Filter using the array of bookmarks.  
objRs.Filter = vBkmkArray  
  
objRs.MoveFirst  
Do While Not objRs.EOF  
    Debug.Print objRs("ProductName")  
    objRs.MoveNext  
Loop  
'EndFilterBkmk  
```  
  
## <a name="creating-a-clone-of-a-recordset"></a>创建记录集的克隆  
 使用**克隆**方法来创建多个重复**记录集**对象，尤其是如果你想要维护一组给定的记录中的多个当前记录。 使用**克隆**方法是创建和打开一个新比效率更高**记录集**具有相同的定义与原始对象。  
  
 新创建的克隆的当前记录最初设置为第一条记录。 为克隆中的当前记录指针**记录集**不会同步其原始，反之亦然。 您可以在每个独立导航**记录集**。  
  
 对一个做的更改**记录集**对象中是可见的所有克隆而不考虑游标类型。 但是，之后执行[Requery](../../../ado/reference/ado-api/requery-method.md)上原始**记录集**，克隆将不再同步到原始。  
  
 关闭原始**记录集**不会关闭其副本，也不关闭副本关闭原始对象或任何其他副本。  
  
 可以克隆**记录集**仅对象是否支持书签。 书签值是可以互换;也就是说，从一个的书签引用**记录集**对象是指任何复本中的同一记录。
