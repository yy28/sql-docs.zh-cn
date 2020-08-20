---
description: SCOPE 语句 (MDX)
title: SCOPE 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4c9f6738b2d7e0764e750b25f09001b7e9d3864a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483860"
---
# <a name="mdx-scripting---scope"></a>MDX 脚本 - SCOPE


  将指定多维表达式 (MDX) 语句的作用域限制于指定的子多维数据集。  
  
## <a name="syntax"></a>语法  
  
```  
  
SCOPE(Subcube_Expression)   
   [ MDX_Statement ]  
END SCOPE  
  
Subcube_Expression ::=(Auxiliary_Subcube [, Auxiliary_Subcube,...n])  
  
Auxiliary_Subcube ::=   
        Limited_Set   
    | Root([dimension_name])   
    | Leaves([dimension_name])  
  
Limited_Set ::=   
        single_tuple   
    | member   
    | Common_Grain_Members   
    | hierarchy.members   
    | level.members   
    | {}   
    | Descendants  
            (  
                  Member  
         , [level  
         [  
            , SELF   
             | AFTER   
                          | BEFORE   
                          | SELF_AND_AFTER   
                          | SELF_AND_BEFORE   
                          | SELF_BEFORE_AFTER   
                          | LEAVES  
                  ]  
            )   
[* <limited set>]  
```  
  
## <a name="arguments"></a>参数  
 *Subcube_Expression*  
 有效的 MDX 子多维数据集表达式。  
  
 *MDX_Statement*  
 有效的 MDX 语句。  
  
 *Common_Grain_Members*  
 有效的 MDX 语句，该语句的值为粒度相同的成员。  
  
 *single_tuple*  
 单个元组。  
  
## <a name="remarks"></a>备注  
 SCOPE 语句用于确定执行一个或多个 MDX 语句时会影响到的子多维数据集。 除非 MDX 语句包含在 SCOPE 语句中，否则 MDX 语句的隐式作用域为整个多维数据集。  
  
> [!NOTE]  
>  SCOPE 语句会处理隐藏的成员。  
  
 SCOPE 语句将创建公开 "洞" 的子多维数据，而不考虑 **MDX 兼容性** 设置。 例如，`Scope( Customer.State.members )` 语句可以在不包含州的国家或地区中包括州，但在其他情况下会插入不可见的占位符成员。  
  
 在 SCOPE 语句中创建的计算成员和命名集不受 SCOPE 语句的影响。  
  
## <a name="example"></a>示例  
 下面的示例（来自艾德公司示例解决方案中的 MDX 计算脚本）将当前范围定义为会计年度2005中的会计季度和销售配额度量值，然后使用 **ParallelPeriod** 函数将值分配给当前范围中的单元格。 然后，该示例使用其他 SCOPE 语句修改作用域，然后使用 [This (MDX) ](../mdx/this-mdx.md) 函数执行其他分配。  
  
```  
Scope   
 (   
    [Date].[Fiscal Year].&[2005],  
    [Date].[Fiscal].[Fiscal Quarter].Members,  
    [Measures].[Sales Amount Quota]  
 ) ;     
  
   This = ParallelPeriod                               
          (   
             [Date].[Fiscal].[Fiscal Year], 1,  
             [Date].[Fiscal].CurrentMember   
          ) * 1.35 ;  
  
/*-- Allocate equally to months in FY 2002 -----------------------------*/  
  
  Scope   
  (   
     [Date].[Fiscal Year].&[2002],  
     [Date].[Fiscal].[Month].Members   
  ) ;     
  
    This = [Date].[Fiscal].CurrentMember.Parent / 3 ;     
  
  End Scope ;     
End Scope ;     
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 脚本编写语句 (MDX)](../mdx/mdx-scripting-statements-mdx.md)  
  
  
