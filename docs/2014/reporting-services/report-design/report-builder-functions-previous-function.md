---
title: Previous 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 540bf8367ba32fbebe4e27ee6e2cd3e1aa01ae0d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105203"
---
# <a name="previous-function-report-builder-and-ssrs"></a>Previous 函数（报表生成器和 SSRS）
  返回指定作用域内某项的前一个实例的值或该实例的指定聚合值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>parameters  
 *expression*  
 （`Variant` 或 `Binary`）用于标识数据和检索以前值的表达式，例如 `Fields!Fieldname.Value` 或 `Sum(Fields!Fieldname.Value)`。  
  
 *作用域*  
 (`String`) 可选。 组或数据区域的名称，或者为 null （`Nothing`在中[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]为），它指定要从中检索*expression*指定的以前值的作用域。  
  
## <a name="return-type"></a>返回类型  
 返回`Variant`或`Binary`。  
  
## <a name="remarks"></a>备注  
 
  `Previous` 函数返回在应用所有排序和筛选之后，指定作用域内计算的表达式的前一个值。  
  
 如果*expression*不包含聚合，则`Previous`函数默认为报表项的当前作用域。  
  
 在详细信息组中，使用 `Previous` 可以在详细信息行的前一实例中指定字段引用的值。  
  
> [!NOTE]  
>  `Previous`函数只支持详细信息组中的字段引用。 例如，在详细信息组的文本框中， `=Previous(Fields!Quantity.Value)` 将返回上一行中 `Quantity` 字段的数据。 在第一行中，此表达式返回一个 Null（在 `Nothing` 中为 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]）。  
  
 如果*expression*包含使用默认作用域的聚合函数， `Previous`则聚合聚合函数调用中指定的作用域的前一个实例内的数据。  
  
 如果*expression*包含指定非默认作用域的聚合函数，则该`Previous`函数的*作用域*参数必须是聚合函数调用中指定的作用域的包含作用域。  
  
 在 expression `Level`参数`InScope`中`Aggregate`不`Previous`能使用函数、和**。 不支持将 *recursive* 参数指定给任何聚合函数。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>说明  
 下面的代码示例置于数据区域的默认数据行时，提供上一行中 `LineTotal` 字段的值。  
  
### <a name="code"></a>代码  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### <a name="description"></a>说明  
 下面的示例显示一个表达式，该表达式计算某月特定天的销售额和上一年该月该天的销售额的总和。 该表达式将添加至属于子组 `GroupbyDay`的行的某个单元格中。 它的父组是 `GroupbyMonth`，该父组的父组是 `GroupbyYear`。 该表达式显示 GroupbyDay（默认作用域）和 `GroupbyYear` （父组 `GroupbyMonth`的父组）的结果。  
  
 例如，对于具有名为 `Year`的父组的数据区域，其子组名为 `Month`，子组的子组名为 `Day` （3 个嵌套级别）。 与组 `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` 关联的行中的表达式 `Day` 返回上一年同一月同一天的销售额值。  
  
### <a name="code"></a>代码  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## <a name="see-also"></a>另请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
