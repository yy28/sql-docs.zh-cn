---
title: "使用记录集 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 368e3b3a793bce6b6182ba262493d9a8ed1ac1bd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="working-with-recordsets"></a>使用记录集
**记录集**对象具有的内置功能，可让您重新排列结果集中的数据的顺序，来搜索特定记录根据你提供的条件并甚至优化使用索引这些搜索操作。 这些功能是否可供使用取决于提供程序以及在某些情况下 — 例如[索引](../../../ado/reference/ado-api/index-property.md)属性-数据源本身的结构。  
  
## <a name="arranging-data"></a>排列数据  
 通常情况下，排序中的数据的最高效方式你**记录集**是用于将结果返回到它的 SQL 命令中指定 ORDER BY 子句。 但是，你可能需要更改中的数据的顺序**记录集**已创建。 你可以使用**排序**属性中的哪些行建立顺序**记录集**会来回进行。 此外，**筛选器**属性确定哪些行是遍历行时可以访问。  
  
 **排序**属性设置或返回**字符串**中的值，该值指示字段名称**记录集**排序依据。 每个名称用逗号分隔和 （可选） 后跟一个空格和关键字**ASC** （其中进行排序以升序字段） 或**DESC** （其中进行排序的字段以降序顺序）。 默认情况下，如果未指定关键字，该字段是以升序排序。  
  
 排序操作是高效的因为数据不以物理方式重新排列，但由索引指定的顺序访问。  
  
 **排序**属性需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。 对于每个字段中指定将创建一个临时索引**排序**如果索引不存在的属性。  
  
 设置**排序**属性为空字符串将行重置为其原始顺序并删除临时索引。 将删除现有索引。  
  
 假设**记录集**包含名为的三个字段*firstName*，*没为*，和*lastName*。 设置**排序**到字符串的属性"`lastName DESC, firstName ASC`"，顺序将**记录集**按姓氏以降序顺序，然后按名字以升序排序。 中间名首字母将被忽略。  
  
 没有排序条件字符串中引用的字段可以命名为"ASC"或"DESC"，因为这些名称与关键字冲突**ASC**和**DESC**。 提供通过使用具有冲突的名称别名的字段**AS**返回的查询中的关键字**记录集**。  
  
 有关详细信息**记录集**筛选，查看本主题中后面的"筛选结果"。  
  
## <a name="finding-a-specific-record"></a>查找特定的记录  
 ADO 提供[查找](../../../ado/reference/ado-api/find-method-ado.md)和[Seek](../../../ado/reference/ado-api/seek-method.md)方法，用于查找中的特定记录**记录集**。 **查找**方法支持各种提供程序，但仅限于单个搜索条件。 **Seek**方法支持多个条件进行搜索，但不是支持许多提供程序。  
  
 字段的索引可以极大地提高的性能**查找**方法和**排序**和**筛选器**属性**记录集**对象。 你可以创建的内部索引**字段**对象通过设置其动态[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)属性。 此动态属性添加到**属性**集合**字段**对象设置时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性**adUseClient**. 请记住此索引是内部 ADO-无法对其进行访问，或将其用于任何其他用途。 此外，此索引是不同于[索引](../../../ado/reference/ado-api/index-property.md)属性**记录集**对象。  
  
 **查找**方法快速查找的列 （字段） 内的某个值**记录集**。 经常可以提高的速度**查找**方法上使用的列**优化**若要在其上创建索引的属性。  
  
 **查找**方法将搜索限制为一个字段的内容。 **Seek**方法要求你有索引，并且具有其他限制以及。 如果你必须搜索不是索引的基础的多个字段，或如果你的提供程序不支持索引，则可以通过使用来限制结果**筛选器**属性**记录集**对象。  
  
