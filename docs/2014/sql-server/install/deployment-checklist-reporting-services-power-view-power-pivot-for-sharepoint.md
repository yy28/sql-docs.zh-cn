---
title: 部署清单：Reporting Services、Power View 和 PowerPivot for SharePoint |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9a2575c8-06fc-4ef4-9f24-c19e52b1bbcf
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f1eb0f6892192e5ed328386e6730ec3b1c41f05b
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952554"
---
# <a name="deployment-checklist-reporting-services-power-view-and-powerpivot-for-sharepoint"></a>部署清单：Reporting Services、Power View 和 PowerPivot for SharePoint
  使用以下清单在同一 SharePoint 场中安装这些 BI 功能：PowerPivot for SharePoint、报表生成器和 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]。 虽然此清单建议按照特定的安装顺序进行，但实际上您几乎可以按照任意顺序来安装这些功能。 此清单假定安装以下产品或功能：  
  
1.  SharePoint Server 2010 Service Pack 1 (SP1)  
  
2.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 数据库引擎  
  
3.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services 和 Reporting Services 外接程序  
  
4.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot for SharePoint  
  
 安装了这些功能后，您将能够执行以下操作。  
  
-   通过 SharePoint 网站访问在 PowerPivot for Excel 中创建的 PowerPivot 工作簿。  
  
-   基于 SharePoint 中的 PowerPivot 工作簿生成交互式 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表。  
  
-   在 SharePoint 中启动报表生成器时创建报表生成器报表。  
  
> [!NOTE]  
>  PowerPivot for SharePoint 要求在 SharePoint 场中安装 SharePoint 2010 Service Pack 1 (SP1)。 如果您为了评估而要安装该软件，请考虑从一台干净的服务器开始，这样可以避免场升级步骤所带来的开销。 对场进行升级会影响 SharePoint 操作，通常需要仔细进行规划。 如果您的目的是尽快安装 PowerPivot for SharePoint，则请按照此方法进行操作：安装 SharePoint 2010，安装 SharePoint 2010 SP1，然后在后面的步骤中配置场。 应避免进行升级，因为在安装 SharePoint 2010 SP1 时尚未配置场。  
>   
>  在此清单中，假定在使用 SharePoint 配置工具配置 PowerPivot for SharePoint 的过程中执行场配置步骤。 或者，可以使用 SharePoint 产品配置向导进行配置（如果您愿意采用该方法）。 这两种方法都能生成支持 PowerPivot for SharePoint 的正常运行的场。  
  
## <a name="prerequisites"></a>先决条件  
 您必须是本地管理员才能运行 SQL Server 安装程序。  
  
 SharePoint Server 2010 企业版是 PowerPivot for SharePoint 所必需的。 您也可以使用评估企业版。  
  
 必须安装 SharePoint Server 2010 SP1。 如果没有该软件，您就无法将场配置为使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 功能。  
  
 必须将计算机加入到域中。  
  
 您必须有一个或多个域用户帐户才能设置服务。 你将需要以下服务的域用户帐户：SharePoint web 服务和管理服务、Reporting Services、Analysis Services、Excel Services、安全存储区服务和 PowerPivot 系统服务。 域帐户是 SharePoint 中的托管帐户功能所必需的。 数据库引擎可以使用虚拟帐户来设置，但所有其他服务均应以域用户身份来运行。  
  
 必须提供 PowerPivot 实例名称。 在您要在其上安装新的 PowerPivot for SharePoint 的计算机上，您无法拥有现有的 PowerPivot 命名实例。  
  
 如果要在现有场中安装 PowerPivot for SharePoint，则必须具有为经典模式身份验证配置的一个或多个 SharePoint Web 应用程序。 只有该 Web 应用程序支持经典模式身份验证，PowerPivot 数据访问才有效。 有关经典模式要求的详细信息，请参阅[PowerPivot 身份验证和授权](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization)。  
  
 查看以下其他主题以了解系统和版本要求：  
  
