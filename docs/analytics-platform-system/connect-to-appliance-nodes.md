---
title: 连接到设备节点的分析平台系统 |Microsoft Docs
description: 此文章介绍了连接到分析平台系统设备的每个节点的各种方法。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 873ce3cf5ad2707979d66068b3930d6f59f7057c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66186796"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>连接到分析平台系统中的设备节点
此文章介绍了连接到分析平台系统设备的每个节点的各种方法。  
  
## <a name="connecting-with-hadoop"></a>使用 Hadoop 连接  
将 Hadoop 与 SQL Server PDW 中使用之前, 要求设备管理员安装到 SQL Server PDW 上的 Java 运行时环境。 有关说明，请参阅[配置到外部数据的 PolyBase 连接&#40;Analytics Platform System&#41; ](configure-polybase-connectivity-to-external-data.md)设备操作指南 》 中。  
  
## <a name="ConnectingToIndividualNodes"></a>连接到设备节点  
可直接访问每个设备节点仅在特定应用场景下，由特定用户类型。 下表列出了每个设备节点以及在其下的用户将直接连接到该节点的方案。  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> 更改数据库或表设置，而无需明确许可的产品团队或 AP 客户支持团队的控件或计算节点上可能会导致不支持将 APS 设备。
  
|||  
|-|-|  
|**Node**|**访问控制方案**|  
|控制节点|使用 web 浏览器访问管理控制台中，在控制节点运行。 有关详细信息，请参阅[通过使用管理控制台监视设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />所有客户端应用程序和工具连接到控制节点，无论连接使用以太网或 InfiniBand。<br /><br />若要配置以太网连接到控制节点，使用的控制节点的群集 IP 地址和端口**17001**。 例如，"192.168.0.1,17001"。<br /><br />若要配置到控制节点的 InfiniBand 连接，请使用 <strong>*appliance_domain*-SQLCTL01</strong>和端口**17001**。 通过使用 <strong>*appliance_domain*-SQLCTL01</strong>，设备 DNS 服务器会将服务器连接到活动的 InfiniBand 网络。 若要配置非设备服务器以使用此选项，请参阅[配置无线带宽技术网络适配器](configure-infiniband-network-adapters.md)。<br /><br />设备管理员连接到控制节点，以执行管理操作。 例如，设备管理员从控制节点执行以下操作：<br /><br />配置使用的分析平台系统**dwconfig.exe**配置工具。|  
|计算节点|计算节点连接将定向由控制节点。 计算节点的 IP 地址永远不会作为参数输入到应用程序的命令。<br /><br />对于加载，备份、 远程表复制和 Hadoop 和 SQL Server PDW 不发送或接收直接并行计算节点和非设备节点或服务器之间的数据。 这些应用程序通过连接到控制节点中，使用 SQL Server PDW 连接和控制节点然后指示 SQL Server PDW 的计算节点和非设备服务器之间建立通信。<br /><br />例如，这些数据传输操作的操作以并行方式直接连接到计算节点：<br /><br />从加载服务器加载到 SQL Server PDW。<br /><br />备份数据库从 SQL Server PDW 到备份服务器。<br /><br />备份服务器将数据库还原到 SQL Server PDW 中。<br /><br />从 SQL Server PDW 查询 Hadoop 数据。<br /><br />SQL Server PDW 数据导出到外部 Hadoop 表中。<br /><br />如果将 SQL Server PDW 表复制到远程 SMP SQL Server 数据库。|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>连接到以太网和 InfiniBand 网络  
远程服务器可以通过设备 InfiniBand 网络或通过以太网网络连接。 由于性能原因，正在加载服务器，备份服务器，以及服务器接收数据通过**REMOTE TABLE AS SELECT**语句，通常将通过设备 InfiniBand 网络数据传输。  
  
您可以将非设备服务器属于您自己的客户工作组或域中，配置为，然后使用客户网络来连接到这些服务器和将数据转移到它们。 此外，非设备服务器连接到设备 InfiniBand 可以选择将数据传输到彼此，通过设备 InfiniBand 网络;要与此小心因为它会降低 SQL Server PDW 的性能。  
  
例如，此语句将添加执行到 InfiniBand IP 地址 192.168.0.1 备份服务器备份通过 InfiniBand 的网络凭据。 设备域是*mypdw*，并从备份服务器执行该语句。 运行此语句，您需要填写您自己的参数。  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
例如，加载命令将启动与以下：  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
