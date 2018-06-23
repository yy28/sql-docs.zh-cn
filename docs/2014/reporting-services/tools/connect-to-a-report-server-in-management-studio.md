---
title: 在 Management Studio 中连接到报表服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], connections
- connections [Reporting Services], report server
- registering report servers
- report servers [Reporting Services], registering
ms.assetid: c875ff87-ee7d-443a-a702-bdb4b6c27c6e
caps.latest.revision: 51
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 34145968707e6ccc2a531fdddead84ba805aadb5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017033"
---
# <a name="connect-to-a-report-server-in-management-studio"></a>在 Management Studio 中连接到报表服务器
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 提供了对象资源管理器，可用于连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系列中的任何服务器，并以图形方式浏览其内容。 对于 Reporting Services，可以使用对象资源管理器执行以下操作：  
  
-   启用报表服务器功能。  
  
-   设置服务器默认值并配置角色定义。  
  
-   管理正在运行的作业。  
  
-   管理作业计划。  
  
 您可以连接到本机模式的报表服务器，也可以连接到在 SharePoint 集成模式下运行的报表服务器。 连接语法和可执行的操作类型因报表服务器的服务器模式和您的权限而异。 如果在连接到报表服务器或执行特定任务时遇到问题，则可能表示您的权限不足或所指定的报表服务器名称不正确。 有关权限和连接语法的详细信息，请参阅本主题结尾处的表格。  
  
 请注意，您不能使用对象资源管理器来查看或管理报表服务器内容。 如果报表服务器在本机模式下运行，则通过报表管理器执行内容管理；如果报表服务器在 SharePoint 集成模式下运行，则通过 SharePoint 站点执行内容管理。  
  
 通过对象资源管理器，可以与同一工作区中的多个服务器实例建立连接，条件是这些服务器是在同一个服务器组中注册的。 在连接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的报表服务器实例之前，必须注册该服务器。 如果已注册报表服务器，则可跳过此步骤。 本主题结尾介绍了有关注册报表服务器的说明。  
  
### <a name="to-connect-to-a-native-mode-report-server"></a>连接到本机模式的报表服务器  
  
1.  如果对象资源管理器尚未打开报表服务器，请从“视图”菜单中选择该服务器。  
  
2.  单击 **“连接”** 查看服务器类型列表，然后选择 **Reporting Services**。  
  
3.  在 **“连接到服务器”** 对话框中，输入报表服务器实例的名称。 报表服务器实例的名称基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。 默认情况下，本地报表服务器实例的实例名称就是计算机的名称。 如果将报表服务器作为命名实例进行安装，请使用此语法来指定该服务器：\<servername>[\\<instancename\>]。  
  
4.  选择身份验证类型。 如果使用的是 Windows 身份验证，则必须使用凭据进行连接。 如果选择“基本身份验证”或“窗体身份验证”，请键入帐户和密码。  
  
5.  单击 **“连接”**。 此时，相应的报表服务器将显示在对象资源管理器中。  
  
6.  右键单击服务器节点以设置系统属性和服务器默认值。 有关详细信息，请参阅[设置报表服务器属性 (Management Studio)](set-report-server-properties-management-studio.md)。  
  
### <a name="to-connect-to-a-sharepoint-integrated-mode-report-server"></a>连接到 SharePoint 集成模式的报表服务器  
  
1.  如果对象资源管理器尚未打开报表服务器，请从“视图”菜单中选择该服务器。  
  
2.  单击“连接”查看服务器类型列表，然后选择 **Reporting Services**。  
  
3.  在 **“连接到服务器”** 对话框中，输入指向 SharePoint 站点的 URL。 下面的示例说明了语法： http://\<web 服务器 > /sites/\<站点 >。  
  
4.  选择身份验证类型。 如果使用的是 Windows 身份验证，则必须使用凭据进行连接。 如果选择“基本身份验证”或“窗体身份验证”，请键入帐户和密码。  
  
5.  单击 **“连接”**。 此时，相应的报表服务器将显示在对象资源管理器中。  
  
6.  右键单击服务器节点以设置系统属性和服务器默认值。 有关详细信息，请参阅[设置报表服务器属性 (Management Studio)](set-report-server-properties-management-studio.md)。  
  
### <a name="to-register-a-report-server"></a>注册报表服务器  
  
