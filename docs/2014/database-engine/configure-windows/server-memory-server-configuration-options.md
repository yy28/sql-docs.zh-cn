---
title: “服务器内存”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Virtual Memory Manager
- max server memory option
- virtual memory [SQL Server]
- VMM
- server memory options [SQL Server]
- servers [SQL Server], memory
- buffer pools [SQL Server]
- min server memory option
- manual memory options [SQL Server]
- memory [SQL Server], servers
ms.assetid: 29ce373e-18f8-46ff-aea6-15bbb10fb9c2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c366a239ca3459bc8fe4517736a4c0bcc64301cb
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68475967"
---
# <a name="server-memory-server-configuration-options"></a>“服务器内存”服务器配置选项
  使用“min server memory”和“max server memory”这两个服务器内存选项可以重新配置由 SQL Server 内存管理器为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例使用的 SQL Server 进程所管理的内存量 (MB)。  
  
 **min server memory** 的默认设置为 0， **max server memory** 的默认设置为 2147483647 MB。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内存要求会根据可用系统资源的情况动态变化。  
  
> [!NOTE]  
>  将 **max server memory** 设置为最小值可能会严重降低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 性能，甚至导致无法启动。 如果在更改此选项之后无法启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请使用“-f”启动选项启动它，并将“max server memory”重置为以前的值。 有关详细信息，请参阅 [Database Engine Service Startup Options](database-engine-service-startup-options.md)。  
  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 动态使用内存时，它会定期查询系统以确定可用内存量。 保持此可用内存可避免操作系统 (OS) 进行分页。 如果可用内存较少， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将会释放内存以供操作系统使用。 如果有更多的内存可用， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会分配更多的内存。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仅在其工作负荷需要更多内存时才增加内存；空闲的服务器不会增加其虚拟地址空间的大小。  
  
 请参阅查询的示例 B 以返回当前使用的内存。 **最大服务器内存** 控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存分配，包括缓冲池、编译内存、所有缓存、QE 内存授权、锁管理器内存和 CLR 内存（实质上是 **sys.dm_os_memory_clerks**中存在的所有内存分配器）。 线程堆栈的内存、内存堆、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之外的联接的服务器提供程序以及非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL 分配的所有内存均不由最大服务器内存控制。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用内存通知 API **QueryMemoryResourceNotification** 来确定 SQL Server 内存管理器何时可以分配内存和释放内存。  
  
 建议允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 动态使用内存；但可以手动设置内存选项并限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以访问的内存量。 在设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的内存量之前，请通过从总物理内存中减去操作系统和任何其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所需的内存（如果计算机并非完全由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]专用，则还要减去其他系统使用的内存量）来确定适当的内存设置。 这个差值就是可以分配给 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的最大内存量。  
  
## <a name="setting-the-memory-options-manually"></a>手动设置内存选项  
可以将 min server memory 和 max server memory 设置成一个内存范围。 在需要兼顾同一台主机上运行的其他应用程序或其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的内存要求时，此方法对于配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的系统或数据库管理员来说非常有用。

> [!NOTE]
> **min server memory** 和 **max server memory** 选项都是高级选项。 如果使用 **sp_configure** 系统存储过程来更改这些设置，则只有在“显示高级选项”设置为 1 时才能更改它们。 这些设置更改后会立即生效，不需要重新启动服务器。  
  
<a name="min_server_memory"></a> 使用 min_server_memory 可以保证可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存管理器使用的最小内存量。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会在启动时立即分配 **min server memory** 中指定的内存量。 不过，除非降低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] min server memory **的值，否则当内存使用量由于客户端负荷而达到该值后，** 不能释放内存。 例如，同一个主机中可同时存在多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，为了给实例保留内存，请设置 min_server_memory 参数而不是 max_server_memory。 此外，为了确保来自基础主机的内存压力不会尝试从来宾 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 虚拟机 (VM) 上的缓冲池释放超过可接受性能所需的内存，在虚拟环境中设置 min_server_memory 值非常必要。
 
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并不一定分配“最小服务器内存”中指定的内存量。 如果服务器上的负荷从不需要分配 **min server memory**指定的内存量，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将以较少的内存运行。  
  
<a name="max_server_memory"></a> 使用 max_server_memory 来保证 OS 不会遇到不利的内存压力。 若要设置 max server memory 配置，请监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的总体消耗，以确定内存要求。 使单个实例的这些计算更准确：
 -  从 OS 总内存中，为 OS 自身保留 1GB - 4GB。
 -  然后减去等于“max server memory”控制之外的潜在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存分配的值，即_堆栈大小 <sup>1</sup> \* 计算出的最大工作线程数 <sup>2</sup> + -g 启动参数 <sup>3</sup>（如果未设置 -g，则为 256 MB）_ 。 所得结果就是一个实例设置的 max_server_memory 设置。
 
