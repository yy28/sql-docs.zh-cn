---
title: 定义被引用的关系 |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 4a34ba52-e3b3-4e8a-8e55-73e0cd5a97bd
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ba7dcd01ce03f661de6f929f748944a91dea46c0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-5-1---defining-a-referenced-relationship"></a>Lesson 5-1-定义被引用的关系
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

在本教程中到目前为止，您定义的每个多维数据集维度都基于一个按主键到外键的关系直接链接到度量值组事实数据表的表。 在本主题的各任务中，你会将“地域”维度通过一个称为“引用维度”的“分销商”维度链接到分销商销售额的事实数据表。 这允许用户按地域定义经销商销售额的维度。 有关详细信息，请参阅 [定义引用的关系和引用的关系属性](../analysis-services/multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)。  
  
## <a name="dimensioning-reseller-sales-by-geography"></a>按地域定义分销商销售维度  
  
1.  在解决方案资源管理器中，右键单击“多维数据集”文件夹中的“Analysis Services 教程”，然后单击“浏览”。  
  
2.  删除“数据”窗格中的所有层次结构，然后验证“分销商销售-销售额”度量值是否出现在“数据”窗格的数据区域中。 如果未出现该度量值，则请将其添加到“数据”窗格中。  
  
3.  将“地域”用户定义层次结构从“元数据”窗格中的“地域”维度拖到“数据”窗格的“将行字段拖至此处”区域。  
  
    请注意，“分销商销售-销售额”度量值并未按照“区域”层次结构中的“国家/地区-区域”属性成员正确确定维度。 对于每个“国家/地区-区域”属性成员都重复“分销商销售-销售额”的值。  
  
    ![分销商销售 Sales Amount 度量值进行维度化](../analysis-services/media/l5-referencedrelationship-1.gif "进行维度化分销商销售 Sales Amount 度量值")  
  
4.  打开 **Adventure Works DW 2012** 数据源视图的数据源视图设计器。  
  
5.  在“关系图组织程序”窗格中，查看 **Geography** 表和 **ResellerSales** 表之间的关系。  
  
    注意，这些表之间没有直接链接。 但是，它们之前存在通过“Reseller”表和“SalesTerritory”表进行的间接链接。  
  
6.  双击表示 **Geography** 表和 **Reseller** 表之间的关系的箭头。  
  
    在“编辑关系”对话框中，注意 **GeographyKey** 列既是 **Geography** 表中的主键，又是 **Reseller** 表中的外键。  
  
7.  单击“取消”，切换到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器，然后单击“维度用法”选项卡。  
  
    注意，“地域”多维数据集维度当前与“Internet 销售”度量值组或“分销商销售”度量值组都没有关系。  
  
8.  单击“客户”维度和“Internet 销售”度量值组相交处的“全名”单元中的省略号按钮 (**…**)。  
  
    在“定义关系”对话框中，注意，在 **DimCustomer** 维度表和 **FactInternetSales** 度量值组表之间，根据每个表中的 **CustomerKey** 列定义了“常规”关系。 到目前为止，您在本教程中定义的所有关系都是常规关系。  
  
    下图显示了“定义关系”对话框，其中常规关系是 **DimCustomer** 维度表和 **FactInternetSales** 度量值组表之间的关系。  
  
    ![定义关系对话框](../analysis-services/media/l5-referencedrelationship-4.gif "定义关系对话框中")  
  
9. 单击“取消”。  
  
10. 单击“地域”维度和“分销商销售”度量值组相交处的未命名单元中的省略号按钮 (**…**)。  
  
    在“定义关系”对话框中，可查看当前未定义“地域”多维数据集维度和“分销商销售”度量值组之间的关系。 无法定义常规关系，因为“地域”维度的维度表和“分销商销售”度量值组的事实数据表之间没有直接关系。  
  
11. 在“选择关系类型”列表中，选择“被引用的”。  
  
    你可以通过指定直接连接到度量值组表的维度来定义引用关系，该维度称为“中间维度”，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可以使用该维度将引用维度链接到事实数据表。 然后指定将引用维度链接到中间维度的属性。  
  
12. 在“中间维度”列表中，选择“分销商”。  
  
    “地域”维度的基础表通过“分销商”维度的基础表链接到事实数据表。  
  
