---
description: UniqueName (MDX)
title: UniqueName (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3108cf8fdfbd0bc6864438be9ac95ff909308bc6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341163"
---
# <a name="uniquename-mdx"></a>UniqueName (MDX)


  返回指定的维度、层次结构、级别或成员的唯一名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
Dimension expression syntax  
Dimension_Expression.UniqueName  
  
Hierarchy expression syntax  
Hierarchy_Expression.UniqueName  
  
Level expression syntax  
Level_Expression.UniqueName  
  
Member expression syntax  
Member_Expression.UniqueName  
```  
  
## <a name="arguments"></a>参数  
 *Dimension_Expression*  
 解析为维度的有效多维表达式 (MDX)。  
  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **UniqueName**函数返回对象的唯一名称，而不是[name](../mdx/name-mdx.md)函数返回的名称。 返回的名称不包括多维数据集的名称。 返回的结果取决于服务器端设置或 MDX Unique Name Style 连接字符串属性。   
  
## <a name="example"></a>示例  
 下例将返回 Adventure Works 多维数据集中的 Product 维度、Product Categories 层次结构、Subcategory 级别和 Bike Racks 成员的唯一名称值。  
  
```  
WITH MEMBER DimensionUniqueName   
   AS [Product].UniqueName  
MEMBER HierarchyUniqueName   
   AS [Product].[Product Categories].UniqueName  
MEMBER LevelUniqueName   
   AS [Product].[Product Categories].[Subcategory].UniqueName  
MEMBER MemberUniqueName   
   AS [Product].[Product Categories].[Subcategory].[Bike Racks]  
SELECT   
   {DimensionUniqueName  
   , HierarchyUniqueName  
   , LevelUniqueName  
   , MemberUniqueName }  
   ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