-   [使用 SharePoint 2010 场中的 SQL Server BI 功能的指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>步骤  
 下面的步骤假定管理员正在安装和配置服务器。 SharePoint 中的安装用户也是场管理员，通常是默认网站集的主要网站管理员。 如果您要将以下步骤分配给若干个人，则可能需要具有附加权限才能使这些步骤正常进行。  
  
|步骤|链接|  
|----------|----------|  
|运行 SharePoint 2010 产品准备工具|您必须拥有 SharePoint 2010 安装介质。 准备工具是安装介质中的 PrerequisiteInstaller.exe。|  
|安装 SharePoint Server 2010 企业版或企业评估版。|安装 SharePoint 时，可以通过以下方式选择以后再配置场：完成安装后不运行 SharePoint 2010 产品配置向导。 如果等待配置场，则可以使用在稍后的步骤中作为场的数据库服务器安装的 @no__t 数据库引擎实例。 若要配置场，则将使用 PowerPivot 配置工具。 其中包括在尚未配置场时用于设置场的操作。|  
|安装 SharePoint Server 2010 SP1。|从[@no__t](https://go.microsoft.com/fwlink/p/?linkID=219697)下载 SP1。|  
|运行 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 安装程序，以便安装数据库引擎和 PowerPivot for SharePoint。|[安装 PowerPivot for SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> 步骤 1 说明了如何安装 PowerPivot for SharePoint。 在此步骤中，请务必单击“设置角色”页上向角色添加数据库引擎的复选框。 这样做会将数据库引擎添加到安装中，以便在下一步中配置场时，可以将其用作场的数据库服务器。 但是，如果已配置场，则可以跳过此步骤。<br /><br /> 步骤 2 要求您配置服务器。 对于此步骤，请选择 PowerPivot 配置工具。 虽然有多种方法可以使用，但对于独立安装来说，使用配置工具是最有效的方法。<br /><br /> 如果已经安装了 SharePoint 2010 但未进行配置，则该工具将预先选择将创建场、默认 Web 应用程序和根网站集的操作。 请务必使这些选项保留选中状态，以便创建场。 如果您已经配置了场，则该工具将忽略这些操作，而将仅提供配置 PowerPivot for SharePoint 所必需的操作。<br /><br /> 步骤 3 指示您安装 Analysis Services OLE DB 访问接口的 Server SQL 2008 R2 版本。 此步骤对在 2008 R2 版的 PowerPivot for Excel 中创建的工作簿的支持版本很重要。|  
|验证场是否正常运行。|首先，请启动管理中心并确认它可用。 接下来，输入 http://localhost 打开团队网站。  您应该会看到一个 SharePoint 工作组网站。|  
|验证 PowerPivot for SharePoint 是否正常运行。|[验证 PowerPivot for SharePoint 安装](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation)<br /><br /> 此任务确认使用您所上载的示例工作簿进行 PowerPivot 数据访问。|  
|运行 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 安装程序，以便安装和配置 Reporting Services 和 Reporting Services 外接程序。|[安装用于 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)<br /><br /> （可选）安装 Reporting Services 时，如果您想让第二个资源来承载表格数据，则可将另外一个 Analysis Services 实例添加到安装功能树中。 另外这个 Analysis Services 实例将用于承载您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中创建的表格模型数据库。 表格数据库是 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表的有效数据源。<br /><br /> [在表格模式下安装 Analysis Services](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)|  
|验证 Reporting Services 是否正常运行。|[验证 Reporting Services 安装](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)|  
|（网站管理员）配置 SharePoint 权限。|若要在 SharePoint 库中添加、编辑或删除项，必须具有参与讨论权限。 若要对存在嵌入数据的报表和 PowerPivot 工作簿进行只读访问，拥有查看级别的权限就足够了。<br /><br /> 作为外部数据源（其中，URL 工作簿是另一个工作簿或报表中的连接字符串）访问的 PowerPivot 工作簿要求具有读取权限，这种权限的级别要比查看权限高。<br /><br /> BI 语义模型连接也要求具有读取权限。 您可能需要创建新的权限级别或 SharePoint 组才能拥有正确的权限。|  
|（网站管理员）扩展文档库|扩展文档库以使用 BI 内容类型：BI 语义模型连接，Reporting Services 共享数据源，报表生成器报表：<br /><br /> 1) <br />                    **启用内容类型管理**。 在 "共享文档" 或其他文档库的 "库" 选项卡中，单击 "**库设置**"。 在 "常规设置" 下，单击 "**高级设置**"。 在 "内容类型" 中，选择 **"是"** 以允许管理内容类型，然后单击 **"确定"** 。<br /><br /> 2) <br />                    **选择 BI 内容类型**。 在 "库" 选项卡中，单击 "**库设置**"。 在 "内容类型" 下，单击 "**从现有网站内容类型添加**"。 从 "商业智能内容类型" 组中，添加 " **BI 语义模型连接文件**" 和 "**报表数据源**"。 或者，您也可以添加其他 Reporting Services 内容类型（如报表模型）以启用其他报表生成方案。<br /><br /> <br /><br /> 有关详细信息，请参阅[将 BI 语义模型连接内容类型添加到库&#40;PowerPivot for SharePoint&#41; ](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library)和[将报表服务器内容类型添加到 SharePoint &#40;集成模式下&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|（网站管理员）创建用于启动 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 的数据连接文件。|必须创建作为 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 数据源的 BI 语义模型连接 (.bism) 或 Reporting Services 共享数据源 (.rsds)。 创建了数据连接文件后，可以将该数据连接作为其数据源来启动 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]。<br /><br /> [创建与 PowerPivot 工作簿的 BI 语义模型连接](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook)<br /><br /> [创建与表格模型数据库的 BI 语义模型连接](../../relational-databases/databases/model-database.md)<br /><br /> 注意：由于您安装了 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 版本的 Reporting Services 并将服务器配置为共享服务，因此可以使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。 如果您安装了 Reporting Services 并为 SQL Server 2008 级别的集成配置了它，则 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 不可用。|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2012 的各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)  
  
  
