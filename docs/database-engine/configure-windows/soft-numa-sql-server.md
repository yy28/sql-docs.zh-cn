---
title: "软件 NUMA (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- NUMA
- soft-NUMA
helpviewer_keywords:
- NUMA
- non-uniform memory access
- soft-NUMA
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
caps.latest.revision: 53
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2f57a1d59210a002ebd03b04be4158e514e725cd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="soft-numa-sql-server"></a>软件 NUMA (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  当今的处理器在每个插槽上都有多个内核。 通常每个插槽表示为单个 NUMA 节点。 SQL Server 数据库引擎在每个 NUMA 节点上划分多个不同内部结构和分区服务线程。  借助每个插槽包含 10 个或更多内核的处理器，使用软件 NUMA 拆分硬件 NUMA 节点通常可以提高可伸缩性和性能。 在 SQL Server 2014 SP2 之前，基于软件的 NUMA (soft-NUMA) 需要编辑注册表才能添加节点配置关联掩码，并且针对每台计算机而不是每个实例进行配置。  使用 SQL Server 2014 SP2 和 SQL Server 2016，当 SQL Server 服务启动时会在数据库实例级别自动配置 soft-NUMA。  
  
> [!NOTE]  
>  软件 NUMA 不支持热添加处理器。  
  
## <a name="automatic-soft-numa"></a>自动软件 NUMA  
 使用 SQL Server 2016，只要数据库引擎服务器在启动时检测到每个 NUMA 或插槽内的物理内核数目超过 8 个，在默认情况下就会自动创建 soft-NUMA 节点。 计算节点中的物理内核时，不区分超线程处理器内核。  如果检测到每个插槽内的物理内核数目多于 8 个，数据库引擎服务会创建 soft-NUMA 节点，在理想情况下包含 8 个内核，但也可少至每节点 5 个逻辑内核，或多达 9 个。 可以通过 CPU 关联掩码限制硬件节点的大小。 请参阅   
            [ALTER SERVER CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-server-configuration-transact-sql.md)。 NUMA 节点数永远不会超过支持的 NUMA 节点的最大数目。  
  
 你可以使用带有 SET SOFTNUMA 参数的 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) 语句来禁用或重新启用 soft-NUMA。 更改此设置的值后，需要重新启动数据库引擎才会生效。  
  
 SQL Server 检测到硬件 NUMA 节点的每个节点或插槽内物理内核多于 8 个时，此图显示可在 SQL Server 错误日志中看到的关于 soft-NUMA 的信息类型。  


``2016-11-14 13:39:43.17 Server      SQL Server detected 2 sockets with 12 cores per socket and 24 logical processors per socket, 48 total logical processors; using 48 logical processors based on SQL Server licensing. This is an informational message; no user action is required.``  
  **``2016-11-14 13:39:43.35 Server      Automatic soft-NUMA was enabled because SQL Server has detected hardware NUMA nodes with greater than 8 physical cores.``**  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 0: CPU mask: 0x0000000000555555:0 Active CPU mask: 0x0000000000555555:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 1: CPU mask: 0x0000000000aaaaaa:0 Active CPU mask: 0x0000000000aaaaaa:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 2: CPU mask: 0x0000555555000000:0 Active CPU mask: 0x0000555555000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 3: CPU mask: 0x0000aaaaaa000000:0 Active CPU mask: 0x0000aaaaaa000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``

  
## <a name="manual-soft-numa"></a>手动软件 NUMA  
 通过禁用自动 soft_NUMA 并编辑注册表，可手动配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来使用软件 NUMA，以添加节点配置关联掩码。 借助这种方法，软件 NUMA 掩码可以表示为二进制、DWORD（十六进制或十进制）或 QWORD（十六进制或十进制）注册表项。 若要配置头 32 个 CPU 以后的 CPU，请使用 QWORD 或 BINARY 注册表值。 （在低于 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的版本中，不能使用 QWORD 值。）修改注册表后，必须重启 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，soft-NUMA 配置才会生效。  
  
