---
title: 行为更改 Analysis Services SQL Server 2014 中的功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0f7cc154a79a329bc18d02535e3f3332aa7e8b61
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391780"
---
# <a name="behavior-changes-to-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014 中 Analysis Services 功能的行为更改
  本主题针对多维、表格、数据挖掘和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 部署介绍 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 中的行为更改。 与早期版本的 SQL Server 相比，当前版本中的功能的工作或交互方式会受到行为更改的影响。  
  
> [!NOTE]  
>  相反，阻止与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 集成的数据模型或应用程序运行是一项重大更改。 若要了解更多信息，请参阅 [Breaking Changes to Analysis Services Features in SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)。  
  
 本主题内容：  
  
-   [SQL Server 2014 中的行为更改](#bkmk_sql2014)  
  
-   [SQL Server 2012 SP1 中的行为更改](#bkmk_sql2012sp1)  
  
-   [SQL Server 2012 中的行为更改](#bkmk_sql2012)  
  
##  <a name="bkmk_sql2014"></a> 中的行为更改 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 此版本中，没有针对表格、多维、数据挖掘或 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 功能的新的行为更改。  但是，由于  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 非常类似于 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 版本，因而如果要从 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]进行升级，为方便起见，此处提供了这两个以前版本的行为更改。  
  
##  <a name="bkmk_sql2012sp1"></a> 中的行为更改 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]  
 本节介绍针对 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]功能报告的行为更改。 这些更改也适用于 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]。  
  
|问题|Description|  
|-----------|-----------------|  
|在 SQL Server 2012 SP1 PowerPivot for SharePoint 2013 中使用时，SQL Server 2008 R2 PowerPivot 工作簿将不会在不进行提示的情况下升级和刷新模型。 因此，计划的数据刷新将不适用于 SQL Server 2008 R2 PowerPivot 工作簿。|2008 R2 工作簿将在 [!INCLUDE[ssGeminiShortvnext](../includes/ssgeminishortvnext-md.md)]中打开，但计划的刷新将不起作用。 如果查看刷新历史记录，您将会看到如下错误消息：<br /> "工作簿包含不受支持的 PowerPivot 模型。 该工作簿中的 PowerPivot 模型采用 SQL Server 2008 R2 PowerPivot for Excel 2010 格式。 支持的 PowerPivot 模型如下： <br />SQL Server 2012 PowerPivot for Excel 2010<br />SQL Server 2012 PowerPivot for Excel 2013"<br /><br /> **如何升级工作簿：** 在将工作簿升级到 2012 工作簿之前，计划的刷新将不起作用。 若要升级工作簿以及工作簿中所包含的模型，请完成以下操作之一：<br /><br /> 下载工作簿并在安装有 SQL Server 2012 PowerPivot for Excel 外接程序的 Microsoft Excel 2010 中打开该工作簿。 然后保存该工作簿并将其重新发布到 SharePoint 服务器。<br /><br /> 下载该工作簿并在 Microsoft Excel 2013 中打开它。 然后保存该工作簿并将其重新发布到 SharePoint 服务器。<br /><br /> <br /><br /> 工作簿升级的详细信息，请参阅[升级工作簿和计划的数据刷新&#40;SharePoint 2013&#41;](instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。|  
|DAX [ALL Function](https://msdn.microsoft.com/library/ee634802(v=sql.120).aspx)中的行为更改。|在 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]之前，如果您在“标记为日期表”中指定 [Date] 列以在时间智能中使用，且将 [Date] 列作为参数传递到 ALL 函数或作为筛选器传递给 CALCULATE 函数，则无论日期列中的切片器如何，都忽略表中所有列的所有筛选器。<br /><br /> 例如，<br /><br /> `= CALCULATE (<expression>, ALL (DateTable[Date]))`<br /><br /> 在 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]以前，对于 DateTable 的所有列忽略所有筛选器，无论作为参数传递给 ALL 的 [Date] 列是什么。<br /><br /> 在 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 和 Excel 2013 的 PowerPivot 中，此行为将仅对作为参数传递给 ALL 的指定列忽略筛选器。<br /><br /> 要解决新行为问题，忽略作为整个表的筛选器的所有列，您可以从参数中排除 [Date] 列，例如：<br /><br /> `=CALCULATE (<expression>, ALL(DateTable))`<br /><br /> 这将产生与 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]以前的行为相同的结果。|  
  
##  <a name="bkmk_sql2012"></a> 中的行为更改 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 本节介绍针对 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]功能报告的行为更改。 这些更改也适用于 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]。  
  
### <a name="analysis-services-multidimensional-mode"></a>Analysis Services，多维模式  
  
#### <a name="nullprocessing-option-set-to-preserve-is-no-longer-supported-for-distinct-count-measures"></a>非重复计数度量值不再支持设置为“保留”的 NullProcessing 选项  
 早于[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]，可以设置[NullProcessing 元素&#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl)到`Preserve`非重复计数度量值。  遗憾的是，这种做法通常生成无效的结果，有时甚至损坏处理作业。 因此，此配置在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中不再有效。 尝试使用它将会导致会发生以下验证错误："元数据管理器中的错误。 保留不是有效的 NullProcessing 值\<measurename > 非重复计数度量值。"  
  
#### <a name="cube-browser-in-management-studio-and-cube-designer-has-been-removed"></a>Management Studio 和多维数据集设计器中的多维数据集浏览器已被删除  
 可用于在 Management Studio 或多维数据集设计器中将字段拖放到数据透视表结构中的多维数据集浏览器控件已从产品中删除。 该控件是 Office Web Control (OWC) 组件。 OWC 在 Office 中已不推荐使用，并且不再继续提供。  
  
### <a name="powerpivot-for-sharepoint"></a>PowerPivot for SharePoint  
  
#### <a name="higher-permission-requirements-for-using-a-powerpivot-workbook-as-an-external-data-source"></a>将 PowerPivot 工作簿用作外部数据源的较高权限要求  
 Excel 工作簿可以呈现嵌入在同一工作簿或外部工作簿中的 PowerPivot 数据。 在以前的版本中，无论 PowerPivot 数据是嵌入的还是外部的，权限要求都是相同的。 如果您对某一 PowerPivot 工作簿具有 **“仅查看”** 权限，则无论是对嵌入连接还是外部连接，均可获取对该工作簿中所有 PowerPivot 数据的完全访问权限。  
  
 在此版本中，对于呈现来自外部文件的 PowerPivot 数据的 Excel 工作簿，其权限要求已更改。 在这一版本中，您必须具有 **“读取”** 权限（或更明确地说，必须具有 **“打开项”** 权限），才能从客户端应用程序连接到外部 PowerPivot 工作簿。 其他权限指定用户具有下载权限，才能查看工作簿中嵌入的源数据。 其他权限反映这一事实，即模型数据完全可用于链接到它的客户端应用程序或工作簿，从而导致在权限要求与实际数据连接行为之间的更好地进行协调。  
  
 若要继续将 PowerPivot 工作簿用作外部数据源，您必须为连接到外部 PowerPivot 数据的用户提高 SharePoint 权限。 在更改权限之前，如果用户尝试通过数据源连接访问 PowerPivot 工作簿，将获得以下错误："PowerPivot Web 服务返回了错误 （拒绝访问。 您请求的文档不存在或您没有权限打开该文件。）"  
  
> [!WARNING]  
>  以下步骤将指导您断开库级别的权限继承，将用户针对此库中特定文档的权限从 **“仅查看”** 提高到 **“读取”** 。 在继续之前，请仔细查看现有的权限和文档，并确认这些步骤适用于您的网站。  
>   
>  此外，您可以在库中创建一个文件夹，将所有受影响的文档移到该文件夹，并设置针对此文件夹的独特权限。  
  
> [!NOTE]  
>  如果您的工作簿存储在 PowerPivot 库中，当该工作簿已配置为进行数据刷新时，断开此工作簿的权限继承将中断为该工作簿生成缩略图的过程。 若要同时允许访问库中的工作簿和预览图像，请考虑在库级别向特定用户授予针对库中所有文档的 **“读取”** 权限。  
  
 您必须是网站所有者才能更改权限。  
  
 **如何增加读取各个工作簿的权限级别的权限**  
  
1.  单击向下箭头以打开菜单，找到单独文档。  
  
2.  单击 **“管理权限”**。  
  
3.  默认情况下，库将继承权限。 若要更改此库中单独工作簿的权限，请单击 **“停止继承权限”**。  
  
4.  按需要针对 PowerPivot 工作簿的附加权限的用户名或组名选中复选框。 附加权限将允许这些用户链接到嵌入的 PowerPivot 数据并且使用这些数据作为其他文档中的外部数据源。  
  
5.  单击 **“编辑用户权限”**。  
  
6.  选择 **“读取”** 权限，然后单击 **“确定”**。  
  
#### <a name="powerpivot-gallery-new-rules-for-snapshot-generation-for-some-powerpivot-workbooks"></a>PowerPivot 库：为一些 PowerPivot 工作簿生成快照的新规则  
 此版本中引入了在 PowerPivot 库中生成快照映像的新要求，这消除了泄露信息的潜在根源（也即，显示来自您无权查看的数据源的数据的快照）。 这些要求仅适用于您每次查看 PowerPivot 工作簿时都连接到外部数据源的工作簿。 如果您只使用直观显示嵌入 PowerPivot 数据的工作簿，将看不到在 PowerPivot 库中生成快照的方式发生了什么变化。  
  
 对于每次打开时均刷新其数据的工作簿，快照生成的新要求如下所示：  
  
-   由其他工作簿或报表用作外部数据源的 PowerPivot 工作簿必须与使用数据的工作簿位于同一个库中。 例如，如果您具有向 sales-report.xlsx 提供数据的 sales-data.xlsx，则这两个工作簿都必须位于该库中，才能显示快照映像。  
  
-   一起使用的工作簿必须从一个公共父级（即 PowerPivot 库）继承权限。 在我们的示例中，sales-data.xlsx 和 sales-report.xlsx 必须从 PowerPivot 库继承。  
  
 如果工作簿未能满足上述任何条件，则将显示下面的锁定图标，而不是您所期望的缩略图：  
  
 ![GMNI_PowerPivotGalleryIcon_Locked](media/gmni-powerpivotgalleryicon-locked.gif "GMNI_PowerPivotGalleryIcon_Locked")  
  
#### <a name="new-default-setting-for-load-balancing-requests-changed-from-round-robin-to-health-based"></a>负载平衡请求的新默认设置已从“循环”更改为“基于运行状况”  
 PowerPivot 服务应用程序具有一些默认设置，这些设置确定如何在场中的多台 PowerPivot for SharePoint 服务器之间分配对 PowerPivot 数据的请求。 在前一版本中，默认设置是 **“循环”**，其中请求在可用服务器之间按顺序进行分配。 在这一版本中，默认值现在为 **“基于运行状况”**。 PowerPivot 服务应用程序使用服务器运行状况统计数据（如可用内存或 CPU）来确定哪些服务器实例获取 xt 请求。  
  
 如果您从前一版本升级服务器，PowerPivot 服务应用程序将保留以前的默认设置（**“循环”**）。 若要使用 **“基于运行状况”** 分配方法设置，您必须修改配置设置。 有关详细信息，请参阅[创建和配置 PowerPivot 服务应用程序在管理中心内](power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)。  
  
## <a name="see-also"></a>另请参阅  
 [后向兼容性](../../2014/getting-started/backward-compatibility.md)   
 [重大更改 Analysis Services SQL Server 2014 中的功能](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
  
