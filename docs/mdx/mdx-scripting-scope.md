---
title: SCOPE 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 497fdfb11ec186ffba56470f2b0ede2ed2f4221a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187527"
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
  
 作用域语句将创建子多维数据集显示"空位置"，而不考虑**MDX 兼容性**设置。 例如，`Scope( Customer.State.members )` 语句可以在不包含州的国家或地区中包括州，但在其他情况下会插入不可见的占位符成员。  
  
 在 SCOPE 语句中创建的计算成员和命名集不受 SCOPE 语句的影响。  
  
## <a name="example"></a>示例  
 以下示例中的，从 MDX 计算脚本中 Adventure Works 示例解决方案、 定义为在 2005年会计年度和销售配额度量值，会计季度的当前作用域，然后到当前作用域中的单元格分配值，通过使用**ParallelPeriod**函数。 该示例然后修改使用另一个 SCOPE 语句，作用域，然后执行另一个分配使用[This (MDX)](../mdx/this-mdx.md)函数。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 脚本编写语句 (MDX)](../mdx/mdx-scripting-statements-mdx.md)  
  
  
