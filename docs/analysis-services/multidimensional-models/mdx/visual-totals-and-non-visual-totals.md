---
title: "直观合计和非直观合计 |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea9d02f2-a668-4547-ade5-e3d077a2e1bd
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f966f4108f3ad029b6c069216cd7713f3b4ac7e7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="visual-totals-and-non-visual-totals"></a>直观合计和非直观合计
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]直观合计是得到的列或行的末尾添加所有列或行中可见的项的总数。 这是大多数表在显示时的默认行为。 但有一些情况，用户想要只显示表中的某些列，但保留针对整个行的合计，包括那些未显示的行。 这称作 **非直观总计**，因为合计来自可见值以及非可见值。  
  
 下面的应用场景对非直观合计的行为进行了演示。 第一步显示直观合计的默认行为。  
  
 下面的示例用于查询 [Adventure Works]，以获取表中的 [Reseller Sales Amount] 数字，在该表中产品类别为列，分销商业务类型为行。 请注意，合计是在发出以下 SELECT 语句时为产品和分销商给出的：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 产生以下结果：  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|**Clothing**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
## <a name="non-visual-on-rows-and-columns"></a>针对行和列的非直观合计  
 要生成一个仅具有“附件”和“服装”产品、“增值分销商”和“仓库分销商”数据的表，但仍保留总合计，则使用 NON VISUAL 编写如下语句：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 产生以下结果：  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
## <a name="non-visual-on-rows"></a>针对行的非直观合计  
 要生成一个表，其中列是进行直观加和，对于行总数则是所有 [类别] 的实际总和，应发出以下查询：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 请注意，NON VISUAL 仅应用到 [Category]。  
  
 上述查询产生以下结果：  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 与上述结果比较时，您可以观察到 [All Resellers] 行现在是将 [Value Added Reseller] 和 [Warehouse] 仓库的显示值相加，但 [All Products] 列会显示所有产品的总值，包括那些未显示的值。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 中的重要概念 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [使用成员、元组和集 (MDX)](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [MDX 查询基础知识 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [基本 MDX 查询 &#40;MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)   
 [限制查询中的使用查询和切片器轴 &#40;MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)   
 [在查询中建立多维数据集上下文 (MDX)](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)  
  
  
