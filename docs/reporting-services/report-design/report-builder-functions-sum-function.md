---
title: "Sum 函数 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b45a024-398d-43b8-9948-b8b23fb674c9
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3506f267e481c1810b2f862b40353f762bcdd63a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---sum-function"></a>报表生成器功能-Sum 函数
  返回在给定作用域中计算的、由表达式指定的所有非 Null 数值的和。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
Sum(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parameters  
 *expression*  
 （**Integer** 或 **Float**）要对其执行聚合的表达式。  
  
 *作用域*  
 (**String**) 可选。 包含要对其应用聚合函数的报表项的数据集、组或数据区域的名称。 如果未指定 *scope* ，则使用当前作用域。  
  
 *递归*  
 (**Enumerated Type**) 可选。 **Simple** （默认）或 **RdlRecursive**。 指定是否以递归方式执行聚合。  
  
## <a name="return-type"></a>返回类型  
 对于十进制表达式，返回 **Decimal** ；对于所有其他类型的表达式，返回 **Double** 。  
  
## <a name="remarks"></a>注释  
 表达式中指定的数据集必须具有相同的数据类型。 若要将具有多个数值数据类型的数据转换为同一数据类型，请使用类似 **CInt**、 **CDbl** 或 **CDec**的转换函数。 有关详细信息，请参阅 [Type Conversion Functions](http://go.microsoft.com/fwlink/?LinkId=96142)（类型转换函数）。  
  
 *scope* 的值必须是字符串常量，不能是表达式。 对于外部聚合或未指定其他聚合的聚合， *scope* 必须引用当前作用域或包含作用域。 对于聚合的聚合，嵌套聚合可以指定子作用域。  
  
 *Expression* 可以包含对嵌套聚合函数的调用，但具有以下例外和条件：  
  
-   嵌套聚合的*Scope* 必须与外部聚合的作用域相同，或者包含在外部聚合的作用域中。 对于表达式中的所有非重复作用域，一个作用域必须相对所有其他作用域处于子关系中。  
  
-   嵌套聚合的*Scope* 不能为数据集的名称。  
  
-   *Expression* 不得包含 **First**、 **Last**、 **Previous**或 **RunningValue** 函数。  
  
-   *Expression* 不得包含用于指定 *recursive*的嵌套聚合。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 有关递归聚合的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>示例  
 以下两个代码示例提供了 `Order` 组或数据区域中所有行项总计值的和。  
  
```  
=Sum(Fields!LineTotal.Value, "Order")  
' or   
=Sum(CDbl(Fields!LineTotal.Value), "Order")  
```  
  
## <a name="example"></a>示例  
 在具有嵌套行组 Category 和 Subcategory 以及嵌套列组 Year 和 Quarter 的矩阵数据区域中，在属于最内侧的行组和列组的单元中，以下表达式的计算结果为所有子类别的所有季节中的最大值。  
  
```  
=Max(Sum(Fields!Sales.Value))  
```  
  
## <a name="see-also"></a>另请参阅  
 [在报表 &#40; 中使用表达式报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式 &#40; 中的数据类型报表生成器和 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [总计、 聚合和内置集合 &#40; 的表达式作用域报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
