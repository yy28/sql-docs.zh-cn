---
title: 连接到远程 Integration Services 服务器（SSIS 服务） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], remote instance
- Integration Services service, connecting
- Integration Services service, remote instance
- service [Integration Services], connecting
ms.assetid: 9487aff1-44d8-42c1-8176-bb9891d4632d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e0e7e62510338b9dd47d59ce50626ecffebfcf85
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060415"
---
# <a name="connect-to-a-remote-integration-services-server-ssis-service"></a>连接到远程 Integration Services 服务器（SSIS 服务）
    
> [!IMPORTANT] 
> 本主题论述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]支持服务以便与的早期版本向后兼容[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。 从 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
 若要从 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 或其他管理应用程序连接到远程服务器上的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 实例，应用程序的用户需要拥有服务器上的一组特定权限。  
  
> [!IMPORTANT] 
> 若要管理存储在某远程服务器上的包，您不必连接到该远程服务器上 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的实例。 只需编辑 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的配置文件，以便 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 显示存储在远程服务器上的包。 有关详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](service/integration-services-service-ssis-service.md)。  
  
## <a name="connecting-to-integration-services-on-a-remote-server"></a>连接到远程服务器上的 Integration Services  
  
#### <a name="to-connect-to-integration-services-on-a-remote-server"></a>连接到远程服务器上的 Integration Services  
  
1.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  选择 **“文件”** 菜单上的 **“连接对象资源管理器”** 以显示 **“连接到服务器”** 对话框。  
  
3.  在 **“服务器类型”** 列表中选择 **Integration Services** 。  
  
4.  在“服务器名称”[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]文本框中键入 **** 服务器的名称。  
  
    > [!NOTE]  
    >  
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务是不特定于实例的。 通过使用正运行 Integration Services 服务的计算机的名称连接到该服务。  
  
5.  单击“连接”  。  
  
> [!NOTE]  
>  
  **“查找服务器”** 对话框中不显示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的远程实例。 此外， **“连接到服务器”** 对话框中的 **“连接选项”** 选项卡上的选项不适用于 **连接（该选项卡在单击** “选项” [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 按钮后显示）。  
  
## <a name="eliminating-the-access-is-denied-error"></a>消除“拒绝访问”错误  
 当没有足够权限的用户尝试连接到远程服务器上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 实例时，服务器将以“拒绝访问”错误消息进行响应。 确保用户具有所需的 DCOM 权限可避免出现此错误消息。  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-server-2003-or-windows-xp"></a>在 Windows Server 2003 或 Windows XP 上配置远程用户的权限  
  
1.  如果用户不是本地 Administrators 组的成员，请将用户添加至 Distributed COM Users 组。 可以从“管理工具”**** 菜单访问“计算机管理”MMC 管理单元完成此操作。  
  
2.  打开“控制面板”，双击“管理工具”****，然后双击“组件服务”**** 以启动组件服务 MMC 管理单元。  
  
3.  展开控制台左侧窗格中的 **“组件服务”** 节点。 展开 **“计算机”** 节点，展开 **“我的电脑”**，然后单击 **“DCOM 配置”** 节点。  
  
4.  选中 **“DCOM 配置”** 节点，然后在可以配置的应用程序列表中选择“SQL Server Integration Services 11.0”。  
  
5.  右键单击 SQL Server Integration Services 11.0，然后选择“属性”****。  
  
6.  在 **“SQL Server Integration Services 11.0 属性”** 对话框中，选择 **“安全性”** 选项卡。  
  
7.  在 **“启动和激活权限”** 下，选择 **“自定义”**，然后单击 **“编辑”** 以打开 **“启动权限”** 对话框。  
  
8.  在 **“启动权限”** 对话框中，添加或删除用户，并为适当的用户和组分配相应的权限。 可用的权限为“本地启动”、“远程启动”、“本地激活”和“远程激活”。 启动权限可授予或拒绝启动和停止服务的权限；激活权限可授予或拒绝连接到服务的权限。  
  
9. 单击“确定”关闭对话框。  
  
10. 在 **“访问权限”** 下，重复步骤 7 和步骤 8 以为适当的用户和组分配适当的权限。  
  
11. 关闭 MMC 管理单元。  
  
12. 重新启动 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务。  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-2000-with-the-latest-service-packs"></a>在带有最新 Service Pack 的 Windows 2000 上为远程用户配置权限  
  
1.  在命令提示符下运行 **dcomcnfg.exe** 。  
  
2.  在 **“分布式 COM 配置属性”** 对话框的 **“应用程序”** 页上，选择“SQL Server Integration Services 11.0”，再单击 **“属性”**。  
  
3.  选择“安全性”**** 页。  
  
4.  使用两个单独的对话框来分别配置 **“访问权限”** 和 **“启动权限”**。 您无法区分远程访问和本地访问 - 访问权限包括了本地访问和远程访问，启动权限也包括了本地启动和远程启动。  
  
5.  关闭对话框和 **dcomcnfg.exe**。  
  
6.  重新启动 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务。  
  
## <a name="connecting-by-using-a-local-account"></a>使用本地帐户连接  
 如果您是在客户端计算机上使用本地 Windows 帐户工作，则只有远程计算机上存在与客户端计算机上的本地帐户的帐户名和密码相同并且具有相应权限的本地帐户时，才可以连接到远程计算机上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务。  
  
## <a name="by-default-the-ssis-service-does-not-support-delegation"></a>默认情况下，SSIS 服务不支持委派  
默认情况下[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ，该服务不支持委托凭据，或有时称为双跃点。 在此方案中，你在客户端计算机上工作， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务在第二台计算机上运行和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在第三台计算机上运行。 首先， [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 成功地将你的凭据从客户端计算机传递到第二台计算机上， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务正在这台计算机上运行。 但是，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务不能将你的凭据从第二台计算机委派到正在运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的第三台计算机上。

可通过将“信任此用户对任何服务的委派(仅 Kerberos)”**** 的权限授予 SQL Server 服务帐户（它将 Integration Services 服务 (ISServerExec.exe) 作为子进程启动），从而启用凭据委派。 在授予此权限之前，请考虑它是否符合组织的安全要求。

有关详细信息，请参阅 [Getting Cross Domain Kerberos and Delegation working with SSIS Package](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/)（获取跨域 Kerberos 和委派使用 SSIS 包）。
  
## <a name="see-also"></a>另请参阅  
 [为访问 SSIS 服务配置 Windows 防火墙](../../2014/integration-services/configure-a-windows-firewall-for-access-to-the-ssis-service.md)  
  
  
