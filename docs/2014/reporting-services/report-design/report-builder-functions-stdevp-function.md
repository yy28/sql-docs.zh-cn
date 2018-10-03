---
title: StDevP 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: cbcc0b3f-7b6d-4dd7-accb-cb375be8d852
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 7ebc16495635d2059c60bf7cddcdfacd90c9139c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116297"
---
# <a name="stdevp-function-report-builder-and-ssrs"></a>StDevP 函数（报表生成器和 SSRS）
  返回在给定作用域上下文中计算的，由表达式指定的所有非 Null 数值的总体标准偏差。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
StDevP(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parameters  
 *expression*  
 (`Integer`或`Float`) 对其执行聚合的表达式。  
  
 *作用域*  
 (`String`) 可选。 包含要对其应用聚合函数的报表项的数据集、组或数据区域的名称。 如果未指定 *scope* ，则使用当前作用域。  
  
 *递归*  
 (**Enumerated Type**) 可选。 `Simple` （默认值） 或`RdlRecursive`。 指定是否以递归方式执行聚合。  
  
## <a name="return-type"></a>返回类型  
 返回`Decimal`对于十进制表达式和`Double`对于所有其他表达式。  
  
## <a name="remarks"></a>备注  
 表达式中指定的数据集必须具有相同的数据类型。 若要将转换具有多个数值数据类型为相同的数据类型的数据，请使用转换函数，例如`CInt`，`CDbl`或`CDec`。 有关详细信息，请参阅 [Type Conversion Functions](http://go.microsoft.com/fwlink/?LinkId=96142)（类型转换函数）。  
  
 *scope* 的值必须是字符串常量，不能是表达式。 对于外部聚合或未指定其他聚合的聚合， *scope* 必须引用当前作用域或包含作用域。 对于聚合的聚合，嵌套聚合可以指定子作用域。  
  
 *Expression* 可以包含对嵌套聚合函数的调用，但具有以下例外和条件：  
  
-   嵌套聚合的*Scope* 必须与外部聚合的作用域相同，或者包含在外部聚合的作用域中。 对于表达式中的所有非重复作用域，一个作用域必须相对所有其他作用域处于子关系中。  
  
-   嵌套聚合的*Scope* 不能为数据集的名称。  
  
-   *表达式*不能包含`First`， `Last`， `Previous`，或`RunningValue`函数。  
  
-   *Expression* 不得包含用于指定 *recursive*的嵌套聚合。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 有关递归聚合的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例提供了 `Order` 组或数据区域中所有行项总计值的总体标准偏差。  
  
```  
=StDevP(Fields!LineTotal.Value, "Order")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式&#40;报表生成器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、 聚合和内置集合的表达式作用域&#40;报表生成器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