<sup>1</sup> 有关每个体系结构的线程堆栈大小的信息，请参阅[内存管理体系结构指南](https://docs.microsoft.com/sql/relational-databases/memory-management-architecture-guide#stacksizes)。

<sup>2</sup> 有关为当前主机中给定数量的关联 CPU 计算得出的默认工作线程数的信息，请参阅介绍如何[配置最大工作线程数服务器配置选项](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)的文档页。

<sup>3</sup> 有关 -g 启动参数的信息，请参阅介绍[数据库引擎服务启动选项](../../database-engine/configure-windows/database-engine-service-startup-options.md)的文档页。 Aplicable 仅适用于32位[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]到[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。

|操作系统类型|**最大服务器内存**允许的最小内存量|  
|-------------|----------------------------------------------------------------|  
|32 位|64 MB|  
|64 位|128 MB| 

## <a name="how-to-configure-memory-options-using-sql-server-management-studio"></a>如何使用 SQL Server Management Studio 配置内存选项  
 使用“min server memory”和“max server memory”这两个服务器内存选项可以重新配置由 SQL Server 内存管理器为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所管理的内存量 (MB)。 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内存要求会根据可用系统资源的情况动态变化。  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory"></a>配置固定内存量的过程  
 **设置固定的内存量:**  
  
1.  在对象资源管理器中，右键单击服务器并选择 **“属性”** 。  
  
2.  单击 **“内存”** 节点。  
  
3.  在 **“服务器内存选项”** 中，为 **“最小服务器内存”** 和 **“最大服务器内存”** 输入所需的内存量。  
  
     使用默认设置，将允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根据可用系统资源动态更改其内存需求。 “min server memory”的默认设置为 0，“max server memory”的默认设置为 2147483647 MB。  
  
## <a name="maximize-data-throughput-for-network-applications"></a>最大化网络应用程序数据吞吐量  
 若要优化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的系统内存使用情况，应该限制系统用于文件缓存的内存量。 若要限制文件系统缓存，请确保未选择 **“最大化文件共享数据吞吐量”** 。 通过选择 **“最小化使用的内存”** 或 **“平衡”** ，可以指定最小文件系统缓存。  
  
#### <a name="to-check-the-current-setting-on-your-operating-system"></a>检查操作系统的当前设置  
  
1.  依次单击“开始”和“控制面板”，双击“网络连接”，然后双击“本地连接”。  
  
2.  在 **“常规”** 选项卡上，单击 **“属性”** ，选择 **“Microsoft 网络的文件和打印机共享”** ，然后单击 **“属性”** 。  
  
3.  如果选中了 **“最大化网络应用程序数据吞吐量”** ，请任选一个相应的其他选项，单击 **“确定”** ，再关闭其余对话框。  
  
## <a name="lock-pages-in-memory"></a>锁定内存页  
 此 Windows 策略将确定哪些帐户可以使用进程将数据保留在物理内存中，从而阻止系统将数据分页到磁盘的虚拟内存中。 锁定内存中的页可以在发生将内存分页到磁盘时保持服务器的响应能力。 如果已向有权运行 sqlservr.exe 的帐户授予 Windows "锁定内存页" (LPIM) 用户权限[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , 则在32位和64位的 Standard edition 和更高版本中, "SQL Server**锁定内存页**" 选项设置为 ON。 在 SQL Server 的早期版本中，为 32 位的 SQL Server 实例设置“锁定页”选项时，需要有权运行 sqlservr.exe 的帐户具有 LPIM 用户权限并且将“awe_enabled”配置选项设置为 ON。  
  
 若要禁用 "**锁定内存页**" 选项[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 请删除 SQL Server 启动帐户的 "锁定内存页" 用户权限。  
  
### <a name="to-disable-lock-pages-in-memory"></a>禁用“锁定内存页”  
 **禁用 "锁定内存页" 选项:**  
  
1.  在 **“开始”** 菜单上，单击 **“运行”** 。 在 "**打开**" 框中`gpedit.msc`, 键入。  
  
     将打开 **“组策略”** 对话框。  
  
2.  在 **“组策略”** 控制台上，展开 **“计算机配置”** ，再展开 **“Windows 设置”** 。  
  
3.  展开 **“安全设置”** ，再展开 **“本地策略”** 。  
  
4.  选择 **“用户权利指派”** 文件夹。  
  
     细节窗格中随即显示出策略。  
  
5.  在该窗格中，双击“锁定内存页”。  
  
6.  在 **“本地安全策略设置”** 对话框中，选择有权运行 sqlservr.exe 的帐户，然后单击 **“删除”** 。  
  
## <a name="virtual-memory-manager"></a>虚拟内存管理器  
 在 32 位操作系统中，可以访问 4 GB 的虚拟地址空间。 2 GB 的虚拟内存专用于进程，由应用程序使用。 2 GB 保留给操作系统使用。 所有操作系统版本都包含一个开关，该开关允许应用程序访问多达 3 GB 的虚拟地址空间，从而将操作系统使用的内存限制为 1 GB。 有关如何使用开关内存配置的详细信息，请参阅介绍 4 GB 优化的 Windows 文档。 当 32 位 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 运行在 64 位操作系统上时，其用户可用虚拟地址空间为整个 4 GB。  
  
 提交的地址空间区域由 Windows 虚拟内存管理器 (VMM) 映射到可用的物理内存。  
  
 有关不同操作系统所支持的物理内存量的详细信息，请参阅 Windows 文档“Windows 版本的内存限制”。  
  
 虚拟内存系统允许虚拟内存超过物理内存，这样虚拟内存与物理内存的比率可以大于 1:1。 因此，大型程序在计算机上运行时可以具有多种物理内存配置。 但是，使用比所有进程的平均组合工作集大得多的虚拟内存可能会导致性能降低。  
  
 **min server memory** 和 **max server memory** 选项都是高级选项。 如果使用 **sp_configure** 系统存储过程来更改这些设置，则只有在“显示高级选项”设置为 1 时才能更改它们。 这些设置更改后会立即生效，不需要重新启动服务器。  
  
## <a name="running-multiple-instances-of-sql-server"></a>运行多个 SQL Server 实例  
 当运行多个 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例时，可以使用三种方法来管理内存：  
  
-   使用 **max server memory** 控制内存使用量。 为每个实例建立最大设置，注意总的允许设置值不能大于计算机上的物理总内存。 可能需要为每个实例提供与预期的工作负荷或数据库大小成正比的内存。 这种方法的优势体现在：当启动新的进程或实例时，可以立即为这些进程或实例提供可用内存。 这种方法的缺点为：如果没有运行所有实例，则所有运行中的实例都无法使用剩余的可用内存。  
  
-   使用 **min server memory** 控制内存使用量。 为每个实例建立最小设置，以使这些最小值的和比计算机上总的物理内存小 1-2 GB。 此外，可能需要建立与该实例的预期负荷成正比的最小值。 这种方法的优势体现在：如果没有同时运行所有实例，则运行中的实例可以使用剩余的可用内存。 当计算机上存在其他占用大量内存的进程时，这种方法也十分有用，因为它可确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 至少获得合理的内存量。 这种方法的缺点是：当启动新的实例（或任何其他进程）时，运行的实例可能会花费一些时间来释放内存，如果实例必须将修改后的页写回到数据库中来释放内存，则花费的时间可能会更长。  
  
-   不执行任何操作（不推荐）。 带有工作负荷的第一个实例通常分配所有的内存。 空闲实例或稍后启动的实例最终可能会只使用最少的可用内存量运行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会尝试均衡分配各个实例的内存使用量。 但是，所有实例均将响应 Windows 内存通知信号以调整它们内存需求量的大小。 Windows 不会使用内存通知 API 来平衡各个应用程序使用的内存。 它只提供有关系统内存可用性的全局反馈。  
  
 您可以在不重新启动实例的情况下更改这些设置，以便可以轻松地进行尝试以找到适合使用模式的最佳设置。  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>为 SQL Server 提供最大内存量  
  
||32 位|64 位|  
|-|-------------|-------------|  
|常规内存|所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的最大进程虚拟地址空间限制：<br /><br /> 2 GB<br /><br /> 3 GB, 带有 **/3gb** boot 参数 *<br /><br /> 4 GB, 在 WOW64 上\*\*|所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的最大进程虚拟地址空间限制：<br /><br /> 8 TB，在 x64 体系结构上|  
  
 * **/3gb** 是一个操作系统的启动参数。 有关详细信息，请访问 [MSDN Library](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409)。  
  
 \* * WOW64 (windows on windows 64 上的 windows) 是一个 32 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在64位操作系统上运行的一种模式。 有关详细信息，请访问 [MSDN Library](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409)。  
  
## <a name="examples"></a>示例  
  
### <a name="example-a"></a>示例 A  
 以下示例将 `max server memory` 选项设置为 4 GB：  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'max server memory', 4096;  
GO  
RECONFIGURE;  
GO  
```  
  
### <a name="example-b-determining-current-memory-allocation"></a>示例 B. 确定当前内存分配  
 以下查询返回有关当前分配内存的信息。  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
## <a name="see-also"></a>请参阅  
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
