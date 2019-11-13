---
title: 配置服务帐户（SSRS Configuration Manager） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Server Web service, accounts
- service accounts [Reporting Services]
- Report Server Windows service, accounts
- Web service [Reporting Services], report server
ms.assetid: 25000ad5-3f80-4210-8331-d4754dc217e0
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 04dff943d1227f84ff514e593f65c2ce4d7a918f
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952586"
---
# <a name="configure-a-service-account-ssrs-configuration-manager"></a>配置服务帐户（SSRS 配置管理器）
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装中，报表服务器 Web 服务、报表管理器和后台处理应用程序在一个服务内运行。 运行该服务的帐户是在安装过程中定义的，即在“服务标识”页中指定的帐户；但是，如果希望使用不同的帐户或更改密码，可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具。  
  
 如果 Report Server 配置为使用 SharePoint 集成模式，并且您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具更改了服务帐户，则您还必须打开 SharePoint 管理中心并使用 "[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**授予数据库访问权限**" 页重新应用 Report Server 和实例设置。 此步骤向新服务帐户授予对 SharePoint 数据库的访问权限，这是将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 与 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]集成所必需的。  
  
 请始终使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具来更新服务帐户，以便可以同时更新依赖服务标识的其他设置。  
  
> [!NOTE]  
>  不支持将内置 Windows 服务帐户（Local Service 或 Network Service）用作作为域控制器的计算机上的报表服务器服务帐户。  
  
 过程  
  
### <a name="to-configure-the-report-server-service-account"></a>配置报表服务器服务帐户  
  
1.  启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器并连接到报表服务器。  
  
2.  在“服务帐户”页上，选择描述您要使用的帐户类型的选项。 有关指定哪种帐户类型的建议，请参阅[配置报表服务器服务帐户&#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
3.  如果选择了一个 Windows 用户帐户，请指定新的帐户名和密码。 帐户名不能超过 20 个字符。  
  
     如果报表服务器部署在支持 Kerberos 身份验证的网络中，则必须使用刚刚指定的域用户帐户注册报表服务器服务主体名称 (SPN)。 有关详细信息，请参阅[为报表服务器注册服务主体名称 (SPN)](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)。  
  
4.  单击 **“应用”** 。  
  
5.  当系统提示您备份对称密钥时，请键入对称密钥备份的文件名和位置，并键入用于锁定和解锁该文件的密码，然后单击 **“确定”** 。  
  
6.  如果报表服务器使用该服务帐户连接到报表服务器数据库，则连接信息将更新为使用新的帐户或密码。 更新连接信息要求连接到数据库。 如果出现“ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **数据库连接”** 对话框，请输入拥有连接到数据库的权限的凭据，然后单击 **“确定”** 。  
  
7.  当系统提示您还原对称密钥时，请键入在步骤 5 中指定的密码，并单击 **“确定”** 。  
  
8.  查看“结果”窗格中的状态消息以验证所有任务是否均已成功完成。  
  
## <a name="troubleshooting-service-identity-update-errors"></a>服务标识更新错误故障排除  
 更改服务标识将启动一系列事件，其中包括重新启动服务、更新受密码保护的加密密钥、更新 URL 预留以及更新报表服务器数据库连接信息（如果使用该服务帐户来连接报表服务器数据库）。 您可以通过查看页面底部“结果”窗格中的通知来监视这些事件的状态。 如果在此过程中出现错误，可以尝试使用以下方法进行解决：  
  
-   如果无法还原对称密钥，可以尝试使用“加密密钥”页中的 **“还原”** 手动还原它。 如果这不起作用，可以考虑删除加密的内容。 您必须重新创建数据源连接信息和订阅，但其余内容仍然可用。 有关详细信息，请参阅 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。  
  
-   如果服务未启动，请使用管理工具中的“服务”控制台应用程序手动重新启动它。  
  
-   更新服务帐户时可能会发生 URL 预留错误。 每个 URL 预留都包含一个安全描述符，其中包含授权该服务帐户接受该 URL 上的请求的自由访问控制列表 (DACL)。 更新帐户时，必须重新创建该 URL，以便用新帐户信息更新 DACL。 如果无法重新创建 URL 预留，并且你知道该帐户是有效的，请尝试重新启动计算机。 如果错误仍然存在，请尝试使用不同的帐户。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services Configuration Manager（本机模式）](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [配置报表服务器数据库连接（SSRS 配置管理器）](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [服务帐户&#40;SSRS 本机模式&#41; ](../../../2014/sql-server/install/service-account-ssrs-native-mode.md)   
 [配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
