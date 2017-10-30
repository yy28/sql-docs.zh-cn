---
title: "ALTER CUBE 语句 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Cube
- ALTER_CUBE
- ALTER CUBE
- ALTER
dev_langs:
- kbMDX
helpviewer_keywords:
- ALTER CUBE statement
- cubes [Analysis Services], modifying
- modifying cubes
ms.assetid: 2f0af61b-f509-4e1a-990f-20a215d22994
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e20832dac862a4a4973c4350c64efdd23a35b461
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---alter-cube"></a>MDX 数据定义的 ALTER 多维数据集
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改指定多维数据集的结构，通常用于支持维度写回。 有关应用程序中使用写回的详细信息，请参阅此博客文章：[构建写回应用程序与 Analysis Services （博客）](http://go.microsoft.com/fwlink/?LinkId=394977)  
  
 请注意，并发写回会造成死锁，其中，第一个写回会因为由第二个写回保持的共享锁而无法完成提交。 在这种情况下，不会生成错误，但是也不能继续操作。 最终会发生超时和回滚。  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER CUBE  
      Cube_Name | CURRENTCUBE  
      <alter clause>   
            [ < alter clause> ...n]  
  
< alter clause> ::=   
   <create dimension member clause>   
  | <remove dimension member clause>  
  | <move dimension member clause>   
    | <update clause>   
    | <create cell calculation clause>  
  
<create dimension member clause> ::=  
CREATE DIMENSION MEMBER [ParentName.]MemberName  
    , [[KEY = Key_Value]   
    | [Property_Name = Property_Value[, ...n]]  
  
<dropping clause>::=  
DROP   
      DIMENSION MEMBER Member_Name   
            Member_Name ...n ]   
      [WITH DESCENDANTS]  
      | [ SESSION ] [ CALCULATED ] MEMBER Member_Name   
                  [ ,Member_Name,...n ]   
    | SET Set_Name  
                  [ ,Set_Name,...n ]   
    | [ SESSION ] CELL CALCULATION CellCalc_Name  
                  [ ,CellCalc_Name,...n ]   
    | ACTION Action_Name  
  
<move dimension member clause> ::=  
MOVE DIMENSION MEMBER MemberName  
        [, SKIPPED_LEVELS = Unsigned_Integer]   
      [WITH DESCENDANTS]  
    UNDER ParentName      
  
<update clause> ::=  
UPDATE   
    CUSTOM ROLLUP FOR MEMBER MemberName  
      [,MemberName, ...n] AS MDX_Expression  
   | DIMENSION Dimension_Name | Hierarchy_Name  
      , DEFAULT_MEMBER = MDX_Expression  
   | DIMENSION MEMBER MemberName AS  
   [MDX_Expression]  
   [Property_Name = Property_Value[, ...n]]  
  
<create cell calculation clause>::=  
CELL CALCULATION Calculation_Name   
   FOR Set_Expression AS MDX_Expression   
            [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="creating-a-dimension-member"></a>创建维度成员  
 将一个新行添加到基础维度表中。  
  
### <a name="arguments"></a>参数  
 *ParentName*  
 除非在根节点新建维度成员，否则提供该维度成员父级名称的有效字符串表达式。  
  
 *成员名称*  
 提供成员名称的有效字符串表达式。  
  
 *Key_Value*  
 定义新维度成员键值的有效标量表达式。  
  
 *Property_Name*  
 代表成员属性的有效多维表达式 (MDX) 标识符。  
  
 *Property_Value*  
 定义计算成员属性值的有效多维表达式 (MDX) 标量表达式。  
  
## <a name="dropping-a-dimension-member"></a>删除维度成员  
 如果从可写维度中删除一个维度成员，就会从基础维度表中删除该成员和与其对应的行。  
  
### <a name="arguments"></a>参数  
 *Cube_Name*  
 提供一个多维数据集的名称是有效的字符串表达式。  
  
 *Member_Name*  
 提供成员名称或成员键的有效字符串表达式。  
  
### <a name="remarks"></a>備註  
 如果未使用 WITH DESCENDANTS 子句，则已删除成员的子级将成为已删除成员父级的子级。 如果使用 WITH DESCENDANTS 子句，则还会删除维度表内的所有后代及其对应的行。  
  
> [!NOTE]  
>  有关删除计算的成员、 命名集、 操作和单元计算，请参阅[DROP 成员语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-member.md)，[删除 SET 语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-set.md)， [DROP 操作语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-action.md)，和[删除单元格计算语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="updating-the-default-dimension-member"></a>更新默认维度成员  
 该子句更新多维数据集的默认成员，并且在定义默认成员的 MDX 计算脚本中使用。 可以为数据库维度、多维数据集维度或者用户登录名指定默认成员。 还可以在会话期间更改默认成员。  
  
### <a name="arguments"></a>参数  
 *Dimension_Name*  
 提供维度名称的有效字符串。  
  
 *MDX_Expression*  
 返回单个成员的有效 MDX 表达式。  
  
### <a name="remarks"></a>注释  
 指定的 MDX 表达式可以为静态或动态。  
  
## <a name="moving-a-dimension-member"></a>移动维度成员  
 在基础维度表内修改某行。  
  
### <a name="arguments"></a>参数  
 *ParentName*  
 提供要移动维度成员的新父级名称的有效字符串表达式。  
  
 *成员名称*  
 提供成员名称的有效字符串表达式。  
  
 Unsigned_*整数*  
 指定要跳过的级别数的有效数字。  
  
 如果指定了 WITH DESCENDANTS 子句，则移动整个树。 如果未指定 WITH DESCENDANTS 子句，则所移动父级的子级将成为所移动成员父级的子级。 移动造成的影响仅仅是在基础维度表中更新了父键列的值。  
  
## <a name="updating-a-dimension-member"></a>更新维度成员  
 UPDATE DIMENSION MEMBER 子句可以修改成员的属性以及与成员相关的自定义成员公式。  
  
### <a name="arguments"></a>参数  
 *成员名称*  
 提供成员名称的有效字符串表达式。  
  
 *MDX_Expression*  
 返回单个成员的有效 MDX 表达式。  
  
 *Property_Value*  
 定义计算成员属性值的有效 MDX 标量表达式。  
  
## <a name="creating-a-cell-calculation"></a>创建单元计算  
 有关创建使用 ALTER CUBE 语句的单元计算的详细信息，请参阅[DROP 单元格计算语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="see-also"></a>另请参阅  
 [MDX 数据定义语句 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

