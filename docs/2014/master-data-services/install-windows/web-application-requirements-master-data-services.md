---
title: Web 应用程序要求 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 15b394c836cb24229944f4e0775dfccad847a32b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482886"
---
# <a name="web-application-requirements-master-data-services"></a>Web 应用程序要求 (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 是 Internet Information Services (IIS) 托管的 Web 应用程序。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 仅适用于 Internet Explorer (IE) 7 或更高版本。 IE 7 及早期版本、Microsoft Edge 和 Chrome 均不受支持。  
  
 使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 可以创建和配置 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序。 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 在本地计算机上配置 IIS，因此适用于初始 Web 配置任务。 例如，配置具有单个 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 应用程序的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 环境，或在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]的扩展部署中配置第一个 Web 应用程序。 使用 IIS 工具来执行一些更复杂的任务，如在扩展部署中配置多个 Web 服务器。  
  
> [!NOTE]  
>  您安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 组件的任何计算机必须具有许可证。 有关详细信息，请参阅“最终用户许可协议 (EULA)”。  
  
## <a name="requirements"></a>要求  
  
### <a name="operating-system"></a>操作系统  
 下面的 Windows 操作系包括 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 应用程序和 Web 服务所需的 Internet Information Services (IIS) 功能。  
  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer（64 位）x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise（64 位）x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence（64 位）x64|  
