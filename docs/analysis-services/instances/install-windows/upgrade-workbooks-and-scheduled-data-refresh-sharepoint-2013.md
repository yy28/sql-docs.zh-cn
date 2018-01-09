---
title: "升级工作簿和计划的数据刷新 (SharePoint 2013) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a49c4af4-e243-4926-be97-74da1f9d54eb
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b2a122ab3ac28879a1fbcf3790953ba229a285df
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>升级工作簿和计划的数据刷新 (SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]本主题说明在以前创建的工作簿的用户体验[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]环境以及如何升级[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]工作簿以便你可以利用此版本中引入的新功能。 若要了解有关新增功能的详细信息，请参阅 [Power Pivot 中的新增功能](http://go.microsoft.com/fwlink/?LinkID=203917)。  
  
> [!WARNING]  
>  对于在服务器上自动升级的工作簿，不能回滚升级。 一旦升级某一工作簿后，它就将保持升级状态。 若要使用以前的版本，可以将以前的工作簿重新发布到 SharePoint，还原以前的版本，或者回收工作簿。 有关在 SharePoint 中还原或回收文档的详细信息，请参阅 [通过使用回收站和版本控制计划保护内容](http://go.microsoft.com/fwlink/?LinkId=238669)。  
  
 本主题包含以下各节：  
  
-   [升级工作簿的概述](#bkmk_overview)  
  
-   [从 2008 R2 工作簿升级到 SQL Server 2012 Service Pack 1 (SP1) 工作簿](#bkmk_to_2012sp1_from_2008r2)  
  
-   [从通过使用适用于 Excel 的 2012 Power Pivot 外接程序创建的版本升级到 Office 2013 工作簿](#bkmk_to_2012sp1_from_2012)  
  
-   [从通过使用用于 Excel 2010 的 2008 R2 Power Pivot 外接程序创建的版本升级到 SQL Server 2012 工作簿](#bkmk_to_2012_from_2008R2)  
  
-   [在较新版本的服务器上运行多个工作簿版本](#bkmk_runold)  
  
##  <a name="bkmk_overview"></a> 升级工作簿的概述  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿是包含嵌入的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 数据的 Excel 工作簿。 升级工作簿有两个好处：  
  
-   使用 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]中的新功能。  
  
-   为与在 SharePoint 模式下的 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] Analysis Services 服务器一起运行的工作簿实现了计划的数据刷新功能。  
  
> [!IMPORTANT]  
>  您无法回滚已升级的工作簿，所以，如果想在 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]的早期版本或 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]的早期版本中使用该文件，就一定要制作该文件的副本。  
  
 下表基于在其中创建工作簿的环境，列出了对 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿的支持和行为。 描述的行为包括一般的用户体验、用于将工作簿升级到特定环境的支持的升级选项以及尚未升级的工作簿的计划的数据刷新。  
  
### <a name="workbook-behavior-and-upgrade-options"></a>工作簿行为和升级选项  
  
|创建于|\<|支持和行为|>|  
|----------------|--------|--------------------------|--------|  
||**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2010**|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2010**|**2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013**|  
|**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010**|所有功能|**体验：** 用户可在浏览器中与工作簿交互，并且将其用作其他解决方案的数据源。<br /><br /> **升级：** 如果为 SharePoint 场中的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 系统服务启用了“自动升级”，则工作簿将在文档库中自动升级。<br /><br /> **计划数据刷新：** 不支持。 工作簿需要升级。|**体验：** 用户可与工作簿交互，并且将其用作其他解决方案的数据源。<br /><br /> **升级：** 自动升级不可用。 用户必须将其 2008 R2 工作簿手动升级到 2012 版本或 Office 2013 版本。<br /><br /> **计划数据刷新：** 不支持。 工作簿需要升级。|  
|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel**|不支持|所有功能|**体验：** 用户可在浏览器中与工作簿交互，并且将其用作其他解决方案的数据源。 计划数据刷新可用。<br /><br /> **升级：** 不支持自动升级。 用户可以将其工作簿手动升级到 Office 2013 版本。<br /><br /> **计划数据刷新：** 支持。|  
|**Excel 2013**|不支持|不支持|所有功能|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a> 从 2008 R2 工作簿升级到 SQL Server 2012 Service Pack 1 (SP1) 工作簿  
 本节介绍了如何从 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 工作簿升级到 SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2013 工作簿。  
  
 **行为更改：** 在 SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 中使用时，SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿将不会自动升级。 因此，计划的数据刷新将不适用于 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿。  
  
 2008 R2 工作簿将在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 中打开，但计划的数据刷新将不起作用。 如果查看刷新历史记录，您将会看到如下错误消息：  
  
 “该工作簿包含不支持的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型”。 该工作簿中的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型采用 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 格式。 支持的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型如下：  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010。  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2013。  
  
 **如何升级工作簿：** 在将工作簿升级到 2012 工作簿之前，计划的数据刷新将不起作用。 若要升级工作簿以及工作簿中所包含的模型，请完成以下操作之一：  
  
-   下载工作簿并在安装有 SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 外接程序的 Microsoft Excel 2010 中打开该工作簿。  
  
     打开 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 窗口，并且升级 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型。  
  
     然后保存该工作簿并将其重新发布到 SharePoint。  
  
-   下载该工作簿并在 Microsoft Excel 2013 中打开它。  
  
     打开 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 窗口，并且升级 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型。  
  
     然后保存该工作簿并将其重新发布到 SharePoint 服务器。  
  
 有关对 Analysis Services 功能的更改的详细信息，请参阅 [SQL Server 2016 中对 Analysis Services 功能的行为更改](../../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)  
  
 有关刷新历史记录的详细信息，请参阅 [查看数据刷新历史记录 (PowerPivot for SharePoint)](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)。  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a> 从通过使用适用于 Excel 的 2012 Power Pivot 外接程序创建的版本升级到 Office 2013 工作簿  
 本节介绍了如何 **从** SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 工作簿升级 **到** Excel 2013 中的 SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 。  
  
 升级工作簿将解决在以前版本的工作簿上尝试计划的数据刷新时出现的以下错误：  
  
 “针对使用 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 的以前版本创建的工作簿的刷新操作不可用。”  
  
 **如何升级工作簿**  
  
1.  通过在 Microsoft Excel 2013 中打开工作簿来手动升级每个工作簿。  
  
2.  若要升级工作簿以及工作簿中所包含的模型，请下载该工作簿并在 Microsoft Excel 2013 中打开它。  
  
3.  打开 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 窗口，并且升级 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 模型。  
  
4.  然后保存该工作簿并将其重新发布到 SharePoint 2013 服务器。  
  
##  <a name="bkmk_to_2012_from_2008R2"></a> 从通过使用用于 Excel 2010 的 2008 R2 Power Pivot 外接程序创建的版本升级到 SQL Server 2012 工作簿  
 本节介绍了如何 **从** SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 工作簿升级 **到** SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010。  
  
 升级工作簿将解决在以前版本的工作簿上尝试计划的数据刷新时出现的以下错误：  
  
 “针对使用 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 的以前版本创建的工作簿的刷新操作不可用。”  
  
 **如何升级工作簿**  
  
 可以使用两种方法进行升级：  
  
1.  通过在安装有 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 版本的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 的计算机上在 Excel 中打开工作簿，然后将其重新发布到服务器，手动升级各工作簿。 当您在外接程序的较新版本中打开此工作簿时，将发生以下内部操作：工作簿数据连接字符串中的数据访问接口将更新为 MSOLAP.5，更新元数据，并重新创建关系以符合较新的实现。  
  
2.  或者，SharePoint 管理员可以在 SharePoint 场中启用针对 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 系统服务的自动升级功能，以便在计划数据刷新运行时自动升级 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿（仅升级为计划的数据刷新配置的工作簿）。  
  
    > [!NOTE]  
    >  自动升级是一种服务器配置功能；您不能为特定的工作簿、库或网站集启用或禁用该自动升级功能。  
  
 **如何配置在数据刷新过程中自动升级**  
  
 若要使用自动升级，你必须在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 配置工具中选中“自动升级 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿以便从服务器启用数据刷新”复选框。 在该工具中，该复选框位于“升级 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 系统服务”页上和“创建 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序”页上（如果你在配置新安装）。  
  
 您可以运行以下 cmdlet 以便验证是否启用了自动升级：  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 Get-PowerPivotSystemService 的输出是属性和相应值的列表。 您应该会在属性列表中看到 **WorkbookUpgradeOnDataRefresh** 。 如果启用自动升级，该属性将设置为 **true** 。 如果该属性为 **false**，则继续执行下一步，启用自动工作簿升级。  
  
 若要启用自动工作簿升级，请运行以下命令：  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService –WorkbookUpgradeOnDataRefresh:$true –Confirm:$false  
```  
  
 升级工作簿后，可使用计划数据刷新和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 外接程序中的新功能。  
  
##  <a name="bkmk_runold"></a> 在较新版本的服务器上运行多个工作簿版本  
 可以在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 的 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 实例上并行运行 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]工作簿的较旧和较新版本。  
  
 根据您安装服务器的方式， **可能需要** 安装以前版本的 Analysis Services OLE DB 访问接口，之后才能访问同一服务器上的较旧和较新工作簿。  
  
 请注意，不支持在 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 的以前的 SQL Server 实例上发布更新版本的工作簿。 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 实例将不加载在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 的 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]版本中创建的工作簿，而 SQL Server 2012 实例将不加载具有你在 Excel 中使用 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 版本创建的高级数据模型的 Office 2013 工作簿。  
  
###  <a name="bkmk_msolapxslx"></a> 如何检查 Power Pivot 工作簿中的 MSOLAP 数据提供程序信息  
 使用下面的说明检查 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿中使用的是哪个 OLE DB 提供程序。 检查数据连接信息不需要安装 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] 外接程序。  
  
1.  在 Excel 中的“数据”选项卡上，单击 **“连接”**。 单击 **“属性”**。  
  
2.  在 **“定义”** 选项卡上，访问接口的版本显示在连接字符串的开头。  
  
     **Provider=MSOLAP.5** 指示工作簿是 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。  
  
     **Provider=MSOLAP.4** 指示 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]。  
  
     **Data Source=$Embedded$** 指示工作簿是使用嵌入式数据库的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿。  
  
###  <a name="bkmk_msolappc"></a> 如何检查本地计算机上 MSOLAP 数据访问接口的当前版本  
 使用下面的说明检查 OLE DB 提供程序在运行 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 工作簿的服务器或工作站上是否为当前版本。 了解当前版本可帮助您排除升级后出现的数据连接错误。  
  
1.  在注册表编辑器中，转至 HKEY_CLASSES_ROOT。  
  
2.  向下滚动到 MSOLAP。 验证 MSOLAP.5 已列在系统上安装的 OLAP 访问接口中。 验证 MSOLAP | CurVer 设置为 MSOLAP.5  
  
## <a name="see-also"></a>另请参阅  
 [将 Power Pivot 迁移到 SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [升级 Power Pivot for SharePoint](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Analysis Services 中的新增功能](../../../analysis-services/what-s-new-in-analysis-services.md)   
 [查看数据刷新历史记录 &#40;Power Pivot for SharePoint &#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
