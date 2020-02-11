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
ms.openlocfilehash: 39a0db181f3b1d1a40af1a5fa27ba78366a9d2b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135022"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 和 DAX 中的 VBA 函数


  本文档包含在 MDX 支持的[Visual Basic for Applications 函数](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications)中提供的所有 VBA 函数的交叉引用;此外，此列表还包含与 DAX 语言的功能等效性时的注释。  
  
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
|CDate|仅 MDX||  
|CDbl|仅 MDX||  
|CDec|仅 MDX||  
|选择|仅 MDX||  
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
|Date|仅 MDX|**警告**DAX 实现了具有相同名称的不同函数;DATE （Year，Month，Day）函数，用于从给定参数生成日期类型值|  
|DateAdd|仅 MDX|**警告**DAX 实现了具有相同名称的不同函数;DATEADD （\<日期>，<number_of_intervals>，\<interval>）函数，用于按给定的时间间隔移位给定日期|  
|DateDiff|仅 MDX||  
|DatePart|仅 MDX||  
|DateSerial|仅 MDX||  
|DateValue|DAX、MDX||  
|日期|DAX、MDX||  
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
|“筛选器”|不支持|**警告**MDX 实现同名的不同函数;FILTER （Set_Expression，Logical_Expression）函数返回根据给定自变量中的搜索条件筛选指定集而生成的集<br /><br /> **警告**DAX 实现了具有相同名称的不同函数;FILTER （\<table>，\<Filter>）函数返回一个表，该表表示来自给定参数的另一个表或表达式的子集|  
|解决方法|仅 MDX||  
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
|Iif|仅 MDX|**警告**DAX 实现了类似于名称的函数： IF （logical_test、value_if_true、value_if_false）函数。|  
|IMEStatus|不支持||  
|输入|不支持||  
|InputBox|不支持||  
|InStr|仅 MDX||  
|InStrRev|不支持||  
|Int|DAX、MDX||  
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
|日志|仅 MDX|**重要提示**DAX 实现了具有相同名称的不同函数;日志（number，base）函数。 从给定参数返回指定底数的数字的对数。|  
|LTrim|仅 MDX||  
|MacID|不支持||  
|MacScript|不支持||  
|Mid|DAX、MDX||  
|分钟|DAX、MDX||  
|MIRR|仅 MDX||  
|月份|DAX、MDX||  
|MonthName|不支持||  
|MsgBox|不支持||  
|Now|DAX、MDX||  
|NPer|仅 MDX||  
|NPV|仅 MDX||  
|10 月|仅 MDX||  
|Partition|仅 MDX||  
|Pmt|仅 MDX||  
|PPmt|仅 MDX||  
|PV|仅 MDX||  
|QBColor|仅 MDX||  
|费率|仅 MDX||  
|将|不支持||  
|RGB|仅 MDX||  
|Right|DAX、MDX||  
|Rnd|仅 MDX||  
|Round|DAX、MDX||  
|RTrim|仅 MDX||  
|秒|DAX、MDX||  
|Seek|不支持||  
|Sgn|DAX、MDX||  
|Shell|不支持||  
|Sin|仅 MDX||  
|SLN|仅 MDX||  
|空格|仅 MDX||  
|Spc|不支持||  
|拆分|不支持||  
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
|时间|不支持||  
|计时器|仅 MDX||  
|TimeSerial|仅 MDX||  
|TimeValue|DAX、MDX||  
|Trim|DAX、MDX||  
|TypeName|仅 MDX||  
|UBound|不支持||  
|UCase|仅 MDX||  
|Val|仅 MDX||  
|VarType|不支持||  
|星期|DAX、MDX||  
|WeekdayName|不支持||  
|年龄|DAX、MDX||  
  
  