13. 在“引用维度属性”列表中，选择“地域关键字”，然后尝试在“中间维度属性”列表中选择“地域关键字”。  
  
    注意，“地域关键字”并未出现在“中间维度属性”列表中。 这是因为 **GeographyKey** 列尚未定义为“分销商”维度中的属性。  
  
14. 单击“取消”。  
  
在下一个任务中，您将通过定义基于“分销商”维度中 GeographyKey 列的属性来解决此问题。  
  
## <a name="defining-the-intermediate-dimension-attribute-and-the-referenced-dimension-relationship"></a>定义中间维度属性和引用维度关系  
  
1.  打开“分销商”维度的维度设计器，然后查看“数据源视图”窗格中 **Reseller** 表内的列，再查看“属性”窗格中“分销商”维度内已定义的属性。  
  
    注意，尽管已将 GeographyKey 定义为 Reseller 表中的一列，但在“分销商”维度中并未基于此列定义任何维度属性。 Geography 被定义为“地域”维度中的维度属性，原因在于它是将该维度的基础表链接到事实数据表的键列。  
  
2.  若要将“地域关键字”属性添加到“分销商”维度中，右键单击“数据源视图”中的 **GeographyKey**，然后单击“从列新建属性”。  
  
3.  在“特性”窗格中，选择“地域关键字”，然后在“属性”窗口中，将 **AttributeHierarchyOptimizedState** 属性设置为**NotOptimized**，将 **AttributeHierarchyOrdered** 属性设置为 **False**，并将 **AttributeHierarchyVisible** 属性设置为**False**。  
  
    “分销商”维度中的“地域关键字”属性只能用于将“地域”维度链接到 Reseller Sales 事实数据表。 因为它不能用于浏览，所以不存在将该属性层次结构定义为可见的值。 而且，对该属性层次结构进行排序和优化只能为处理性能带来负面影响。 但是，必须启用该属性，使其作为两个维度之间的链接。  
  
4.  切换到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器，单击“维度用法”选项卡，然后单击“分销商销售”度量值组和“地域”多维数据集维度相交处的省略号按钮 (**…**)。  
  
5.  在“选择关系类型”列表中，选择“被引用的”。  
  
6.  在“中间维度”列表中，选择“分销商”。  
  
7.  在“引用维度属性”列表中，选择“地域关键字”，然后在“中间维度属性”列表中选择“地域关键字”。  
  
    注意，已选中“具体化”复选框。 这是 MOLAP 维度的默认设置。 在处理过程中，具体化维度属性链接可在维度的 MOLAP 结构中具体化或存储事实数据表和每行的引用维度之间的链接值。 这样做对处理性能和存储要求的影响不大，但会增强查询性能（有时会很显著）。  
  
8.  单击 **“确定”**。  
  
    注意，“地域”多维数据集维度现在已链接到“分销商销售”度量值组。 该图标指示此关系是引用维度关系。  
  
9. 在“维度用法”选项卡上的“维度”列表中，右键单击“地域”，然后单击“重命名”。  
  
10. 将该多维数据集维度的名称更改为 **Reseller Geography**。  
  
    由于该多维数据集维度现在已链接到“分销商销售”度量值组，所以用户可以从显式定义它在多维数据集中的用法中受益，避免可能造成的用户混淆。  
  
## <a name="successfully-dimensioning-reseller-sales-by-geography"></a>按地域成功定义分销商销售维度  
  
1.  在“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
2.  在部署成功完成后，在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器中单击“浏览器”选项卡，再单击“重新连接”按钮。  
  
3.  在“元数据”窗格中，展开“分销商所在地域”，右键单击“地域”，然后单击“添加到行区域”。  
  
    请注意，“分销商销售-销售额”度量值现在已按照“区域”用户定义层次结构中的“国家/地区-区域”属性正确确定了维度，如下图所示。  
  
    ![定义关系对话框](../analysis-services/media/l5-referencedrelationship-5.gif "定义关系对话框中")  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[定义事实关系](../analysis-services/lesson-5-2-defining-a-fact-relationship.md)  
  
## <a name="see-also"></a>另请参阅  
[属性关系](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
[定义引用的关系和引用的关系属性](../analysis-services/multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
  
  
