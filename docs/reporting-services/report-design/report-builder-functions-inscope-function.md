---
title: "InScope 函数 （报表生成器和 SSRS） |Microsoft 文档"
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
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d8dacf74335cafa2585168288ea88d316b23d037
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---inscope-function"></a>报表生成器功能-InScope 函数
  指示项的当前实例是否位于指定的作用域中。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>Parameters  
 *作用域*  
 (**String**) 数据集、数据区域或指定某个作用域的组的名称。  
  
## <a name="return-type"></a>返回类型  
 返回 **Boolean**。  
  
## <a name="remarks"></a>注释  
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
 [在报表 &#40; 中使用表达式报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式 &#40; 中的数据类型报表生成器和 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [总计、 聚合和内置集合 &#40; 的表达式作用域报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
