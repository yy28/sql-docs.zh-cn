---
title: InScope 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ecb91bd2a4b570a1e625a013270e59a121e6430a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025468"
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
 (`String`) 数据集、数据区域或指定某个作用域的组的名称。  
  
## <a name="return-type"></a>返回类型  
 返回 `Boolean`。  
  
## <a name="remarks"></a>备注  
 `InScope`函数测试中指定的作用域的成员的当前实例的报表项作用域*作用域*参数。  
  
 *Scope* 不能是表达式。  
  
 `InScope` 函数通常用在具有动态作用域的数据区域中。 例如，`InScope` 可在数据区域单元格的钻取链接中使用，以便提供不同的报表名称和不同的参数集，具体取决于所单击的单元格。 应用示例如下：  
  
-   如果单击的单元格位于 `ProductDetail` 组，则以下在钻取链接中用作报表名称的表达式将打开 `Month` 报表；否则将打开 `ProductSummary` 报表。  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   仅当单击的单元位于 `Product` 组时，以下在钻取报表参数的 `Omit` 属性中使用的表达式才会将参数传递到目标报表。  
  
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
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
