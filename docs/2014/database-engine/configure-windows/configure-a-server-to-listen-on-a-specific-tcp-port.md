---
title: 配置服务器以侦听特定 TCP 端口 （SQL Server 配置管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- fixed port
- static ports
- ports [SQL Server], assigning numbers
- assigning port numbers
- dynamic ports [SQL Server]
- TCP/IP [SQL Server], port numbers
ms.assetid: 2276a5ed-ae3f-4855-96d8-f5bf01890640
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d408c25216139a173dced0ae19f9ddea7d1ba4d5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088067"
---
# <a name="configure-a-server-to-listen-on-a-specific-tcp-port-sql-server-configuration-manager"></a>配置服务器以侦听特定 TCP 端口（SQL Server 配置管理器）
  本主题说明如何使用 SQL Server 配置管理器配置 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例以便侦听特定的固定端口。 如果启用， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的默认实例将侦听 TCP 端口 1433。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的命名实例配置为使用动态端口。 这意味着启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务时，它们将选择可用的端口。 在通过防火墙连接到命名实例时，请配置 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 以侦听特定端口，以便能够在防火墙中打开相应的端口。  
  
 有关默认 Windows 防火墙设置的详细信息以及有关影响数据库引擎、Analysis Services、Reporting Services 和 Integration Services 的 TCP 端口的说明，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
> [!TIP]  
>  选择端口号时，请查看 [http://www.iana.org/assignments/port-numbers](http://www.iana.org/assignments/port-numbers) 以了解分配给特定应用程序的端口号列表。 请选择一个未分配的端口号。 更多详细信息，请参阅 [TCP/IP 的默认动态端口范围在 Windows Vista 和 Windows Server 2008 中已更改](http://support.microsoft.com/kb/929851)。  
  
> [!WARNING]  
>  重新启动时，数据库引擎开始侦听新端口。 但是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务监视注册表并在配置更改时报告新端口号，即使数据库引擎可能未使用该端口。 重新启动数据库引擎可确保一致性并避免连接失败。  
  
 **本主题内容**  
  
-   **若要配置服务器以侦听特定 TCP 端口，请使用：**  
  
     [SQL Server 配置管理器](#SSMSProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-assign-a-tcpip-port-number-to-the-sql-server-database-engine"></a>为 SQL Server 数据库引擎分配 TCP/IP 端口号  
  
1.  在 SQL Server 配置管理器的控制台窗格中，展开“SQL Server 网络配置”，展开“\<实例名称> 的协议”，然后双击“TCP/IP”。  
  
2.  在“TCP/IP 属性”对话框的“IP 地址”选项卡上，将显示若干个 IP 地址，格式为：**IP1**、**IP2**...，一直到 **IPAll**。 这些 IP 地址中有一个是环回适配器的 IP 地址 (127.0.0.1)。 其他 IP 地址是计算机上的各个 IP 地址。 右键单击每个地址，再单击“属性”，标识要配置的 IP 地址。  
  
3.  如果 **“TCP 动态端口”** 对话框中包含 **0**，则表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 正在侦听动态端口，请删除 0。  
  
4.  在“IPn 属性”区域框的“TCP 端口”框中，键入希望此 IP 地址侦听的端口号，然后单击“确定”。  
  
5.  在控制台窗格中，单击“SQL Server 服务”。  
  
6.  在详细信息窗格中，右键单击“SQL Server (\<实例名称>)”，然后单击“重启”以停止并重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 在配置完 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以侦听特定端口后，可以通过下列三种方式使用客户端应用程序连接到特定端口：  
  
-   运行服务器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务以按名称连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例。  
  
-   在客户端上创建一个别名，指定端口号。  
  
-   对客户端进行编程，以便使用自定义连接字符串进行连接。  
  
## <a name="see-also"></a>请参阅  
 [创建或删除供客户端使用的服务器别名（SQL Server 配置管理器）](create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
  
