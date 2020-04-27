---
title: 向场中添加另一个报表服务器（SSRS 横向扩展）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b90bb5624e5b5cdbf3f1542ad0bef0d2765da248
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108969"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>向场中添加另一个报表服务器（SSRS 扩展）
  将第二个或更多的 SharePoint 模式报表服务器添加到您的 SharePoint 场可改进报表服务器处理的性能和响应时间。 如果您在将更多的用户、报表和其他应用程序添加到报表服务器时发现性能下降，则添加其他报表服务器可改进性能。 在存在硬件问题或者您在对环境中的单独服务器执行一般性的维护时，也建议添加第二个报表服务器以便提高报表服务器的可用性。 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本开始，用于在 SharePoint 模式中扩展 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 环境的步骤遵循标准 SharePoint 场部署并且利用 SharePoint 负载平衡功能。  
  
> [!IMPORTANT]  
>  并非所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本都支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的扩展。 有关详细信息，请参阅[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [SQL Server 2014 的各个版本支持的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)部分。  
  
> [!TIP]  
>  从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，您将不使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器添加服务器和扩展报表服务器。 将带有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务的 SharePoint 服务器添加到场中时，SharePoint 产品管理 Reporting Services 的扩展。  
  
 有关如何扩展本机模式报表服务器的信息，请参阅[配置本机模式报表服务器扩展部署（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)。  
  
-   [负载平衡](#bkmk_loadbalancing)  
  
-   [先决条件](#bkmk_prerequisites)  
  
-   [步骤](#bkmk_steps)  
  
-   [其他配置](#bkmk_additional)  
  
##  <a name="load-balancing"></a><a name="bkmk_loadbalancing"></a>负载均衡  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的负载平衡将由 SharePoint 自动管理，除非您的环境具有自定义或第三方负载平衡解决方案。 默认 SharePoint 负载平衡行为是，每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序都将在您启动了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务的所有应用程序服务器之间保持平衡。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 若要确认 **** 服务是否安装和启动，请在 SharePoint 管理中心中单击“管理服务器上的服务”。  
  
##  <a name="prerequisites"></a><a name="bkmk_prerequisites"></a>先决条件  
  
-   您必须是本地管理员才能运行 SQL Server 安装程序。  
  
-   必须将计算机加入到域中。  
  
-   您需要知道承载 SharePoint 配置和内容数据库的现有数据库服务器的名称。  
  
-   该数据库服务器必须配置为允许远程数据库连接。  如果没有这样配置，将无法将新的服务器连接到场，因为这个新服务器将无法建立与 SharePoint 配置数据库的连接。  
  
-   新服务器将需要安装有与当前场服务器正在运行的 SharePoint 相同的版本。 例如，如果该场已安装了 SharePoint 2010 Service Pack 1 (SP1)，则您还需要在新的服务器上安装 SP1，然后才能将其联接到该场。  
  
-   查看以下其他主题以了解系统和版本要求：  
  
     [在 SharePoint 2010 场中使用 SQL Server BI 功能的指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="steps"></a><a name="bkmk_steps"></a>逐步  
 本主题中的步骤假定 SharePoint 场管理员正在安装和配置服务器。 下图说明一个典型的三层环境，下面的列表中将说明图中的编号项：  
  
-   (1) 多个 Web 前端 (WFE) 服务器。 WFE 服务器要求用于 SharePoint 2010 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序。  
  
-   (2) 运行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和网站的单个应用程序服务器，例如管理中心。 以下步骤将第二个应用程序服务器添加到这一层。  
  
-   (3) 两个 SQL Server 数据库服务器。  
  
-   (4) 表示软件或硬件的网络负载平衡解决方案 (NLB)  
  
 ![添加 Reporting Services 应用程序服务器](../../../2014/sql-server/install/media/rs-sharepointscale.gif "添加 Reporting Services 应用程序服务器")  
  
 下面的步骤假定管理员正在安装和配置服务器。 服务器将设置为场中的新的应用程序服务器，并且不用作 Web 前端 (WFE)。  
  
|步骤|说明和链接|  
|----------|--------------------------|  
|运行 SharePoint 2010 产品准备工具|您必须拥有 SharePoint 2010 安装介质。 准备工具是安装介质中的 **PrerequisiteInstaller.exe** 。|  
|安装 SharePoint 2010 产品。|1）选择 "**服务器场**" 安装类型。<br /><br /> 2）为服务器类型选择 "**完成**"。<br /><br /> 3) 安装完成后，如果你的现有 SharePoint 场已安装 SharePoint 2010 SP1，则不要运行 SharePoint 产品配置向导。 您应该在运行 SharePoint 产品配置向导之前安装 SharePoint SP1。|  
|安装 SharePoint Server 2010 SP1。|如果现有 SharePoint 场安装了 SharePoint 2010 SP1，请从中下载并安装 SharePoint 2010[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697)sp1：。<br /><br /> 有关 SharePoint 2010 SP1 的详细信息，请参阅 [安装 Office 2010 SP1 和 SharePoint 2010 SP1 时的已知问题](https://support.microsoft.com/kb/2532126)：|  
|运行 SharePoint 产品配置向导以便向场中添加服务器。|1）在 " **Microsoft sharepoint 2010 products** " 程序组中，单击 " **Microsoft Sharepoint 2010 产品配置向导**"。<br /><br /> 2）在 "**连接到服务器场**" 页上，选择 "**连接到现有场**" 并单击 "**下一步**"。<br /><br /> 3）在 "**指定配置数据库设置**" 页上，键入用于现有场的数据库服务器的名称以及配置数据库的名称。 单击“下一步”  。<br />** \* \*重要\*提示**如果你看到类似于以下内容的错误消息，并且已验证你具有权限，请验证**SQL Server**中的 SQL Server 网络配置是否启用了哪些协议 Configuration Manager： "无法连接到数据库服务器。 请确保数据库存在，是 Sql Server，并且您具有访问服务器的相应权限。 "<br />** \* \*重要\*提示**如果你看到 "**服务器场产品和修补程序状态**" 页，则需要查看该页上的信息，然后用所需文件更新服务器，然后才能继续将服务器加入到场。<br /><br /> 4）在 "**指定场安全设置**" 页上键入场密码，然后单击 "**下一步**"。 在确认页上单击 **“下一步”** 以便运行向导。<br /><br /> 5）单击 "**下一步**" 运行**场配置向导**。|  
|验证服务器已添加到 SharePoint 场。|1) 在 SharePoint 管理中心的“系统设置”组中，单击“管理此场中的服务器”********。<br /><br /> 2) 确认新的服务器是否已添加且状态是否正确。<br /><br /> 3）请注意，你看不到服务**SQL Server Reporting Services 服务**正在运行。 该服务将在下一步中安装。<br /><br /> 4）若要从 WFE 角色中删除此服务器，请单击 "**管理服务器上的服务"** 并停止服务 " **Microsoft SharePoint Foundation Web 应用程序**"。|  
|安装和配置 Reporting Services SharePoint 模式。|运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装。 有关[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint 模式安装的详细信息，请参阅[Install Reporting Services SharePoint mode for sharepoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)如果该服务器将仅用作应用程序服务器，并且该服务器将不用作 WFE，则无需在以下项中选择**用于 SharePoint 产品的 Reporting Services 外接程序**：<br /><br /> "**设置角色**" 页上，选择**SQL Server 功能安装**<br /><br /> 在 "**功能选择**" 页上，选择**Reporting Services-SharePoint**<br /><br /> - 或 -<br /><br /> 在 " **Reporting Services 配置**" 页上，验证是否选择了 "**仅安装**" 选项以**Reporting Services SharePoint 模式**。|  
|验证 Reporting Services 是否正常运行。|1) 在 SharePoint 管理中心的“系统设置”组中，单击“管理此场中的服务器”********。<br /><br /> 2) 验证“SQL Server Reporting Services 服务”服务****。<br /><br /> 有关详细信息，请参阅[验证 Reporting Services 安装](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)|  
  
##  <a name="additional-configuration"></a><a name="bkmk_additional"></a>其他配置  
 可以优化扩展部署中的单个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务器以仅执行后台处理，从而不与交互式报表执行争用资源。 后台处理包括计划、订阅和数据警报。  
  
 若要更改单个报表服务器的行为，请在**rsreportserver.config**配置文件中将** \<iswebserviceenable>>** 设置为 false。  
  
 默认情况下，将配置报表服务器且 \<IsWebServiceEnable> 将设置为 TRUE。 当所有服务器都配置为 TRUE 时，将在场中的所有节点上均衡交互式操作和后台处理的负载。  
  
 如果配置所有报表服务器且 \<IsWebServiceEnable> 设置为 False，则在尝试使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能时将看到类似以下内容的一条错误消息：  
  
 未启用 Reporting Services Web 服务。 至少配置一个 Reporting Services SharePoint 服务的实例，使\<iswebserviceenable>> 设置为 true。 有关详细信息，请参阅[Rsreportserver.config 配置文件 &#40;修改 Reporting Services&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
## <a name="see-also"></a>另请参阅  
 [在 SharePoint 2013 中将 web 服务器或应用程序服务器添加到场](https://technet.microsoft.com/library/cc261752.aspx)   
 [配置服务 (SharePoint Server 2010)](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
