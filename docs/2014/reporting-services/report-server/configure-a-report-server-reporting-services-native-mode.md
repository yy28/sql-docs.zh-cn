---
title: 配置报表服务器（Reporting Services 本机模式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report server configuration
- report servers [Reporting Services], configuring
ms.assetid: ef84ce9d-9156-48e9-8073-7e0535476932
caps.latest.revision: 16
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 0ec1501c32505b760fba2ec88e21140de1cf0211
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015189"
---
# <a name="configure-a-report-server-reporting-services-native-mode"></a>配置报表服务器（Reporting Services 本机模式）
  报表服务器可能需要进行其他配置后才能使用，具体取决于安装过程中所选的选项。 至少，报表服务器配置应包含以下内容：  
  
-   报表服务器服务帐户（在安装过程中配置的）。  
  
-   用于访问报表服务器的 Web 服务 URL。  
  
-   用于存储应用程序数据、报表和其他项的报表服务器。  
  
 如果选择了以下安装选项之一：本机模式默认配置或 SharePoint 集成模式默认配置，则安装程序会配置最低设置。 如果在“仅文件”模式下安装报表服务器（即通过安装向导中的 **“安装但不配置”** 选项），则只需要配置服务帐户。 完成安装之后，必须配置 Web 服务 URL 和报表服务器数据库。  
  
 报表管理器是本机模式报表服务器的可选功能，但建议您配置报表管理器，以便授予用户访问报表服务器和管理报表服务器内容的权限。 如果在 SharePoint 集成模式下部署报表服务器，可使用 SharePoint 服务器的 Web 前端授予访问权限。  
  
 可以根据需要配置其他功能，例如报表服务器电子邮件和无人参与的执行帐户。 有关详细信息，请参阅[管理 Reporting Services 本机模式报表服务器](manage-a-reporting-services-native-mode-report-server.md)。  
  
 若要配置报表服务器，请使用 Reporting Services 配置工具。  
  
### <a name="to-minimally-configure-a-report-server-installation"></a>对报表服务器安装进行最小配置  
  
1.  启动 Reporting Services 配置管理器，然后连接到报表服务器实例。 有关说明，请参阅 [Reporting Services Configuration Manager（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
2.  单击 **“Web 服务 URL”** ，打开用于配置报表服务器 URL 的页。 有关如何定义 URL 的说明，请参阅[配置 URL（SSRS 配置管理器）](../install-windows/configure-a-url-ssrs-configuration-manager.md)。  
  
3.  单击 **“数据库”** 创建报表服务器数据库。 有关指导，请参阅[创建本机模式报表服务器数据库（SSRS 配置管理器）](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。  
  
4.  返回到 **“Web 服务 URL”** 页，单击该 URL 以验证其是否有效。  
  
5.  按照“后续步骤”中的说明完成您的部署。  
  
## <a name="next-steps"></a>后续步骤  
 若要完成部署，应配置报表管理器或 SharePoint 集成。 有关详细信息，请参阅[配置报表管理器（本机模式）](configure-web-portal.md)。  
  
 如果 Windows 防火墙已开启，配置为报表服务器使用的端口很可能已关闭。 表明端口可能已关闭的一个迹象是在尝试从远程客户端计算机打开报表管理器时出现空白页。 有关配置防火墙的信息，请参阅[为报表服务器访问配置防火墙](configure-a-firewall-for-report-server-access.md)。  
  
 如果使用的是 Windows Vista 或 Windows Server 2008，则可能需要执行其他步骤，才能在本地打开报表管理器。 有关详细信息，请参阅 [为本地管理配置本机模式报表服务器 (SSRS)](configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
 通过创建文件夹、上载项和运行报表来验证您的安装。 按照中的说明[验证 Reporting Services 安装](../install-windows/verify-a-reporting-services-installation.md)以验证你的安装。  
  
## <a name="see-also"></a>请参阅  
 [管理 Reporting Services 本机模式报表服务器](manage-a-reporting-services-native-mode-report-server.md)   
 [将防火墙配置为允许报表服务器访问](configure-a-firewall-for-report-server-access.md)   
 [配置本机模式报表服务器以进行本地管理 (SSRS)](configure-a-native-mode-report-server-for-local-administration-ssrs.md)   
 [配置报表服务器以进行远程管理](configure-a-report-server-for-remote-administration.md)   
 [Reporting Services Configuration Manager（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  