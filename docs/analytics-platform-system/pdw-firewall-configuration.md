---
title: PDW 防火墙配置
description: 利用 SQL Server PDW Configuration Manager 的 "防火墙" 页，您可以启用或禁用允许或阻止访问分析平台系统设备上的特定端口的防火墙规则。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ed739ce12170aa6d0ab79b996de0075cd6723ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400884"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>分析平台系统中的并行数据仓库防火墙配置

利用 SQL Server PDW Configuration Manager 的 "**防火墙**" 页，您可以启用或禁用允许或阻止访问分析平台系统设备上的特定端口的防火墙规则。  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>管理设备节点的端口和防火墙规则  
  
1.  启动 Configuration Manager。 有关详细信息，请参阅[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)。  
  
2.  在 Configuration Manager 的左窗格中，展开 "**并行数据仓库拓扑**"，然后单击 "**防火墙**"。  
  
3.  在配置列表中找到要更新的端口或防火墙规则，然后选中或清除该项旁边的框。 此列表中仅显示 SQL Server PDW 管理员可配置的选项，包括在面向外部的节点上打开和关闭端口。  
  
4.  单击 "**应用**" 以保存所做的更改。  
  
![DWConfig 工具 PDW 防火墙](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>外部端口  
对于来自 PDW 之外的客户端连接，将打开以下端口。  
  
|目的|口#|Nodes|  
|-----------|-----------|---------|  
|PDW 的 SQL 客户端访问（TDS）|17001|CTL|  
|加载程序客户端访问（dwloader & SSIS）|8001|CTL|  
|远程桌面访问|3389|CTL、CMP|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL 加密连接（用于内部通信），用于访问管理控制台|443|所有节点|  
|SQL Server PDW 负载控制流-Windows 凭据|8002|CTL|  
|_Kerberos|88|AD01 和 AD02，|  
|_ldap|389|AD01 和 AD02|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>内部端口  
PDW 使用以下端口进行内部通信，但不会为来自 PDW 设备之外的连接打开。  
  
|目的|口#|Nodes|  
|-----------|-----------|---------|  
|DMS 控制通道流量|16450|CTL、CMP|  
|DMS 数据通道流量|16550|CTL、CMP|  
|内部诊断|16650|CTL、CMP|  
|故障转移状态（DMS）|15000|CTL、CMP|  
|故障转移状态（引擎）|15001|CMP|  
|动态（临时）端口范围|20000-65535|CTL、CMP|  
|SQL Server 端口范围（TDS）|1433、1500-1508|CTL、CMP|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> 默认情况下，创建外部表或外部数据源会使用 TCP 端口8020。 这些语句可以配置为使用其他端口。 Hortonworks JOB_TRACKER_LOCATION 默认端口为50300。 与其他系统和工具集成可能需要更多端口。  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
