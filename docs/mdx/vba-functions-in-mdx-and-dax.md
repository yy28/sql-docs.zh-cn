---
title: "MDX 和 DAX 中的 VBA 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/30/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 420452fd-9507-4093-8857-71d3e70d96cc
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 6356a6c841072490e10f9c32933606010ce0b9f9
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 和 DAX 中的 VBA 函数
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  本文档包含所有 VBA 函数中可用的交叉的引用[应用程序函数的 Visual Basic](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) ，支持在 MDX 中; 此外，该列表包含注释，使用 DAX 语言的功能等效性时.  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 函数引用  
  
|函数名称|Supported|说明|  
|-------------------|---------------|-----------|  
|Abs|DAX、MDX||  
|Array|不支持||  
|Asc|仅 MDX||  
|AscW|仅 MDX||  
|Atn|仅 MDX||  
|CallByName|不支持||  
|CBool|仅 MDX||  
|CByte|仅 MDX||  
|CCur|仅 MDX||  
|Cdate|仅 MDX||  
|CDbl|仅 MDX||  
|CDec|仅 MDX||  
|Choose|仅 MDX||  
|Chr|仅 MDX||  
|CInt|仅 MDX||  
|CLng|仅 MDX||  
|CLngLng|不支持||  
|CLngPtr|不支持||  
|Command|不支持||  
|Cos|仅 MDX||  
|CreateObject|不支持||  
|CSng|仅 MDX||  
|CStr|仅 MDX||  
|CurDir|不支持||  
|CVar|仅 MDX||  
|CVErr|不支持||  
|日期|仅 MDX|**警告**DAX 实现不同的函数具有相同名称; 用来从给定的自变量生成日期类型值的日期 （年、 月、 日） 函数|  
|DateAdd|仅 MDX|**警告**DAX 实现不同的函数具有相同名称; DATEADD (\<日期 >，< number_of_intervals >\<间隔 >) 函数，用于移动给定的日期由大量给定的时间间隔|  
|DateDiff]|仅 MDX||  
|DatePart|仅 MDX||  
|DateSerial|仅 MDX||  
|DateValue]|DAX、MDX||  
|Day|DAX、MDX||  
|DDB|仅 MDX||  
|Dir|不支持||  
|DoEvents|不支持||  
|Environ|不支持||  
|EOF|不支持||  
|错误|不支持||  
|Exp|DAX、MDX||  
|FileAttr|不支持||  
|FileDateTime|不支持||  
|FileLen|不支持||  
|筛选|不支持|**警告**MDX 实现不同的函数具有相同的名称; 筛选器 （值赋，Logical_Expression） 函数返回筛选基于搜索条件从给定的自变量的指定的集后得到的集<br /><br /> **警告**DAX 实现不同的函数具有相同名称; 筛选器 (\<表 >，\<筛选器 >) 函数返回表示另一个表或从给定的自变量的表达式的一个子集的表|  
|Fix|仅 MDX||  
|Format  (Visual Basic for Applications)|DAX、MDX||  
|FormatCurrency|不支持||  
|FormatDateTime|不支持||  
|FormatNumber|不支持||  
|FormatPercent|不支持||  
|FreeFile|不支持||  
|FV|仅 MDX||  
|GetAllSettings|不支持||  
|GetAttr|不支持||  
|GetObject|不支持||  
|GetSetting|不支持||  
|Hex|仅 MDX||  
|Hour|DAX、MDX||  
|Iif|仅 MDX|**警告**DAX 实现具有名称的类似函数： 如果 （满足，value_if_true，value_if_false） 函数。|  
|IMEStatus|不支持||  
|輸入|不支持||  
|InputBox|不支持||  
|InStr|仅 MDX||  
|InStrRev|不支持||  
|int|DAX、MDX||  
|IPmt|仅 MDX||  
|IRR|仅 MDX||  
|IsArray|仅 MDX||  
|仅 IsDateMDX||  
|IsEmpty|仅 MDX||  
|IsError|DAX、MDX||  
|IsMissing|仅 MDX||  
|IsNull|仅 MDX||  
|IsNumeric|仅 MDX||  
|IsObject|不支持||  
|Join|不支持||  
|LBound|不支持||  
|LCase|仅 MDX||  
|Left|DAX、MDX||  
|Len|DAX、MDX||  
|Loc|不支持||  
|LOF|不支持||  
|日志|仅 MDX|**重要**DAX 实现不同的函数具有相同名称; 日志 (数字，base) 函数。 从给定参数返回指定底数的数字的对数。|  
|LTrim|仅 MDX||  
|MacID|不支持||  
|MacScript|不支持||  
|Mid|DAX、MDX||  
|Minute|DAX、MDX||  
|MIRR|仅 MDX||  
|Month|DAX、MDX||  
|MonthName|不支持||  
|MsgBox|不支持||  
|现在|DAX、MDX||  
|NPer]|仅 MDX||  
|NPV|仅 MDX||  
|Oct|仅 MDX||  
|分区|仅 MDX||  
|Pmt|仅 MDX||  
|PPmt|仅 MDX||  
|PV|仅 MDX||  
|QBColor|仅 MDX||  
|Rate|仅 MDX||  
|替换|不支持||  
|RGB|仅 MDX||  
|Right|DAX、MDX||  
|Rnd|仅 MDX||  
|舍入|DAX、MDX||  
|RTrim|仅 MDX||  
|第二个|DAX、MDX||  
|Seek|不支持||  
|Sgn|DAX、MDX||  
|Shell|不支持||  
|Sin|仅 MDX||  
|SLN|仅 MDX||  
|Space|仅 MDX||  
|Spc|不支持||  
|Split|不支持||  
|Sqr|仅 MDX||  
|Str|仅 MDX||  
|StrComp|仅 MDX||  
|StrConv|仅 MDX||  
|String]|仅 MDX||  
|StrReverse|不支持||  
|开关|仅 MDX||  
|SYD|仅 MDX||  
|选项卡|不支持||  
|Tan|仅 MDX||  
|Time|不支持||  
|Timer|仅 MDX||  
|TimeSerial|仅 MDX||  
|TimeValue|DAX、MDX||  
|Trim]|DAX、MDX||  
|TypeName|仅 MDX||  
|UBound|不支持||  
|UCase|仅 MDX||  
|Val|仅 MDX||  
|VarType|不支持||  
|Weekday|DAX、MDX||  
|WeekdayName|不支持||  
|Year|DAX、MDX||  
  
  
