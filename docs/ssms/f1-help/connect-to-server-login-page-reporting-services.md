---
title: "连接到服务器（“登录”页）(Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttors.login.f1
helpviewer_keywords:
- Connect to Server dialog box, Reporting Services
ms.assetid: d312c740-19d7-4931-84a2-88b805ec8439
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f1dfb11e842436e8787624e3b16ba178423859b2
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-login-page-reporting-services"></a>连接到服务器（“登录”页）(Reporting Services)
连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] 时，使用此选项卡可查看或指定以下选项。  
  
## <a name="options"></a>选项  
**服务器类型**  
从对象资源管理器进行服务器注册时，请选择要连接到何种类型的服务器： [!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。 对话框的其余部分只显示适用于所选服务器类型的选项。 从“已注册的服务器”注册某服务器时，“服务器类型”框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择 [!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。  
  
**服务器名称**  
您要连接到的报表服务器实例的服务器模式决定了必须输入的值。  
  
对于在本机模式下运行的报表服务器，指定要连接到的报表服务器实例。 如果使用默认实例，服务器名通常是计算机的名称。 如果安装了命名实例，请将实例名追加到服务器名后面，格式如下： <servername>\\<InstanceName>。 Reporting Services 使用反斜杠字符分隔实例名。  
  
对于在 SharePoint 集成模式下运行的报表服务器，必须指定 SharePoint 站点。 可以指定与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]集成的站点集合中的任意站点。 您提供的 URL 必须包含 HTTP 或 HTTPS 前缀。 您必须有权访问 SharePoint 站点，才能在 Management Studio 中连接到该站点。 分配给您的权限级别将决定您可以查看和管理的项目。 有关详细信息，请参阅 [如何注册和连接报表服务器](http://msdn.microsoft.com/en-us/c875ff87-ee7d-443a-a702-bdb4b6c27c6e)。  
  
**身份验证**  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] 可以配置为接受由你提供的自定义身份验证扩展插件处理的 Windows 身份验证请求或窗体身份验证请求。 请从以下身份验证模式中选择一个，以便在连接到 Reporting Services 时使用：  
  
**Windows 身份验证模式（Windows 身份验证）**  
使用 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 凭据连接到报表服务器实例。  
  
**基本身份验证**  
如果将 Reporting Services 安装配置为使用基本身份验证，则使用“基本身份验证”进行连接。  
  
**窗体身份验证**  
如果将 Reporting Services 安装配置为使用自定义身份验证扩展插件，则使用“窗体身份验证”进行连接。  
  
**用户名**  
输入用于连接的登录名。 只有在选择了 **“基本身份验证”** 或 **“窗体身份验证”**时，此选项才可用。  
  
**密码**  
输入用户名的密码。 只有在选择了 **“基本身份验证”** 或 **“窗体身份验证”**时，此选项才可编辑。  
  
**记住密码**  
存储已经输入的密码。 仅当单击“选项”时才显示此选项，而且仅当选择了使用“基本身份验证”或“窗体身份验证”进行连接时，它才是可编辑的。  
  
**连接**  
连接到所选服务器。  
  
**选项**  
显示其他服务器连接选项，例如记住密码。  
  
## <a name="see-also"></a>另请参阅  
[配置报表服务器连接](http://msdn.microsoft.com/en-us/9759a9fb-35e9-4215-969b-a9f1fea18487)  
[如何注册和连接报表服务器](http://msdn.microsoft.com/en-us/c875ff87-ee7d-443a-a702-bdb4b6c27c6e)  
[在 Reporting Services 中配置身份验证](http://msdn.microsoft.com/en-us/753c2542-0e97-4d8f-a5dd-4b07a5cd10ab)  
  

