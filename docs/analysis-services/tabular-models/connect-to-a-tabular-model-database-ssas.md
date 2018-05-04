---
title: 连接到表格模型数据库 |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 983d0c8a-77da-4c6e-8638-283bcb14f143
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 06265dfa0b66cc5cd1cc24a8bd6fd74675fb72d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-a-tabular-model-database"></a>连接到表格模型数据库  
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  在您生成表格模型并且将其部署到某一 Analysis Services 表格模式服务器后，需要设置权限以使其可供客户端应用程序使用。 此文章介绍了如何权限以及如何从客户端应用程序连接到数据库。  
  
> [!NOTE]  
>  默认情况下，在您配置防火墙之前，与 Analysis Services 的远程连接将不可用。 如果您在为客户端连接配置命名实例或默认实例，则请确保您打开了适当的端口。 有关详细信息，请参阅 [将 Windows 防火墙配置为允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
##  <a name="bkmk_userpermissions"></a> 针对数据库的用户权限  
 连接到表格数据库的用户必须在指定读取访问权限的数据库角色中具有成员身份。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创作模型时或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]创作模型时（对于已部署的模型）会定义角色（有时会定义角色成员身份）。 有关使用角色管理器中创建角色的详细信息[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]，请参阅[创建和管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。 有关创建和管理角色的已部署的模型的详细信息，请参阅[表格模型角色](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md)。  
  
> [!CAUTION]  
>  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中通过角色管理器使用已定义的角色重新部署表格模型项目，将覆盖已部署的表格模型中定义的角色。  
  
##  <a name="bkmk_admin"></a> 针对服务器的管理权限  
 对于使用 SharePoint 来承载 Excel 工作簿或 Reporting Services 报表的组织，需要附加的配置以使表格模型数据可供 SharePoint 用户使用。 如果您未在使用 SharePoint，则跳过本节。  
  
 查看包含表格数据的 Excel 工作簿或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表要求用于运行 Excel Services 或 Reporting Services 的帐户对 Analysis Services 实例具有管理员权限。 需要管理权限，以便这些服务为 Analysis Services 实例所信任。  
  
#### <a name="grant-administrative-access-on-the-server"></a>授予针对服务器的管理权限  
  
1.  在“管理中心”中，打开“配置服务帐户”页。  
  
2.  选择 Excel Services 使用的服务应用程序池。 该应用程序池可以是 **“服务应用程序池 - SharePoint Web 服务系统”** 或自定义的应用程序池。 由 Excel Services 使用的托管帐户将出现在该页上。  
  
     对于包括 SharePoint 模式下 Reporting Services 的 SharePoint 场，还要获取 Reporting Services 服务应用程序的帐户信息。  
  
     在以下步骤中，您要将这些帐户添加到 Analysis Services 实例上的服务器角色中。  
  
3.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，再右键单击该服务器实例，然后选择“属性”。 在对象资源管理器中，右键单击“角色”，然后选择“新建角色”。  
  
4.  在“Analysis Services 属性”页中，选择 **“安全性”**。  
  
5.  单击 **“添加”**，然后输入 Excel Services 使用的帐户，后跟 Reporting Services 使用的帐户。  
  
##  <a name="bkmk_excelconn"></a> 从 Excel 或 SharePoint 进行连接  
 提供对 Analysis Services 数据库的访问权限的客户端库可用于连接到在表格模式服务器上运行的模型数据库。 库包括 Analysis Services OLE DB 访问接口、ADOMD.NET 和 AMO。  
  
 Excel 使用 OLE DB 访问接口。 如果你具有来自 SQL Server 2008 R2 的 MSOLAP.4（文件名 msolap100.dll，版本 10.50.1600.1），或者具有随 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 一起安装的 MSOLAP.5（文件名 msolap110.dll），则你具有连接到表格数据库的版本。  
  
 从以下方法中进行选择以便从 Excel 连接到模型数据库：  
  
-   从 Excel 内创建一个数据连接，并且使用在下一节中提供的说明。  
  
-   在 SharePoint 中创建一个 BI 语义模型连接 (.bism) 文件，该文件提供重定向到在 Analysis Services 表格模式服务器上运行的数据库。 BI 语义模型连接文件提供一个右键单击命令，该命令通过使用您在连接中指定的模型数据库启动 Excel。 如果安装了 Reporting Services，则该命令还将启动 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 。 有关创建和使用 BI 语义模型连接文件的详细信息，请参阅 [创建与表格模型数据库的 BI 语义模型连接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)。  
  
-   创建将表格数据库引用为数据源的 Reporting Services 共享数据源。 您可以在 SharePoint 中创建共享数据源，并使用该数据源启动 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]。  
  
