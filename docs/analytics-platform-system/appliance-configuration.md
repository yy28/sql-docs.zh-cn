---
title: 配置清单
description: 提供针对你自己的环境配置分析平台系统所需任务的清单。 这些配置任务是必需的，才能使用设备。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 80fc899400be167badaae9d617d43a61e0d346b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289735"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>用于分析平台系统的设备配置清单
提供针对你自己的环境配置分析平台系统所需任务的清单。 这些配置任务是必需的，才能使用设备。  
  
> [!WARNING]  
> 使用分析平台系统**Configuration Manager**是执行工具中可用任务的最佳方法，也是唯一受支持的方法。  
  
## <a name="before-you-begin"></a><a name="BeforeTasks"></a>开始之前  
  
### <a name="prerequisites"></a>先决条件  
  
1.  设备必须安装在数据中心并接通电源。  
  
2.  请确保你具有以下信息，这是由 IHV 提供的：  
  
    -   PDW 控制节点的外部 IP 地址（*PDW_region*CTL01）  
  
    -   设备域名  
  
    -   设备域管理员的用户名和密码  
  
3.  获取受信任的证书。 你将在后面的步骤中导入此项，以允许客户端使用安全连接连接到**管理控制台**。 将证书保存到受密码保护的 PFX 文件中的控制节点。  
  
4.  使用以下步骤启动**Configuration Manager**：  
  
    1.  使用**远程桌面**连接到 PDW 控制节点（*PDW_region*CTL01）。 （可能需要连接到 CTL01 的外部 IP 地址。）  
  
    2.  从 PDW 控件节点的 "**开始**" 菜单启动**Configuration Manager** 。 Configuration Manager 的第一个屏幕显示由 IHV 创建的设备拓扑。 它是你的设备 SQL Server PDW 软件识别的硬件节点的列表。 你不需要更改 "设备拓扑" 屏幕上的任何设置。  
  
## <a name="perform-configuration-manager-tasks"></a><a name="CMTasks"></a>执行 Configuration Manager 任务  
SQL Server PDW**Configuration Manager** （PDWCM）是一种设备管理工具，SQL Server PDW 系统管理员使用该工具执行设备级别的操作并更改设备级别设置。 例如，使用 PDWCM 重置密码，设置时区，更改 IP 地址，配置 SSL 证书，通过防火墙启用远程访问，启动或停止设备，并设置即时文件初始化。  
  
使用**Configuration Manager**执行以下配置任务。  
  
