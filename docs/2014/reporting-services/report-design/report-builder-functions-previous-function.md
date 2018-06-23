---
title: Previous 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 65f8f0bdc7db2e58efd27522a93e4edf6c4e0bf3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125790"
---
# <a name="previous-function-report-builder-and-ssrs"></a>Previous 函数（报表生成器和 SSRS）
  返回指定作用域内某项的前一个实例的值或该实例的指定聚合值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>Parameters  
 *expression*  
 (`Variant`或`Binary`) 要用于标识的数据的表达式和为其检索以前的值中，例如，`Fields!Fieldname.Value`或`Sum(Fields!Fieldname.Value)`。  
  
 *作用域*  
 (`String`) 可选。 为组或数据区域中或空值的名称 (`Nothing`中[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])，指定要从其检索以前的值指定的作用域*表达式*。  
  
## <a name="return-type"></a>返回类型  
 返回`Variant`或`Binary`。  
  
## <a name="remarks"></a>Remarks  
 `Previous` 函数返回在应用所有排序和筛选之后，指定作用域内计算的表达式的前一个值。  
  
 如果*表达式*不包含聚合，`Previous`函数默认为当前范围中为报表项。  
  
 在详细信息组中，使用`Previous`在以前的实例的详细信息行中指定的字段引用的值。  
  
> [!NOTE]  
>  `Previous`函数仅支持在详细信息组中的字段引用。 例如，在详细信息组的文本框中， `=Previous(Fields!Quantity.Value)` 将返回上一行中 `Quantity` 字段的数据。 在第一行中，此表达式返回一个 Null（在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 中为 `Nothing`）。  
  
 如果*表达式*包含使用默认作用域的聚合函数`Previous`聚合的作用域的前一个实例内的数据指定在聚合函数调用。  
  
 如果*表达式*包含指定作用域而不是默认的聚合函数*作用域*参数`Previous`函数必须是包含作用域中指定作用域聚合函数调用中。  
  
 函数`Level`， `InScope`，`Aggregate`和`Previous`不能在*表达式*参数。 不支持将 *recursive* 参数指定给任何聚合函数。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>Description  
 下面的代码示例置于数据区域的默认数据行时，提供上一行中 `LineTotal` 字段的值。  
  
### <a name="code"></a>代码  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### <a name="description"></a>Description  
 下面的示例显示一个表达式，该表达式计算某月特定天的销售额和上一年该月该天的销售额的总和。 该表达式将添加至属于子组 `GroupbyDay`的行的某个单元格中。 它的父组是 `GroupbyMonth`，该父组的父组是 `GroupbyYear`。 该表达式显示 GroupbyDay（默认作用域）和 `GroupbyYear` （父组 `GroupbyMonth`的父组）的结果。  
  
 例如，对于具有名为 `Year`的父组的数据区域，其子组名为 `Month`，子组的子组名为 `Day` （3 个嵌套级别）。 与组 `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` 关联的行中的表达式 `Day` 返回上一年同一月同一天的销售额值。  
  
### <a name="code"></a>代码  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式&#40;报表生成器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、 聚合和内置集合的表达式作用域&#40;报表生成器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  