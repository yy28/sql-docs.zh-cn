---
title: Reporting Services 配置管理器（本机模式）| Microsoft Docs
ms.custom: ''
ms.date: 09/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a8bfa3073551c1a4881a5f3a13158a955b8fead8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993486"
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Reporting Services 配置管理器（本机节点）

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器可配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式安装。 如果通过使用仅安装文件选项安装报表服务器，必须使用配置管理器来配置服务器，然后才能使用服务器。 如果使用默认配置安装选项安装了报表服务器，则可以使用配置管理器来验证或修改在安装过程中指定的设置。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器可以用来配置本地或远程报表服务器实例。

> [!NOTE]
> 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本开始， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理员不设计用来管理 SharePoint 模式报表服务器。 SharePoint 模式通过使用 SharePoint 管理中心和 PowerShell 脚本进行管理和配置。  
  
##  <a name="bkmk_scenarios"></a> 要使用 Reporting Services 配置管理器的情形  
 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器执行下列任务：  
  
-   配置报表服务器服务帐户。 此帐户最初是在安装过程中配置的，但是，如果需要更新密码或使用其他帐户，则可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器进行修改。  
  
-   创建和配置的 URL。 报表服务器和 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 都是可通过 URL 进行访问的 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序。 报表服务器 URL 提供对报表服务器 SOAP 端点访问。 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] URL 用于打开 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] ，你可以为每个应用程序配置一个或多个 URL。  
  
-   创建和配置报表服务器数据库。 报表服务器是一个无状态服务器，它需要将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库用于内部存储。 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器来创建报表服务器数据库并配置与该数据库的连接。 还可以选择已包含要使用的内容的现有报表服务器数据库。  
  
-   配置本机模式扩展部署。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持允许多个报表服务器实例使用一个共享报表服务器数据库的部署拓扑。 若要部署报表服务器扩展部署，请使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器将每个报表服务器连接到共享的报表服务器数据库。  
  
-   备份、还原或替换用于加密存储的连接字符串以及凭据的对称密钥。 如果更改服务帐户或将报表服务器数据库移动到其他计算机上，则必须对对称密钥进行备份。  
  
-   配置无人参与的执行帐户。 在计划操作过程中或用户凭据不可用时，可以使用此帐户进行远程连接。  
  
-   配置报表服务器电子邮件。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了一个报表服务器电子邮件传递扩展插件，该插件使用简单邮件传输协议 (SMTP) 将报表或报表处理通知传递到电子邮箱。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器指定网络中用于电子邮件传递的 SMTP 服务器或网关。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器并不帮助您管理报表服务器内容、启用额外功能或授予服务器的访问权。 完全部署还需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 启用额外功能或修改默认值，以及使用 Web 门户授予用户对服务器的访问权。

##  <a name="bkmk_requirements"></a> 要求

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器是版本特定的。 随此版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 一起安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器不能用于配置早期版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 如果在同一计算机上并行运行新版本和旧版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，则必须使用随每个版本安装的 Reporting Service 配置管理器来配置每个实例。  

若要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，必须具有以下权限：

- 对承载要配置的报表服务器的计算机具有本地系统管理员权限。 如果您正在配置远程计算机，则您还必须对该计算机具有本地系统管理员权限。

- 您必须有权针对用于承载报表服务器数据库的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 创建数据库。

- Windows Management Instrumentation (WMI) 服务必须启用并在任何正在配置的报表服务器上运行。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器使用报表服务器 WMI 提供程序连接至本地和远程报表服务器。 如果您正在配置远程报表服务器，则计算机必须允许远程 WMI 访问。 有关详细信息，请参阅 [配置报表服务器以进行远程管理](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)。  

- 在可以连接到远程报表服务器实例并对其进行配置之前，必须使远程 Windows Management Instrumentation (WMI) 调用能够通过 Windows 防火墙。 有关详细信息，请参阅 [联机丛书中的](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) 配置报表服务器以进行远程管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

安装 SQL Server Reporting Services 时，将自动安装 Reporting Services 配置管理器。

##  <a name="bkmk_start_configuration_manager"></a> 启动 Reporting Services 配置管理器

1.  使用适合于您的 Microsoft Windows 版本的以下步骤：

    - 从 Windows“开始”屏幕上，键入“Reporting”，然后从搜索结果中选择“Reporting Services 配置管理器”。

    - 选择“开始”，依次指向“所有程序”、[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] 和“配置工具”。

         如果要从先前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中配置报表服务器实例，请打开此版本的程序文件夹。 例如，在打开 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 服务器组件的配置工具时，应指向 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] 而非 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。

         选择“Reporting Services 配置管理器”。

2. 此时将出现 **“Reporting Services 配置连接”** 对话框，可以选择要配置的报表服务器实例。 选择“连接”。

3. 在 **“服务器名称”** 中，指定安装报表服务器实例的计算机的名称。 默认情况下，将显示本地计算机的名称，但如果要连接到安装在远程计算机上的报表服务器，则可以键入远程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。

4. 如果指定远程计算机，请选择“查找”以建立连接。

5. 在 **Report Server 在stance**中，选择要配置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例。 在列表中只显示此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的报表服务器实例。 不能配置较早版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。

6. 选择“连接”。

## <a name="next-steps"></a>后续步骤

[Web 门户](../../reporting-services/web-portal-ssrs-native-mode.md)   
[Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)   
[配置报表服务器数据库连接](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)   
[配置和管理报表服务器](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
