---
title: CountRows 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f3414498d0ce399607ab0faa1a438dad88efc35c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105281"
---
# <a name="countrows-function-report-builder-and-ssrs"></a>CountRows 函数（报表生成器和 SSRS）
  返回指定作用域内的行数，包括含有 Null 值的行。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### <a name="parameters"></a>Parameters  
 *作用域*  
 (`String`) 包含要计数报表项的数据集、数据区域或组的名称。  
  
 *递归*  
 (**Enumerated Type**) 可选。 `Simple`（默认值）或 `RdlRecursive`。 指定是否以递归方式执行聚合。  
  
## <a name="return-type"></a>返回类型  
 返回`Integer`。  
  
## <a name="remarks"></a>备注  
 `CountRows` 计数指定作用域内的所有行，其中包括具有 Null 值的行。  
  
 *scope* 的值不能是表达式，并且必须引用当前作用域或包含作用域。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 有关递归聚合的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例显示一个表达式，该表达式计算名为 `GroupbyCategory` 的行组中的行数（基于表达式 `[Category]`）。  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