|-------------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows 7 Professional、Enterprise 和 Ultimate<br /><br /> Windows 8.0 Professional、Enterprise 和 Ultimate|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|  
  
 有关支持的版本的 Windows 操作系统的完整列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[硬件和软件要求安装 SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 在使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序时，Silverlight 5 必须安装在客户端计算机上。 如果您不具有所需版本的 Silverlight，则在您导航到需要 Silverlight 的 Web 应用程序区域时，系统将提示您安装 Silverlight。 您可以从 [此处](https://go.microsoft.com/fwlink/?LinkId=243096)安装 Silverlight 5。  
  
### <a name="role-and-role-services-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>角色和角色服务（Windows Server 2008 或 Windows Server 2008 R2、Windows 7 操作系统）  
 在 Windows Server 2008 R2 中，可以使用 **“服务器管理器”** （在 Microsoft 管理控制台 (MMC) 中提供）来安装 **“Web 服务器(IIS)”** 角色和以下必需的角色服务。  
  
> [!NOTE]  
>  在 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 和 Windows 7 操作系统中，使用控制面板中的 **“程序和功能”** 启用 **“Windows 功能”** 对话框中的这些选项。  
  
||  
|-|  
|Web 服务器<br /><br /> 常见的 HTTP 功能<br /><br /> 静态内容<br /><br /> 默认文档<br /><br /> 目录浏览<br /><br /> HTTP 错误<br /><br /> 应用程序开发<br /><br /> ASP.NET<br /><br /> .NET 可扩展性<br /><br /> ISAPI 扩展插件<br /><br /> ISAPI 筛选器<br /><br /> 运行状况和诊断<br /><br /> HTTP 日志记录<br /><br /> 请求监视器<br /><br /> 安全性<br /><br /> Windows 身份验证<br /><br /> 请求筛选<br /><br /> 性能<br /><br /> 静态内容压缩<br /><br /> 管理工具<br /><br /> IIS 管理控制台|  
  
### <a name="role-and-role-services-windows-server-2012-or-windows-8-operating-systems"></a>角色和角色服务 （Windows Server 2012 或 Windows 8 操作系统）  
 在 Windows Server 2012 中，可以使用 **“服务器管理器”** （在 Microsoft 管理控制台 (MMC) 中提供）来安装 **“Web 服务器(IIS)”** 角色和以下必需的角色服务。  
  
> [!NOTE]  
>  在 Windows 8 操作系统中，使用控制面板中的 **“程序和功能”** 启用 **“Windows 功能”** 对话框中的这些选项。  
  
||  
|-|  
|Internet Information Services<br /><br /> Web 管理工具<br /><br /> IIS 管理控制台<br /><br /> 万维网服务<br /><br /> 应用程序开发<br /><br /> .NET Extensibility 3.5<br /><br /> .NET Extensibility 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> ISAPI 扩展插件<br /><br /> ISAPI 筛选器<br /><br /> 常见的 HTTP 功能<br /><br /> 默认文档<br /><br /> 目录浏览<br /><br /> HTTP 错误<br /><br /> 静态内容<br /><br /> [注意：请不要安装 WebDAV 发布]<br /><br /> 运行状况和诊断<br /><br /> HTTP 日志记录<br /><br /> 请求监视器<br /><br /> 性能<br /><br /> 静态内容压缩<br /><br /> 安全性<br /><br /> 请求筛选<br /><br /> Windows 身份验证|  
  
### <a name="features-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>功能（Windows Server 2008 或 Windows Server 2008 R2、Windows 7 操作系统）  
 在 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 或 Windows Server 2008 R2 中，可以使用 **“服务器管理器”** 来安装以下必需的功能。  
  
> [!NOTE]  
>  在 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 和 Windows 7 操作系统中，使用控制面板中的 **“程序和功能”** 启用 **“Windows 功能”** 对话框中的这些选项。  
  
||  
|-|  
|.NET Framework 3.0 功能<br /><br /> WCF 激活<br /><br /> HTTP 激活<br /><br /> 非 HTTP 激活<br /><br /> Windows 进程激活服务<br /><br /> 进程模型<br /><br /> .NET 环境<br /><br /> 配置 API|  
  
### <a name="features-windows-server-2012-or-windows-8-operating-systems"></a>功能 （Windows Server 2012 或 Windows 8 操作系统）  
 在 Windows Server 2012 中，可以使用 **“服务器管理器”** 来安装以下必需的功能。  
  
> [!NOTE]  
>  在 Windows 8 操作系统中，使用控制面板中的 **“程序和功能”** 启用 **“Windows 功能”** 对话框中的这些选项。  
  
||  
|-|  
|.NET Framework 3.5（包括 .NET 2.0 和 3.0）<br /><br /> .NET Framework 4.5 高级服务<br /><br /> ASP.NET 4.5<br /><br /> WCF Services<br /><br /> HTTP 激活［注意：这是必需。]<br /><br /> TCP 端口共享<br /><br /> Windows 进程激活服务<br /><br /> 进程模型<br /><br /> .NET 环境<br /><br /> 配置 API|  
  
### <a name="accounts-and-permissions"></a>帐户和权限  
  
|类型|Description|  
|----------|-----------------|  
|Windows 帐户|您必须使用有权配置 Windows 角色、角色服务和功能以及有权在本地计算机上的 IIS 中创建和管理应用程序池、网站和 Web 应用程序的 Windows 帐户登录到 Web 服务器计算机。|  
|服务帐户|当您在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中创建 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]Web 应用程序时，必须为应用程序运行所在的应用程序池指定标识。 此帐户可不同于在创建 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库时指定的服务帐户。<br /><br /> 此标识必须是域用户帐户，并且添加到 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库中的 mds_exec 数据库角色以便用于数据库访问。 有关详细信息，请参阅[数据库登录、用户和角色 (Master Data Services)](../database-logins-users-and-roles-master-data-services.md)。 此帐户还添加到 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Windows 组 **MDS_ServiceAccounts**，该组有权访问文件系统中的临时编译目录 **MDSTempDir**。 有关详细信息，请参阅[文件夹和文件权限 (Master Data Services)](../folder-and-file-permissions-master-data-services.md)。<br /><br /> 应用程序池帐户需要 VIEW SERVER STATE 权限来避免服务器错误。 例如，“MDS 验证版本”命令因服务器错误而失败。 有关详细信息，请参阅 [MDS 验证版本命令因 SQL Server 2012 和 SQL Server 2014 服务器错误而失败](https://go.microsoft.com/fwlink/p/?LinkId=526304)|  
  
## <a name="see-also"></a>请参阅  
 [安装 Master Data Services](install-master-data-services.md)   
 [创建主数据管理器 Web 应用程序 (Master Data Services)](create-a-master-data-manager-web-application-master-data-services.md)   
 [“Web 配置”页（Master Data Services 配置管理器）](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  
