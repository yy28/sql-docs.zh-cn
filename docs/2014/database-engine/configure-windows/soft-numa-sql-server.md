---
title: 将 SQL Server 配置为使用软件 NUMA （SQL Server） |Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- non-uniform memory access
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ae4bcd90b17228283859e2dd1a2897406e8ea95f
ms.sourcegitcommit: 5a9ec5e28543f106bf9e7aa30dd0a726bb750e25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82924771"
---
# <a name="configure-sql-server-to-use-soft-numa-sql-server"></a>将 SQL Server 配置为使用软件 NUMA (SQL Server)
当今的处理器在每个插槽上都有多个内核。 通常每个插槽表示为单个 NUMA 节点。 SQL Server 数据库引擎在每个 NUMA 节点上划分多个不同内部结构和分区服务线程。 对于每个插槽包含10个或更多内核的处理器，使用软件 NUMA （软 NUMA）拆分硬件 NUMA 节点通常可以提高可伸缩性和性能。   

> [!NOTE]
> 软件 NUMA 不支持热添加处理器。
  
## <a name="automatic-soft-numa"></a>自动软件 NUMA
从 SQL Server 2014 Service Pack 2 开始，每当数据库引擎服务器在启动时检测到8个以上的物理处理器时，如果将跟踪标志8079启用为启动参数，就会自动创建软件 NUMA 节点。 对物理处理器进行计数时，不考虑超线程处理器核心。 当检测到的物理处理器数超过每个套接字8个时，数据库引擎服务将创建理想的软 NUMA 节点，该节点非常适合于8个内核，但每个节点最多可以有5个或多达9个逻辑处理器。 可以通过 CPU 关联掩码限制硬件节点的大小。 NUMA 节点数永远不会超过支持的 NUMA 节点的最大数目。

如果没有跟踪标志，则默认情况下禁用软件 NUMA。 可以使用跟踪标志8079启用软件 NUMA。 更改此设置的值后，需要重新启动数据库引擎才会生效。

下图显示了在 SQL Server 检测到硬件 NUMA 节点的逻辑处理器多于8个且启用了跟踪标志8079时，将在 SQL Server 错误日志中看到的关于软件 NUMA 的信息类型。

![ssNoVersion](./media/soft-numa-sql-server/soft-numa.PNG)

> [!NOTE]
> 从 SQL Server 2016 开始，此行为由引擎控制，跟踪标志8079不起作用。

## <a name="manual-soft-numa"></a>手动软件 NUMA
  
若要将配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为手动使用软件 NUMA，必须编辑注册表以添加节点配置关联掩码。 软件 NUMA 掩码可以表示为二进制、DWORD（十六进制或十进制）或 QWORD（十六进制或十进制）注册表项。 若要配置头 32 个 CPU 以后的 CPU，请使用 QWORD 或 BINARY 注册表值。 （在之前不能使用 QWORD 值 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 。）必须重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 才能配置软件 NUMA。  
  
> [!TIP]  
>  CPU 从 0 开始编号。  
  
 [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 请看下面的示例。 计算机有八个 CPU，但没有硬件 NUMA。 配置了三个软件 NUMA 节点。 将[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例 A 配置为使用第 0 个到第 3 个 CPU。 安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的第二个实例并将其配置为使用第 5 个到第 8 个 CPU。 该示例可以直观表示为：  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 大量使用 I/O 的实例 A 现在有两个 I/O 线程和一个惰性编写器线程，执行大量占用处理器操作的实例 B 仅有一个 I/O 线程和一个惰性编写器线程。 可以向实例分配不同的内存量，但是与硬件 NUMA 不同，它们都从同一个操作系统内存块中接收内存，并且不具有从内存到处理器的关联。  
  
 惰性编写器线程与物理 NUMA 内存节点的 SQL 操作系统视图有关。 因此，不管存在什么硬件，物理 NUMA 节点将等于创建的惰性编写器线程数。 有关详细信息，请参阅 [软件 NUMA、I/O 完成线程、惰性编写器工作线程和内存节点的工作机制](https://docs.microsoft.com/archive/blogs/psssql/how-it-works-soft-numa-io-completion-thread-lazy-writer-workers-and-memory-nodes)。  
  
> [!NOTE]  
>  升级 **的实例时，不复制** Soft-NUMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]注册表项。  
  
### <a name="set-the-cpu-affinity-mask"></a>设置 CPU 关联掩码  
  
1.  在实例 A 中运行下面的语句，通过设置 CPU 关联掩码将它配置为使用 CPU 0、CPU 1、CPU 2 和 CPU 3：  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=0 TO 3;  
    ```  
  
2.  在实例 B 中运行下面的语句，通过设置 CPU 关联掩码将它配置为使用 CPU 4、CPU 5、CPU 6 和 CPU 7：  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=4 TO 7;  
    ```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>将软件 NUMA 节点映射到 CPU  
  
-   使用注册表编辑器程序 (regedit.exe) 添加以下注册表项，从而将软件 NUMA 节点 0 映射到 CPU 0 和 CPU 1、将软件 NUMA 节点 1 映射到 CPU 2 和 CPU 3，以及将软件 NUMA 节点 2 映射到 CPU 4、 CPU 5、CPU 6 和 CPU 7。  
  
     在以下示例中，假定你有 DL580 G9 服务器，每个套接字（共 4 个套接字）具有 18 个核并且每个套接字都位于其自己的 K 组中。 你可能创建的 Soft-NUMA 配置将如下所示。 （每个节点 6 个核，每组 3 个节点，共 4 组）。  
  
    |具有多个 K 组的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 服务器示例|类型|值名称|“数值数据”|  
    |------------------------------------------------------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|组|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|组|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|组|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|组|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|组|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|组|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|组|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|组|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|组|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|组|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|组|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|组|3|  
  
     其他示例：  
  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|类型|值名称|“数值数据”|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|组|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|组|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|组|0|  
  
    > [!TIP]  
    >  若要指定 CPU 60 到 63，请使用 QWORD 值 F000000000000000 或 BINARY 值 1111000000000000000000000000000000000000000000000000000000000000。  
  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|类型|值名称|“数值数据”|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|组|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|组|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|组|0|  
  
    |SQL Server 2008 R2|类型|值名称|“数值数据”|  
    |------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|组|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|组|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|组|0|  
  
    |SQL Server 2008|类型|值名称|“数值数据”|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
    |SQL Server 2005|类型|值名称|“数值数据”|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
## <a name="see-also"></a>另请参阅  
 [将 TCP IP 端口映射到 NUMA 节点 &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [关联掩码服务器配置选项](affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