#### <a name="connect-from-excel"></a>从 Excel 进行连接  
  
1.  在 Excel 中的 **“数据”** 选项卡上的 **“获取外部数据”**中，单击 **“自其他来源”**。  
  
2.  选择 **“从 Analysis Services”**。  
  
3.  在 **“服务器名称”**中，指定将承载数据库的 Analysis Services 实例。 服务器名称通常是运行服务器软件的计算机的名称。 如果服务器作为命名实例安装，你必须按以下格式指定名称： \<servername >\\< instancename\>。  
  
     必须为独立的表格部署配置服务器实例，并且该服务器实例必须具有允许访问的入站规则。 有关详细信息，请参阅 [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md) 和 [将 Windows 防火墙配置为允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
4.  对于登录凭据，如果您对数据库具有读取权限，则选择 **“使用 Windows 身份验证”** 。 否则，请选择 **“使用以下用户名和密码”**，然后输入具有数据库权限的 Windows 帐户的用户名和密码。 单击“下一步” 。  
  
5.  选择数据库。 有效选择将为该数据库显示单个 **“模型”** 多维数据集。 单击 **“下一步”** ，然后单击 **“完成”**。  
  
 在建立连接后，您可以使用数据来创建数据透视表或数据透视图。 有关详细信息，请参阅[在 Excel 中的分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
##  <a name="bkmk_sharepoint"></a> 从 SharePoint 进行连接  
 如果使用的是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，则可在 SharePoint 中创建一个 BI 语义模型连接文件，通过该文件，可重定向到在 Analysis Services 表格模式服务器上运行的数据库。 BI 语义模型连接提供指向数据库的 HTTP 端点。 对于经常要使用 SharePoint 站点上的文档的知识工作者，该连接还简化了表格模型访问。 知识工作者只需要知道 BI 语义模型连接文件的位置或其 URL 就可以访问表格模型数据库。 与服务器位置或数据库名称有关的详细信息封装在 BI 语义模型连接中。 有关创建和使用 BI 语义模型连接文件的详细信息，请参阅 [PowerPivot BI 语义模型连接 (bism)](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md) 和[创建与表格模型数据库的 BI 语义模型连接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)。  
  
##  <a name="bkmk_Tshoot"></a> 解决连接问题  
 本节介绍在连接到表格模型数据库时发生的问题的原因和解决方法步骤。  
  
 **数据连接向导不能从指定的数据源获取数据库列表。**  
  
 在导入数据，此 Microsoft Excel 错误发生在尝试使用向导连接到表格模型数据库在远程 Analysis Services 服务器上，并且你没有足够的权限。 若要纠正此错误，您必须对数据库具有用户访问权限。 请参考在本文前面部分中提供的说明，授予用户对数据的访问权限。  
  
 **在尝试建立与外部数据源的连接的过程中出现错误。以下连接刷新失败：\<模型名称 > 沙盒**  
  
 在 SharePoint 上，当您尝试在使用模型数据的数据透视表中进行数据交互（例如筛选数据）时，将会发生此 Microsoft Excel 错误。 发生此错误的原因是您对远程 Analysis Services 服务器没有足够的权限。 若要纠正此错误，您必须对数据库具有用户访问权限。 请参考在本文前面部分中提供的说明，授予用户对数据的访问权限。  
  
 **尝试执行此操作时出错。重新加载工作簿，然后尝试再次执行此操作。**  
  
 在 SharePoint 上，当您尝试在使用模型数据的数据透视表中进行数据交互（例如筛选数据）时，将会发生此 Microsoft Excel 错误。 发生此错误的原因是部署了模型数据的 Analysis Services 实例不信任 Excel Services。 若要纠正此错误，请对 Analysis Services 实例授予 Excel Services 管理权限。 请参考在本文前面部分中提供的说明，授予管理员权限。 如果此错误仍存在，请回收 Excel Services 应用程序池。  
  
 **在尝试与在工作簿中使用的外部数据源建立连接的过程中出现错误。**  
  
 在 SharePoint 上，当您尝试在使用模型数据的数据透视表中进行数据交互（例如筛选数据）时，将会发生此 Microsoft Excel 错误。 发生此错误的原因是该用户对工作簿没有足够的 SharePoint 权限。 该用户必须具有 **“读取”** 权限或更高权限。 “仅查看”权限对于数据访问是不够的。  
  
## <a name="see-also"></a>另请参阅  
 [表格模型解决方案部署](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