> [!TIP]
> CPU 从 0 开始编号。  

> [!WARNING]
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 请参考如下示例。 计算机有八个 CPU，但没有硬件 NUMA。 配置了三个软件 NUMA 节点。   
            将[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例 A 配置为使用第 0 个到第 3 个 CPU。 安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的第二个实例并将其配置为使用第 5 个到第 8 个 CPU。 该示例可以直观表示为：  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 大量使用 I/O 的实例 A 现在有两个 I/O 线程和一个惰性编写器线程，执行大量占用处理器操作的实例 B 仅有一个 I/O 线程和一个惰性编写器线程。 可以向实例分配不同的内存量，但是与硬件 NUMA 不同，它们都从同一个操作系统内存块中接收内存，并且不具有从内存到处理器的关联。  
  
 惰性编写器线程与物理 NUMA 内存节点的 SQL 操作系统视图有关。 因此，不管存在什么硬件，物理 NUMA 节点将等于创建的惰性编写器线程数。 有关详细信息，请参阅   
            [Soft NUMA、I/O 完成线程、惰性编写器工作线程和内存节点的工作机制](http://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)。  
  
> [!NOTE]
> 升级 **的实例时，不复制** Soft-NUMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]注册表项。  
  
### <a name="set-the-cpu-affinity-mask"></a>设置 CPU 关联掩码  
 在实例 A 中运行下面的语句，通过设置 CPU 关联掩码将它配置为使用 CPU 0、CPU 1、CPU 2 和 CPU 3：  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 3;  
```  
  
 在实例 B 中运行下面的语句，通过设置 CPU 关联掩码将它配置为使用 CPU 4、CPU 5、CPU 6 和 CPU 7：  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=4 TO 7;  
```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>将软件 NUMA 节点映射到 CPU  
 使用注册表编辑器程序 (regedit.exe) 添加以下注册表项，从而将软件 NUMA 节点 0 映射到 CPU 0 和 CPU 1、将软件 NUMA 节点 1 映射到 CPU 2 和 CPU 3，以及将软件 NUMA 节点 2 映射到 CPU 4、 CPU 5、CPU 6 和 CPU 7。  
  
> [!TIP]
> 若要指定 CPU 60 到 63，请使用 QWORD 值 F000000000000000 或 BINARY 值 1111000000000000000000000000000000000000000000000000000000000000。  
  
 在以下示例中，假定你有 DL580 G9 服务器，每个套接字（共 4 个套接字）具有 18 个核并且每个套接字都位于其自己的 K 组中。 你可能创建的 Soft-NUMA 配置将如下所示。 （每个节点 6 个核，每组 3 个节点，共 4 组）。  
  
|具有多个 K 组的 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 服务器示例|类型|值名称|值数据|  
|-----------------------------------------------------------------------------------------------------------------|----------|----------------|----------------|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|分组|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|分组|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|分组|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|分组|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|分组|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|分组|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|分组|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|分组|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|分组|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|分组|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|分组|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|分组|3|  
  
## <a name="metadata"></a>元数据  
 可以使用以下 DMV 来查看软件 NUMA 的当前状态和配置。  
  
-   [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)：显示 SOFTNUMA 的当前值（0 或 1）  
  
-   [sys.dm_os_nodes (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md)：每个 NUMA 节点的 node_state_desc 列将显示节点是否是由 soft-NUMA 创建的。  
  
-   [sys.dm_os_sys_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)：softnuma 和 softnuma_desc 列将显示配置值。  
  
> [!NOTE]
> 虽然可以使用 [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 来查看自动软件 NUMA 的运行值，但不能使用 **sp_configure** 更改其值。 必须使用带有 SET SOFTNUMA 参数的 [ALTER SERVER CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-server-configuration-transact-sql.md) 语句。  
  
## <a name="see-also"></a>另请参阅  
 [将 TCP IP 端口映射到 NUMA 节点 (SQL Server)](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [关联掩码服务器配置选项](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  


