---
title: Count 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 7b50b101-daf8-4fb0-ae04-57384755779f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2e90a3d1e7b5e00c61be2ed4d1d50db501474e35
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292425"
---
# <a name="count-function-report-builder-and-ssrs"></a>Count 函数（报表生成器和 SSRS）
  返回在给定作用域上下文中计算的，由表达式指定的非 Null 值的计数。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
Count(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parameters  
 *expression*  
 （`Variant` 或 `Binary`）要对其执行聚合的表达式，例如，`=Fields!FieldName.Value`。  
  
 *作用域*  
 (`String`) 包含要对其应用聚合函数的报表项的数据集、组或数据区域的名称。 如果未指定 *scope* ，则使用当前作用域。  
  
 *递归*  
 (**Enumerated Type**) 可选。 `Simple`（默认值）或 `RdlRecursive`。 指定是否以递归方式执行聚合。  
  
## <a name="return-type"></a>返回类型  
 返回`Integer`。  
  
## <a name="remarks"></a>备注  
 *scope* 的值必须是字符串常量，不能是表达式。 对于外部聚合或未指定其他聚合的聚合， *scope* 必须引用当前作用域或包含作用域。 对于聚合的聚合，嵌套聚合可以指定子作用域。  
  
 *Expression* 可以包含对嵌套聚合函数的调用，但具有以下例外和条件：  
  
-   嵌套聚合的*Scope* 必须与外部聚合的作用域相同，或者包含在外部聚合的作用域中。 对于表达式中的所有非重复作用域，一个作用域必须相对所有其他作用域处于子关系中。  
  
-   嵌套聚合的*Scope* 不能为数据集的名称。  
  
-   *表达式*不能包含`First`， `Last`， `Previous`，或`RunningValue`函数。  
  
-   *Expression* 不得包含用于指定 *recursive*的嵌套聚合。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 有关递归聚合的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
 示例  
  
## <a name="description"></a>Description  
 下面的代码示例显示一个表达式，该表达式为默认作用域和父组作用域计算 `Size` 的非 Null 值数。 该表达式将添加至属于子组 `GroupbySubcategory`的行的某个单元格中。 父组是 `GroupbyCategory`。 该表达式显示 `GroupbySubcategory` （默认作用域）和 `GroupbyCategory` （父组作用域）的结果。  
  
> [!NOTE]  
>  表达式中不应包含实际的回车符和换行符；这些回车符和换行符包含在示例中是为了支持文档呈现器。 如果您要复制以下示例，请删除每一行中的回车符。  
  
## <a name="code"></a>代码  
  
```  
="Count (Subcategory): " & Count(Fields!Size.Value) &   
"Count (Category): " & Count(Fields!Size.Value,"GroupbyCategory")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
