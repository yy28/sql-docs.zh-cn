---
title: 直观合计和非直观合计 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ea9d02f2-a668-4547-ade5-e3d077a2e1bd
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b211305babfee92a85469257795b6124f2ab4b54
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253029"
---
# <a name="visual-totals-and-non-visual-totals"></a>直观合计和非直观合计
  直观合计是位于列尾或行尾的合计，它将列或行中可见的所有项相加。 这是大多数表在显示时的默认行为。 但有一些情况，用户想要只显示表中的某些列，但保留针对整个行的合计，包括那些未显示的行。 这称作 `Non Visual Totals`，因为合计来自可见值以及非可见值。  
  
 下面的应用场景对非直观合计的行为进行了演示。 第一步显示直观合计的默认行为。  
  
 下面的示例用于查询 [Adventure Works]，以获取表中的 [Reseller Sales Amount] 数字，在该表中产品类别为列，分销商业务类型为行。 请注意，合计是在发出以下 SELECT 语句时为产品和分销商给出的：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 产生以下结果：  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|服装|**Components**|  
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
|所有分销商|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 与上述结果比较时，您可以观察到 [All Resellers] 行现在是将 [Value Added Reseller] 和 [Warehouse] 仓库的显示值相加，但 [All Products] 列会显示所有产品的总值，包括那些未显示的值。  
  
## <a name="see-also"></a>请参阅  
 [MDX 中的重要概念&#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Autoexists](autoexists.md)   
 [使用成员、 元组和集&#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [MDX 查询基础知识&#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)   
 [基本 MDX 查询&#40;MDX&#41;](mdx-query-the-basic-query.md)   
 [用查询轴和切片器轴限定查询&#40;MDX&#41;](mdx-query-and-slicer-axes-restricting-the-query.md)   
 [在查询中建立多维数据集上下文&#40;MDX&#41;](establishing-cube-context-in-a-query-mdx.md)  
  
  
