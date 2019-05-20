---
title: 从数据挖掘模型检索数据 (DMX) (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- retrieving report data
- datasets [Reporting Services], with DMX queries
- datasets [Reporting Services], Analysis Services
- queries [Reporting Services], data mining prediction
ms.assetid: d9cd3624-1594-4707-8887-55437dd7e07c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fd2ff43f969f198b418a1bf6437e351c2c663391
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571202"
---
# <a name="retrieve-data-from-a-data-mining-model-dmx-ssrs"></a>从数据挖掘模型检索数据 (DMX) (SSRS)
  若要在报表中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据挖掘模型中的数据，则必须定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源以及一个或多个报表数据集。 创建数据源定义时，必须指定连接字符串和凭据，以便能够从客户端计算机访问该数据源。  
  
 可以创建供单个报表使用的嵌入数据源定义，也可以创建可由多个报表使用的共享数据源定义。 本主题中的过程介绍如何创建嵌入数据源。 有关共享数据源的详细信息，请参阅[嵌入和共享的数据连接或数据源（报表生成器和 SSRS）](https://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56)和[创建、修改和删除共享数据源 (SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)。  
  
 创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源后，可以创建一个或多个数据集。 对于每个数据集，您都可以使用数据挖掘预测表达式 (DMX) 查询设计器来创建指定字段集合的 DMX 查询。 有关详细信息，请参阅 [Analysis Services DMX 查询设计器用户界面](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)。  
  
 创建数据集后，数据集的名称将在“报表数据”窗格中该数据集的数据源节点下显示为节点。  
  
 报表发布后，您可能需要更改数据源的凭据，以使报表在报表服务器上运行时，用于检索数据的权限有效。  
  
### <a name="to-create-an-embedded-microsoft-sql-server-analysis-services-data-source"></a>创建 Microsoft SQL Server Analysis Services 嵌入数据源  
  
1.  在“报表数据”窗格的工具栏上，单击 **“新建”**，然后单击 **“数据源”**。  
  
2.  在 **“数据源属性”** 对话框的 **“名称”** 文本框中键入名称，或接受默认名称。  
  
3.  确保已选中 **“嵌入连接”** 。  
  
4.  从“类型”下拉列表中，选择“Microsoft SQL Server Analysis Services”。  
  
5.  指定使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源的连接字符串。  
  
     请联系数据库管理员，获取连接信息以及用于连接到数据源的凭据。 下面的连接字符串示例指定本地客户端上的 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 示例数据库。  
  
    ```  
    Data Source=localhost;Initial Catalog=AdventureWorksDW2012  
    ```  
  
6.  单击 **“凭据”**。  
  
     设置用于连接到数据源的凭据。 有关详细信息，请参阅[为报表数据源指定凭据和连接信息](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
    > [!NOTE]  
    >  若要测试数据源连接，请单击 **“编辑”**。 单击 **“连接属性”** 对话框中的 **“测试连接”**。 如果测试成功，您将会看到信息性消息“连接测试成功”。 如果测试失败，您将会看到一条警告消息，其中包含有关测试失败原因的详细信息。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     数据源将显示在“报表数据”窗格中。  
  
### <a name="to-create-a-dataset-for-a-microsoft-sql-server-analysis-services"></a>创建 Microsoft SQL Server Analysis Services 的数据集  
  
1.  在“报表数据”窗格中，右键单击连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源的数据源的名称，然后单击“添加数据集”。  
  
2.  在 **“数据集属性”** 对话框的 **“名称”** 文本框中键入名称。  
  
3.  在 **“数据源”** 框中，验证名称是否为连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源的数据源的名称。  
  
4.  单击 **“查询设计器”** 打开图形查询设计器，从而以交互方式生成查询。 如果查询设计器以 MDX 模式打开，请单击工具栏上的“命令类型 DMX”（![更改为 DMX 查询语言视图](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "Change to DMX query language view")）以切换到数据挖掘查询设计器。 有关详细信息，请参阅 [Analysis Services DMX 查询设计器用户界面](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)。  
  
     或者，若要从另一个报表导入现有的 DMX 查询，请单击 **“导入”**，然后导航到包含 DMX 查询的 .rdl 文件。 不支持从 .dmx 文件导入查询。  
  
5.  通过创建并运行查询查看示例结果后，请单击 **“确定”**。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     数据集及其字段集合显示在“报表数据”窗格的数据源节点下。  
  
## <a name="see-also"></a>另请参阅  
 [针对 DMX 的 Analysis Services 连接类型 (SSRS)](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [数据集字段集合（报表生成器和 SSRS）](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