1.  如果无法连接到报表服务器，则可能是您没有访问报表服务器的权限，也可能是必须注册报表服务器。 若要注册服务器，请单击“视图”菜单中的 **“已注册的服务器”** 。  
  
2.  单击 Reporting Services 图标。  
  
3.  右键单击 Reporting Services，指向“新建”，再单击“服务器注册”。 此时，将显示 **“新建服务器注册”** 对话框。  
  
4.  在 **“服务器名称”** 中，输入一个值。 您必须指定的值因服务器模式而异：  
  
    -   对于本机模式的报表服务器，请键入报表服务器实例的名称。 报表服务器实例的名称取决于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。 默认情况下，本地报表服务器实例的实例名称就是计算机的名称。 如果将报表服务器作为命名实例进行安装，请使用此语法来指定该服务器：\<servername>[\\<instancename\>]。  
  
    -   对于在 SharePoint 集成模式下运行的报表服务器，要连接到的服务器是连接报表服务器的 SharePoint 站点。 为查看用于控制对报表服务器内容和操作的访问的权限级别，必须连接到 SharePoint 站点。 可以指定网站集中的任何站点。 下例说明了相应的语法：http://mysharepointsite。  
  
5.  对于 **“身份验证”**，请选择访问 Web 服务器时所用的身份验证模式。 必须选择报表服务器已经使用的身份验证模式。  
  
    -   如果您使用的是默认安全性，请选择 **“Windows 身份验证”**。  
  
    -   如果已安装和部署了自定义的安全扩展插件，请选择 **“窗体身份验证”**。  
  
    -   如果已将报表服务器配置为使用基本身份验证，请选择 **“基本身份验证”**。  
  
    -   如果将报表服务器配置为 SharePoint 集成模式，请选择 **“Windows 身份验证”**。  
  
6.  单击 **“测试”** 验证连接是否可用。  
  
7.  在出现提示时，单击 **“确定”**，再单击 **“保存”**。  
  
## <a name="connection-syntax-and-permissions"></a>连接语法和权限  
 下表概述了连接语法、操作和执行特定操作所需的权限。  
  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] “连接到服务器” **对话框中将** 指定为服务器类型时，可以指定报表服务器名称或 Web 服务端点。  
  
|连接到|“任务”|权限|  
|----------------|-----------|-----------------|  
|本机模式的报表服务器，作为默认实例或命名实例进行连接：<br /><br /> \<server name>\<_instance><br /><br /> 与报表服务器的连接是通过报表服务器 WMI 提供程序建立的。|查看和设置服务器属性与默认值。<br /><br /> 查看和取消作业。<br /><br /> 创建和管理共享计划。<br /><br /> 创建、修改或删除角色定义。|分配给“系统管理员”角色。|  
|本机模式的报表服务器，作为默认实例或命名实例进行连接，通过报表服务器 Web 服务端点：<br /><br /> http://\<服务器名 > / reportserver<br /><br /> 指定指向报表服务器的 URL 提供了另一种连接到报表服务器的方法。|查看和设置服务器属性与默认值。<br /><br /> 查看和取消作业。<br /><br /> 创建和管理共享计划。<br /><br /> 创建、修改或删除角色定义。|分配给“系统管理员”角色。|  
|SharePoint 集成模式的报表服务器，通过 SharePoint 站点进行连接：<br /><br /> http://\<web 服务器 > /\<SharePointSite >|查看和设置服务器属性与默认值。<br /><br /> 查看和取消作业。<br /><br /> 创建和管理为所连接的站点定义的共享计划。<br /><br /> 查看为所连接的站点定义的权限级别。|对所连接的 SharePoint 站点拥有“完全控制”级权限。|  
|SharePoint 集成模式的报表服务器，通过报表服务器实例的名称进行连接：<br /><br /> \<server name>\<_instance>|查看和设置服务器属性与默认值。<br /><br /> 查看和取消作业。|对与报表服务器集成的 SharePoint 站点拥有“完全控制”级权限。<br /><br /> 请注意，当您连接到报表服务器而非 SharePoint 站点时，可以执行的任务数将会明显减少。 这是因为报表服务器只能返回在报表服务器数据库，而不是 SharePoint 配置数据库和内容数据库中存储或管理的应用程序数据。|  
  
## <a name="see-also"></a>请参阅  
 [配置报表服务器数据库连接&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [SQL Server Management Studio 中的 Reporting Services (SSRS)](reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  