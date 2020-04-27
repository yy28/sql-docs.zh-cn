---
title: 创建会话作用域的计算单元 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4388ef278c0762184859162dc55f656aae1c9a15
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074431"
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
  
|类别|说明|  
|--------------|-----------------|  
|空集|解析为空集的 MDX 集表达式。 在这种情况下，计算单元的作用域是整个多维数据集。|  
|单个成员集|解析为单个成员的 MDX 集表达式。|  
|级别成员集|解析为单个级别的成员的 MDX 集表达式。 *Level_Expression*就是其中的一个示例。`Members` MDX 函数。 若要包括计算成员，请使用*Level_Expression*。`AllMembers` MDX 函数。<br /><br /> 有关详细信息，请参阅 [AllMembers (MDX)](/sql/mdx/allmembers-mdx)。|  
|后代集|解析为指定成员的后代的 MDX 集表达式。 `Descendants`这是（*Member_Expression*、 *Level_Expression* *Desc_Flag*） MDX 函数的一个示例。<br /><br /> 有关详细信息，请参阅 [Descendants (MDX)](/sql/mdx/descendants-mdx)。|  
  
## <a name="see-also"></a>另请参阅  
 [在 MDX 中生成单元格计算 (MDX)](../../multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
