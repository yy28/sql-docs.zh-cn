---
title: 配置报表服务器服务帐户（SSRS 配置管理器）| Microsoft Docs
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: ''
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/10/2018
ms.openlocfilehash: cb867bfdfc8d9ecb686d3ecc52c48c80bc60d9cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63261073"
---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>配置报表服务器服务帐户（SSRS 配置管理器）

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 是作为单个服务实现的，其中包含报表服务器 Web 服务、报表管理器以及用于计划的报告处理和订阅传递的后台处理应用程序。 本主题说明最初如何配置服务帐户以及如何使用 Reporting Services 配置工具修改帐户或密码。  
  
## <a name="initial-configuration"></a>初始配置

 报表服务器服务帐户是在安装过程中定义的。 可以在域用户帐户或内置帐户（如 `NetworkService` 帐户）下运行服务。 没有默认帐户;在中指定所用的帐户[服务器配置-服务帐户](../../sql-server/install/server-configuration-service-accounts.md)安装向导页将成为报表服务器服务的初始帐户。  
  
> [!IMPORTANT]
> 尽管报表服务器 Web 服务和报表管理器均为 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序，但它们不在 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帐户下运行。 由单个服务体系结构在同一个报表服务器进程标识下运行这两个 ASP.NET 应用程序。 与先前版本相比，这是一个重大的更改，在先前版本中，报表服务器 Web 服务和报表管理器均在 IIS 中指定的 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 辅助进程标识下运行。
  
## <a name="changing-the-service-account"></a>更改服务帐户

 若要查看和重新配置服务帐户信息，请始终使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具。 服务标识信息在内部存储在多个位置上。 使用该工具可确保在更改帐户或密码的同时相应地更新所有引用。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具将执行以下附加步骤以确保报表服务器仍然可用：  
  
- 自动将新帐户添加到本地计算机上创建的报表服务器组中。 此组是在用于保护 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的访问控制列表 (ACL) 中指定的。  
  
- 自动更新用于承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的登录权限。 新帐户将添加到 **RSExecRole**。  
  
     旧帐户的数据库登录名不会被自动删除。 请务必删除不再使用的帐户。 有关详细信息，请参阅 SQL Server 联机丛书中的[管理报表服务器数据库（SSRS 本机模式）](../report-server/report-server-database-ssrs-native-mode.md)。  
  
     只有在首先将报表服务器数据库连接配置为使用新服务帐户的情况下，才需要将数据库权限授予该服务帐户。 如果将报表服务器数据库连接配置为使用域用户帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库登录名，连接信息将不受服务帐户更新的影响。  
  
- 自动更新加密密钥，以包括新帐户的配置文件信息。  
  
    > [!NOTE]  
    > 如果报表服务器是扩展部署的一部分，则只有正在更新的报表服务器会受到影响。 该部署中的其他报表服务器的加密密钥不会受到服务帐户更改的影响。  
  
 有关如何设置帐户的说明，请参阅[配置服务帐户&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)。  
  
## <a name="choosing-an-account"></a>选择帐户

 可以将报表服务器服务配置为在以下任何帐户类型下运行：  
  
- 具有最小权限的 Windows 用户帐户  
  
- NetworkService  
  
- LocalSystem  
  
- LocalService  
  
 没有用来选择帐户类型的唯一最佳方法。 每个帐户都有优点和缺点，选择时必须予以考虑。 如果在生产服务器上部署 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，则最好将服务配置为在域用户帐户下运行，以避免共享帐户遭恶意用户破坏后造成大范围的损害。 这样做还能更轻松地审核该帐户的登录活动。 使用 Windows 用户帐户的折中方案为：如果在使用 Kerberos 身份验证的网络中部署 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，则必须用该用户帐户来注册服务。 有关详细信息，请参阅[为报表服务器注册服务主体名称 (SPN)](../report-server/register-a-service-principal-name-spn-for-a-report-server.md)。  
  
 本部分中的下列指南和链接可以帮助您确定部署的最佳方法。  
  
- [服务帐户&#40;SSRS 本机模式&#41;](../../sql-server/install/service-account-ssrs-native-mode.md)。  
  
- SQL Server 联机丛书中的[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 。  
  
- [服务和服务帐户安全计划指南](http://usergroup.doubletake.com/file_cabinet/download/0x000021733)。  
  
## <a name="updating-an-expired-password"></a>更新过期密码

 如果报表服务器服务在域帐户下运行，并且密码还未在 Reporting Services 配置工具中更新就已过期，则指定新密码之前，该服务将无法启动。 如果服务无法启动，则不能使用 Reporting Services 配置工具连接到该服务器以更新帐户。 在这种情况下，必须使用多种工具来使服务器恢复联机状态。  
  
 若要重置密码，请执行下列操作：  
  
1. 上**启动**菜单，依次指向**控制面板**，指向**管理工具**，然后单击**服务**。  
  
2. 右键单击**SQL Server Reporting Services**，选择**属性**。  
  
3. 单击**Log On**，然后键入新密码。  
  
4. 更新密码后，启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具并在“服务帐户”页中更新密码。 若要更新由报表服务器存储在内部的帐户信息，必须执行此附加步骤。  
  
 如果[!INCLUDE[ssDE](../../includes/ssde-md.md)]的服务帐户密码已过期，则尝试连接到报表服务器时，将出现 `rsReportServerDatabaseUnavailable` 错误。 重置密码可以解决此错误。  
  
## <a name="configuring-the-report-server-service-for-a-sharepoint-integrated-report-server"></a>为 SharePoint 集成报表服务器配置报表服务器服务

 如果在 SharePoint 集成模式下运行报表服务器，且符合下列条件之一，则必须更新存储在 SharePoint 配置数据库中的服务帐户信息。  
  
- 修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务帐户（例如，从 NetworkService 帐户切换到域用户帐户）。  
  
- 扩展 SharePoint 场以包含其他 SharePoint Web 应用程序。 如果服务器场是针对报表服务器集成配置的，且配置的用于运行新添加的应用程序的用户帐户与用于运行该场中其他应用程序的用户帐户不同，则必须更新数据库访问信息。  
  
 重置数据库访问信息后，应当重新启动 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 服务以确保不再使用旧连接。  
  
1. 在中**管理工具**，单击**SharePoint 2010 管理中心**。  
  
2. 单击**应用程序管理**。  
  
3. 在 Reporting Services 部分中，单击**授予数据库访问权限**。  
  
4. 单击“确定”  。 将出现“输入凭据”对话框。  
  
5. 输入用户凭据，该用户必须是报表服务器所在的计算机上本地管理员组的成员。 这些凭据将用于一次性连接到报表服务器计算机以便检索服务帐户信息。 在 SharePoint 数据库中将对为每个服务帐户创建的数据库登录名进行更新。  
  
6. 若要重新启动服务，请单击**操作**。  
  
7. 在拓扑和服务中，单击**服务器上的服务**。  
  
8. Windows SharePoint Services Web 应用程序，请单击**停止**。  
  
9. 等待服务停止。  
  
10. 单击**启动**。  
  
> [!NOTE]  
> SharePoint 产品和技术需要域帐户来完成服务配置，如报表服务 SharePoint 模式。  
  
## <a name="next-steps"></a>后续步骤

 [配置服务帐户&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md) [服务帐户&#40;SSRS 本机模式&#41;](../../sql-server/install/service-account-ssrs-native-mode.md) [配置报表服务器 Url &#40;SSRS 配置管理器&#41;](configure-report-server-urls-ssrs-configuration-manager.md) [Reporting Services 配置管理器&#40;本机模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)
