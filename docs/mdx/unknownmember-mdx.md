---
title: UnknownMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 84eda6f42b674ebde8793605816f98e82af350d8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065039"
---
# <a name="unknownmember-mdx"></a>UnknownMember (MDX)


  返回与级别或成员相关联的未知成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member expression syntax  
Member_Expression.UnknownMember  
  
Hierarchy_expression syntax  
Hierarchy_Expression.UnknownMember  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 Analysis Services 将创建一个未知的成员，若要将事实数据表数据与层次结构相关联的层次结构未知时。 未知成员可位于下列级别之一：  
  
-   位于未聚合的属性层次结构的顶级。  
  
-   在下面的第一级**所有**自然层次结构级别。  
  
-   位于非自然层次结构的任何一级。  
  
 如果指定成员表达式，则**UnknownMember**函数返回指定成员的未知的成员子级。 如果指定的成员不存在，该函数将返回空。  
  
 如果指定的层次结构表达式，则**UnknownMember**函数返回在顶级的未知的成员，如果存在。  
  
 如果级别或成员，不存在未知的成员**UnknownMember**函数创建一个空成员。  
  
> [!NOTE]  
>  如果层次结构或成员中不存在未知成员，将生成一个错误。  
  
## <a name="examples"></a>示例  
 下面的示例为 Measures 维度的所有成员返回 Product 属性层次结构中 All Products 成员的未知成员。  
  
```  
SELECT [Product].[Product].[All Products].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
 下面的示例为 Measures 维度的所有成员返回 Product Categories 层次结构的未知成员。  
  
```  
SELECT [Product].[Product Categories].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
