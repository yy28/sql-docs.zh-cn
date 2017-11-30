---
title: "MDX 和 DAX 中的 VBA 函数 |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 420452fd-9507-4093-8857-71d3e70d96cc
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: e56f0c499f16242d3dc6332ee62824c3542d9dd1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 和 DAX 中的 VBA 函数
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  本文档包含所有 VBA 函数中可用的交叉的引用[Microsoft Visual Basic for Applications 语言参考适用于 Office 2010](https://msdn.microsoft.com/library/gg264383(v=office.14).aspx) ，支持在 MDX 中; 此外，该列表包含注释，使用 DAX 语言的功能等效性时。  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 函数引用  
  
|函数名称|是否支持|说明|  
|-------------------|---------------|-----------|  
|[Abs](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007544&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[数组](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007545&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Asc](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007546&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[AscW](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007546&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[Atn](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007547&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[CallByName](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007548&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[CBool](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CByte](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CCur](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CDate](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CDbl](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CDec](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[选择](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007549&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[Chr 使用](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007550&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[CInt](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CLng](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CLngLng](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|不支持||  
|[CLngPtr](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|不支持||  
|[Command](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007551&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Cos](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007553&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[CreateObject](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007554&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[CSng](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CStr](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CurDir](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007555&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[CVar](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007662&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&CTT=5&origin=HV080007552)|仅 MDX||  
|[CVErr](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007556&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[日期](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007557&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX|**\*\*警告\* \***  DAX 实现不同的函数具有相同名称; 用来从给定的自变量生成日期类型值的日期 （年、 月、 日） 函数|  
|[DateAdd](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007558&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX|**\*\*警告\* \***  DAX 实现不同的函数具有相同名称; DATEADD (\<日期 >，< number_of_intervals >\<间隔 >) 函数，用于移动给定的日期由大量给定的时间间隔|  
|[DateDiff](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007559&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[DatePart](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007560&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[DateSerial](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007561&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[DateValue](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007562&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[Day](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007563&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[DDB](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007564&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[Dir](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007566&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[DoEvents](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007567&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Environ](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007568&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[EOF](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007569&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[错误](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007570&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Exp](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007571&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[FileAttr](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007572&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[FileDateTime](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007573&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[FileLen](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007574&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Filter](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007575&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持|**\*\*警告\* \***  MDX 实现不同的函数具有相同的名称; 筛选器 （值赋，Logical_Expression） 函数返回筛选基于搜索条件从给定的自变量的指定的集后得到的集<br /><br /> **\*\*警告\* \***  DAX 实现不同的函数具有相同名称; 筛选器 (\<表 >，\<筛选器 >) 函数返回表示另一个表或从给定的自变量的表达式的一个子集的表|  
|[修复](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007595&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[格式 (Visual Basic for Applications)](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007576&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[FormatCurrency](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007577&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[FormatDateTime](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007578&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[FormatNumber](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007579&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[FormatPercent](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007580&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[可](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007581&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[FV](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007582&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[GetAllSettings](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007583&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[GetAttr](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007584&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[GetObject](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007585&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[GetSetting](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007586&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[十六进制](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007587&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[小时](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007588&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[Iif](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007589&lcid=1033&NS=EXCEL.DEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX|**\*\*警告\* \***  DAX 实现具有名称的类似函数： 如果 （满足，value_if_true，value_if_false） 函数。|  
|[IMEStatus](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007590&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[输入](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007591&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[InputBox](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007592&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[InStr](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007593&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[InStrRev](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007594&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Int](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007595&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[IPmt](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007596&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[IRR](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007597&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[IsArray](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007598&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[IsDate](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007599&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[IsEmpty](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007600&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[IsError](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007601&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[IsMissing](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007602&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[IsNull](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007603&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[IsNumeric](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007604&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[IsObject](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007605&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[联接](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007606&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[LBound](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007607&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[LCase](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007608&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[左](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007609&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[Len](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007610&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[Loc](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007611&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[LOF](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007612&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[日志](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007613&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX|**\*\*重要\* \***  DAX 实现不同的函数具有相同名称; 日志 (数字，base) 函数。 从给定参数返回指定底数的数字的对数。|  
|[LTrim](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007614&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[MacID](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007615&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[MacScript](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007616&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Mid](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007618&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[分钟](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007619&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[MIRR](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007620&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[月](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007621&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[月份名称](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007622&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[MsgBox](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007623&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[现在](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007624&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[NPer](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007625&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[NPV](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007626&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[年 10 月](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007627&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[分区](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007628&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[Pmt](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007629&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[PPmt](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007630&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[PV](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007631&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[QBColor](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007632&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[速率](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007633&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[替换](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007634&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[RGB](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007635&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[右](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007636&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[Rnd](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007637&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[舍入](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007638&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|**RTrim**|仅 MDX||  
|[第二个](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007639&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[查找](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007640&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Sgn](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007641&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[Shell](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007642&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Sin](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007643&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[SLN](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007644&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[空间](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007645&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[Spc](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007646&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Split](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007647&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Sqr](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007648&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[Str](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007649&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[StrComp](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007650&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[StrConv](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007651&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[字符串](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007652&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[StrReverse](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007653&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[开关](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007654&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[SYD](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007655&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[选项卡](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007656&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[Tan](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007657&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[Time](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007658&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[计时器](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007659&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[TimeSerial](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007660&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[TimeValue](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007661&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[Trim](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007614&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[类型名称](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007663&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[UBound](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007664&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[UCase](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007665&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[Val](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007666&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|仅 MDX||  
|[VarType](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007667&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[工作日](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007668&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
|[WeekdayName](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007669&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|不支持||  
|[年](http://office.microsoft.com/client/helppreview14.aspx?AssetId=HV080007670&lcid=1033&NS=EXCEL%2EDEV&Version=14&tl=2&pid=CH080007543&CTT=4)|DAX、MDX||  
  
  
