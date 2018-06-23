---
title: RowNumber 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 150a46a736a9c6ddd2f8c394f3f173906cd07132
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018539"
---
# <a name="rownumber-function-report-builder-and-ssrs"></a>RowNumber 函数（报表生成器和 SSRS）
  返回指定作用域内行数的运行计数。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>Parameters  
 *作用域*  
 (`String`) 的数据集、 数据区域或组或为 null 的名称 (`Nothing`中[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])，，指定在其中计算的行数的上下文。 `Nothing` 指定的最外层的上下文，通常报表数据集。  
  
## <a name="remarks"></a>Remarks  
 `RowNumber` 返回在指定范围内，行的计数的运行值一样[RunningValue](report-builder-functions-runningvalue-function.md)返回聚合函数的运行值。 指定作用域时，需要指定何时将行计数重新设置为 1。  
  
 *scope* 不能是表达式。 *scope* 必须是包含作用域。 典型的从最外层到最内层包容的作用域是报表数据集、数据区域、行组或列组。  
  
 若要在列间递增值，请指定一个为列组名称的作用域。 若要沿行递增值，请指定一个为行组名称的作用域。  
  
> [!NOTE]  
>  不能包括指定一个表达式中同时具有行组和列组的聚合。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="code-example"></a>代码示例  
 以下是可用于表达式`BackgroundColor`Tablix 数据区域详细信息行以改变每个组，始终从白色开始的详细信息行的颜色的属性。  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式&#40;报表生成器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、 聚合和内置集合的表达式作用域&#40;报表生成器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  