---
title: 配置报表生成器访问权限 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, Report Builder
- Report Builder 1.0, configuring access
- configuring servers [Reporting Services]
ms.assetid: a79003d0-c905-4d4c-9560-93a7cc1e1dd4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: be19f42fa5e8a154d8f29e359b6a52395c6504d8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104031"
---
# <a name="configure-report-builder-access"></a>配置报表生成器访问权限
  报表生成器是一个特别报告生成工具，该工具随为本机模式或 SharePoint 集成模式配置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器一起安装。  
  
 报表生成器的访问权限取决于以下因素：  
  
-   服务器属性，确定报表生成器是否可以在报表服务器上使用。  
  
-   角色分配或权限，它们使报表生成器可用于单个用户或组。  
  
-   身份验证设置，用于确定用户凭据是否可以传递到报表服务器或者是否对应用程序文件配置匿名访问权。  
  
 若要使用报表生成器，必须有已发布的报表模型可供使用。  
  
## <a name="prerequisites"></a>先决条件  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均不提供报表生成器。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅 SQL Server 2014 的各个[版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 客户端计算机必须[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]安装了2.0。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 提供运行 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 应用程序的基础结构。  
  
 必须使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 6.0 或更高版本。  
  
 报表生成器始终在完全信任模式下运行；不能将其配置为在部分信任模式下运行。 在以前的版本中，可以在部分信任模式下运行报表生成器，但是 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中不支持该选项。  
  
## <a name="enabling-and-disabling-report-builder"></a>启用和禁用报表生成器  
 默认情况下，将启用报表生成器。 报表服务器管理员可以通过将报表服务器系统属性 `EnableReportDesignClientDownload` 设置为 `false`，以禁用报表生成器功能。 设置此属性将会禁用该报表服务器的报表生成器下载功能。  
  
 若要设置报表服务器系统属性，可以使用 Management Studio 或脚本：  
  
-   若要使用 Management Studio，请连接到报表服务器并使用“高级服务器属性”页将 `EnableReportDesignClientDownload` 设置为 `false`。 有关如何打开该页面的详细信息，请参阅[设置报表服务器属性 (Management Studio)](../tools/set-report-server-properties-management-studio.md)。  
  
-   若要查看设置报表服务器属性的示例脚本，请参阅 [为部署和管理任务编写脚本](../tools/script-deployment-and-administrative-tasks.md)。  
  
## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>在本机模式报表服务器上授予报表生成器访问权的角色分配  
 在本机模式报表服务器上，创建包括使用报表生成器的任务的用户角色分配。 您必须是内容管理员和系统管理员，才能在项级和站点级创建或修改角色定义和角色分配。  
  
 以下说明假定您使用的是预定义角色。 如果您修改了角色定义或者从 SQL Server 2000 进行了升级，则对角色进行检查以验证其是否包含必需的任务。 有关创建角色分配的详细信息，请参阅[授予用户对报表服务器的访问权限（报表管理器）](../security/grant-user-access-to-a-report-server.md)。  
  
 创建角色分配之后，用户将拥有执行以下操作的权限：  
  
-   分配给系统用户角色和浏览者角色的用户可以在报表服务器上查看已发布的报表生成器报表，而不必启动报表生成器。  
  
-   分配给系统用户角色和报表生成者角色的用户可以生成模型，启动报表生成器和创建报表，以及将报表保存到报表服务器。  
  
-   分配给系统用户角色和发布者角色的用户可以将模型从模型设计器发布到报表服务器。 模型用作报表生成器中的数据源。  
  
-   分配给系统管理员角色和内容管理员角色的用户拥有创建、查看和管理报表生成器报表的完全权限。  
  
#### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>验证必需的任务是否在角色定义中  
  
1.  启动 Management Studio 并连接到报表服务器。  
  
2.  打开 **“安全性”** 文件夹。  
  
3.  打开 **“系统角色”** 文件夹。  
  
4.  右键单击“系统管理员”，然后选择“属性”********。  
  
5.  选择 **“执行报表定义”** ，然后单击 **“确定”**。  
  
6.  右键单击“系统用户”，然后选择“属性”********。  
  
7.  选择 **“执行报表定义”** ，然后单击 **“确定”**。  
  
8.  打开 **“角色”** 文件夹。  
  
9. 右键单击“浏览器”，然后选择“属性”********。  
  
10. 选择 **“查看模型”** ，然后单击 **“确定”**。  
  
