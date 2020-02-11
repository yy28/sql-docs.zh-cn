---
title: 将防火墙配置为允许报表服务器访问 | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [Reporting Services]
- configuring servers [Reporting Services]
ms.assetid: 04dae07a-a3a4-424c-9bcb-a8000e20dc93
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 00590faa3ef5fb63338465d85202f4010cd3b72d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104155"
---
# <a name="configure-a-firewall-for-report-server-access"></a>Configure a Firewall for Report Server Access
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可以通过指定 IP 地址、端口和虚拟目录的 URL 访问报表服务器应用程序和已发布的报表。 如果 Windows 防火墙已开启，配置为报表服务器使用的端口很可能已关闭。 表明端口可能已关闭的迹象包括请求报表后出现空白网页，或尝试从远程客户端计算机打开报表管理器时出现空白页。  
  
 若要打开端口，必须在报表服务器计算机上使用 Windows 防火墙实用工具。 Reporting Services 不会帮您打开端口，您必须手动执行该步骤。  
  
 默认情况下，报表服务器侦听端口 80 的 HTTP 请求。 因此，以下操作说明包括用来指定该端口的步骤。 如果将报表服务器 URL 配置为使用其他端口，则在按照以下说明进行操作时必须指定相应的端口号。  
  
 如果要访问外部计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据库，或者如果报表服务器数据库在外部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上，则必须在外部计算机上打开端口 1433 和 1434。 有关详细信息，请参阅 [联机丛书中的](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) 为数据库引擎访问配置 Windows 防火墙 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 有关默认 Windows 防火墙设置的详细信息，以及有关影响 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的 TCP 端口的说明，请参阅 [联机丛书中的](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md) 配置 Windows 防火墙以允许 SQL Server 访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="prerequisites"></a>必备条件  
 这些操作说明假定您已经配置了服务帐户，创建了报表服务器数据库，并为报表服务器 Web 服务和报表管理器配置了 URL。 有关详细信息，请参阅 [管理 Reporting Services 本机模式报表服务器](manage-a-reporting-services-native-mode-report-server.md)。  
  
 您还应验证是否可以通过将本地 Web 浏览器连接到本地报表服务器实例来访问报表服务器。 此步骤可确保您拥有有效的安装。 开始打开端口之前，应验证是否已对安装进行了正确的配置。 若要在 Windows Server 中完成该步骤，还必须将报表服务器站点添加到“受信任的站点”中。 有关详细信息，请参阅 [为本地管理配置本机模式报表服务器 (SSRS)](configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## <a name="opening-ports-in-windows-firewall"></a>在 Windows 防火墙中打开端口  
 针对不同版本的 Windows 防火墙分别有不同的说明。  
  
#### <a name="to-open-port-80-on-windows-7-windows-server-2008-r2-windows-server-2012-and-2012-r2"></a>要在 Windows 7、Windows Server 2008 R2、Windows Server 2012 和 2012 R2 中打开端口 80  
  
1.  在 **“开始”** 菜单上单击 **“控制面板”** ，单击 **“系统和安全”** ，然后单击 **“Windows 防火墙”** 。 不为“类别”视图配置控制面板，您只需要选择 **“Windows 防火墙”** 。  
  
2.  单击“高级设置”  。  
  
3.  单击 **“入站规则”** 。  
  
4.  单击 "**操作**" 窗口中的 "**新建规则**"**。**  
  
5.  单击 **“端口”** 的 **“规则类型”** 。  
  
6.  单击“下一步”。   
  
7.  在 **“协议和端口”** 页上，单击 **TCP**。  
  
8.  选择 **“特定本地端口”** ，然后键入值 **80**。  
  
9. 单击“下一步”。   
  
10. 在 **“操作”** 页上，单击 **“允许连接”** 。  
  
11. 单击“下一步”。   
  
12. 在 **“配置文件”** 页上，单击适合您的环境的选项。  
  
13. 单击“下一步”。   
  
14. 在“名称”页上，输入名称“ReportServer (TCP on port 80)”    
  
15. 单击“完成”  。  
  
16. 重新启动计算机。  
  
#### <a name="to-open-port-80-on-windows-vista-or-windows-server-2008"></a>在 Windows Vista 或 Windows Server 2008 中打开端口 80  
  
1.  从 "**开始**" 菜单中，单击 "**控制面板**"，单击 "**安全**"，然后单击 " **Windows 防火墙**"。  
  
2.  单击“允许程序通过 Windows 防火墙”****。  
  
3.  单击“继续”****。  
  
4.  在 "例外" 选项卡上，单击 "**添加端口**"。  
  
5.  在 "名称" 中，键入**ReportServer （TCP on 端口80）**。  
  
6.  在 "端口号" 中，键入**80**。  
  
7.  验证是否选择了 " **TCP** "。  
  
8.  单击 "**更改范围**"。  
  
9. 单击 "**仅我的网络（子网）**"，然后单击 **"确定"**。  
  
10. 单击 **“确定”** 关闭对话框。  
  
11. 重新启动计算机。  
  
## <a name="next-steps"></a>后续步骤  
 打开端口后，必须在确认远程用户是否可以通过所打开的端口访问报表服务器之前，通过主文件夹或站点级别的角色分配授予用户访问报表服务器的权限。 如果用户不具有足够的权限，那么虽然可以正确地打开端口，但报表服务器连接仍会失败。 有关详细信息，请参阅 [ 联机丛书中的](../security/grant-user-access-to-a-report-server.md)授予用户对报表服务器的访问权限（报表管理器）[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 您还可以通过在其他计算机上启动报表管理器来验证是否正确打开了端口。 有关详细信息，请参阅 [ 联机丛书中的](../report-manager-ssrs-native-mode.md)报表管理器（SSRS 本机模式）[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [配置报表服务器服务帐户（SSRS 配置管理器）](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [配置报表服务器 URL（SSRS 配置管理器）](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [创建报表服务器数据库（SSRS 配置管理器）](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [配置报表服务器服务帐户（SSRS 配置管理器）](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [管理 Reporting Services 本机模式报表服务器](manage-a-reporting-services-native-mode-report-server.md)  
  
  
