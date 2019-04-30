---
title: 服务帐户 （SSRS 本机模式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serviceaccount.F1
ms.assetid: face8120-4d32-4c6c-a1e8-99f27d1ff15d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 96cee57e82cc9fbb01a43dc1ec13bf0691f737fc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185531"
---
# <a name="service-account-ssrs-native-mode"></a>服务帐户（SSRS 本机模式）
  使用“服务帐户”页可以指定运行报表服务器服务的帐户。 此帐户最初在安装过程中进行配置。 如果要更改此帐户或密码，则可以对其进行修改。 报表服务器 Web 服务、报表管理器和后台处理应用程序都使用此页上指定的服务标识运行。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
 为报表服务器服务指定的帐户需要拥有访问注册表、报表服务器程序文件和报表服务器数据库的权限。 在您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器设置此帐户时，所有权限都会自动配置给此帐户。 如果使用的服务帐户连接到报表服务器数据库，Configuration Manager 创建帐户的数据库登录名，并将此帐户分配到 RSExecRole 上配置数据库权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]托管实例报表服务器数据库。 报表服务器数据库是报表服务器可以写入的唯一数据存储区。 此服务帐户不需要其他任何数据存储区的权限。  
  
 若要打开此页，请启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，然后在导航窗格中选择相应链接。 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
> [!IMPORTANT]  
>  我们极力建议您在每次更新帐户或密码时都使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器。 使用配置管理器更新帐户可确保其他基于此服务标识的内部设置都能同时自动更新。  
  
## <a name="options"></a>选项  
 **使用内置帐户**  
 从此列表中选择 **Network Service**、 **Local System**或 **Local Service** 。 建议只选择 **Network Service** ；不过，可以将帐户配置为使用任何可用的帐户。  
  
 **使用其他帐户**  
 选择此选项可以指定 Windows 用户帐户。 可以输入本地 Windows 用户帐户或域用户帐户。 按以下格式指定域帐户： *\<域 >\\< 用户\>*。 按以下格式指定本地 Windows 用户帐户： *\<计算机名 >\\< 用户\>*。 您只能选择现有的帐户；不能在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置中创建新帐户。  
  
 帐户的最大字符数限制为 20 个字符。  
  
 如果网络使用 Kerberos 身份验证，且您将报表服务器配置为使用域用户帐户运行，则必须使用此用户帐户注册服务。 有关详细信息，请参阅[为报表服务器注册服务主体名称 (SPN)](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)。  
  
 如果您要切换帐户类型（例如，将一个 Windows 帐户替换为另一个 Windows 帐户，或者将内置帐户替换为 Windows 域帐户），系统将提示您创建加密密钥的备份副本。 在选择新帐户时将自动还原备份副本。  
  
