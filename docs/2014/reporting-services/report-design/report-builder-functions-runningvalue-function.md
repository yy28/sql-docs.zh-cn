---
title: RunningValue 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 02e670fd13f249e1278675b02097f4921dd41ebe
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285965"
---
# <a name="runningvalue-function-report-builder-and-ssrs"></a>RunningValue 函数（报表生成器和 SSRS）
  返回在给定作用域中计算的，由表达式指定的所有非 Null 数值的运行聚合。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
RunningValue(expression, function, scope)  
```  
  
#### <a name="parameters"></a>Parameters  
 *expression*  
 要对其执行聚合的表达式，例如， `[Quantity]`。  
  
 *函数*  
 (`Enum`) 要应用于表达式的聚合函数的名称，例如，`Sum`。 此函数不能为 `RunningValue`、`RowNumber` 或 `Aggregate`。  
  
 *作用域*  
 (`String`) 一个字符串常量，表示数据集、数据区域或组的名称，也可以为 Null（在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 中为 `Nothing`），它指定在其中计算聚合的上下文。 `Nothing` 指定最外层的上下文，通常为报表数据集。  
  
## <a name="return-type"></a>返回类型  
 由 *function* 参数中指定的聚合函数确定。  
  
## <a name="remarks"></a>备注  
 作用域的每个新实例 `RunningValue` 的值都会重置为 0。 如果指定组，则会在更改组表达式时重置该运行值。 如果指定数据区域，则会为该数据区域的每个新实例重置该运行值。 如果指定数据集，则不会在整个数据集中重置该运行值。  
  
 `RunningValue` 不能在筛选器或排序表达式中使用。  
  
 为其计算运行值的数据集必须具有相同的数据类型。 若要将具有多个数值数据类型的数据转换为同一数据类型，请使用类似 `CInt`、`CDbl` 或 `CDec` 的转换函数。 有关详细信息，请参阅 [Type Conversion Functions](https://go.microsoft.com/fwlink/?LinkId=96142)（类型转换函数）。  
  
 *Scope* 不能是表达式。  
  
 *Expression* 可以包含对嵌套聚合函数的调用，但具有以下例外和条件：  
  
-   嵌套聚合的作用域必须与外部聚合的作用域相同，或者包含在外部聚合的作用域中。 对于表达式中的所有非重复作用域，一个作用域必须相对所有其他作用域处于子关系中。  
  
-   嵌套聚合的作用域不能为数据集的名称。  
  
-   *表达式*不能包含`First`， `Last`， `Previous`，或`RunningValue`函数。  
  
-   *Expression* 不得包含用于指定 *recursive*的嵌套聚合。  
  
 若要计算行数的运行值，请使用 `RowNumber`。 有关详细信息，请参阅 [RowNumber 函数（报表生成器和 SSRS）](report-builder-functions-rownumber-function.md)。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 有关递归聚合的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="examples"></a>示例  
 下面的代码示例提供了最外层作用域（数据集）中名为 `Cost` 的字段的运行总和。  
  
```  
=RunningValue(Fields!Cost.Value, Sum, Nothing)  
```  
  
 下面的代码示例提供了名为 `Score` 的数据集中名为 `DataSet1`的字段的运行总和。  
  
```  
=RunningValue(Fields!Score.Value,sum,"DataSet1")  
```  
  
 下面的代码示例提供了最外层作用域中名为 `Traffic Charges` 的字段的运行总和。  
  
```  
=RunningValue(Fields!Traffic Charges.Value, Sum, Nothing)  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
