---
title: 连接到服务器 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connection.login.reportserver.f1
ms.assetid: ef81b658-8eb5-4636-ac81-eead10cc7b9f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 18afc2a57f4e86417f4228baa459117f1dc7f7a2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934588"
---
# <a name="connect-to-server-reporting-services"></a>连接到服务器 (Reporting Services)
  连接到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 时，可以使用此对话框查看或指定选项。  
  
## <a name="options"></a>选项  
 **服务器类型**  
 从**对象资源管理器**注册服务器时，请选择要连接到的服务器的类型： [!INCLUDE[ssDE](../includes/ssde-md.md)] 、Analysis Services、Reporting Services 或 Integration Services。 对话框的其余部分只显示适用于所选服务器类型的选项。 从**已注册的服务器**注册服务器时，"**服务器类型**" 框是只读的，并且与 "**已注册的服务器**" 组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在 [!INCLUDE[ssDE](../includes/ssde-md.md)] 开始注册新服务器之前，从 "**已注册的服务器**" 工具栏中选择、Analysis Services、Reporting Services 或 Integration Services。  
  
 **服务器名称**  
 您要连接到的报表服务器实例的服务器模式决定了必须输入的值。  
  
 对于在本机模式下运行的报表服务器，指定要连接到的报表服务器实例。 如果使用默认实例，服务器名通常是计算机的名称。 如果安装了命名实例，请按以下格式将实例名称附加到服务器名称： \<servername> \\<InstanceName \> 。 Reporting Services 使用反斜杠字符分隔实例名。  
  
 对于在 SharePoint 集成模式下运行的报表服务器，必须指定 SharePoint 站点。 可以指定与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]集成的站点集合中的任意站点。 您提供的 URL 必须包含 HTTP 或 HTTPS 前缀。 您必须有权访问 SharePoint 站点，才能在 Management Studio 中连接到该站点。 分配给您的权限级别将决定您可以查看和管理的项目。 有关详细信息，请参阅[连接到 Management Studio 中的报表服务器](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)。  
  
 **身份验证**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 可以配置为接受由你提供的自定义身份验证扩展插件处理的 Windows 身份验证请求或窗体身份验证请求。 请从以下身份验证模式中选择一个，以便在连接到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]时使用：  
  
 **Windows 身份验证模式（Windows 身份验证）**  
 使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 凭据连接到报表服务器实例。  
  
 **基本身份验证**  
 如果将 Reporting Services 安装配置为使用基本身份验证，则使用“基本身份验证”**** 进行连接。  
  
 **窗体身份验证**  
 如果将 Reporting Services 安装配置为使用自定义身份验证扩展插件，则使用“窗体身份验证”**** 进行连接。  
  
 **用户名**  
 输入用于连接的登录名。 只有在选择了 **“基本身份验证”** 或 **“窗体身份验证”** 时，此选项才可用。  
  
 **密码**  
 输入用户名的密码。 只有在选择了 **“基本身份验证”** 或 **“窗体身份验证”** 时，此选项才可编辑。  
  
 **“连接”**  
 单击此项可连接到在上面选择的服务器。  
  
 **选项**  
 单击此项可显示其他服务器连接选项，如注册服务器和记住密码。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSRS Configuration Manager 配置报表服务器数据库连接&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [在 Management Studio 中连接到报表服务器](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [针对报表服务器的身份验证](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
