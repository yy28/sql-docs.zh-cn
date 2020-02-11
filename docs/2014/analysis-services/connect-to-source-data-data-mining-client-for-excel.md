---
title: 连接到源数据（Excel 数据挖掘客户端） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
ms.assetid: 548672ce-e403-4aca-b67a-c2c797f053dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 468686314bb2446415a6883c6233708f9cbd1d2b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087103"
---
# <a name="connect-to-source-data-data-mining-client-for-excel"></a>连接到源数据（Excel 数据挖掘客户端）
  本主题介绍如何创建和使用连接来存储数据挖掘模型以及访问 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中存储的外部数据。  
  
 **数据挖掘连接。** 您在启动外接程序时创建的初始连接用于访问算法、分析数据以及存储挖掘结构和模型。  
  
 要使用外接程序中的建模和可视化工具需要与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的连接，因为这些外接程序依赖 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 所提供的算法和数据结构。  
  
 **与外部数据源的连接。** 生成模型或保存结果时还可以创建与外部数据的连接。 例如，您可以在一个服务器上创建数据挖掘模型，然后使用存储在另一个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例、Excel 数据表或者外部数据源（如 [!INCLUDE[msCoName](../includes/msconame-md.md)] Access）中的数据对该数据挖掘模型执行预测查询。 每次访问新的数据源时，系统都通过一个对话框提示您创建连接。  
  
##  <a name="bkmk_prereq2"></a>先决条件  
 此版本的外接程序要求您的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例为 SQL Server 2012。 若要连接到早期版本的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，则可使用外接程序的一个单独版本。 有很多外接程序版本支持 SQL Server 2005、SQL Server 2008 和 SQL Server 2008 R2。  
  
 要连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，您必须具有访问数据库服务器的权限。 而且，还必须启用数据挖掘会话，您还必须具有服务器上存储的数据库对象的读或读/写权限。  
  
##  <a name="bkmk_connect"></a>创建数据挖掘服务器连接  
 Excel 数据挖掘客户端和 Excel 表分析工具中的 "**连接**" 组提供了用于管理与实例的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]连接的工具。  
  
-   您可以在安装外接程序时创建连接，也可以在以后添加连接。  
  
-   您可以创建多个连接，而且可以随时更改这些连接，模型创建或查询过程中除外。  
  
     不要在处理数据挖掘模型时更改或关闭连接。 数据挖掘模型可能会丢失数据，或者模型可能无法使用。  
  
-   任意特定时间只能有一个连接处于活动状态。  
  
### <a name="connections-in-the-excel-add-ins"></a>Excel 外接程序中的连接  
 使用 Excel 数据挖掘客户端和 Excel 表分析工具中的 "**连接**" 组，您可以在其中管理与实例的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]连接。  
  
##### <a name="create-a-new-server-connection-in-the-excel-add-ins"></a>在 Excel 外接程序中创建新的服务器连接  
  
1.  单击 "**分析**" 或 "**数据挖掘**" 功能区上的 "**连接**" 按钮。  
  
    > [!NOTE]  
    >  按钮的文字可指示连接是否存在。 如果未在工作表中建立连接，则该按钮将包含 "\<没有连接>" 文本。 如果以前在工作簿中创建过连接，则该连接的名称将出现在按钮上。  
  
2.  在 " **Analysis Services 连接**" 对话框中，单击 "**新建**"。  
  
3.  在 "**新建 Analysis Services 连接**" 对话框中，键入服务器的名称。  
  
4.  指定身份验证方法。  
  
5.  从 "**目录名称**" 下拉列表中选择数据库。 如果实例中不存在数据库，请选择 " **（默认）**"。  
  
6.  键入该连接的友好名称。  
  
7.  单击 "**测试连接**" 以验证服务器和数据库是否可用。  
  
8.  单击 **"确定"**，然后单击 "**关闭**"。  
  
### <a name="connections-using-a-web-service"></a>使用 Web 服务连接  
 如果您使用瘦客户端体系结构支持浏览 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维数据集和数据，则还可以通过 Web 服务配置到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器的连接。 有关如何定义基于 Web 的客户端的信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书。  
  
 如果您具有已经为 Web 服务配置的服务器的访问权限，则您可以在首次创建连接时指定连接类型。  
  
##### <a name="create-an-http-connection-to-analysis-services"></a>创建与 Analysis Services 的 HTTP 连接  
  
1.  打开 "**新建 Analysis Services 连接**" 对话框。  
  
2.  对于服务器名称，请键入 http://，后跟分配给 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器的 URL。  
  
3.  键入访问 Web 服务所需的用户名和密码。  
  
