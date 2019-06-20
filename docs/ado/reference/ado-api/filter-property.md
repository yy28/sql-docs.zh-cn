---
title: 筛选器属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5d68f0e74e4bbfb275cbe23641c72eca4c941559
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697963"
---
# <a name="filter-property"></a>Filter 属性
指示数据中的筛选器[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>设置和返回值

设置或返回**变体**值，该值可以包含以下各项之一：  
  
-   **条件字符串：** 一个或多个串联在一起，多个子句组成的字符串**AND**或**OR**运算符。  
  
-   **书签的数组：** 唯一的书签的数组值中的记录到那个**记录集**对象。  
  
-   一个[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)值。  
  
## <a name="remarks"></a>备注

使用**筛选器**属性可有选择地筛选掉中的记录**记录集**对象。 筛选**记录集**将成为当前光标。 其他属性的返回值取决于当前**游标**受到影响，如[AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)， [AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)， [RecordCount 属性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)，并[PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)。 设置**筛选器**为特定的新值的属性将当前记录移至满足新值的第一个记录。
  
条件字符串由窗体中的子句组成*FieldName 运算符值*(例如， `"LastName = 'Smith'"`)。 可以通过连接与多个子句来创建复合子句**AND** (例如， `"LastName = 'Smith' AND FirstName = 'John'"`) 或**OR** (例如， `"LastName = 'Smith' OR LastName = 'Jones'"`)。 对于条件字符串，请使用以下准则：

-   *FieldName*必须是有效的字段名称，从**记录集**。 如果字段名称包含空格，必须将名称括在方括号中。  
  
-   运算符必须是以下值之一： \<，>， \<=、 > =、 <>、 =、 或**如**。  
  
-   值是将与之比较的字段值的值 (例如，Smith，#8/24/95 # 12.345 或 50.00 美元)。 使用字符串和日期的井号 （#） 中使用单引号。 对于数字，可以使用小数点、 美元符号和科学记数法。 如果运算符**如**，值可以使用通配符。 仅使用星号 （*） 和百分号 （%）可以使用通配符，并且它们必须是字符串中的最后一个字符。 值不能为空。  
  
> [!NOTE]
>  若要在筛选器值中包含单引号 （'），请使用两个单引号来表示一个。 例如，若要筛选上 O'Malley，条件字符串应为`"col1 = 'O''Malley'"`。 若要包含在开头和筛选器值结束的单引号，请将字符串加上井号 （#）。 例如，若要筛选 '1' 上，条件字符串应为`"col1 = #'1'#"`。  
  
-   没有之间没有优先级 AND 和或。 子句可以在括号内进行分组。 但是，不能通过 OR 联接子句进行分组，然后将组联接到另一个子句通过 AND，如以下代码段所示：  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   相反，您将构造此筛选器设置为  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   在中**如**子句中，你可以使用通配符开头和结尾的模式。 例如，可以使用`LastName Like '*mit*'`。 或使用**如**只能在模式的末尾使用通配符。 例如， `LastName Like 'Smit*'` 。  
  
 筛选器常量使其更轻松地解决个别记录冲突期间通过允许您查看，例如，只有这些记录的批更新模式下受影响在最后一个[UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)方法调用。  
  
设置**筛选器**属性本身可能会因与基础数据发生冲突而失败。 例如，已由另一个用户删除记录时，可能发生此失败。 在这种情况下，访问接口将返回到的警告[错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不会停止程序执行。 仅当在所有请求的记录上不存在冲突，就会在运行时出错。 使用[Status 属性 （ADO 记录集）](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性来查找有冲突的记录。  
  
设置**筛选器**属性设置为零长度字符串 ("") 具有与使用相同的效果**adFilterNone**常量。
  
每当**筛选器**属性设置，当前记录位置移动到中的记录的筛选子集的第一条记录**记录集**。 同样，当**筛选器**清除属性，则将当前记录位置将移动到的第一个记录**记录集**。

假设**记录集**根据一些变量的类型，如类型为 sql_variant 的字段筛选。 错误 (DISP_E_TYPEMISMATCH 或 80020005) 条件字符串中使用的字段和筛选器值的子类型不匹配时发生。 例如，假设：

- 一个**记录集**对象 (rs) 包含 sql_variant 类型的列 (C)。
- 并且此列的字段已分配 1 个 I4 类型的值。 条件字符串设置为`rs.Filter = "C='A'"`字段上。

此配置会在运行时生成错误。 但是，`rs.Filter = "C=2"`应用在同一个字段将不会生成任何错误。 和字段筛选出当前记录集。

请参阅[书签属性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)可以从中生成要使用的筛选器属性的数组的书签值的说明的属性。

仅条件字符串的形式中的筛选器影响的内容的持久化**记录集**。 条件字符串的一个示例是`OrderDate > '12/31/1999'`。 使用书签，或使用中的值的数组创建的筛选器**FilterGroupEnum**，不会影响的内容的持久**记录集**。 这些规则适用于使用客户端或服务器端游标创建记录集。
  
> [!NOTE]
>  当您将 adFilterPendingRecords 标志应用于筛选和修改**记录集**在批更新模式中，所产生的**记录集**如果筛选的基础的键字段为空单键表并修改了键字段值。 所产生的**记录集**将为非空如果以下语句之一为 true:  
  
-   基于单个键表中的非键字段的筛选。  
  
-   基于多个键表中的任何字段的筛选。  
  
-   单键表中的非键字段进行了修改。  
  
-   在多个键表中的任何字段上进行了修改。  
  
下表总结了的效果**adFilterPendingRecords**中筛选和修改的不同组合。 左侧的列显示了可能的修改。 可以在任何非键字段、 单键表中的键字段或任意多个键表中的键字段上进行修改。 最上面一行显示了筛选条件。 筛选可以基于任何非键字段中，单键控的表，或任意多个键表中的键字段中的键字段。 相交单元格显示的结果。 一个 **+** 加号意味着该应用**adFilterPendingRecords**导致非空**记录集**。 一个 **-** 减号表示空**记录集**。  
  
||非键|单个键|多个密钥|
|-|--------------|----------------|-------------------|
|**非键**|+|+|+|
|**单个键**|+|-|不可用|
|**多个密钥**|+|不可用|+|
|||||
  
## <a name="applies-to"></a>适用范围

[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅

[Filter 和 RecordCount 属性示例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[Filter 和 RecordCount 属性示例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
[Optimize 属性-动态 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
