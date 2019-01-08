---
title: 分析平台系统的配置清单-|Microsoft Docs
description: 提供自己的环境配置分析平台系统所需的任务的清单。 可以使用该设备，还需要执行这些配置任务。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ada3d2f782a33caf5334361a9682c53cf7cdec95
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398600"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>分析平台系统的设备配置清单
提供自己的环境配置分析平台系统所需的任务的清单。 可以使用该设备，还需要执行这些配置任务。  
  
> [!WARNING]  
> 使用 Analytics Platform System**Configuration Manager**是最好的方法，而且唯一受支持的方式来执行该工具中可用的任务。  
  
## <a name="BeforeTasks"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
  
1.  设备必须安装在数据中心，且已打开电源。  
  
2.  请确保你具有由 IHV 提供的以下信息：  
  
    -   PDW 控制节点的外部 IP 地址 (*PDW_region-* CTL01)  
  
    -   设备的域名  
  
    -   用户名称和设备域管理员密码  
  
3.  获取受信任的证书。 你将在后面的步骤以允许客户端连接到导入此**管理员控制台**使用安全连接。 将证书保存到受密码保护 PFX 文件中的控制节点。  
  
4.  启动**Configuration Manager**，使用以下步骤：  
  
    1.  使用**远程桌面**连接到 PDW 控制节点 (*PDW_region*-CTL01)。 （您可能需要连接到外部 IP 地址 for CTL01。）  
  
    2.  启动**Configuration Manager**从**启动**PDW 控制节点的菜单。 第一个屏幕的 Configuration Manager 中显示设备拓扑中，已通过 IHV。 它是设备的 SQL Server PDW 软件识别为属于你的硬件节点的列表。 不需更改工具拓扑屏幕上的任何设置。  
  
## <a name="CMTasks"></a>执行配置管理器任务  
SQL Server PDW**Configuration Manager** (PDWCM) 是 SQL Server PDW 系统管理员使用来执行设备级的操作，以及若要更改设备级设置设备管理工具。 例如，使用 PDWCM 重置密码、 设置时区，更改 IP 地址、 配置 SSL 证书、 启用通过防火墙进行远程访问、 启动或停止设备，以及设置即时文件初始化。  
  
使用**Configuration Manager**执行以下配置任务。  
  