> [!NOTE]  
>  每次修改服务帐户时， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器都会提示您备份和还原加密密钥。 必须执行这些步骤，才能确保加密数据在报表服务器上可用。 有关这些操作的详细信息，请参阅[加密密钥&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)。  
  
 此外，如果必须是报表服务器配置为运行在 SharePoint 集成模式并且您的服务帐户使用更改[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]配置管理器中，您还必须打开 SharePoint 管理中心并使用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**授予数据库访问权限**页后，可以重新应用报表服务器和实例设置。 此步骤将授予新服务帐户访问 SharePoint 数据库的权限，将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 与 SharePoint 产品或技术集成在一起时需要此权限。 有关如何授予在 SharePoint 管理中心内的数据库访问权限的详细信息，请参阅[配置和管理报表服务器的&#40;Reporting Services SharePoint 模式&#41;](../../../2014/reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md)并[Reporting Services SharePoint 模式下安装&#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
## <a name="choosing-an-account"></a>选择帐户  
 为了实现最佳的结果，请指定一个拥有网络连接权限、可以访问网络域控制器和公司 SMTP 服务器或网关的帐户。 下表汇总了各个帐户，并为使用这些帐户提供了建议。  
  
|帐户|解释|  
|-------------|-----------------|  
|域用户帐户|如果您有一个拥有报表服务器操作所需的最小权限的 Windows 域用户帐户，则应使用此帐户。<br /><br /> 之所以建议使用域帐户，是因为这种帐户可以将报表服务器服务与其他应用程序隔离开。 使用共享帐户（如 Network Service）运行多个应用程序会增加恶意用户控制报表服务器的风险，因为在这种情况下，任何一个应用程序的安全漏洞会很容易扩散到使用同一帐户运行的所有其他应用程序。<br /><br /> 如果是为受约束委托或 SharePoint 集成模式（包含的 SharePoint 2010 产品要求使用域用户帐户而非内置的计算机帐户）配置报表服务器，则必须使用域用户帐户。<br /><br /> 请注意，如果您使用域用户帐户，并且您的组织实施了密码过期策略，则您必须定期更改密码。 您可能还需要使用此用户帐户注册服务。 有关详细信息，请参阅[为报表服务器注册服务主体名称 (SPN)](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)。<br /><br /> 避免使用本地 Windows 用户帐户。 本地帐户通常没有足够的权限访问其他计算机上的资源。 有关如何使用本地帐户限制报表服务器功能的详细信息，请参阅本主题中的 [使用本地帐户的注意事项](#localaccounts) 。|  
|**Network Service**|**Network Service** 是一个拥有网络登录权限的内置最低特权帐户。 如果没有可用的域用户帐户，或者要避免因密码过期策略而可能导致的任何服务中断，建议使用此帐户。<br /><br /> 如果您选择 **Network Service**，请尝试将使用同一帐户运行的其他服务的数量降到最低。 对于使用同一帐户运行的多个应用程序，如果一个应用程序出现安全漏洞，则所有其他应用程序的安全都会受到影响。|  
|**Local Service**|**Local Service** 是一个与经过身份验证的本地 Windows 用户帐户类似的内置帐户。 以 **“Local Service”** 帐户运行的服务将以一个没有凭据的 Null 会话形式访问网络资源。 此帐户不适合于 Intranet 部署方案。因为在此部署方案下，报表服务器必须连接至远程报表服务器数据库或网络域控制器，以在打开报表或处理订阅之前对用户进行身份验证。|  
|**Local System**|**Local System** 是一个高特权帐户，运行报表服务器时不需要此帐户。 请勿将此帐户用于报表服务器的安装。 此时应选择域帐户或 **Network Service** 。|  
  
##  <a name="localaccounts"></a> 使用本地帐户的注意事项  
 使用本地帐户的主要注意事项是报表服务器是否需要访问远程数据库服务器、邮件服务器和域控制器。 如果将报表服务器配置为作为本地 Windows 用户帐户、Local Service 或 Local System 运行，则必须考虑如何设置其他配置设置以及订阅创建和传递方面的注意事项：  
  
-   如果使用本地帐户运行服务，则以后在配置远程报表服务器数据库的连接时，选项将受到限制。 具体来说，如果您使用的是远程报表服务器数据库，则必须将连接配置为使用有权登录到远程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的域用户帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库用户。  
  
-   在本地帐户下运行服务将对订阅的创建具有新的要求。 报表服务器存储创建订阅的用户的信息。 如果用户在使用域帐户登录时创建订阅，则在处理订阅时，报表服务器服务将尝试连接到域控制器以对用户进行身份验证。 如果此服务使用本地帐户运行，则在报表服务器尝试将身份验证请求发送到远程域控制器时，此请求将失败。 若要消除此限制，可以使用基于窗体的自定义身份验证扩展插件或让所有用户使用本地用户帐户连接到报表服务器。  
  
-   在本地帐户下运行服务将对订阅的传递具有新的要求。 某些传递扩展插件在订阅定义中包含有用户帐户信息。 如果要将报表发送到基于域用户帐户的电子邮件地址，并且使用本地帐户运行报表服务器服务，则此服务将无法访问远程域控制器以解析目标电子邮件帐户。  
  
-   不支持将内置 Windows 服务帐户（Local Service 或 Network Service）用作作为域控制器的计算机上的报表服务器服务帐户。  
  
## <a name="see-also"></a>请参阅  
 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [配置服务帐户（SSRS 配置管理器）](../../../2014/sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [Reporting Services 配置管理器 F1 帮助主题&#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
