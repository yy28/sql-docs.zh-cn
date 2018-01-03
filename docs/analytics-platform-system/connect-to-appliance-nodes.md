---
title: "连接到设备的节点 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f975aa91-c816-4b29-89bf-923ab5b4abb4
caps.latest.revision: "19"
ms.openlocfilehash: 8d7a6f0def6b7cedb5bf7a7306fd10a3f167335e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="connect-to-appliance-nodes"></a>连接到设备节点
本主题说明连接到分析平台系统设备在每个节点的各种方法。  
  
## <a name="connecting-with-hadoop"></a>使用 Hadoop 连接  
然后才能使用 Hadoop 以 SQL Server PDW，要求设备管理员安装到 SQL Server PDW Java 运行时环境。 有关说明，请参阅[配置 PolyBase 连接到外部数据 &#40;分析平台系统 &#41;](configure-polybase-connectivity-to-external-data.md)中的设备操作指南。  
  
## <a name="ConnectingToIndividualNodes"></a>连接到设备节点  
可直接访问每个设备节点仅在特定使用方案和由特定用户类型。 下表列出每个设备节点并在其下用户将直接连接到该节点的方案。  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  
  
|||  
|-|-|  
|**Node**|**访问控制方案**|  
|控制节点|使用 web 浏览器访问管理控制台中，在管理节点运行。 有关详细信息，请参阅[使用管理控制台 &#40; 监视设备分析平台系统 &#41;](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />所有客户端应用程序和工具连接到控制节点，无论连接使用以太网或无线带宽。<br /><br />若要配置以太网连接到管理节点，使用的控制节点的群集 IP 地址和端口**17001**。 例如，"192.168.0.1,17001"。<br /><br />若要配置 InfiniBand 连接到管理节点，使用 ***appliance_domain*-SQLCTL01**和端口**17001**。 通过使用 ***appliance_domain*-SQLCTL01**，设备 DNS 服务器将连接到活动的 InfiniBand 网络的你的服务器。 若要配置你的非设备服务器以使用此，请参阅[配置无线带宽技术网络适配器](configure-infiniband-network-adapters.md)。<br /><br />设备管理员连接到管理节点以执行管理操作。 例如，设备管理员从管理节点中执行以下操作：<br /><br />配置分析平台系统**dwconfig.exe**配置工具。|  
|计算节点|计算节点连接定向由控制节点。 计算节点的 IP 地址将永远不会输入到应用程序命令中，作为参数。<br /><br />用于加载，备份，远程表复制，和 Hadoop、 SQL Server PDW 不发送或接收直接在并行计算节点和非设备节点或服务器之间的数据。 这些应用程序通过连接到管理节点中，连接 SQL Server PDW 和控制节点然后引导 SQL Server PDW 的计算节点和非设备服务器之间建立通信。<br /><br />例如，这些数据传输操作发生在与直接连接到计算节点并行：<br /><br />从加载服务器加载到 SQL Server PDW。<br /><br />备份数据库从 SQL Server PDW 到备份服务器。<br /><br />备份服务器的数据库还原到 SQL Server PDW 中。<br /><br />查询 Hadoop 数据从 SQL Server PDW。<br /><br />将数据从 SQL Server PDW 导出到外部 Hadoop 表。<br /><br />如果将 SQL Server PDW 表复制到远程 SMP SQL Server 数据库。|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>连接到的以太网和 InfiniBand 网络  
通过设备 InfiniBand 网络或通过以太网网络，可以连接远程服务器。 进行性能原因，加载服务器，备份服务器，以及服务器接收数据通过**远程 TABLE AS SELECT**语句，通常将通过设备 InfiniBand 网络的数据传输。  
  
你可以非设备将服务器配置为属于自己的客户工作组或域，以及如何将客户网络以连接到这些服务器和将数据转移到它们。 此外，非设备连接到服务器设备 InfiniBand 有通过设备 InfiniBand 网络; 将数据传输到每个其他选项因为这会降低 SQL Server PDW 的性能，则请慎用此。  
  
例如，此语句将添加用于执行通过 InfiniBand 给 InfiniBand IP 地址 192.168.0.1 备份服务器备份的网络凭据。 设备域是*mypdw*，和从备份服务器执行语句。 运行此语句，你需要填写您自己的参数。  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
例如，加载命令将启动替换为以下内容：  
  
```  
dwloader –S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