### <a name="find"></a>查找  
 **查找**方法搜索**记录集**满足指定的条件的行。 （可选） 可以指定的搜索、 起始行和与起始行的偏移量的方向。 如果满足条件，则在找到的记录; 上设置的当前行位置否则，该位置设置为的终点 （或起点）**记录集**，取决于搜索方向。  
  
 可以为条件指定仅包含单列的名称。 换而言之，此方法不支持多列的搜索。  
  
 比较运算符中的条件可以是"**>**"（大于）、"**\<**"（小于）、"="（等于）、"> ="（大于或等于），"< ="（小于或等于）、"<>"（不等于）、 或"LIKE"（模式匹配）。  
  
 条件值可以是字符串、 浮点数或日期。 字符串值是用单引号引起来或"#"（数字符号） 标记分隔 (例如，"状态 = WA"或"状态 = #WA #")。 日期值分隔用"#"（数字符号） 标记 (例如，"start_date > #7/22/&#97;")。  
  
 如果"like"的比较运算符，字符串值可以包含一个星号 （*） 以找到一个或多个出现的任何字符或子字符串。 例如，"等状态正在\*"与缅因和麻省匹配。 前导和尾随星号还可用于查找的值中包含的子字符串。 例如，"状态，如\*作为\*"与阿拉斯加、 阿肯色和麻省。  
  
 星号可以仅在条件字符串的末尾或在一起的开头和末尾的条件字符串中，使用前面所示。 不能将星号用作前导通配符 (* str) 或嵌入通配符 ('s\*r)。 这会导致错误。  
  
### <a name="seek-and-index"></a>查找和索引  
 使用**Seek**连同方法**索引**如果基础提供程序上支持索引属性**记录集**对象。 使用[支持](../../../ado/reference/ado-api/supports-method.md)**(adSeek)**方法，以确定基础提供程序是否支持**Seek**，和**Supports(adIndex)**若要确定此提供程序是否支持索引的方法。 (例如， [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)支持**Seek**和**索引**。)  
  
 如果**Seek**功能不查找所需的行，没有错误发生，以及行是否定位在的结尾**记录集**。 设置**索引**为之前执行此方法所需索引的属性。  
  
 此方法仅支持服务器端游标。 查找时不支持[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性值**记录集**对象是**adUseClient**。  
  
 可以使用此方法时，才**记录集**对象使用打开[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值**adCmdTableDirect**。  
  
## <a name="filtering-the-results"></a>筛选结果  
 **查找**方法将搜索限制为一个字段的内容。 **Seek**方法要求你有索引，并且具有其他限制以及。 如果你必须搜索不是索引的基础的多个字段，或如果你的提供程序不支持索引，则可以通过使用来限制结果**筛选器**属性**记录集**对象。  
  
 使用**筛选器**属性可以有选择地剔除中记录**记录集**对象。 将筛选**记录集**将成为当前光标，意味着记录不满足**筛选器**条件中均不提供**记录集**之前**筛选器**中删除。 返回基于当前光标值其他属性会受到影响，如**AbsolutePosition**， **AbsolutePage**， **RecordCount**，和**PageCount**。 这是因为设置**筛选器**为特定值的属性会将当前记录移到满足的新值的第一个记录。  
  
 **筛选器**属性采用 variant 参数。 此值表示使用的三种方法之一**筛选器**属性： string 条件**FilterGroupEnum**常量或数组的书签。 有关详细信息，请参阅本主题后面的筛选条件字符串与、 与一个常量，筛选和用书签筛选。  
  
> [!NOTE]
>  在你知道你想要选择的数据时，它是通常更高效打开**记录集**与 SQL 语句有效地筛选结果集，而不是依靠**筛选器**属性。  
  
 若要删除筛选器从**记录集**，使用**adFilterNone**常量。 设置**筛选器**属性设置为零长度字符串 ("") 具有相同的效果与使用**adFilterNone**常量。  
  
### <a name="filtering-with-a-criteria-string"></a>使用条件字符串进行筛选  
 条件字符串包含窗体中的子句*FieldName 运算符值*(例如， `"LastName = 'Smith'"`)。 你可以通过串联与单个子句创建复合子句**AND** (例如， `"LastName = 'Smith' AND FirstName = 'John'"`) 和**或者**(例如， `"LastName = 'Smith' OR LastName = 'Jones'"`)。 条件字符串中使用以下准则：  
  
-   *FieldName*必须是来自有效字段名称**记录集**。 如果字段名称包含空格，必须将名称括在方括号中。  
  
-   *运算符*必须是以下之一：  **\<** ，  **>** ，  **\< =** ，  **>=**  **<>** ，  **=** ，或**如**。  
  
-   *值*是将与之比较的字段值的值 (例如， `'Smith'`， `#8/24/95#`， `12.345`，或`$50.00`)。 与字符串一起使用单引号 （'） 和井号 (`#`) 的日期。 对于数字，可以使用小数点、 美元符号和科学记数法。 如果*运算符*是**如**，*值*可以使用通配符。 只能星号 (\*) 和百分号 （%） 通配符允许使用字符，并且它们必须是字符串中的最后一个字符。 *值*不能为 null。  
  
    > [!NOTE]
    >  要包含在筛选器中的单引号 （'）*值*，使用两个单引号来表示一个。 例如，若要筛选*O'Malley*，条件字符串应该是`"col1 = 'O''Malley'"`。 若要包含在起点和筛选器值的末尾的单引号，请将字符串括在井号 （#）。 例如，若要筛选*'1'*，条件字符串应该是`"col1 = #'1'#"`。  
  
 没有之间没有优先**AND**和**或**。 可以对子句进行分组，这在括号内。 但是，你不能分组子句通过联接**或**然后加入组通过 AND，另一个子句，如下所示。  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 相反，将按以下方式构造此筛选器。  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 在**如**子句中，你可以在起点和模式的末尾使用通配符 (例如， `LastName Like '*mit*'`) 或仅在模式的末尾 (例如， `LastName Like 'Smit*'`)。  
  
### <a name="filtering-with-a-constant"></a>使用常量进行筛选  
 以下常量是可用于筛选**记录集**。  
  
|常量|Description|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|用于查看仅由最后一个受影响的记录的筛选器**删除**，**重新同步**， **UpdateBatch**，或**执行**调用。|  
|**adFilterConflictingRecords**|用于查看失败的最后一个批处理更新的记录的筛选器。|  
|**adFilterFetchedRecords**|用于查看当前的缓存中的记录的筛选器 — 也就是说，若要从数据库检索记录的最后一个调用的结果。|  
|**adFilterNone**|移除当前筛选器并还原所有记录以进行查看。|  
|**adFilterPendingRecords**|用于查看仅记录的筛选器的已更改但尚未发送到服务器。 仅适用于批处理更新模式。|  
  
 筛选器常量更加轻松地解决期间，它允许你查看，例如，仅这些记录的批更新模式下的各个记录冲突期间最后受影响**UpdateBatch**方法调用，如中所示下面的示例。  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>使用书签进行筛选  
 最后，将传递到的书签的 variant 数组**筛选器**属性。 所得到的游标将包含其书签传递给属性的那些记录。 下面的代码示例从记录中创建的书签数组**记录集**"B"进行*ProductName*字段。 然后将其传递到的数组**筛选器**有关生成筛选的属性并显示信息**记录集**。  
  
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
  
## <a name="creating-a-clone-of-a-recordset"></a>创建一个克隆的记录集  
 使用**克隆**方法来创建多个重复**记录集**对象，尤其是如果你想要维护多个给定的一组记录中的当前记录。 使用**克隆**方法是比创建并打开新更高效**记录集**具有与原始相同的定义对象。  
  
 新创建的克隆的当前记录最初设置为第一条记录。 中对克隆的当前记录指针**记录集**不同步与原始，反之亦然。 你可以在每个独立导航**记录集**。  
  
 对一个所做的更改**记录集**对象中是可见的所有克隆无论何种游标类型。 但是，之后执行[Requery](../../../ado/reference/ado-api/requery-method.md)上原始**记录集**，克隆人的进攻将不再同步到原始。  
  
 关闭原始**记录集**不会关闭其副本，也不会关闭副本关闭原始对象或任何其他副本。  
  
 您可以克隆**记录集**仅对象是否支持书签。 书签值是可互换;即，从一个的书签引用**记录集**对象是指任何个克隆中的同一记录。

