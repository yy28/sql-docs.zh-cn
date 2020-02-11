---
title: 创建共享数据集或嵌入数据集（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d1d7bc71-f0e9-4ce5-b3ad-6fee54388a31
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 208c5608037d99b9dc02f1ab7fefd151cd4bdecf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107427"
---
# <a name="create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs"></a>创建共享数据集或嵌入数据集（报表生成器和 SSRS）
  您可以创建供单个报表使用的嵌入数据集，也可以创建供多个报表使用的保存到报表服务器的共享数据集。 若要创建数据集，必须具有嵌入数据源或共享数据源。  
  
 使用报表生成器可以执行以下任务：  
  
-   在数据集设计视图下创建共享数据集。 共享数据集必须使用已发布的共享数据源。  
  
-   在报表设计视图中创建嵌入数据集。  
  
-   将数据集直接保存到报表服务器或 SharePoint 站点。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中使用报表设计器可以执行以下任务：  
  
1.  在解决方案资源管理器中创建共享数据集。 共享数据集必须使用来自解决方案资源管理器的“共享数据源”文件夹中的数据源。  
  
2.  在“报表数据”窗格中创建嵌入数据集。  
  
3.  也可以将共享数据集和共享数据源与报表一起部署。 对于每种类型的项，使用“项目属性”可以指定指向报表服务器或 SharePoint 站点上的文件夹的路径。  
  
 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-open-report-builder-and-create-a-shared-dataset"></a>打开报表生成器和创建共享数据集  
  
1.  打开报表生成器。 
  **“新建报表或数据集”** 窗格将打开，如下图所示：  
  
     ![rs_NewSharedDataset](../media/rs-newshareddataset.gif "rs_NewSharedDataset")  
  
    > [!NOTE]  
    >  如果不显示“新建报表或数据集”窗格，则从“报表生成器”按钮中单击“新建”********。  
  
2.  在左窗格的 **“创建数据集”** 下，单击 **“共享数据集”**。  
  
3.  在右窗格中，单击 **“浏览”** 从报表服务器选择共享数据源，然后单击 **“创建”**。 将打开与共享数据源关联的查询设计器。  
  
4.  在查询设计器中，指定要包含在数据集中的字段。  
  
5.  单击 "**运行**" （**！**）以运行查询。  
  
6.  在 **“报表生成器”** 按钮上，单击 **“保存”** 或 **“另存为”** 将共享数据集保存到报表服务器。  
  
7.  若要退出报表生成器，请单击 **“报表生成器”**，然后单击 **“退出报表生成器”**。 若要处理报表，请单击 **“报表生成器”**，然后单击 **“新建”** 或 **“打开”**。  
  
### <a name="to-set-query-parameter-options"></a>设置查询参数选项  
  
1.  打开报表生成器。  
  
2.  单击 **“打开”** 。  
  
3.  浏览到报表服务器，为共享数据源选择文件夹。  
  
4.  在 **“项类型”** 的下拉列表中单击“数据集 (*.rsd)”。  
  
5.  选中共享数据集，然后单击 **“打开”**。 将打开关联的查询设计器。  
  
6.  在功能区上，单击 **“数据集属性”**。  
  
7.  单击 **“参数”** 。 在此页上，将默认值设置为一个常量或者一个表达式，将该参数标记为只读、可以为 null 或“从查询中省略”****。 有关详细信息，请参阅[“数据集属性”对话框 ->参数（报表生成器）](../dataset-properties-dialog-box-parameters-report-builder.md)。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
### <a name="to-create-a-dataset-from-a-sql-server-relational-database"></a>从 SQL Server 关系数据库创建数据集  
  
1.  在“报表数据”窗格中，右键单击数据源的名称，然后单击 **“添加数据集”**。 此时将打开 **“数据集属性”** 对话框的 **“查询”** 页。  
  
2.  在 **“名称”** 中，键入数据集的名称，或接受默认名称。  
  
    > [!NOTE]  
    >  数据集名称将在报表内部使用。 为便于识别，建议在数据集名称中对查询所返回的数据予以描述。  
  
3.  在 **“数据源”** 中，浏览并选择现有共享数据源的名称，或单击 **“新建”** 创建新的嵌入数据源。  
  
4.  选择 **“查询类型”** 选项。 具体选项取决于数据源类型。  
  
    -   选择 **Text** 可以采用该数据源的查询语言编写查询。  
  
    -   选择 **Table** 可以返回关系数据库表中的所有字段。  
  
    -   选择 **StoredProcedure** 可以按名称运行存储过程。  
  
5.  在 **“查询”** 中，键入查询、存储过程或表名。 此外，也可以单击 **“查询设计器”** 打开图形查询设计器或基于文本的查询设计器工具，或单击 **“导入”** 从现有报表中导入查询。  
  
     在少数情况下，查询指定的字段集合只能通过在数据源中运行查询来确定。 例如，存储过程可能在结果集中返回可变字段集。 单击 **“刷新字段”** 可以在数据源中运行查询，并检索填充“报表数据”窗格中的数据集字段集合时所需的字段名称。 关闭 **“数据集属性”** 对话框后，将在数据集节点下显示字段集合。  
  
6.  在 **“超时”** 中，键入报表服务器等待数据库响应的秒数。 默认值为 0 秒。 超时值为 0 秒时，查询将不会超时。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     数据集及其字段集合显示在“报表数据”窗格的数据源节点下。  
  
## <a name="see-also"></a>另请参阅  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)   
 [查询设计器 &#40;报表生成器&#41;](../query-designers-report-builder.md)   
 [报表生成器对话框、窗格和向导的帮助](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md)   
 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [嵌入数据集和共享数据集 &#40;报表生成器和 SSRS&#41;](embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
