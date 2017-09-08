---
title: "使用修改后的版本的 Analysis Services Tutorial 项目 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 685aa217-de1b-4df2-bf22-095228c40775
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 10cb63369b23a19ecb126ee210de2a90ed114fc4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-4-1---using-a-modified-version-of-the-analysis-services-tutorial-project"></a>Lesson 4-1-使用 Analysis Services 教程项目的修改的版本
本教程中的其余几节课基于您已在前三课中完成的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目的增强版本。 已向 **Adventure Works DW 2012[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源视图中添加了额外的表和命名计算；已向该项目添加了额外的维度，并且已将这些新维度添加到**  Tutorial 多维数据集内。 此外，还添加了另一个度量值组，该组包含另一个事实数据表中的度量值。 这一增强项目使您无需重复学习前面已了解的技能，即可继续学习如何在商业智能应用程序中添加功能。  
  
在继续本教程之前，必须下载、解压缩、加载和处理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目的增强版本。  请使用本课程中的说明以确保您已执行了所有步骤。  
  
## <a name="downloading-and-extracting-the-project-file"></a>下载并解压缩项目文件  
  
1.  [单击此处](http://go.microsoft.com/fwlink/?LinkID=221866) 可以转到下载页，此页提供本教程随附的示例项目。 教程项目包括在 **Analysis Services 教程 SQL Server 2012** 下载中。  
  
2.  单击“Analysis Services 教程 SQL Server 2012”可下载包含此教程项目的包。  
  
    默认情况下，.zip 文件将保存到 Downloads 文件夹。 您必须将该 .zip 文件移到具有更短路径的位置（例如，创建一个 C:\Tutorials 文件夹以便存储这些文件）。  然后，您可以解压缩在该 .zip 文件中包含的文件。 如果您尝试从具有较长路径的 Downloads 文件夹解压缩这些文件，将只会获得课程 1。  
  
3.  在根驱动器处或附近创建一个子文件夹，例如 C:\Tutorial。  
  
4.  将 **Analysis Services Tutorial SQL Server 2012.zip** 文件移到子文件夹。  
  
5.  右键单击该文件，然后选择“全部提取”。  
  
6.  浏览到 **Lesson 4 Start** 文件夹，以便找到 **Analysis Services Tutorial.sln** 文件。  
  
## <a name="loading-and-processing-the-enhanced-project"></a>加载和处理增强的项目  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的“文件”菜单上，单击“关闭解决方案”以便关闭不使用的文件。  
  
2.  在“文件”菜单中，指向“打开”，然后单击“项目”/“解决方案”。  
  
3.  浏览到将教程项目文件解压缩到的位置。  
  
    找到名为 **Lesson 4 Start**的文件夹，双击 Analysis Services Tutorial.sln。  
  
4.  将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目的增强版本部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的本地实例或其他实例，并确认处理已成功完成。  
  
## <a name="understanding-the-enhancements-to-the-project"></a>了解该项目的增强功能  
该项目的增强版本与前三节课程中所完成 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目的版本不同。 下面几节说明了具体的差异。 在继续学习本教程的其余课程之前，请查看此信息。  
  
### <a name="data-source-view"></a>数据源视图  
该增强的项目的数据源视图中新增了来自 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库的一个事实数据表和四个维度表。  
  
可以看到该数据源视图包含十个表， <All Tables> 关系图变得很拥挤， 因此很难轻松理解各表之间的关系并找到特定表。 为了解决这一问题，将这些表组织为两个逻辑关系图：“Internet 销售”关系图和“分销商销售”关系图。 这两个关系图均围绕一个事实数据表进行组织。 通过创建逻辑关系图，您可以在数据源视图中查看和使用表的特定子集，而无需始终在一个关系图中查看所有表及其关系。  
  
#### <a name="internet-sales-diagram"></a>“Internet 销售”关系图  
“Internet 销售”关系图包含与直接通过 Internet 向客户销售 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 产品相关的表。 该关系图包含四个维度表和一个事实表，在第 1 课中已经将这些表添加到 **Adventure Works DW 2012** 数据源视图。 这些表包括：  
  
-   **Geography**  
  
-   **Customer**  
  
-   **日期**  
  
-   **Product**  
  
-   **InternetSales**  
  
#### <a name="reseller-sales-diagram"></a>“分销商销售”关系图  
“分销商销售”关系图包含与分销商销售 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 产品相关的表。 该关系图包含来自 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库的下列七个维度表和一个事实数据表：  
  
-   **Reseller**  
  
-   **Promotion**  
  
-   **SalesTerritory**  
  
-   **Geography**  
  
-   **日期**  
  
-   **Product**  
  
-   **Employee**  
  
-   **ResellerSales**  
  
请注意，“Internet 销售”关系图和“分销商销售”关系图中都使用了 **DimGeography**、**DimDate** 和 **DimProduct** 表。 维度表可链接到多个事实数据表。  
  
### <a name="database-and-cube-dimensions"></a>数据库和多维数据集维度  
[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目包含五个新数据库维度，而 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集包含与此相同的五个维度作为多维数据集维度。 这些维度已定义为具有通过使用命名计算、组合成员键和显示文件夹修改过的用户层次结构和属性。 下面的列表对这些新维度进行了说明。  
  
“分销商”维度  
“分销商”维度基于 **Adventure Works DW 2012** 数据源视图中的 **Reseller** 表。  
  
“促销”维度  
“促销”维度基于 **Adventure Works DW 2012** 数据源视图中的 **Promotion** 表。  
  
“销售区域”维度  
“销售区域”维度基于 **Adventure Works DW 2012** 数据源视图中的 **SalesTerritory** 表。  
  
“雇员”维度  
“雇员”维度基于 **Adventure Works DW 2012** 数据源视图中的 **Employee** 表。  
  
“地域”维度  
“地域”维度基于 **Adventure Works DW 2012** 数据源视图中的 **Geography** 表。  
  
#### <a name="analysis-services-cube"></a>Analysis Services 多维数据集  
现在， **Analysis Services Tutorial** 多维数据集包含两个度量值组：原始度量值组和另一个度量值组；前者基于 **InternetSales** 表，后者基于 **Adventure Works DW 2012** 数据源视图中的 **ResellerSales** 表。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[定义父子层次结构中的父特性属性](../analysis-services/lesson-4-2-defining-parent-attribute-properties-in-a-parent-child-hierarchy.md)  
  
## <a name="see-also"></a>另请参阅  
[部署 Analysis Services 项目](../analysis-services/lesson-2-5-deploying-an-analysis-services-project.md)  
  

