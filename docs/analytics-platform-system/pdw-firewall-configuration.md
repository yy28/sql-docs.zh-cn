---
title: PDW 防火墙配置的分析平台系统 |Microsoft 文档
description: SQL Server PDW 配置管理器中的防火墙页，可启用或禁用防火墙规则，允许或阻止访问分析平台系统设备上的特定端口。
aauthor: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3195007b4346c6010b416fae833643f3a80136fb
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909837"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>分析平台系统中的并行数据仓库防火墙配置
**防火墙**页上的 SQL Server PDW 配置管理器，可启用或禁用防火墙规则，允许或阻止访问分析平台系统设备上的特定端口。  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>若要管理端口和防火墙规则的设备节点  
  
1.  启动配置管理器。 有关详细信息，请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在配置管理器的左窗格中，展开**并行数据仓库拓扑**，然后单击**防火墙**。  
  
3.  找到要更新的配置列表中，然后选中或清除该项旁边的框的端口或防火墙规则。 SQL Server PDW 管理员可配置选项显示在此列表中，包括打开和关闭面向外部的节点上的端口。  
  
4.  单击**应用**以保存所做的更改。  
  
![DWConfig 工具 PDW 防火墙](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>外部端口  
打开以下端口，以便客户端连接来自外部 PDW。  
  
|用途|端口 #|节点|  
|-----------|-----------|---------|  
|SQL 客户端访问的 PDW (TDS)|17001|CTL|  
|加载程序客户端访问 （dwloader 和 SSIS）|8001|CTL|  
|远程桌面访问|3389|CTL CMP|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL 加密连接 （进行内部通信，以访问管理控制台）|443|所有节点|  
|SQL Server PDW 负载控制流的 Windows 凭据|8002|CTL|  
|Kerberos （_k)|88|AD01 和 AD02，|  
|_ldap|389|AD01 和 AD02|  
  
## <a name="internal-ports"></a>内部端口  
以下端口由 PDW 用于内部通信，但未打开用于来自外部 PDW 设备的连接。  
  
|用途|端口 #|节点|  
|-----------|-----------|---------|  
|DMS 控制通道流量|16450|CTL CMP|  
|DMS 数据通道通信|16550|CTL CMP|  
|内部诊断|16650|CTL CMP|  
|故障转移状态 (DMS)|15000|CTL CMP|  
|故障转移状态 （引擎）|15001|CMP|  
|动态 （临时） 端口范围|20000-65535|CTL CMP|  
|SQL Server 端口范围 (TDS)|1433, 1500-1508|CTL CMP|  
  
> [!NOTE]  
> 创建外部表或外部数据源将使用默认的 TCP 端口 8020。 这些语句可以配置为改为使用其他端口。 Hortonworks JOB_TRACKER_LOCATION 默认端口为 50300。 与其他系统和工具集成可能需要其他端口。  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)  -->  
  