11. 右键单击“内容管理器”，然后选择“属性”********。  
  
12. 依次选择 **“查看模型”**， **“管理模型”**， **“使用报表”**，然后单击 **“确定”**。  
  
13. 右键单击“发布服务器”，然后选择“属性”********。  
  
14. 选择 **“管理模型”** ，然后单击 **“确定”**。  
  
15. 如果报表生成者角色不存在，则创建该角色：  
  
    1.  打开 **“安全性”** 文件夹。  
  
    2.  右键单击“角色”选择“新建角色”********。  
  
    3.  在“名称”中，键入 **报表生成者**。  
  
    4.  在“说明”中，输入角色说明，以使报表管理器中的用户了解该角色的作用。  
  
    5.  添加下列任务： **“使用报表”**、 **“查看报表”**、 **“查看模型”**、 **“查看资源”**、 **“查看文件夹”** 和 **“管理单独的订阅”**。  
  
    6.  单击 **"确定"** 以保存角色。  
  
#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>创建授予对报表生成器的访问权的角色分配  
  
1.  启动报表管理器。  
  
2.  单击 **“网站设置”** 。  
  
3.  单击 **“安全性”** 。  
  
4.  如果要为其配置报表生成器访问权的用户或组已经分配有角色，则单击 **“编辑”** 。  
  
     否则，单击 **“新建角色分配”** 。 在“组或用户”中，按如下格式输入一个 Windows 域用户或组帐户：\<domain>\\<account\>。 如果使用窗体身份验证或自定义安全性，则以适用于您的部署的格式指定该用户帐户或组帐户。  
  
5.  选择 **“系统用户”** ，然后单击 **“确定”** 。  
  
6.  单击 **“主页”** 。  
  
7.  单击 **“文件夹设置”** 选项卡。  
  
8.  单击“安全”选项卡。   
  
9. 如果要为其配置报表生成器访问权的用户或组已经分配有角色，则单击 **“编辑”** 。  
  
     否则，单击 **“新建角色分配”** 。 在“组或用户”中，按如下格式输入一个 Windows 域用户或组帐户：\<domain>\\<account\>。 如果使用窗体身份验证或自定义安全性，则以适用于您的部署的格式指定该用户帐户或组帐户。  
  
10. 选择 **“报表生成者”** ，然后单击 **“应用”** 。  
  
11. 重复这些步骤以便为其他用户或组创建或修改角色分配。  
  
## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>授予 SharePoint 集成模式报表服务器上的报表生成器访问权的权限  
 在 SharePoint 集成模式报表服务器上，将报表生成器访问权授予具有“参与讨论”或“完全控制”权限级别的 SharePoint 用户。  
  
 如果使用自定义权限级别，则必须在权限级别包括“添加项”和“编辑项”。 有关通过内置权限级别访问报表生成器的详细信息，请参阅 [将 Windows SharePoint Services 中的内置安全性用于报表服务器项](../security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)。 有关自定义权限级别的权限要求的详细信息，请参阅 [在 SharePoint Web 应用程序中设置报表服务器操作的权限](../security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)。  
  
## <a name="authentication-considerations-and-credential-reuse"></a>身份验证注意事项和凭据重用  
 报表生成器使用 ClickOnce 技术下载其应用程序文件，并在客户端计算机上安装这些文件。 ClickOnce 技术专用于单向应用程序部署，即将程序文件存放在客户端计算机上，然后使用默认用户的标识以单独进程的形式运行应用程序。 由于报表生成器必须再连接回报表服务器以获取应用程序文件和报表服务器数据，因此了解 ClickOnce 如何设置安全上下文以及在不同情况下向远程计算机发出请求非常重要：  
  
-   ClickOnce 在客户端计算机上始终以单独进程的形式运行。 进程标识为默认 Windows 用户凭据。 ClickOnce 不与 Internet Explorer 共享会话数据或从 Internet Explorer 获取当前用户的安全上下文。  
  
-   ClickOnce 发送在身份验证标头中指定 Windows 集成安全性的请求。 如果将服务器配置为使用另一种身份验证类型，则该服务器从 ClickOnce 的请求将失败，同时出现身份验证错误。 若要解决此问题，必须将服务器配置为使用 Windows 集成安全性，或者必须启用匿名访问来排除身份验证检查。  
  
