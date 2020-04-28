---
title: 连接到设备节点
description: 本文介绍连接到 Analytics Platform System 设备中每个节点的各种方式。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e1182d174e3281fda944c0b6490b114d4b6f2244
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401238"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>在分析平台系统中连接到设备节点
本文介绍连接到 Analytics Platform System 设备中每个节点的各种方式。  
  
## <a name="connecting-with-hadoop"></a>与 Hadoop 连接  
在将 Hadoop 与 SQL Server PDW 一起使用之前，要求设备管理员将 Java Runtime Environment 安装到 SQL Server PDW 上。 有关说明，请参阅《设备操作指南》中的[配置与外部数据的 PolyBase 连接 &#40;分析平台系统&#41;](configure-polybase-connectivity-to-external-data.md) 。  
  
## <a name="connecting-to-appliance-nodes"></a><a name="ConnectingToIndividualNodes"></a>连接到设备节点  
每个设备节点仅在特定使用方案和特定用户类型下直接访问。 下表列出了每个设备节点以及用户将直接连接到该节点的情况。  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> 更改控件或计算节点上的数据库或表设置，而无需明确同意产品团队或 AP 客户支持团队可能会导致你的 AP 设备不受支持。
  
|||  
|-|-|  
|**节点**|**访问方案**|  
|控制节点|使用 web 浏览器访问在控制节点上运行的管理控制台。 有关详细信息，请参阅[使用管理控制台监视设备 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />所有客户端应用程序和工具均连接到控制节点，无论连接是使用以太网还是不受控制。<br /><br />若要配置到控制节点的以太网连接，请使用控制节点群集 IP 地址和端口**17001**。 例如，"192.168.0.1，17001"。<br /><br />若要配置到控制节点的未连接连接，请使用<strong> *appliance_domain*SQLCTL01</strong>和端口**17001**。 通过使用<strong> *appliance_domain*-SQLCTL01</strong>，设备的 DNS 服务器会将服务器连接到活动的未受服务网络。 若要将非设备服务器配置为使用此设置，请参阅配置不工作[网络适配器](configure-infiniband-network-adapters.md)。<br /><br />设备管理员连接到控制节点以执行管理操作。 例如，设备管理员从控制节点执行以下操作：<br /><br />配置**dwconfig**配置工具的分析平台系统。|  
|计算节点|计算节点连接由控制节点定向。 计算节点的 IP 地址永远不会作为参数输入到应用程序命令中。<br /><br />对于加载、备份、远程表复制和 Hadoop，SQL Server PDW 会直接在计算节点和非设备节点或服务器之间并行发送或接收数据。 这些应用程序通过连接到控件节点来连接 SQL Server PDW，然后，控制节点会指导 SQL Server PDW 在计算节点和非设备服务器之间建立通信。<br /><br />例如，这些数据传输操作与计算节点的直接连接并行发生：<br /><br />正在从加载服务器加载到 SQL Server PDW。<br /><br />将数据库从 SQL Server PDW 备份到备份服务器。<br /><br />将数据库从备份服务器还原到 SQL Server PDW。<br /><br />查询 SQL Server PDW 中的 Hadoop 数据。<br /><br />将数据从 SQL Server PDW 导出到外部 Hadoop 表。<br /><br />将 SQL Server PDW 表复制到远程 SMP SQL Server 数据库。|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>连接到以太网和不工作网络  
远程服务器可以通过设备设备网络或通过以太网网络进行连接。 出于性能原因，通过将**远程表创建为 SELECT**语句来加载服务器、备份服务器和服务器接收数据，通常通过设备的 "无线传输" 网络传输数据。  
  
你可以将非设备服务器配置为属于你自己的客户工作组或域，然后使用你自己的客户网络连接到这些服务器，并将数据传输到这些服务器。 而且，连接到设备的非设备服务器也可以选择在设备的 "无线传输" 网络上互相传输数据;请注意这一点，因为这会降低 SQL Server PDW 的性能。  
  
例如，此语句将添加网络凭据，以通过不使用的备份服务器执行备份，使 IP 地址为192.168.0.1。 设备域为*mypdw*，并从备份服务器执行该语句。 在运行此语句之前，需要填写自己的参数。  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
例如，加载命令将从以下内容开始：  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
