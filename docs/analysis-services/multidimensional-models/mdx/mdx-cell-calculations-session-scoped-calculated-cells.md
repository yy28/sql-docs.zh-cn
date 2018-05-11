---
title: 创建会话作用域计算单元格 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c1681e8843686f0f5e2e4abf474a401733ce4396
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-cell-calculations---session-scoped-calculated-cells"></a>MDX 单元计算-会话作用域的计算单元
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
    
> [!IMPORTANT]  
>  已不推荐使用此语法。 应当改用 MDX 赋值。 有关分配的详细信息，请参阅[基本 MDX 脚本 (MDX)](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)。  
  
 若要创建适用于同一会话中的所有查询的计算单元，请使用 [CREATE CELL CALCULATION](../../../mdx/mdx-data-definition-create-cell-calculation.md) 语句或 [ALTER CUBE](../../../mdx/mdx-data-definition-alter-cube.md) 语句。 这两个语句的结果相同。  
  
## <a name="create-cell-calculation-syntax"></a>CREATE CELL CALCULATION 语法  
  
> [!IMPORTANT]  
>  已不推荐使用此语法。 应当改用 MDX 赋值。 有关分配的详细信息，请参阅[基本 MDX 脚本 (MDX)](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)。  
  
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
>  已不推荐使用此语法。 应当改用 MDX 赋值。 有关分配的详细信息，请参阅[基本 MDX 脚本 (MDX)](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)。  
  
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
|级别成员集|解析为单个级别的成员的 MDX 集表达式。 有关于此的示例，请参见 Level_Expression **Members** MDX 函数。 若要包括计算成员，请使用 Level_Expression **AllMembers** MDX 函数。<br /><br /> 有关详细信息，请参阅 [AllMembers (MDX)](../../../mdx/allmembers-mdx.md)。|  
|后代集|解析为指定成员的后代的 MDX 集表达式。 有关于此的示例，请参见 **Descendants**(Member_Expression、Level_Expression、Desc_Flag) MDX 函数。<br /><br /> 有关详细信息，请参阅 [Descendants (MDX)](../../../mdx/descendants-mdx.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [在 MDX & #40; 生成单元计算MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)  
  
  
