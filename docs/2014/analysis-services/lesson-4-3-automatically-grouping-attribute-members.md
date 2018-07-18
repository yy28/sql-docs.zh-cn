---
title: 自动将属性成员分组 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9fb2cda3-a122-4a4c-82e0-3454865eef04
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 10a6ae9dee61d211c178a42e38087ad104344343
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183424"
---
# <a name="automatically-grouping-attribute-members"></a>自动将属性成员分组
  在浏览多维数据集时，通常根据一个属性层次结构的成员来确定另一个属性层次结构的成员的维度。 例如，可以按城市、购买的产品或性别将客户销售分组。 但是，对于某些类型的属性，如果由 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 根据属性层次结构中的成员分布自动创建属性成员分组，将会很有用。 例如，可以让 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 创建客户的年收入值组。 进行此操作时，浏览属性层次结构的用户将看到组的名称和值，而不是成员本身。 这就限制了向用户显示的级别的数量，从而更有助于进行分析。  
  
 **DiscretizationMethod** 属性可以确定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 是否创建分组，并可确定要执行的分组类型。 默认情况下， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不执行任何分组。 如果启用了自动分组，则可以让 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 根据属性的结构自动确定最佳分组方法，也可以选择下面列表中的一个分组算法来指定分组方法：  
  
 **EqualAreas**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 创建分组范围，以便在各个组之间平均分布所有维度成员。  
  
 **Clusters**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用 K-Means 聚类分析方法和高斯分布，对输入值执行单一维度聚类分析，以此创建分组。 此选项只对数值列有效。  
  
 指定了一种分组方法后，必须使用 **DiscretizationBucketCount** 属性指定分组的数量。 有关详细信息，请参阅[对属性成员进行分组（离散化）](multidimensional-models/attribute-properties-group-attribute-members.md)。  
  
 在本主题的任务中，将对以下对象启用不同类型的分组： **客户** 维度中的年度收入值； **雇员** 维度中的雇员病假时数； **雇员** 维度中的雇员休假时数。 然后，处理并浏览 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集，以此查看各成员组的情况。 最后，修改成员组的参数，查看组类型更改的效果。  
  
## <a name="grouping-attribute-hierarchy-members-in-the-customer-dimension"></a>为“客户”维度中的属性层次结构成员分组  
  
1.  在解决方案资源管理器中，双击“维度”文件夹中的“客户”，打开“客户”维度的维度设计器。  
  
2.  在“数据源视图”窗格中，右键单击 Customer 表，再单击“浏览数据”。  
  
     注意，**YearlyIncome** 列的值的范围。 如果未启用成员分组，这些值将成为**年收入**属性层次结构的成员。  
  
3.  关闭“浏览 Customer 表”选项卡。  
  
4.  在“属性”窗格中，选择“年收入”。  
  
5.  在属性窗口中的值更改**DiscretizationMethod**属性设置为**自动**和更改的值**DiscretizationBucketCount**属性到`5`。  
  
     下图显示了修改后的“年收入”属性。  
  
     ![修改属性 Yearly Income](../../2014/tutorials/media/l4-discretizationmethod-1.gif "修改 Yearly Income 属性")  
  
## <a name="grouping-attribute-hierarchy-members-in-the-employee-dimension"></a>为“雇员”维度中的属性层次结构成员分组  
  
1.  切换到“雇员”维度的维度设计器。  
  
2.  在“数据源视图”窗格中，右键单击 **Employee** 表，再单击“浏览数据”。  
  
     注意 **SickLeaveHours** 列和 **VacationHours** 列的值。  
  
3.  关闭“浏览 Employee 表”选项卡。  
  
4.  在“属性”窗格中，选择“病假时间”。  
  
5.  在属性窗口中的值更改**DiscretizationMethod**属性设置为**群集**和更改的值**DiscretizationBucketCount**属性`5`.  
  
6.  在“属性”窗格中，选择“休假时间”。  
  
7.  在属性窗口中的值更改**DiscretizationMethod**属性设置为**Equal Areas**和更改的值**DiscretizationBucketCount**属性到`5`。  
  
## <a name="browsing-the-modified-attribute-hierarchies"></a>浏览已修改的属性层次结构  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
2.  成功完成部署后，切换到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器，然后单击“浏览”选项卡上的“重新连接”。  
  
3.  单击 Excel 图标，然后单击“启用”。  
  
4.  将“Internet 销售-销售额”度量值拖到数据透视表字段列表的“值”区域。  
  
5.  在字段列表中，展开“产品”维度，再将“产品型号系列”用户层次结构拖到字段列表的“行标签”区域。  
  
6.  展开字段列表的“客户”维度，再展开“人口统计”显示文件夹，然后将“年收入”属性层次结构拖到“列标签”区域。  
  
     “年收入”属性层次结构的成员现在已分为六个存储桶，其中包括一个用于年收入未知的客户的销量的存储桶。 并非所有的存储桶都会显示出来。  
  
7.  从列区域删除“年收入”属性层次结构，从“值”区域中删除“Internet 销售-销售额”度量值。  
  
8.  将“分销商销售-销售额”度量值添加到数据区域。  
  
9. 在字段列表中，展开“雇员”维度，展开“组织”，然后将“病假时间”拖到“列标签”。  
  
     注意，所有销售是由两个组中的其中一个组的雇员完成的。 另注意，病假时数为 32 - 42 小时的雇员完成的销售比病假时间为 20 - 31 小时的雇员完成的销售多得多。  
  
     下图显示了按雇员病假时数确定维度的销售。  
  
     ![按雇员病假划分销售保留小时](../../2014/tutorials/media/l4-discretizationmethod-2.gif "按雇员病假划分销售保留小时")  
  
10. 从“数据”窗格的列区域删除“病假时间”属性层次结构。  
  
11. 将“休假时间”添加到“数据”窗格的列区域。  
  
     注意，根据等区域分组方法，显示了两个组。 其他三个组因不包含数据值而被隐藏。  
  
## <a name="modifying-grouping-properties-and-reviewing-the-effect-of-the-changes"></a>修改分组属性并检查更改的效果  
  
1.  切换到“雇员”维度的维度设计器，然后在“属性”窗格中选择“休假时间”。  
  
2.  在“属性”窗口中，将 **DiscretizationBucketCount** 属性值更改为 **10**。  
  
3.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
4.  成功完成部署后，切换回 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集的多维数据集设计器。  
  
5.  在“浏览器”选项卡上单击“重新连接”，单击 Excel 图标，然后重新构建数据透视表，以便可以查看对分组方法的更改的效果：  
  
    1.  将“分销商销售-销售额”拖到值  
  
    2.  将休假时间（在“雇员组织”文件夹中）拖到列  
  
    3.  将产品型号系列拖到行  
  
     请注意，现在有三组具有“休假时间”属性的成员，这些成员都有产品销售值。 （其他七个组包含没有销售数据的成员。）  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [隐藏和禁用属性层次结构](../analysis-services/lesson-4-4-hiding-and-disabling-attribute-hierarchies.md)  
  
## <a name="see-also"></a>请参阅  
 [对属性成员进行分组&#40;离散化&#41;](multidimensional-models/attribute-properties-group-attribute-members.md)  
  
  
