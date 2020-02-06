---
title: InScope 函数（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/08/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8b6891ec497b3100206b812fbc8da7b0463fa4d3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65579510"
---
# <a name="report-builder-functions---inscope-function"></a>报表生成器函数 - InScope 函数
  指示项的当前实例是否位于指定的作用域中。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>parameters  
 *作用域*  
 (**String**) 数据集、数据区域或指定某个作用域的组的名称。  
  
## <a name="return-type"></a>返回类型  
 返回 **Boolean**。  
  
## <a name="remarks"></a>备注  
 **InScope** 函数对由 *scope*参数指定的作用域内成员的当前报表项实例的作用域进行测试。  
  
 *Scope* 不能是表达式。  
  
 **InScope** 函数通常用在具有动态作用域的数据区域中。 例如， **InScope** 可在数据区域单元格的钻取链接中使用，以便提供不同的报表名称和不同的参数集，具体取决于所单击的单元格。 应用示例如下：  
  
-   如果单击的单元格位于 `ProductDetail` 组，则以下在钻取链接中用作报表名称的表达式将打开 `Month` 报表；否则将打开 `ProductSummary` 报表。  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   仅当单击的单元位于 **组时，以下在钻取报表参数的** Omit `Product` 属性中使用的表达式才会将参数传递到目标报表。  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例指示项的当前实例是位于 `Product` 数据集、数据区域还是组作用域中。  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>另请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