### <a name="connections-in-the-visio-add-in"></a>Visio 外接程序中的连接  
 与 Excel 不同，Visio 不提供工具功能区，而且也没有专用于创建或监视连接的按钮。 数据连接是在您首次选择数据挖掘形状并将其放置到 Visio 页中时创建的。 向导会提示您为形状选择模型并设置其他选项。  
  
 如果以前在 Excel 中使用了与[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据源的连接，则这些连接将作为可能的数据源列出，从中进行选择。  
  
##### <a name="create-a-connection-for-a-visio-shape"></a>为 Visio 形状创建连接  
  
1.  打开数据挖掘模板，选择某种数据挖掘形状。  
  
2.  将该形状拖放到空白页上。  
  
3.  在 "**选择数据源**" 对话框中，从列表中选择数据源，或单击 "**新建**"。  
  
4.  如果选择 "**新建**"，请按照前面所述的过程指定服务器和目录名称，或通过 Web 服务进行连接。  
  
##  <a name="bkmk_change"></a>更改连接  
 可以在同一个工作表中创建多个连接，但一次只能有一个连接处于活动状态。 当前连接的名称显示在**连接**按钮中。  
  
 在 Excel 数据挖掘客户端中，您还可以通过单击 "**跟踪**"，然后单击 "**当前连接**" 来验证当前连接的连接字符串和状态。  
  
#### <a name="use-a-different-server-connection"></a>使用其他服务器连接  
  
1.  单击 "**连接**"。  
  
2.  在 " **Analysis Services 连接**" 窗格中，从 "**其他连接**" 列表中选择一个连接，然后单击 "**设置为当前**"。  
  
3.  单击 "**测试连接**" 以验证连接是否可用。  
  
 挖掘模型完成处理之后，结果将存储在本地；您关闭与一个服务器的连接，然后连接到另一个服务器，这对数据没有任何影响。 不过，在处理数据挖掘模型的过程中，您应避免更改连接或中断连接，因为这可能会损坏数据。  
  
#### <a name="modify-an-existing-server-connection"></a>修改现有服务器连接  
  
1.  您不能修改现有连接；如果要连接到另一数据库或另一服务器，应创建一个新连接。  
  
2.  如果必须修改连接字符串以增加查询超时或添加特定于您的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的其他参数，有一种选择是编辑 .dmc 文件，连接字符串就存储在该文件中。  
  
     \<驱动器： > \Users\\<Myusername\>\AppData\Local\Microsoft\Data 挖掘外接程序  
  
##  <a name="bkmk_extconnections"></a>连接到外部数据源  
 虽然 "**分析**" 功能区中的工具仅适用于 Excel 中的数据，但使用 "**数据挖掘**" 功能区中的工具可以直接连接到外部数据源，以用作模型的输入或进行采样。  
  
 这些外接程序中的以下工具支持使用外部数据进行数据挖掘：  
  
-   [&#40;SQL Server 数据挖掘外接程序的示例数据&#41;](sample-data-sql-server-data-mining-add-ins.md)  
  
-   [用于 Excel 的数据挖掘外接程序 &#40;分类向导&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
-   [估计向导 &#40;Excel 数据挖掘外接程序&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
-   [群集向导 &#40;Excel 数据挖掘外接程序&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)  
  
-   [预测向导 &#40;Excel 数据挖掘外接程序&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
-   [SQL Server 数据挖掘外接程序创建挖掘结构 &#40;&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
-   [SQL Server 数据挖掘外接程序的准确性图表 &#40;&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
-   [SQL Server 数据挖掘外接程序的利润图 &#40;&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
  
-   [SQL Server 数据挖掘外接程序的分类矩阵 &#40;&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
### <a name="using-analysis-services-as-a-data-source"></a>使用 Analysis Services 作为数据源  
 您不能直接访问 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维数据集或表格模型中存储的数据。 但可以在 Excel 中创建到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器的连接并使用该数据创建模型。  
  
### <a name="relational-data-sources"></a>关系数据源  
 如果要使用关系数据源中的数据作为模型输入，可以连接到以下 SQL Server 版本：  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
 也可以从 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持作为数据源的任意其他关系数据源中获取数据。 有关支持的数据源的信息，请参阅[多维模型中的数据源](multidimensional-models/data-sources-in-multidimensional-models.md)  
  
 请注意，以下数据类型不能用于数据挖掘，如果在生成模型时包括以下数据类型会导致错误：  
  
-   ntext  
  
-   binary  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Excel&#41;的数据挖掘客户端跟踪](trace-data-mining-client-for-excel.md)  
  
  
