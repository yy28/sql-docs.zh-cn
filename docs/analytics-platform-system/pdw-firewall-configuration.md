---
title: "PDW 防火墙配置 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 191f292d-16bc-4166-b855-158854ad062d
caps.latest.revision: "28"
ms.openlocfilehash: 6299717f9f56cb54eb029420a5be2c452101f34a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="pdw-firewall-configuration"></a>PDW 防火墙配置
**防火墙**页的 SQL Server PDW 配置管理器使你可以启用或禁用防火墙规则来允许或阻止对分析平台系统设备上的特定端口的访问。  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>为设备节点管理端口和防火墙规则  
  
1.  启动 Configuration Manager。 有关详细信息，请参阅[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md).  
  
2.  在配置管理器的左窗格中，展开**并行数据仓库拓扑**，然后单击**防火墙**。  
  
3.  找到端口或防火墙规则，以更新中的配置列表中，然后选择或清除该项旁边的框。 只有 SQL Server PDW 管理员可配置选项都显示在此列表，包括开始标记与结束面向外部的节点上的端口。  
  
4.  单击**应用**以保存所做的更改。  
  
![DWConfig 设备 PDW 防火墙](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>外部端口  
以下端口已打开进行外部 PDW 来自的客户端连接。  
  
|用途|端口 #|节点|  
|-----------|-----------|---------|  
|SQL 客户端访问 PDW (TDS)|17001|CTL|  
|加载程序客户端访问 （dwloader 和 SSIS）|8001|CTL|  
|远程桌面访问|3389|CTL CMP|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL 加密连接 （对于内部通信，以便访问管理控制台中，从而访问 HDInsight 群集服务）|443|所有节点|  
|SQL Server PDW 负载控制流的 Windows 凭据|8002|CTL|  
|_Kerberos|88|AD01 和 AD02，|  
|_ldap|389|AD01 和 AD02|  
  
## <a name="internal-ports"></a>内部端口  
以下的端口由 PDW 用于内部通信，但为来自外部 PDW 设备的连接未打开。  
  
|用途|端口 #|节点|  
|-----------|-----------|---------|  
|DMS 控制通道流量|16450|CTL CMP|  
|DMS 数据通道流量|16550|CTL CMP|  
|内部诊断|16650|CTL CMP|  
|故障转移状态 (DMS)|15000|CTL CMP|  
|故障转移状态 （引擎）|15001|CMP|  
|动态 （临时） 端口范围|20000-65535|CTL CMP|  
|SQL Server 端口范围 (TDS)|1433, 1500-1508|CTL CMP|  
  
> [!NOTE]  
> 创建外部表或外部数据源使用 TCP 端口 8020 默认情况下。 这些语句可以配置为改为使用其他端口。 Hortonworks JOB_TRACKER_LOCATION 默认端口为 50300。 与其他系统和工具集成可能需要其他端口。  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)  -->  
  
