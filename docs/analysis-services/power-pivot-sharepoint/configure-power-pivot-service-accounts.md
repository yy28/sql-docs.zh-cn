---
title: 配置 Power Pivot 服务帐户 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54dc66e30356f3896d7ce509bf83e56a1973c5b2
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984839"
---
# <a name="configure-power-pivot-service-accounts"></a>配置 Power Pivot 服务帐户
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]安装包括支持服务器操作的两个服务。 **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])** 服务是一种 Windows 服务，它提供应用程序服务器上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据处理和查询支持。 当您在 SharePoint 集成模式下安装 Analysis Services 时，在 SQL Server 安装期间始终为此服务指定登录帐户。  
  
 必须为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序指定第二个帐户，这是在 SharePoint 场中基于应用程序池标识运行的共享 Web 服务。 在你使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]配置工具或 PowerShell 配置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 安装时指定此帐户。  
  
 每个服务都应该在专用帐户下运行，以便您可以在场中审核连接或启用 Kerberos 身份验证协议。  
  
 一旦设置好服务帐户后，对上述帐户的任何更改都必须通过 SharePoint 管理中心进行。 如果您使用替代工具（例如“服务”控制台应用程序、IIS 管理器或 SQL Server 配置管理器），则对于场中的数据库访问或者对于物理服务器上的本地文件访问，将不会更新权限。  
  
 本主题包含以下各节：  
  
 [更新 SQL Server Analysis Services (Power Pivot) 实例的过期密码](#bkmk_passwordssas)  
  
 [更新 Power Pivot 服务应用程序的过期密码](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md#bkmk_passwordapp)  
  
 [更改运行每个服务所基于的帐户](#bkmk_newacct)  
  
 [创建或更改 Power Pivot 服务应用程序的应用程序池](#bkmk_appPool)  
  
 [帐户要求和权限](#requirements)  
  
 [故障排除：手动授予管理权限](#updatemanually)  
  
 [故障排除：解决由于管理中心或 SharePoint Foundation Web 应用程序服务密码过期而导致的 HTTP 503 错误](#expired)  
  
##  <a name="bkmk_passwordssas"></a> 更新 SQL Server Analysis Services (Power Pivot) 实例的过期密码  
  
1.  指向“开始”，单击 **“管理工具”**，再单击 **“服务”**。 双击 **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**。 单击 **“登录”**，然后为该帐户输入新密码。  
  
2.  在“管理中心”的“安全性”部分中，单击 **“配置托管帐户”**。  
  
3.  单击 **“编辑”** 更改特定帐户。  
  
4.  选择 **“立即更改密码”**。  
  
5.  选择 **“将帐户密码设置为新值”**。 在该托管帐户下运行的所有服务都将使用更新后的凭据。  
  
##  <a name="bkmk_passwordapp"></a> 更新 Power Pivot 服务应用程序的过期密码  
  
1.  在“管理中心”的“安全性”部分中，单击 **“配置托管帐户”**。  
  
2.  单击 **“编辑”** 更改特定帐户。  
  
3.  选择 **“立即更改密码”**。  
  
4.  选择 **“将帐户密码设置为新值”**。 在该托管帐户下运行的所有服务都将使用更新后的凭据。  
  
##  <a name="bkmk_newacct"></a> 更改运行每个服务所基于的帐户  
  
1.  在“管理中心”的“安全性”部分中，单击 **“配置服务帐户”**。  
  
2.  选择“Windows 服务 - SQL Server Analysis Services”以更改 Analysis Services 服务帐户。  
  
3.  在 **“为此服务选择帐户”** 中，选择某个现有托管帐户或创建一个新帐户。 该帐户必须是域用户帐户。  
  
4.  选择“服务应用程序池 - SharePoint Web 服务系统”以更改默认 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序的应用程序池标识。 根据配置您的安装的方式，可基于为 SharePoint 服务创建的现有服务应用程序池运行服务。 默认情况下，[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具将该服务注册为“默认 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序（[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序）”。  
  
     如果 SharePoint 管理员已手动配置该服务，则该服务最有可能具有自己的服务应用程序池。  
  
5.  在 **“为此服务选择帐户”** 中，选择某个现有托管帐户或创建一个新帐户。 该帐户必须是域用户帐户。  
  
6.  单击“确定” 。  
  
##  <a name="bkmk_appPool"></a> 创建或更改 Power Pivot 服务应用程序的应用程序池  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  选择但不要单击 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。 单击应用程序名称将打开 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理面板，其中未提供指向指定应用程序池的属性页的链接。  可以单击行中的空白区域或单击类型名称以选择 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。  
  
3.  在功能区上单击 **“属性”** 。  
  
4.  选择 **“创建新应用程序池”**。 为应用程序池提供名称并为其标识指定托管帐户。  
  
##  <a name="requirements"></a> 帐户要求和权限  
 在规划 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署时，必须规划以下服务帐户。  
  
-   Analysis Services 服务帐户。 Analysis Services 处理场中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查询和数据刷新作业。 安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 时，在 SQL Server 安装期间始终指定该帐户。  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序池。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务相关联，它为场中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查询处理提供 SharePoint 集成和基础结构。 你为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序指定的应用程序池是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务的服务标识。 在一个场中可有多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。 所创建的每个应用程序都应在自己的应用程序池中运行。  
  
#### <a name="analysis-services-service-account"></a>Analysis Services 服务帐户  
  
|要求|Description|  
|-----------------|-----------------|  
|设置要求|在 SQL Server 安装程序使用安装向导中的“Analysis Services – 配置”页（或在命令行安装程序中使用 **ASSVCACCOUNT** 安装参数）的过程中，必须指定该帐户。<br /><br /> 你可以使用管理中心、PowerShell 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具修改用户名或密码。 不支持使用其他工具更改帐户和密码。|  
|域用户帐户要求|此帐户必须是 Windows 域用户帐户。 禁止使用内置计算机帐户（如 Network Service 或 Local Service）。 SQL Server 安装程序通过在指定计算机帐户时就阻止安装来强制执行域用户帐户要求。|  
|权限要求|此帐户必须隶属 SQLServerMSASUser$\<服务器 > $PowerPivot 安全组和本地计算机上的 WSS_WPG 安全组。 应自动授予这些权限。 有关如何检查或授予权限的详细信息，请参阅本主题中的[手动授予 PowerPivot 服务帐户管理权限](#updatemanually)和[初始配置 (Power Pivot for SharePoint)](http://msdn.microsoft.com/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)。|  
|扩展要求|如果你在场中安装多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 服务器实例，则所有 Analysis Services 服务器实例都必须在同一域用户帐户下运行。 例如，如果你将第一个 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 实例配置为以 Contoso\ssas-srv01 身份运行，则随后在同一场中部署的所有其他 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 实例也必须以 Contoso\ssas-srv01（或碰巧为当前帐户）身份运行。<br /><br /> 如果将所有服务实例配置为在同一帐户下运行，则 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务可以将查询处理或数据刷新作业分配到场中的任何 Analysis Services 服务实例。 此外，它还可将管理中心的“托管帐户”功能用于 Analysis Services 服务器实例。 通过对所有 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 实例使用同一帐户，您可以只更改帐户或密码一次，而所有使用这些凭据的服务实例都会自动更新。<br /><br /> SQL Server 安装程序强制执行使用同一帐户的要求。 在 SharePoint 场已安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 实例的扩展部署中，如果你指定的 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 帐户与场中已使用的帐户不同，安装程序将阻止执行新的安装。|  
  
#### <a name="power-pivot-service-application-pool"></a>Power Pivot 服务应用程序池  
  
|要求|Description|  
|-----------------|-----------------|  
|设置要求|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务是服务器场中的共享资源，在你创建服务应用程序时变得可用。 在创建服务应用程序时，必须指定服务应用程序池。 可以通过两种方式指定应用程序池：使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具或通过 PowerShell 命令。<br /><br /> 您可能已配置了应用程序池标识以便基于唯一帐户运行。 但是，如果您没有这样做，请考虑立即将其更改为基于不同的帐户运行。|  
|域用户帐户要求|应用程序池标识必须是 Windows 域用户帐户。 禁止使用内置计算机帐户（如 Network Service 或 Local Service）。|  
|权限要求|此帐户不需要计算机上的本地系统管理员权限。 但是，该帐户对安装在同一计算机上的本地 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 必须具有 Analysis Services 系统管理员权限。 将由 SQL Server 安装程序或当您在管理中心中设置或更改应用程序池标识时自动授予这些权限。<br /><br /> 管理权限是用于将查询转发到 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]所必需的。 在监视运行状况、关闭处于非活动状态的会话和侦听跟踪事件时也需要这些权限。<br /><br /> 该帐户必须对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库具有连接、读取和写入权限。 在创建应用程序时将自动授予这些权限，并且在管理中心中更改权限和密码时将自动更新这些权限。<br /><br /> 在检索文件前 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序将检查 SharePoint 用户是否被授权查看数据，但它不模拟用户。 没有针对模拟的权限要求。|  
|扩展要求|无。|  
  
##  <a name="updatemanually"></a> 故障排除：手动授予管理权限  
 如果更新凭据的人不是计算机上的本地管理员，则管理权限更新将会失败。 如果出现此情况，您可以手动授予管理权限。 为此，最简单的方法是在管理中心运行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置计时器作业。 使用此方法，可以重置场中所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器的权限。 请注意，仅当同时以场管理员身份和计算机上的本地管理员身份运行 SharePoint 计时器作业时，此方法才有效。  
  
1.  在“监视”中，单击 **“查看作业定义”**。  
  
2.  选择“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置计时器作业”。  
  
3.  单击 **“立即运行”**。  
  
 作为最后的手段，您可以通过授予对 Analysis Services 系统管理权限来确保正确的权限[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务应用程序，以及然后明确将服务应用程序标识添加到 SQLServerMSASUser$\<服务器名 > $PowerPivot Windows 安全组。 必须对与 SharePoint 场集成的每个 Analysis Services 实例重复这些步骤。  
  
 您必须是本地管理员才能更新 Windows 安全组。  
  
1.  在 SQL Server Management Studio，连接到 Analysis Services 实例作为\<服务器名称 > \POWERPIVOT。  
  
2.  右键单击服务器名称并选择“属性”。  
  
3.  单击 **“安全性”**。  
  
4.  单击 **“添加”**。  
  
5.  键入用于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序池的帐户名称，然后单击“确定” 。  
  
6.  在“管理工具”中，单击 **“计算机管理”**。  
  
7.  打开 **“本地用户和组”**。  
  
8.  打开 **“组”**。  
  
9. 双击 SQLServerMSASUser$\<服务器名 > $PowerPivot。  
  
10. 单击 **“添加”**。  
  
11. 键入用于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序池的帐户名称，然后单击“确定” 。  
  
##  <a name="expired"></a> 故障排除：解决由于管理中心或 SharePoint Foundation Web 应用程序服务密码过期而导致的 HTTP 503 错误  
 如果管理中心服务或 SharePoint Foundation Web 应用程序服务由于帐户重置或密码过期而停止工作，您在尝试打开 SharePoint 管理中心或 SharePoint 站点时将遇到 HTTP 503“服务不可用”错误消息。 按以下步骤操作可将服务器恢复联机状态。 一旦管理中心可用，您就可以继续更新过期帐户信息。  
  
1.  在“管理工具”中，单击 **“Internet Information Services 管理器”**。  
  
2.  针对属于具有过期密码的域用户帐户的站点或管理中心应用程序池标识，执行以下操作：  
  
    1.  右键单击应用程序池名称并选择“高级设置”。  
  
    2.  选择“标识”  ，然后单击 ... 按钮打开“应用程序池标识”对话框。  
  
    3.  单击 **“设置”**。  
  
    4.  键入用户名和密码。  
  
3.  运行 IISRESET。 为此，请以管理员身份打开命令提示符，键入 **iisreset** 命令。  
  
4.  在 SharePoint 管理中心的“安全性”部分中，选择 **“配置托管帐户”**。  
  
5.  单击 **“编辑”** 以更新具有过期密码的托管帐户的信息。  
  
6.  选择 **“立即更改密码”**。  
  
7.  单击 **“使用现有密码”**。  
  
8.  键入密码，然后单击 **“确定”**。  
  
 如果安装了 Reporting Services，可以使用 Reporting Services 配置管理器来更新报表服务器的密码和与报表服务器数据库的连接。 有关详细信息，请参阅[配置和管理报表服务器（Reporting Services SharePoint 模式）](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)。  
  
## <a name="see-also"></a>请参阅  
 [启动或停止 Power Pivot for SharePoint Server](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)   
 [配置 Power Pivot 无人参与的数据刷新帐户 (Power Pivot for SharePoint)](http://msdn.microsoft.com/81401eac-c619-4fad-ad3e-599e7a6f8493)  
  
  