-   报表生成器将打开其自己的与报表服务器的连接。 如果您未将 Windows 集成安全性用于单一登录，则用户必须为报表生成器与报表服务器的连接重新键入其凭据。  
  
 下表描述报表服务器支持的身份验证类型，以及访问报表生成器是否需要附加配置。  
  
|报表服务器身份验证类型|报表生成器和 ClickOnce 应用程序启动程序如何响应|  
|---------------------------------------|--------------------------------------------------------------------|  
|协商（默认值）<br /><br /> NTLM（默认值）|使用 Windows 集成安全性，发自 ClickOnce 和报表生成器的经过身份验证的请求在以下情况下通常会成功：将客户端和服务器部署在同一个域中，用户使用具有报表生成器访问权的域帐户登录到客户端计算机，并且将报表服务器配置为使用 Windows 身份验证。<br /><br /> 请求成功的原因在于 ClickOnce 和浏览器与报表服务器的连接具有相同的用户标识。<br /><br /> 如果用户通过“运行身份”和指定的非默认凭据打开 Internet Explorer，则请求将失败。 如果报表服务器上的用户会话是使用特定的帐户建立的，并且 ClickOnce 在其他帐户下运行，则该报表服务器将拒绝对文件的访问。|  
|Kerberos|使用报表生成器时必需的 Internet Explorer 不直接支持 Kerberos。|  
|基本身份验证|ClickOnce 不支持基本身份验证。 它不会表述在身份验证标头中指定基本身份验证的请求。 它不会传递凭据或提示用户提供凭据。 可以通过启用对报表生成器应用程序文件的匿名访问来解决这些问题。<br /><br /> 由于报表服务器会忽略身份验证标头，如果启用对报表生成器应用程序文件的匿名访问，则请求将成功。 有关如何启用对报表生成器的匿名访问的详细信息，请参阅 [在报表服务器上配置基本身份验证](../security/configure-basic-authentication-on-the-report-server.md)。<br /><br /> ClickOnce 检索应用程序文件后，报表生成器将打开与报表服务器的单独连接。 用户必须重新键入其凭据以使报表生成器连接到报表服务器。 报表生成器不会从 Internet Explorer 或 ClickOnce 收集凭据。<br /><br /> 如果将报表服务器配置为使用基本身份验证，并且未启用对报表生成器程序文件的匿名访问，则请求将失败。 请求失败的原因在于 ClickOnce 在其请求中指定了 Windows 集成安全性。 如果将报表服务器配置为使用基本身份验证，则该服务器将拒绝请求，原因是它指定的是无效的安全包以及缺少该报表服务器预期的凭据。<br /><br /> 此外，如果将报表服务器配置为使用 SharePoint 集成模式，SharePoint 站点使用基本身份验证，则当用户试图使用 ClickOnce 在客户端计算机上安装报表生成器时，将遇到 401 错误。 发生这种情况是因为 SharePoint 使用 cookie 保持用户在会话期间通过身份验证，但 ClickOnce 不支持 cookie。 用户启动 ClickOnce 应用程序（如报表生成器）时，该应用程序不会将 cookie 传递给 SharePoint，因此 SharePoint 拒绝访问并返回 401 错误。<br /><br /> 您可以尝试下列选项之一来解决此问题：<br /><br /> 提供用户凭据时，请选择 "**记住我的密码**" 选项。<br /><br /> 启用对 SharePoint 站点集的匿名访问。<br /><br /> 对环境进行配置以使用户不用提供凭据。 例如，在 Intranet 环境中，可将 SharePoint 服务器配置为属于一个工作组，然后在本地计算机上创建用户帐户。|  
|自定义|将报表服务器配置为使用自定义身份验证时，会在报表服务器上启用匿名访问并且在不进行身份验证检查的情况下接受请求。<br /><br /> ClickOnce 检索应用程序文件后，报表生成器将打开与报表服务器的单独连接。 用户必须重新键入其凭据以使报表生成器连接到报表服务器。 报表生成器不会从 Internet Explorer 或 ClickOnce 收集凭据。|  
  
## <a name="see-also"></a>另请参阅  
 [针对报表服务器的身份验证](../security/authentication-with-the-report-server.md)   
 [规划 Reporting Services 和 Power View 浏览器支持 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [开始报表生成器 &#40;报表生成器&#41;](../report-builder/start-report-builder.md)   
 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)   
 [在 Management Studio 中连接到报表服务器](../tools/connect-to-a-report-server-in-management-studio.md)   
 [报表服务器系统属性](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)  
  
  
