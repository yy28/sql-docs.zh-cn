---
title: 将数据添加到报表 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f2e42303-e355-4c1f-bb3b-3338fbdd230d
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0f12d893aa1f37ffa3c35f5e295a991502ed9d85
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658211"
---
# <a name="add-data-to-a-report-report-builder-and-ssrs"></a>向报表添加数据（报表生成器和 SSRS）
  若要向报表中添加数据，您需要创建数据集。 每个数据集都表示通过对数据源运行查询命令而获得的结果集。 结果集中的列是字段集合。 结果集中的行是数据。 数据集不包含实际数据。 数据集而是包含从数据源检索一组特定的数据所需的信息。  
  
 有两种类型的数据集：嵌入数据集和共享数据集。 嵌入数据集在某一报表中定义并且只由该报表使用。 共享数据集在报表服务器或 SharePoint 站点上定义，并且可由多个报表使用。 在报表生成器中，您可以在共享数据集模式下创建共享数据集，或者在报表设计器模式下创建嵌入数据集。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的报表设计器中，您可以将共享数据集作为项目的一部分创建，或者将嵌入数据集作为报表的一部分创建。  
  
-   **嵌入数据集。** 与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 之类你可以直接在工作表中使用数据的应用程序不同，在报表生成器或报表设计器中，你所使用的元数据表示在处理报表时将检索的数据。 若要创建嵌入数据集，请选择数据源并且指定一个查询。 创建数据集后，可以使用“报表数据”窗格查看字段集合。 您可以显示来自数据区域（例如表或图表）中的数据集的数据。 在各数据区域中，您可以对数据进行分组、筛选和排序，以便对数据进行组织。 在设计报表布局后，您运行该报表以查看实际的数据。  
  
     在下图中，“报表数据”窗格显示名为 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]的数据源、名为 DataSet1 的数据集，并且在数据集字段集合中有五个字段。 “布局”窗格显示一个表，该表的顶行是列标题，底行具有包含文本的表单元。 占位符文本 [名称] 是字段“Name”的元数据。 在该报表运行时，占位符文本将被实际数据值替换。 可以根据需要扩展表以显示所有数据。  
  
     ![rs_DataDesignandPreview](../media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  
  
-   **共享数据集。** 当你想要在多个报表中使用数据集时创建共享数据集。 若要创建一个共享数据集或者将共享数据集保存到报表服务器或 SharePoint 站点，请在共享数据集设计视图中使用报表生成器。 若要将共享数据集作为可部署到服务器或站点的项目的一部分创建，请使用报表设计器。  
  
     下图显示报表生成器中的共享数据集设计视图。 您可以选择或修改数据连接、数据集属性、查询、筛选器，选择将筛选器标记为参数，以及查看查询结果。 然后，将更改保存回服务器或站点。  
  
     ![rs_SharedDatasetDesignMode](../media/rs-shareddatasetdesignmode.gif "rs_SharedDatasetDesignMode")  
  
 有关详细信息，请参阅[嵌入和共享的数据集（报表生成器和 SSRS）](embedded-and-shared-datasets-report-builder-and-ssrs.md)和[嵌入和共享的数据连接或数据源（报表生成器和 SSRS）](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)。  
  
 您还可以通过添加包括其所依赖的数据集的报表部件，向报表添加数据集。 [!INCLUDE[ssRBrptparts](../../../includes/ssrbrptparts-md.md)]  
  
 若要了解如何创建显示来自数据的报表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，请参阅[教程：生成基本表报表（报表生成器）](../tutorial-creating-a-basic-table-report-report-builder.md)。 若要生成的报表，包括其自己的数据，请参阅[教程：脱机生成快速图表报表（报表生成器）](../report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Methods"></a> 添加报表数据  
 在报表生成器中，您可以通过以下方式添加报表数据。  
  
-   将报表部件从报表服务器添加到报表。 每个报表部件都是独立的并包括相关数据集。 这些数据集是预定义的。  
  
-   使用表/矩阵、图表和地图向导。 从这些向导中，您可以选择共享数据源和共享数据集，或者创建新数据集，并继续设计报表。  
  
-   从报表服务器添加共享数据集。 共享数据集是预定义的数据集并指定从预定义数据源中要使用的数据。 在您向报表中添加共享数据集时，将添加指向共享数据集定义的数据集引用。  
  
 在报表生成器或报表设计器中，您可以通过以下方式添加报表数据。  
  
-   基于共享数据源添加嵌入数据集。  
  
-   基于嵌入数据源添加嵌入数据集。  
  
> [!NOTE]  
>  在报表服务器上，将单独确保共享项的安全，或者通过从发布这些共享项的文件夹继承权限来确保它们的安全。 为了使其他用户有权访问您保存的共享数据集，您必须理解授予权限的方式。 有关详细信息，请参阅[安全性（报表生成器）](../report-builder/security-report-builder.md)或[保护共享数据集项](../security/secure-shared-dataset-items.md)。  
  
 向报表添加数据后，可以使用数据区域对报表页上的数据进行排列，修改报表部件并与其他人共享这些更改，以及使用户能够限制在报表中所看到的数据或者对数据进行排序。 有关详细信息，请参阅下列相关主题：  
  
-   [表、矩阵和列表（报表生成器和 SSRS）](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
-   [图表&#40;报表生成器和 SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
-   [迷你图和数据条（报表生成器和 SSRS）](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
-   [指示器（报表生成器和 SSRS）](../report-design/indicators-report-builder-and-ssrs.md)  
  
-   [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [报表部件（报表生成器和 SSRS）](../report-parts-report-builder-and-ssrs.md)  
  
-   [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  

##  <a name="QuickStart"></a> 通过报表部件添加数据  
 报表部件包含它们所依赖的数据集。 这些数据集是在报表服务器上提供的共享数据源的基础上生成的。 在报表生成器中，在向您的报表中添加报表部件时，相关数据集将添加到报表中，就像您手动添加了它们一样。 例如，一个预定义的图表包含一个数据集。 若要查看数据，请预览报表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBrptparts](../../../includes/ssrbrptparts-md.md)]  
  
 报表部件、共享数据源和共享数据集将预先定义并保存在某一报表服务器上。 若要访问它们，您必须通过连接到该报表服务器，在服务器模式下打开报表生成器。 如果您对该报表服务器具有写入权限，则可以使用它们创建您自己的新版本。  
  
-   有关详细信息，请参阅[报表部件（报表生成器和 SSRS）](../report-parts-report-builder-and-ssrs.md)和[报表设计器中的报表部件 (SSRS)](../report-design/report-parts-in-report-designer-ssrs.md)。  

##  <a name="Queries"></a> 查询和查询设计器  
 若要指定数据源中所需的数据，您应该生成一个查询命令。 每种数据源类型都提供相关的“查询设计器”  ，以帮助您生成查询。 查询设计器可为图形查询设计器或基于文本的查询设计器。 在图形查询设计器中，可查看表示外部数据源中数据的元数据，并且通过将字段或实体拖到查询设计曲面图，以交互方式生成查询。 在基于文本的查询设计器中，您可以按照外部数据源支持的查询语法编写或导入查询。  
  
 在查询设计器中，可以运行查询以查看示例数据并验证查询命令语法。 结果集中的列名将成为您在“报表数据”窗格中看到的字段名称。 结果集必须是单组行和列，在其中，为每行数据存在相同数目的值。 不支持来自单个查询的多个结果集。 不支持不具有固定数目的列并且可为每一行生成不同数目的数据值的不规则层次结构。  
  
 若要运行查询，您必须具有设计时凭据。 有关详细信息，请参阅[在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)并[数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
 数据扩展插件和外部数据源之间的通信由数据提供程序处理。 对查询命令语法的支持、查询参数和结果集中值的数据类型由各数据访问接口确定。 有关详细信息，请参阅针对数据扩展插件和[查询设计器（报表生成器）](../query-designers-report-builder.md)的特定类型的主题。  

##  <a name="HowTo"></a> 操作指南主题  
 [添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [在“报表数据”窗格中添加、编辑和刷新字段（报表生成器和 SSRS）](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
 [在关系查询设计器中生成查询（报表生成器和 SSRS）](build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)  
  
 [为多维数据的参数值显示隐藏的数据集（报表生成器和 SSRS）](show-hidden-datasets-for-parameter-values-multidimensional-data.md)  
  
 [向数据集添加筛选器（报表生成器和 SSRS）](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 [为数据区域设置“无数据”消息（报表生成器和 SSRS）](set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [将查询参数与报表参数相关联（报表生成器和 SSRS）](associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md)  
  
 [在 Analysis Services 的 MDX 查询设计器中定义参数（报表生成器和 SSRS）](define-parameters-in-the-mdx-query-designer-for-analysis-services.md)  

##  <a name="Section"></a> 本节内容  
 [报表生成器中的报表部件和数据集](report-parts-and-datasets-in-report-builder.md)  
  
 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
 [在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)  
  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)  

## <a name="see-also"></a>请参阅  
 [报表设计视图（报表生成器）](../report-builder/report-design-view-report-builder.md)   
 [报表创作概念（报表生成器和 SSRS）](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
