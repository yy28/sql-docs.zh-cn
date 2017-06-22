---
title: "呈现数据区域 （报表生成器和 SSRS） |Microsoft 文档"
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
ms.assetid: 4f3b2c7d-3669-457f-899b-b758d1db3426
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 99ca6c9509f25c118931ccab981987b3427e4b2d
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="rendering-data-regions-report-builder-and-ssrs"></a>呈现数据区域（报表生成器和 SSRS）
  除了适用于所有报表项的常规呈现行为外，数据区域还要遵循其他一些分页和呈现行为。 特定于数据区域的呈现规则包括数据区域如何增长，如何呈现特殊的单元（如角单元或标题单元）以及如何呈现从右向左读的数据区域。 本主题将介绍如何呈现数据区域的各个部分。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="tablix-data-regions"></a>Tablix 数据区域  
 利用 Tablix 数据区域可以创建表、矩阵和列表，这种数据区域呈现为由列和行组成的网格。 行和列相交便形成单元。 呈现时，这种单元可以包含数据或其他报表项，如图像、矩形、文本框或子报表。 Tablix 数据区域可以垂直和/或水平增长。 此外，角单元、数据区域标题单元和数据区域正文单元可以根据其内容增长。 如果数据区域跨越多页，则在显示该数据区域的每一页上都会呈现设置为随该数据区域重复的报表项。 有关详细信息，请参阅 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
### <a name="right-to-left"></a>从右向左  
 当 Tablix 数据区域设置为从右向左显示时，其呈现时的结构就像其从左向右呈现时该数据区域的镜像一样。 数据区域的角显示在右上角。 如果报表中存在动态列，则它们将向左扩展。 从右到左的设置不会影响数据在数据区域中的顺序；只是列的顺序会有所不同。  
  
### <a name="tablix-headers"></a>Tablix 标题  
 Tablix 标题呈现为行标题或列标题，具体取决于标题单元在行组层次结构或列组层次结构中的显示位置。 如果在标题的单元内容内存在逻辑分页符，则会将其忽略。 也会忽略列组上的逻辑分页符。  
  
 组上的逻辑分页符不会导致外部组标题断开。 例如，假定报表具有国家这一外部组和国家地区这一内部组。 如果在国家地区组的实例之间存在逻辑分页符，则报表的两页上都会显示国家这一外部组。  
  
#### <a name="repeated-tablix-headers"></a>重复的 Tablix 标题  
 在“属性”窗格中设置 RepeatWith 属性时，在数据区域内不会改变的项（例如列标题）将会在呈现该部分数据区域的每页上重复显示。 例如，如果某行数据显示在下一页并且设置了 Repeat With 属性，则列标题也会显示在呈现的页上。  
  
### <a name="tablix-corner"></a>Tablix 角  
 左上角称为 Tablix 角。 Tablix 角内可以包含其他报表项，但如果在这种角内插入逻辑分页符，则在呈现 Tablix 数据区域时，将会忽略这些分页符。  
  
### <a name="tablix-body"></a>Tablix 正文  
 Tablix 正文由 Tablix 单元组成。 Tablix 正文根据分页规则和报表项的呈现行为来呈现。 有关详细信息，请参阅 [呈现报表项（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)。  
  
## <a name="chart-gauge-and-map-data-regions"></a>图表、仪表和映射数据区域  
 图表、仪表和映射数据区域在表体中呈现和显示时其行为与图像的行为类似。 数据区域内的值可以具有关联的操作，例如链接到其他报表或转至书签；并且如果呈现器支持，这些操作也可以呈现出来。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的分页（报表生成器和 SSRS）](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [呈现报表项（报表生成器和 SSRS）](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [仪表（报表生成器和 SSRS）](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
