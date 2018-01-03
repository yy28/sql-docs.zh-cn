---
title: "筛选属性 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::Filter
helpviewer_keywords: Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3732e0820c0c258074e2a8b76d35c4af94a8c8a5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="filter-property"></a>筛选器属性
指示数据中的筛选器[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**Variant**值，该值可以包含以下项之一：  
  
-   **条件字符串**??? 一个或多个串联在一起的单个子句组成的字符串**AND**或**OR**运算符。  
  
-   **数组的书签**??? 唯一的书签的数组值中的记录到该点**记录集**对象。  
  
-   A [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)值。  
  
## <a name="remarks"></a>Remarks  
 使用**筛选器**属性可以有选择地剔除中记录**记录集**对象。 将筛选**记录集**将成为当前光标。 其他返回值的属性取决于当前**光标**受到影响，如[AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)， [AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)， [RecordCount 属性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)，和[PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)。 这是因为设置**筛选器**为特定值的属性会将当前记录移到满足的新值的第一个记录。  
  
 条件字符串形式的子句组成*FieldName 运算符值*(例如， `"LastName = 'Smith'"`)。 你可以通过串联与单个子句创建复合子句**AND** (例如， `"LastName = 'Smith' AND FirstName = 'John'"`) 或**OR** (例如， `"LastName = 'Smith' OR LastName = 'Jones'"`)。 条件字符串中使用以下准则：  
  
-   *FieldName*必须是来自有效字段名称**记录集**。 如果字段名称包含空格，必须将名称括在方括号中。  
  
-   运算符必须是以下项之一： \<，>， \<=、 > =、 <>、 =、 或**如**。  
  
-   值是将与之比较的字段值的值 (例如，Smith，#8/24/&#95; 12.345 或 50.00 美元)。 使用字符串和日期的井号 （#） 中使用单引号。 对于数字，可以使用小数点、 美元符号和科学记数法。 如果运算符**如**，值可以使用通配符。 允许的星号 （*） 和百分号 （%） 通配符，并且它们必须是字符串中的最后一个字符。 值不能为空。  
  
> [!NOTE]
>  若要在筛选器值中包含单引号 （'），请使用两个单引号来表示一个。 例如，若要筛选 O'Malley，条件字符串应该是"col1 = O Malley"。 若要包含在起点和筛选器值的末尾的单引号，括起字符串加上井号 （#）。 例如，若要筛选 '1' 上，则条件字符串应为"col1 = '1' # #"。  
  
-   没有之间没有优先 AND 和或。 可以对子句进行分组，这在括号内。 但是，不能通过 OR 联接子句进行分组，然后将组加入到另一个子句的 AND，如下：`(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   相反，将构造此筛选器设置为`(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   在**如**子句中，你可以在起点和模式的末尾使用通配符 (例如，姓氏类似 * mit\*)，或只会在模式的结束 (例如，姓氏类似 Smit\*)。  
  
 筛选器常量更加轻松地解决期间，它允许你查看，例如，仅这些记录的批更新模式下的各个记录冲突期间最后受影响[UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)方法调用。  
  
 将 Filter 属性本身设置可能会失败因为与基础数据冲突 （例如，另一个用户已删除记录）。 在这种情况下，该提供程序返回警告记录到[错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)集合但不是会停止程序执行。 只有在所有请求的记录上冲突，则会发生运行时错误。 使用[状态属性 （ADO 记录集）](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性可以查找具有冲突的记录。  
  
 设置**筛选器**属性设置为零长度字符串 ("") 具有相同的效果与使用**adFilterNone**常量。  
  
 每当**筛选器**设置属性，则当前记录位置移动到中的记录的筛选子集的第一个记录**记录集**。 同样，当**筛选器**清除属性，则当前记录位置移动到第一条记录**记录集**。  
  
 当**记录集**根据某些变量类型 (例如，sql_variant) 错误的字段上筛选条件字符串中使用的字段和筛选器值的子类型不匹配时，将导致 （DISP_E_TYPEMISMATCH 或 80020005）。 例如，如果**记录集**对象 (rs) 包含 sql_variant 类型的列 (C) 并且已在此列的字段分配值为 1 个 I4 类型，设置 rs 条件字符串。筛选器 ="C = 'A'"的字段将生成错误在运行时。 但是，rs。筛选器 ="C = 2"在同一应用字段将不会生成任何错误，尽管该字段将筛选出当前的记录集。  
  
 请参阅[书签属性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)书签可以从中生成一个数组，若要使用的筛选器属性的值的说明的属性。  
  
 仅筛选条件字符串的形式 (例如订购日期 >"12/31/1999年) 会影响的持久化内容**记录集**。 使用书签的数组来创建筛选器或使用从 FilterGroupEnum 值将不会影响的持久内容**记录集**。 这些规则适用于创建与客户端或服务器端游标的记录集。  
  
> [!NOTE]
>  当你将 adFilterPendingRecords 标志应用于筛选和修改**记录集**在批处理更新模式中，所产生的**记录集**如果筛选基于的键字段，则为空键字段值进行了单键表和修改。 所产生的**记录集**将为非空如果下列之一为 true:  
  
-   基于单键表中的非键字段筛选。  
  
-   基于多个键表中的任何字段筛选。  
  
-   单键表中的非键字段进行修改。  
  
-   在多个键表中的任何字段上做了修改。  
  
 下表总结了的效果**adFilterPendingRecords**的筛选和修改的不同组合中。 左列显示可能修改;可在任何非键字段、 单键表中的键字段上或在多个键表中的键字段任一上进行修改。 最上面一行显示的筛选条件;筛选可以基于任何非键字段中，单键控表，或任何多个键表中的键字段中的键字段。 相交的单元格显示结果: + 意味着该应用**adFilterPendingRecords**导致非空**记录集**;-意味着一个空**记录集**。  
  
||非键|单个键|多个密钥|  
|-|--------------|----------------|-------------------|  
|**非键**|+|+|+|  
|**单个键**|+|-|N/A|  
|**多个密钥**|+|N/A|+|  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [筛选器和 RecordCount 属性示例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
 [筛选器和 RecordCount 属性示例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Optimize 属性 - 动态 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
