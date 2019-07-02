---
title: MDX 和 DAX 中的 VBA 函数 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f6b6d89ced88a570ce242ae9490d4c6d8bd6ac8
ms.sourcegitcommit: 0b0f5aba602732834c8439c192d95921149ab4c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67500044"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 和 DAX 中的 VBA 函数


  本文档包含在可用的所有 VBA 函数的交叉的引用[Visual Basic for Applications 函数](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications)支持在 MDX 中; 此外，该列表包括一条注释功能上与 DAX 语言的等效时.  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 函数引用  
  
|函数名称|支持|说明|  
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
|Date|仅 MDX|**警告**DAX 实现同名的不同函数; DATE (Year，Month，Day) 函数，用于从给定参数生成一个 date 类型值|  
|DateAdd|仅 MDX|**警告**DAX 实现同名的不同函数; DATEADD (\<日期 >，< number_of_intervals >\<间隔 >) 函数，用于移动从给定的日期由数量的给定时间间隔|  
|DateDiff|仅 MDX||  
|DatePart|仅 MDX||  
|DateSerial|仅 MDX||  
|DateValue|DAX、MDX||  
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
|“筛选器”|不支持|**警告**MDX 实现同名的不同函数; FILTER （Set_Expression，Logical_Expression） 函数返回一组指定基于从给定参数的搜索条件筛选后得到的集<br /><br /> **警告**DAX 实现同名的不同函数名称; 在筛选器 (\<表 >，\<筛选器 >) 函数返回表示另一个表或从给定参数的表达式的子集的表|  
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
|Iif|仅 MDX|**警告**DAX 实现同名的类似函数：IF (logical_test，value_if_true，value_if_false) 函数。|  
|IMEStatus|不支持||  
|输入|不支持||  
|InputBox|不支持||  
|InStr|仅 MDX||  
|InStrRev|不支持||  
|smallint|DAX、MDX||  
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
|日志|仅 MDX|**重要**DAX 实现同名的不同函数名称; LOG (number，base) 函数。 从给定参数返回指定底数的数字的对数。|  
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
|NPer|仅 MDX||  
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
|String|仅 MDX||  
|StrReverse|不支持||  
|开关|仅 MDX||  
|SYD|仅 MDX||  
|Tab|不支持||  
|Tan|仅 MDX||  
|Time|不支持||  
|Timer|仅 MDX||  
|TimeSerial|仅 MDX||  
|TimeValue|DAX、MDX||  
|Trim|DAX、MDX||  
|TypeName|仅 MDX||  
|UBound|不支持||  
|UCase|仅 MDX||  
|Val|仅 MDX||  
|VarType|不支持||  
|Weekday|DAX、MDX||  
|WeekdayName|不支持||  
|Year|DAX、MDX||  
  
  
