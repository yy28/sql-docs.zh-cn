---
title: InScope 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ebf90710587c73206408dfda1429a90b58f39621
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228837"
---
# <a name="inscope-function-report-builder-and-ssrs"></a>InScope 函数（报表生成器和 SSRS）
  指示项的当前实例是否位于指定的作用域中。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>Parameters  
 *作用域*  
 (`String`) 的数据集、 数据区域或指定某个作用域的组的名称。  
  
## <a name="return-type"></a>返回类型  
 返回`Boolean`。  
  
## <a name="remarks"></a>Remarks  
 `InScope`函数测试中指定的作用域的成员的当前实例的报表项作用域*作用域*参数。  
  
 *Scope* 不能是表达式。  
  
 典型用法`InScope`函数具有动态的数据区域作用域中。 例如，`InScope`可用于在数据区域单元格的钻取链接提供不同的报表名称和不同的参数取决于所单击的单元集。 应用示例如下：  
  
-   如果单击的单元格位于 `ProductDetail` 组，则以下在钻取链接中用作报表名称的表达式将打开 `Month` 报表；否则将打开 `ProductSummary` 报表。  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   下面的表达式中使用`Omit`钻取报表参数的属性会将参数传递到目标报表仅当单击的单元格处于`Product`组。  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例指示项的当前实例是位于 `Product` 数据集、数据区域还是组作用域中。  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式&#40;报表生成器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、 聚合和内置集合的表达式作用域&#40;报表生成器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
