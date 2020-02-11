---
title: 生成（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c7a6008129d6b0a4c59412428c31f6e5de625f1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005904"
---
# <a name="generate-mdx"></a>Generate (MDX)


  将一个集应用于另一个集中的每个成员，然后对得到的集求并集。 另外，此函数返回通过用字符串表达式对集求值而创建的串联字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set expression syntax  
Generate( Set_Expression1 ,  Set_Expression2 [ , ALL ]  )  
  
String expression syntax  
Generate( Set_Expression1 ,  String_Expression [ ,Delimiter ]  )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
 *String_Expression*  
 通常为指定集中每个元组当前成员名称 (CurrentMember.Name) 的有效字符串表达式。  
  
 *后面*  
 以字符串表达式表示的有效分隔符。  
  
## <a name="remarks"></a>备注  
 如果指定第二个集，则**生成**函数将返回一个集，该集通过将第二个集中的元组应用于第一个集中的每个元组，然后按 union 联接结果集。 如果指定**ALL** ，则函数将在结果集中保留重复项。  
  
 如果指定了字符串表达式，则**生成**函数将返回一个字符串，该字符串通过对第一个集中的每个元组计算指定的字符串表达式，然后连接结果。 根据需要，可以分隔字符串，从而分隔得到的串联字符串中的每个结果。  
  
## <a name="examples"></a>示例  
  
### <a name="set"></a>设置  
 在以下示例中，由于 [Date].[Calendar Year].[Calendar Year].MEMBERS 集中有四个成员，因此，查询四次返回包含 Measure Internet Sales Amount 的集：  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]}, ALL)  
ON 0  
FROM [Adventure Works]  
```  
  
 删除 ALL 将更改查询，这样仅返回一次 Internet Sales Amount：  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]})  
ON 0  
FROM [Adventure Works]  
```  
  
 "**生成**" 最常见的实际用法是在一组成员上对复杂集表达式（如 TopCount）进行求值。 以下示例查询显示行上每个日历年的前 10 种产品：  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS  
, TOPCOUNT(  
[Date].[Calendar Year].CURRENTMEMBER  
*  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount]))  
ON 1  
FROM [Adventure Works]  
```  
  
 请注意，每年显示不同的前10个，并且使用 "**生成**" 是获取此结果的唯一方法。 将日历年和前 10 种产品的集进行简单交叉联接将显示所有时间的前 10 种产品（每年都重复），如以下示例所示：  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS  
*   
TOPCOUNT(  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount])  
ON 1  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 下面的示例演示如何使用 "**生成**" 来返回字符串：  
  
```  
WITH   
MEMBER MEASURES.GENERATESTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME)  
MEMBER MEASURES.GENERATEDELIMITEDSTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME, " AND ")  
SELECT   
{MEASURES.GENERATESTRINGDEMO, MEASURES.GENERATEDELIMITEDSTRINGDEMO}  
ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  此形式的**生成**函数在调试计算时非常有用，因为这样可以返回一个字符串，其中显示了集中所有成员的名称。 对于[SetToStr &#40;MDX&#41;](../mdx/settostr-mdx.md)函数返回的集，这可能更易于读取。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
