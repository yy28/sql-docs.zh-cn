---
title: RowNumber 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d4a06a24525b3d9d0c4e4a5f3f0b749a7db70261
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105172"
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
 (`String`) 数据集、数据区域或组的名称，也可以为 Null（在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 中为 `Nothing`），它指定在其中计算行数的上下文。 `Nothing` 指定最外层的上下文，通常为报表数据集。  
  
## <a name="remarks"></a>备注  
 `RowNumber` 返回指定作用域内的行计数的运行值一样[RunningValue](report-builder-functions-runningvalue-function.md)返回聚合函数的运行值。 指定作用域时，需要指定何时将行计数重新设置为 1。  
  
 *scope* 不能是表达式。 *scope* 必须是包含作用域。 典型的从最外层到最内层包容的作用域是报表数据集、数据区域、行组或列组。  
  
 若要在列间递增值，请指定一个为列组名称的作用域。 若要沿行递增值，请指定一个为行组名称的作用域。  
  
> [!NOTE]  
>  不能包括指定一个表达式中同时具有行组和列组的聚合。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="code-example"></a>代码示例  
 以下表达式可用于 Tablix 数据区域详细信息行的 `BackgroundColor` 属性，以改变每个组的详细信息行的颜色（始终从白色开始）。  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
