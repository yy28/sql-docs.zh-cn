---
title: "查看多维数据集和维度属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: dda922b8-6d75-4662-b09e-8a317c6a1c70
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d0913972ef2ca0b1c40c0e23d3d189a6149809cf
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="lesson-2-4---reviewing-cube-and-dimension-properties"></a>课程 2-4-查看多维数据集和维度属性
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

在定义多维数据集后，可以使用多维数据集设计器检查结果。 在下面的任务中，您将检查 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目中多维数据集的结构。  
  
### <a name="to-review-cube-and-dimension-properties-in-cube-designer"></a>在多维数据集设计器中检查多维数据集和维度的属性  
  
1.  若要打开多维数据集设计器，请双击解决方案资源管理器中“多维数据集”节点中的“Analysis Services 教程”多维数据集。  
  
2.  在多维数据集设计器中的“多维数据集结构”选项卡的“度量值”窗格中，展开“Internet 销售”度量值组以显示所定义的度量值。  
  
    将度量值拖到所需的顺序中可以更改它们的顺序。 所创建的度量值顺序将影响某些客户端应用程序对这些度量值进行排序的方式。 度量值组及其包含的每个度量值都有属性，在“属性”窗口中可以编辑这些属性。  
  
3.  在多维数据集设计器中，在“多维数据集结构”选项卡的“维度”窗格中，检查 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集中的多维数据集维度。  
  
    请注意，尽管在数据库级别只创建了三个维度（如解决方案资源管理器所示），但在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集内却有五个多维数据集维度。 该多维数据集包含的维度比数据库多，其原因是，根据事实数据表中与日期相关的不同事实数据，“日期”数据库维度被用作三个与日期相关的单独多维数据集维度的基础。 这些与日期相关的维度也称为“角色扮演维度”。 使用三个与日期相关的多维数据集维度，用户可以按照下列三个与每个产品销售相关的单独事实数据在多维数据集中组织维度：产品订单日期、履行订单的到期日期和订单发货日期。 通过将一个数据库维度重复用于多个多维数据集维度，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 简化了维度管理，降低了磁盘空间使用量，并减少了总体处理时间。  
  
4.  在“多维数据集结构”选项卡的“维度”窗格中，展开“客户”，然后单击“编辑客户”，以便在维度设计器中打开该维度。  
  
    维度设计器包含以下选项卡：“维度结构”、“属性关系”、“转换”和“浏览器”。 请注意，“维度结构”选项卡包含以下三个窗格：“属性”、“层次结构”和“数据源视图”。 维度中包含的属性显示在“属性”窗格中。 有关详细信息，请参阅[维度特性属性参考](../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)、[创建用户定义的层次结构](../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)和[定义属性关系](../analysis-services/multidimensional-models/attribute-relationships-define.md)。  
  
5.  要切换到多维数据集设计器，请在解决方案资源管理器中右键单击“多维数据集”节点中的“Analysis Services 教程”多维数据集，然后单击“视图设计器”。  
  
6.  在多维数据集设计器中，单击“维度用法”选项卡。  
  
    在此 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集视图中，可以看到“Internet 销售”度量值组所用的多维数据集维度。 此外，可以定义每个维度及使用该维度的每个度量值组之间的关系类型。  
  
7.  单击“分区”选项卡。  
  
    多维数据集向导可以使用不带聚合的多维联机分析处理 (MOLAP) 存储模式，为多维数据集定义单个分区。 通过 MOLAP，所有叶级别数据和所有聚合均存储在多维数据集中，以便最大限度地提高性能。 聚合是预先计算好的数据汇总，聚合可以在问题提出之前准备好答案，从而可以缩短查询响应时间。 可在“分区”选项卡上定义其他分区、存储设置和写回设置。有关详细信息，请参阅[分区（Analysis Services - 多维数据）](../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)和[聚合和聚合设计](../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)。  
  
8.  单击 **“浏览器”** 选项卡。  
  
    注意，由于浏览多维数据集尚未部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例中，因此无法对其进行浏览。 此时， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目中的多维数据集只是一个可以部署到任何 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例的多维数据集定义。 部署和处理多维数据集时，将在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中创建定义的对象，然后用基础数据源的数据填充这些对象。  
  
9. 在解决方案资源管理器中，右键单击“多维数据集”节点中的“Analysis Services 教程”，然后单击“查看代码”。 您可能需要等待。  
  
    此时在“[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.cube [XML]”选项卡上显示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的 XML 代码。这是在部署期间在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中创建多维数据集所用的实际代码。 有关详细信息，请参阅[查看 Analysis Services 项目的 XML (SSDT)](../analysis-services/multidimensional-models/view-the-xml-for-an-analysis-services-project-ssdt.md)。  
  
10. 关闭 XML 代码选项卡。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[部署 Analysis Services 项目](../analysis-services/lesson-2-5-deploying-an-analysis-services-project.md)  
  
## <a name="see-also"></a>另请参阅  
[在维度设计器中浏览维度数据](../analysis-services/multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)  
  
  
  