|配置任务|说明|  
|----------------------|---------------|  
|熟悉物理组件名称|[PDW 和设备构造物理组件 &#40;分析平台系统&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|启动 SQL Server PDW Configuration Manager|[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)|  
|更改域管理员密码|设备具有专用 Windows Active Directory 域服务，用于对设备中的节点进行身份验证。<br /><br />IHV 使用默认域管理员密码设置设备。 需要将其更改为安全密码。<br /><br />**Configuration Manager**是更改域管理员密码的唯一受支持的方法。<br /><br />有关详细信息，请参阅[密码重置 &#40;分析平台系统&#41;](password-reset.md)。|  
|更改**sa**登录的密码|SQL Server PDW 具有一个名为**sa**的系统管理员登录名。 **Sa**登录具有所有权限。 它可以授予、拒绝或撤消任何权限。 它还可以查看所有系统视图。<br /><br />有关详细信息，请参阅[密码重置 &#40;分析平台系统&#41;](password-reset.md)。|  
|设置设备时区|为所有设备节点设置时间（本地或其他所需时间）。<br /><br />有关详细信息，请参阅 "[装置时区配置 &#40;分析平台系统"&#41;](appliance-time-zone-configuration.md)。|  
|为 SQL Server PDW 设备指定面向外部的网络设置|[设备网络配置 &#40;分析平台系统&#41;](appliance-network-configuration.md)|  
|导入管理控制台的安全证书|通过[使用管理控制台 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)，证书可以通过 HTTPS 向监视设备提供安全套接字层（SSL）连接。 默认情况下，**管理控制台**包括提供隐私的自签名证书，但不包括服务器身份验证。 此证书还会在 Internet Explorer 中返回一个错误，指出当用户连接时 "此网站的安全证书有问题"。 尽管此连接对客户端和服务器之间的正在进行的数据进行加密，但该连接仍存在攻击者的风险。<br /><br />SQL Server PDW 管理员应立即获取链接到客户端识别的受信任证书颁发机构的证书，以便建立安全连接并删除 Internet Explorer 报告的错误。 这需要一个完全限定的域名，该域名映射控件节点的虚拟 IP 地址（推荐）或与用户键入其浏览器地址栏以访问管理控制台的值匹配的证书名称。<br /><br />使用**Configuration Manager**可添加或删除受信任的证书。 不支持直接使用 Microsoft Windows HTTP 服务证书配置工具`winHttpCertCfg.exe`（）来管理证书。<br /><br />有关详细信息，请参阅[PDW Certificate 预配 &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md)。|
|功能切换|显示有关分析平台系统 AU7 中引入的功能开关的信息。 使用此页可以更新或启用/禁用分析平台系统中的功能和设置。 更改功能开关值需要重启服务。<br /><br />有关详细信息，请参阅[PDW 功能开关 &#40;分析平台系统&#41;](appliance-feature-switch.md)。|
|启用或禁用允许或阻止访问 SQL Server PDW 设备上的特定端口的 Windows 防火墙规则。|IHV 将配置和启用设备正常运行所需的防火墙规则。 在大多数情况下，你不会启用或禁用防火墙规则。<br /><br />有关详细信息，请参阅[PDW Firewall Configuration &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md)。|  
|启动和停止 SQL Server PDW 设备|停止或启动 SQL Server PDW 设备。 有关详细信息，请参阅[PDW 服务状态 &#40;分析平台系统&#41;](pdw-services-status.md)。|  
|使用 "**特权**" 对话框查看即时文件初始化选项|即时文件初始化是一项 SQL Server 功能，使数据文件操作能够更快地运行。 仅当已向网络服务帐户授予了 SE_MANAGE_VOLUME_NAME 权限时，才会在 SQL Server PDW 上启用它。 默认情况下，它处于关闭状态。<br /><br />有关详细信息，请参阅[即时文件初始化配置 &#40;分析平台系统&#41;](instant-file-initialization-configuration.md)。|  
|从备份中还原 master 数据库|删除当前的**master**数据库，并将其替换为备份。 有关详细信息，请参阅[Restore Master Database &#40;Analytics Platform System&#41;](restore-the-master-database.md)。|  
  
## <a name="perform-additional-configuration-tasks"></a><a name="AddTasks"></a>执行其他配置任务  
执行**Configuration Manager**任务后，请执行以下其他配置任务列表。 其中一些任务是可选的。  
  
|配置任务|说明|  
|----------------------|---------------|  
|可以在面向外部节点的 SQL Server PDW 设备上安装和配置第三方防病毒软件。<br /><br />(可选)|有关详细信息，请参阅[防病毒软件 &#40;分析平台系统&#41;](antivirus-software.md)。|  
|可以更改 DSRM 的密码。<br /><br />(可选)|有关详细信息，请参阅[在目录服务还原模式下为登录 AD 节点设置管理员密码 &#40;DSRM&#41; &#40;Analytics 平台系统&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)。|  
|配置设备以接收软件更新<br /><br />（建议）|需要将设备配置为接收 SQL Server PDW 和基础软件的更新。<br /><br />有关详细信息，请参阅[配置 Windows Server Update Services &#40;WSUS&#41; &#40;分析平台系统&#41;](configure-windows-server-update-services-wsus.md)。 有关 WSUS 的信息，请参阅[软件服务 &#40;分析平台系统&#41;](software-servicing.md)。|  
|配置与外部数据（如 Hadoop 或 Azure blob 存储）的连接。<br /><br />(可选)|有关详细信息，请参阅[配置与外部数据的 PolyBase 连接 &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md)。|  
|配置防病毒软件<br /><br />(可选)|第三方防病毒解决方案可用于保护面向外部的节点，但不是必需的。 遵循中的准则。|  
|在备份和加载服务器上配置无限网络适配器<br /><br />(可选)|若要通过使用不受支持的网络配置备份和加载服务器以连接到 SQL Server PDW，需要将网络适配器配置为允许设备 DNS 解析与当前处于活动状态的用户的连接。|  
|配置以将遥测数据发送给 Microsoft<br /><br />(可选)|若要将分析平台系统配置为将遥测数据发送到 Microsoft，需要在控制节点上运行 PowerShell 脚本。 有关具体说明，请参阅[将遥测反馈发送到 Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)。|  
  
## <a name="see-also"></a>另请参阅  
[防病毒软件 &#40;分析平台系统&#41;](antivirus-software.md)  
[配置 &#40;SQL Server PDW 的无线网络适配器&#41;](configure-infiniband-network-adapters.md)  
  
