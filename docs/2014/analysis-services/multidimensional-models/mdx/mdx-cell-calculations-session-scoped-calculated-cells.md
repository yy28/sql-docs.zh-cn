---
title: 创建会话作用域的计算单元格 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1df213e83122d3d93a57c2bbdd131741043ffe7c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232087"
---
# <a name="creating-session-scoped-calculated-cells"></a>创建会话作用域的计算单元
    
> [!IMPORTANT]  
>  已不推荐使用此语法。 应当改用 MDX 赋值。 有关分配的详细信息，请参阅[基本 MDX 脚本 (MDX)](the-basic-mdx-script-mdx.md)。  
  
 若要创建适用于同一会话中的所有查询的计算单元，请使用 [CREATE CELL CALCULATION](/sql/mdx/mdx-data-definition-create-cell-calculation) 语句或 [ALTER CUBE](/sql/mdx/mdx-data-definition-alter-cube) 语句。 这两个语句的结果相同。  
  
## <a name="create-cell-calculation-syntax"></a>CREATE CELL CALCULATION 语法  
  
> [!IMPORTANT]  
>  已不推荐使用此语法。 应当改用 MDX 赋值。 有关分配的详细信息，请参阅[基本 MDX 脚本 (MDX)](the-basic-mdx-script-mdx.md)。  
  
 按照以下语法使用 CREATE CELL CALCULATION 语句定义会话作用域的计算单元：  
  
```  
CREATE CELL CALCULATION Cube_Expression.<CREATE CELL CALCULATION body clause>  
  
<CREATE CELL CALCULATION body clause> ::=CellCalc_Identifier FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
## <a name="alter-cube-syntax"></a>ALTER CUBE 语法  
  
> [!IMPORTANT]  
>  已不推荐使用此语法。 应当改用 MDX 赋值。 有关分配的详细信息，请参阅[基本 MDX 脚本 (MDX)](the-basic-mdx-script-mdx.md)。  
  
 按照以下语法使用 ALTER CUBE 语句定义会话作用域的计算单元：  
  
```  
ALTER CUBE Cube_Identifier CREATE CELL CALCULATION  
FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
 `String_Expression` 值包含一个正交、单维度 MDX 集表达式列表，每个表达式都必须解析为下表列出的集类别之一。  
  
|类别|Description|  
|--------------|-----------------|  
|空集|解析为空集的 MDX 集表达式。 在这种情况下，计算单元的作用域是整个多维数据集。|  
|单个成员集|解析为单个成员的 MDX 集表达式。|  
|级别成员集|解析为单个级别的成员的 MDX 集表达式。 这就*Level_Expression*。`Members` MDX 函数。 若要包括计算的成员，请使用*Level_Expression*。`AllMembers` MDX 函数。<br /><br /> 有关详细信息，请参阅 [AllMembers (MDX)](/sql/mdx/allmembers-mdx)。|  
|后代集|解析为指定成员的后代的 MDX 集表达式。 这就`Descendants`(*Member_Expression*， *Level_Expression*， *Desc_Flag*) MDX 函数。<br /><br /> 有关详细信息，请参阅 [Descendants (MDX)](/sql/mdx/descendants-mdx)。|  
  
## <a name="see-also"></a>请参阅  
 [构建在 MDX 中的单元格计算&#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
