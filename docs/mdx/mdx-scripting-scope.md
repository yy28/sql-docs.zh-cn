---
title: "SCOPE 语句 (MDX) |Microsoft 文档"
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
f1_keywords: SCOPE
dev_langs: kbMDX
helpviewer_keywords:
- scope [MDX]
- SCOPE statement
ms.assetid: ceab459d-b601-4468-b3fc-4f5bb4a1805f
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 9487e1e71916e07232eed6ee7f60c013f9598197
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-scripting---scope"></a>MDX 脚本编写的作用域
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>注释  
 SCOPE 语句用于确定执行一个或多个 MDX 语句时会影响到的子多维数据集。 除非 MDX 语句包含在 SCOPE 语句中，否则 MDX 语句的隐式作用域为整个多维数据集。  
  
> [!NOTE]  
>  SCOPE 语句会处理隐藏的成员。  
  
 作用域语句将创建子多维数据集，而不考虑公开"的漏洞" **MDX Compatibility**设置。 例如，`Scope( Customer.State.members )` 语句可以在不包含州的国家或地区中包括州，但在其他情况下会插入不可见的占位符成员。  
  
 在 SCOPE 语句中创建的计算成员和命名集不受 SCOPE 语句的影响。  
  
## <a name="example"></a>示例  
 以下示例中的，从 MDX 计算脚本在 Adventure Works 示例解决方案中，将定义与在会计年度 2005年和销售额配额度量值，会计季度位于当前作用域，然后分配到使用的当前作用域中的单元格的值**ParallelPeriod**函数。 该示例然后修改使用另一个 SCOPE 语句，作用域，然后执行另一个分配使用[此 (MDX)](../mdx/this-mdx.md)函数。  
  
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
 [MDX 脚本语句 &#40;MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
