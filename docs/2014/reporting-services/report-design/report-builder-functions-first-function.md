---
title: First 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d0914520-30c5-4d63-9b59-8d9342ed63b9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a47169bc3c628e4bf33fb9ed6a19e612320b585c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105269"
---
# <a name="first-function-report-builder-and-ssrs"></a>First 函数（报表生成器和 SSRS）
  返回指定表达式的给定作用域中的第一个值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
First(expression, scope)  
```  
  
#### <a name="parameters"></a>Parameters  
 *expression*  
 （`Variant` 或 `Binary`）要对其执行聚合的表达式，例如，`=Fields!FieldName.Value`。  
  
 *作用域*  
 (`String`) 可选。 包含要对其应用聚合函数的报表项的数据集、组或数据区域的名称。 如果未指定 *scope* ，则使用当前作用域。  
  
## <a name="return-type"></a>返回类型  
 视表达式的类型而定。  
  
## <a name="remarks"></a>备注  
 `First` 函数返回在指定作用域中应用所有排序和筛选后的一组数据的第一个值。  
  
 `First` 函数只能用在当前作用域（默认）相关的组筛选表达式中。  
  
 您还可以在页眉中使用 `First` 函数，返回 `ReportItems` 集合中属于某页面的第一个值，以便在页面中生成显示首项和尾项的字典样式标题。  
  
 *scope* 的值必须是字符串常量，不能是表达式。 对于外部聚合或未指定其他聚合的聚合， *scope* 必须引用当前作用域或包含作用域。 对于聚合的聚合，嵌套聚合可以指定子作用域。  
  
 *Expression* 可以包含对嵌套聚合函数的调用，但具有以下例外和条件：  
  
-   嵌套聚合的*Scope* 必须与外部聚合的作用域相同，或者包含在外部聚合的作用域中。 对于表达式中的所有非重复作用域，一个作用域必须相对所有其他作用域处于子关系中。  
  
-   嵌套聚合的*Scope* 不能为数据集的名称。  
  
-   *表达式*不能包含`First`， `Last`， `Previous`，或`RunningValue`函数。  
  
-   *Expression* 不得包含用于指定 *recursive*的嵌套聚合。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 有关递归聚合的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例返回数据区域 `Category` 组中的第一个产品编号：  
  
```  
=First(Fields!ProductNumber.Value, "Category")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
