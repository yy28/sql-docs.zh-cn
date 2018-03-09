---
title: "Find 方法 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: be29e1bc1126673f59dbd66f5f3c432b3ed2cc85
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="find-method-ado"></a>Find 方法 (ADO)
搜索[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)满足指定的条件的行。 （可选） 可以指定的搜索、 起始行和与起始行的偏移量的方向。 如果满足条件，则在找到记录; 设置当前行位置否则，该位置设置为的终点 （或起点）**记录集**。  
  
## <a name="syntax"></a>语法  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parameters  
 *条件*  
 A**字符串**值，该值包含在搜索中指定要使用的列名称、 比较运算符和值的语句。  
  
 *SkipRows*  
 Optional*.* A**长**值，其默认值为零，用于指定从当前行的行偏移量或*启动*书签以开始执行搜索。 默认情况下，搜索将开始在当前行。  
  
 *SearchDirection*  
 Optional*.* A [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)值，该值指定是否应在当前行或搜索方向的下一步可用行上开始的搜索。 结尾处停止时的不成功的搜索**记录集**如果值为**adSearchForward**。 在开始时停止失败搜索**记录集**如果值为**adSearchBackward**。  
  
 *开始*  
 選擇性。 A **Variant**充当搜索的起始位置的书签。  
  
## <a name="remarks"></a>注释  
 可以以指定仅包含单个列名称*条件*。 此方法不支持多列搜索。  
  
 中的比较运算符*条件*可能"**>**"（大于）、"**\<**"（小于）、"="（等于）、"> ="（大于或等于）"< ="（小于或等于）、"<>"（不等于），或"like"（模式匹配）。  
  
 中的值*条件*可能是字符串、 浮点数或日期。 字符串值不与单引号或"#"（数字符号） 标记分隔 (例如，"状态 = WA"或"状态 = #WA #")。 日期值分隔用"#"（数字符号） 标记 (例如，"start_date > #7/22/&#97;")。 这些值可以包含小时数、 分钟和秒以表示时间戳，但不是应包含毫秒或将发生错误。  
  
 如果"like"的比较运算符，字符串值可能包含一个星号 （*） 以找到一个或多个出现的任何字符或子字符串。 例如，"等状态正在\*"与缅因和麻省匹配。 前导和尾随星号还可用于查找的值中包含的子字符串。 例如，"状态，如\*作为\*"与阿拉斯加、 阿肯色和麻省。  
  
 星号可以仅在条件字符串末尾或开头和末尾的条件字符串中，使用上面所示。 不能将星号用作前导通配符 (* str)，或作为嵌入的通配符 ('s\*r)。 这会导致错误。  
  
> [!NOTE]
>  如果当前行位置不在调用之前设置，将出现错误**查找**。 设置行位置，如任何方法[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)，应在调用之前调用**查找**。  
  
> [!NOTE]
>  如果调用**查找**记录集和中记录集的当前位置上的方法是在最后一条记录或文件尾 (EOF)，您将无法找到任何内容。 你需要调用**MoveFirst**方法以设置每个光标的位置当前到记录集的开头。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [查找方法示例 (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [索引属性](../../../ado/reference/ado-api/index-property.md)   
 [优化属性的动态 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