|配置任务|Description|  
|----------------------|---------------|  
|熟悉物理组件名称|[PDW 和设备结构物理组件&#40;分析平台系统&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|启动 SQL Server PDW 配置管理器|[启动配置管理器&#40;分析平台系统&#41;](launch-the-configuration-manager.md)|  
|更改域管理员密码|设备具有专用 Windows Active Directory 域服务用于进行身份验证在装置内的节点。<br /><br />IHV 设置设备，但默认域管理员密码。 这需要将更改为安全的密码。<br /><br />**Configuration Manager**唯一受支持的方式来更改域管理员密码。<br /><br />有关详细信息，请参阅[密码重置&#40;Analytics Platform System&#41;](password-reset.md)。|  
|更改的密码**sa**登录|SQL Server PDW 具有系统管理员登录名**sa**。 **Sa**登录帐户是否具有所有权限。 它可以授予、 拒绝或撤消的任何权限。 它还可以看到所有的系统视图。<br /><br />有关详细信息，请参阅[密码重置&#40;Analytics Platform System&#41;](password-reset.md)。|  
|设置设备时区|设置设备的所有节点的时间 （本地或其他所需的时间）。<br /><br />有关详细信息，请参阅[设备时区配置&#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md)。|  
|指定 SQL Server PDW 设备的面向外部网络设置|[设备网络配置&#40;分析平台系统&#41;](appliance-network-configuration.md)|  
|安全证书导入的管理控制台|证书可以提供安全套接字层 (SSL) 连接通过 HTTPS 向[通过使用管理控制台监视设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。 默认情况下**管理员控制台**包含一个自签名的证书，它提供的隐私，但不是服务器身份验证。 此证书还在 Internet Explorer 指出返回错误："没有此网站的安全证书有问题"用户连接时。 尽管此连接对客户端和服务器之间传输的数据的数据进行加密，则将连接仍面临攻击的风险。<br /><br />SQL Server PDW 管理员应立即获取证书链接至受信任的证书颁发机构的客户端，以便建立安全连接，并删除 Internet Explorer 报告的错误识别。 这需要完全限定的域名映射 （推荐） 管理节点的虚拟 IP 地址或用户在其浏览器地址中键入的值匹配的证书名称条访问管理控制台。<br /><br />使用**Configuration Manager**添加或删除受信任的证书。 直接使用 Microsoft Windows HTTP 服务证书配置工具 (`winHttpCertCfg.exe`) 若要管理的证书不受支持。<br /><br />有关详细信息，请参阅[PDW 证书预配&#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md)。|
|功能开关|有关在分析平台系统 AU7 中引入的功能开关的显示信息。 使用此页可以更新或启用/禁用功能和分析平台系统中的设置。 更改功能切换值需要重新启动服务。<br /><br />有关详细信息，请参阅[PDW 功能开关&#40;Analytics Platform System&#41;](appliance-feature-switch.md)。|
|启用或禁用 Windows 防火墙规则来允许或阻止对 SQL Server PDW 设备上的特定端口访问。|IHV 将配置并启用所需的设备都能正常运行的防火墙规则。 在大多数情况下将启用或禁用防火墙规则。<br /><br />有关详细信息，请参阅[PDW 防火墙配置&#40;Analytics Platform System&#41;](pdw-firewall-configuration.md)。|  
|启动和停止 SQL Server PDW 设备|停止或启动 SQL Server PDW 设备。 有关详细信息，请参阅[PDW 服务状态&#40;Analytics Platform System&#41;](pdw-services-status.md)。|  
|查看使用的即时文件初始化选项**特权**对话框|即时文件初始化功能允许数据文件操作，以更快地运行的 SQL Server 功能。 它是 SQL Server PDW 上启用仅当已向网络服务帐户授予了 SE_MANAGE_VOLUME_NAME 特权。 默认情况下，它处于关闭状态。<br /><br />有关详细信息，请参阅[即时文件初始化配置&#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md)。|  
|从备份还原 master 数据库|删除当前**主**数据库并将替换备份。 有关详细信息，请参阅[恢复主数据库&#40;Analytics Platform System&#41;](restore-the-master-database.md)。|  
  
## <a name="AddTasks"></a>执行其他配置任务  
执行后**Configuration Manager**任务，执行下面列出的其他配置任务。 其中一些任务是可选的。  
  
|配置任务|Description|  
|----------------------|---------------|  
|第三方防病毒软件可以安装和配置 SQL Server PDW 设备的面向外部的节点上。<br /><br />（可选）|有关详细信息，请参阅[防病毒软件&#40;Analytics Platform System&#41;](antivirus-software.md)。|  
|可以更改为 DSRM 密码。<br /><br />（可选）|有关详细信息，请参阅[设置用于登录到 AD 节点以目录服务还原模式管理员密码&#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)。|  
|配置设备以接收软件更新<br /><br />（建议）|设备需要将配置为接收到的 SQL Server PDW 和基础软件更新。<br /><br />有关详细信息，请参阅[配置 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。 有关 WSUS 的信息，请参阅[软件维护服务&#40;Analytics Platform System&#41;](software-servicing.md)。|  
|配置与外部数据，例如 Hadoop 或 Azure blob 存储的连接。<br /><br />（可选）|有关详细信息，请参阅[配置到外部数据的 PolyBase 连接&#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md)。|  
|配置防病毒软件<br /><br />（可选）|第三方防病毒解决方案可用于保护面向外部的节点，但不是必需的。 遵循中的准则。|  
|备份和加载服务器上配置 InfiniBand 网络适配器<br /><br />（可选）|若要配置备份和正在加载服务器以使用 InfiniBand 网络连接到 SQL Server PDW，您需要配置网络适配器，以允许设备 DNS 来解析 InfiniBand 连接到当前处于活动状态的 InfiniBand 网络。|  
|配置为将遥测数据发送给 Microsoft<br /><br />（可选）|若要配置分析平台系统将遥测数据发送给 Microsoft，您需要在控制节点上运行 PowerShell 脚本。 有关具体说明，请参阅[向 Microsoft 发送遥测反馈&#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)。|  
  
## <a name="see-also"></a>请参阅  
[防病毒软件&#40;分析平台系统&#41;](antivirus-software.md)  
[配置 InfiniBand 网络适配器&#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
