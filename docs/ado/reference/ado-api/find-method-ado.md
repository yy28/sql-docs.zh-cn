---
title: Find 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e71776a43aa338246b4acb3b4d9f620c19234f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028128"
---
# <a name="find-method-ado"></a>Find 方法 (ADO)
搜索[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)满足指定的条件的行。 （可选） 可以指定搜索、 起始行和偏移量开始的行的方向。 找到的记录; 如果满足条件，则设置的当前行位置否则，将位置设置为的终点 （或起点）**记录集**。  
  
## <a name="syntax"></a>语法  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parameters  
 *条件*  
 一个**字符串**值，该值包含在搜索中指定要使用的列名称、 比较运算符和值的语句。  
  
 *SkipRows*  
 可选 *。* 一个**长**值，其默认值为零，用于指定从当前行的行偏移量或*启动*书签以开始执行搜索。 默认情况下，搜索将从当前行开始。  
  
 *SearchDirection*  
 可选 *。* 一个[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)值，该值指定搜索是否应在当前行或搜索的方向中的下一个可用行上开始。 结尾处停止时的不成功搜索**记录集**如果值为**adSearchForward**。 不成功搜索停止的开头**记录集**如果值为**adSearchBackward**。  
  
 *开始*  
 可选。 一个**变体**充当搜索的起始位置的书签。  
  
## <a name="remarks"></a>备注  
 仅包含单列的名称可能中指定*条件*。 此方法不支持多列搜索。  
  
 中的比较运算符*条件*可能是"**>**"（大于）、"**\<**"（小于）、"="（等于）"> ="（大于或等于）"< ="（小于或等于）、"<>"（不等于），或"like"（模式匹配）。  
  
 中的值*条件*可以是字符串、 浮点数或日期。 字符串值是使用单引号或"#"（数字符号） 标记分隔 (例如，"状态 = WA"或"状态 = #WA #")。 日期值以"#"（数字符号） 标记 (例如，"start_date > #7/22/97 #")。 这些值可以包含小时、 分钟和秒表示时间戳，但不是应包含毫秒或不会发生错误。  
  
 如果"like"比较运算符，字符串值可能包含一个星号 （*） 来找到的任何字符或子字符串的一个或多个匹配项。 例如，"等状态是\*"匹配 Maine 和马萨诸塞州。 前导和尾随星号还可用于查找的值中包含的子字符串。 例如，"等状态\*作为\*"匹配阿拉斯加州、 阿肯色州和马萨诸塞州。  
  
 星号可以仅在条件字符串末尾或开头和末尾条件字符串，使用上面所示。 您不能使用星号作为前导通配符 (* str')，或作为嵌入式的通配符 ('s\*r)。 这会导致错误。  
  
> [!NOTE]
>  如果在调用之前未设置当前行位置，将会出错**查找**。 设置行位置，例如任何方法[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)，在调用之前，应调用**查找**。  
  
> [!NOTE]
>  如果您调用**查找**上一个记录集和记录集中当前位置的方法是在最后一条记录或文件尾 (EOF)，您将找不到任何内容。 您需要调用**MoveFirst**方法将每个游标的位置当前设置为记录集的开头。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Find 方法示例 (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [索引属性](../../../ado/reference/ado-api/index-property.md)   
 [Optimize 属性-动态 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
