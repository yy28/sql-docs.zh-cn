---
title: Reporting Services 配置管理器（本机模式）| Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
ms.assetid: 379eab68-7f13-4997-8d64-38810240756e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f3dc4e2b2df66b9670bf00e39e6f4a2624c4105e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059054"
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Reporting Services 配置管理器（本机节点）
  使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器可配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式安装。 如果通过使用仅安装文件选项安装报表服务器，必须使用配置管理器来配置服务器，然后才能使用服务器。 如果使用默认配置安装选项安装了报表服务器，则可以使用配置管理器来验证或修改在安装过程中指定的设置。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器可以用来配置本地或远程报表服务器实例。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。  
  
> [!NOTE]  
>  从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本开始， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理员不设计用来管理 SharePoint 模式报表服务器。 SharePoint 模式通过使用 SharePoint 管理中心和 PowerShell 脚本进行管理和配置。 有关信息，请参阅[sharepoint 2010 和 sharepoint 2013&#41;&#40;Reporting Services Sharepoint 模式安装](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
 **本部分内容：**  
  
 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 提供有关如何修改服务帐户和密码的建议和步骤。  
  
 [配置报表服务器 URL（SSRS 配置管理器）](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 介绍如何配置用来访问报表服务器 Web 服务和报表管理器的 URL。  
  
 [创建报表服务器数据库（SSRS 配置管理器）](../../../2014/sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
 介绍如何创建存储服务器元数据和对象所必需的报表服务器数据库。  
  
 [配置报表服务器数据库连接（SSRS 配置管理器）](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 介绍如何修改报表服务器用于连接到报表服务器数据库的连接字符串。  
  
 [配置无人参与的执行帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 介绍如何配置用户帐户以便以无人参与的方式处理报表。  
  
 [配置报表服务器，以便 &#40;SSRS Configuration Manager 发送电子邮件&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 介绍如何配置报表服务器，以便通过电子邮件来分发报表。  
  
 [配置本机模式报表服务器扩展部署（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 提供有关配置多个报表服务器实例以使用共享报表服务器数据库的信息。  
  
 [配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
 介绍如何使用和管理存储敏感数据时使用的加密密钥。  
  
 [管理 Reporting Services 本机模式报表服务器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
 提供常见任务的分步说明。  
  
 [Reporting Services 配置管理器的 F1 帮助主题 &#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
 提供有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具页面的帮助主题。  
  
 **本主题内容：**  
  
-   [要使用 Reporting Services 配置管理器的情形](#bkmk_scenarios)  
  
-   [要求](#bkmk_requirements)  
  
-   [启动 Reporting Services 配置管理器](#bkmk_start_configuration_manager)  
  
##  <a name="scenarios-to-use-reporting-services-configuration-manager"></a><a name="bkmk_scenarios"></a>使用方案 Reporting Services 配置管理器  
 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器执行下列任务：  
  
-   配置报表服务器服务帐户。 此帐户最初是在安装过程中配置的，但是，如果需要更新密码或使用其他帐户，则可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器进行修改。  
  
-   创建和配置的 URL。 报表服务器和报表管理器都是可通过 URL 进行访问的 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序。 报表服务器 URL 提供对报表服务器 SOAP 端点访问。 报表管理器 URL 用于打开报表管理器。 可以为每个应用程序配置一个或多个 URL。  
  
-   创建和配置报表服务器数据库。 报表服务器是一个无状态服务器，它需要将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库用于内部存储。 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器来创建报表服务器数据库并配置与该数据库的连接。 还可以选择已包含要使用的内容的现有报表服务器数据库。  
  
-   配置本机模式扩展部署。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持允许多个报表服务器实例使用一个共享报表服务器数据库的部署拓扑。 若要部署报表服务器扩展部署，请使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器将每个报表服务器连接到共享的报表服务器数据库。  
  
-   备份、还原或替换用于加密存储的连接字符串以及凭据的对称密钥。 如果更改服务帐户或将报表服务器数据库移动到其他计算机上，则必须对对称密钥进行备份。  
  
-   配置无人参与的执行帐户。 在计划操作过程中或用户凭据不可用时，可以使用此帐户进行远程连接。  
  
-   配置报表服务器电子邮件。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了一个报表服务器电子邮件传递扩展插件，该插件使用简单邮件传输协议 (SMTP) 将报表或报表处理通知传递到电子邮箱。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器指定网络中用于电子邮件传递的 SMTP 服务器或网关。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器并不帮助您管理报表服务器内容、启用额外功能或授予服务器的访问权。 完全部署要求你还使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 启用附加功能或修改默认值，并报表管理器向用户授予对服务器的访问权限。  
  
##  <a name="requirements"></a><a name="bkmk_requirements"></a>要求  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器是版本特定的。 随此版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 一起安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器不能用于配置早期版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 如果在同一计算机上并行运行新版本和旧版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，则必须使用随每个版本安装的 Reporting Service 配置管理器来配置每个实例。  
  
 若要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，必须具有以下权限：  
  
-   对承载要配置的报表服务器的计算机具有本地系统管理员权限。 如果您正在配置远程计算机，则您还必须对该计算机具有本地系统管理员权限。  
  
-   您必须有权针对用于承载报表服务器数据库的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 创建数据库。  
  
-   Windows Management Instrumentation (WMI) 服务必须启用并在任何正在配置的报表服务器上运行。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器使用报表服务器 WMI 提供程序连接至本地和远程报表服务器。 如果您正在配置远程报表服务器，则计算机必须允许远程 WMI 访问。 有关详细信息，请参阅 [配置报表服务器以进行远程管理](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)。  
  
-   在可以连接到远程报表服务器实例并对其进行配置之前，必须使远程 Windows Management Instrumentation (WMI) 调用能够通过 Windows 防火墙。 有关详细信息，请参阅 [联机丛书中的](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) 配置报表服务器以进行远程管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 随此版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 时，会自动安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
##  <a name="to-start-the-reporting-services-configuration-manager"></a><a name="bkmk_start_configuration_manager"></a>启动 Reporting Services 配置管理器  
  
#### <a name="to-start-reporting-services-configuration"></a>启动 Reporting Services 配置  
  
1.  使用适合于您的 Microsoft Windows 版本的以下步骤：  
  
    -   从 Windows“开始”屏幕上，键入 **Reporting** ，然后从搜索结果中选择 **“Reporting Services 配置管理器”** 。  
  
    -   单击 **“开始”**，依次指向 **“所有程序”**、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]和 **“配置工具”**。  
  
         如果要从先前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中配置报表服务器实例，请打开此版本的程序文件夹。 例如，在打开 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 服务器组件的配置工具时，应指向 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] 而非 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 。  
  
         单击 **“Reporting Services 配置管理器”**。  
  
2.  此时将出现 **“Reporting Services 配置连接”** 对话框，可以选择要配置的报表服务器实例。 单击“连接”。  
  
3.  在 **“服务器名称”** 中，指定安装报表服务器实例的计算机的名称。 默认情况下，将显示本地计算机的名称，但如果要连接到安装在远程计算机上的报表服务器，则可以键入远程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。  
  
4.  如果指定远程计算机，请单击 **“查找”** 以建立一个连接。  
  
5.  在“报表服务器实例”**** 中，选择要配置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例。 在列表中只显示此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的报表服务器实例。 不能配置较早版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
6.  单击“连接”。  
  
## <a name="see-also"></a>另请参阅  
 [报表管理器（SSRS 本机模式）](../../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)   
 [&#40;SSRS Configuration Manager 配置报表服务器数据库连接&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)   
 [配置和管理报表服务器（SSRS 本机模式）](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
