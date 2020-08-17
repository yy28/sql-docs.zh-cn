---
description: UnknownMember (MDX)
title: UnknownMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0489556836b943ba91d4e17b3a164aeca0c648d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341143"
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
 Analysis Services 创建一个未知成员，以便在层次结构未知时将事实数据表数据与层次结构相关联。 未知成员可位于下列级别之一：  
  
-   位于未聚合的属性层次结构的顶级。  
  
-   在自然层次结构的 " **所有** " 级别下的第一个级别。  
  
-   位于非自然层次结构的任何一级。  
  
 如果指定了成员表达式，则 **UnknownMember** 函数返回指定成员的未知成员子级。 如果指定的成员不存在，该函数将返回空。  
  
 如果指定了层次结构表达式，则 **UnknownMember** 函数将在顶级返回未知成员（如果存在）。  
  
 如果级别或成员中不存在未知成员，则 **UnknownMember** 函数将创建 null 成员。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
