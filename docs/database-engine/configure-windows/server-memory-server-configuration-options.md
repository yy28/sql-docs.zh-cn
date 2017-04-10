---
title: "“服务器内存”服务器配置选项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "虚拟内存管理器"
  - "max server memory 选项"
  - "虚拟内存 [SQL Server]"
  - "VMM"
  - "服务器内存选项 [SQL Server]"
  - "服务器 [SQL Server]，内存"
  - "缓冲池 [SQL Server]"
  - "min server memory 选项"
  - "手动内存选项 [SQL Server]"
  - "内存 [SQL Server]，服务器"
ms.assetid: 29ce373e-18f8-46ff-aea6-15bbb10fb9c2
caps.latest.revision: 78
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 78
---
# “服务器内存”服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用“min server memory”和“max server memory”这两个服务器内存选项可以重新配置由 SQL Server 内存管理器为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例使用的 SQL Server 进程所管理的内存量 (MB)。  
  
 **min server memory** 的默认设置为 0， **max server memory** 的默认设置为 2147483647 MB。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内存要求会根据可用系统资源的情况动态变化。  
  
> [!NOTE]  
>  将 **max server memory** 设置为最小值可能会严重降低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 性能，甚至导致无法启动。 如果在更改此选项之后无法启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请使用 **–f** 启动选项启动它，并将 **max server memory** 重置为以前的值。 有关详细信息，请参阅 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 动态使用内存时，它会定期查询系统以确定可用内存量。 保持此可用内存可避免操作系统 (OS) 进行分页。 如果可用内存较少，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将会释放内存以供操作系统使用。 如果有更多的内存可用， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会分配更多的内存。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仅在其工作负荷需要更多内存时才增加内存；空闲的服务器不会增加其虚拟地址空间的大小。  
  
 请参阅查询的示例 B 以返回当前使用的内存。 **最大服务器内存**控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存分配，包括缓冲池、编译内存、所有缓存、QE 内存授权、锁管理器内存和 CLR 内存（实质上是 **sys.dm_os_memory_clerks** 中存在的所有内存分配器）。 线程堆栈的内存、内存堆、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之外的联接的服务器提供程序以及非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL 分配的所有内存均不由最大服务器内存控制。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用内存通知 API **QueryMemoryResourceNotification** 来确定 SQL Server 内存管理器何时可以分配内存和释放内存。  
  
 建议允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 动态使用内存；但可以手动设置内存选项并限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以访问的内存量。 在设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内存量之前，请通过从总物理内存中减去操作系统和任何其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所需的内存（如果计算机并非完全由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 专用，则还要减去其他系统使用的内存量）来确定适当的内存设置。 这个差值就是可以分配给 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的最大内存量。  
  
## 手动设置内存选项  
 将 **min server memory** 和 **max server memory** 设置成一个内存范围。 在需要兼顾同一台计算机上运行的其他应用程序的内存要求时，此方法对于配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的系统或数据库管理员来说非常有用。  
  
 使用 **min server memory** 可以保证可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的 SQL Server 内存管理器使用的最小内存量。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会在启动时立即分配 **min server memory** 中指定的内存量。 不过，除非降低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] min server memory **的值，否则当内存使用量由于客户端负荷而达到该值后，** 不能释放内存。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并不一定分配 **min server memory**指定的内存量。 如果服务器上的负荷从不需要分配 **min server memory**指定的内存量，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将以较少的内存运行。  
  
 **max server memory** 所允许的最小内存量是 128 MB。  
  
## 如何使用 SQL Server Management Studio 配置内存选项  
 使用“min server memory”和“max server memory”这两个服务器内存选项可以重新配置由 SQL Server 内存管理器为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所管理的内存量 (MB)。 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内存要求会根据可用系统资源的情况动态变化。  
  
### 配置固定内存量的过程  
 设置固定内存量  
  
1.  在对象资源管理器中，右键单击“服务器”并选择“属性”。  
  
2.  单击 **“内存”** 节点。  
  
3.  在 **“服务器内存选项”**中，为 **“最小服务器内存”** 和 **“最大服务器内存”**输入所需的内存量。  
  
     使用默认设置，将允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根据可用系统资源动态更改其内存需求。 “min server memory”的默认设置为 0，“max server memory”的默认设置为 2147483647 MB。  
  
## 最大化网络应用程序数据吞吐量  
 若要优化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的系统内存使用情况，应该限制系统用于文件缓存的内存量。 若要限制文件系统缓存，请确保未选择 **“最大化文件共享数据吞吐量”** 。 通过选择 **“最小化使用的内存”** 或 **“平衡”**，可以指定最小文件系统缓存。  
  
#### 检查操作系统的当前设置  
  
1.  依次单击“开始”和“控制面板”，双击“网络连接”，然后双击“本地连接”。  
  
2.  在 **“常规”** 选项卡上，单击 **“属性”**，选择 **“Microsoft 网络的文件和打印机共享”**，然后单击 **“属性”**。  
  
3.  如果选中了 **“最大化网络应用程序数据吞吐量”** ，请任选一个相应的其他选项，单击 **“确定”**，再关闭其余对话框。  
  
## 锁定内存页  
 此 Windows 策略将确定哪些帐户可以使用进程将数据保留在物理内存中，从而阻止系统将数据分页到磁盘的虚拟内存中。 锁定内存中的页可以在发生将内存分页到磁盘时保持服务器的响应能力。 已向有权运行 sqlservr.exe 的帐户授予 Windows“锁定内存页”(LPIM) 用户权限时，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard Edition 和更高版本的实例中将 SQL Server 的“锁定内存页”选项设置为 ON。  
  
 若要对 **禁用** “锁定内存页” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选项，请删除 SQL Server 启动帐户的“锁定内存页”用户权限。  
  
### 禁用“锁定内存页”  
 禁用“锁定内存页”选项  
  
1.  在 **“开始”** 菜单上，单击 **“运行”**。 在“打开”  框中，键入 **gpedit.msc**  
  
     将打开 **“组策略”** 对话框。  
  
2.  在 **“组策略”** 控制台上，展开 **“计算机配置”**，再展开 **“Windows 设置”**。  
  
3.  展开 **“安全设置”**，再展开 **“本地策略”**。  
  
4.  选择 **“用户权利指派”** 文件夹。  
  
     细节窗格中随即显示出策略。  
  
5.  在该窗格中，双击“锁定内存页”。  
  
6.  在 **“本地安全策略设置”** 对话框中，选择有权运行 sqlservr.exe 的帐户，然后单击 **“删除”**。  
  
## 虚拟内存管理器  
 提交的地址空间区域由 Windows 虚拟内存管理器 (VMM) 映射到可用的物理内存。  
  
 有关不同操作系统所支持的物理内存量的详细信息，请参阅 Windows 文档“Windows 版本的内存限制”。  
  
 虚拟内存系统允许虚拟内存超过物理内存，这样虚拟内存与物理内存的比率可以大于 1:1。 因此，大型程序在计算机上运行时可以具有多种物理内存配置。 但是，使用比所有进程的平均组合工作集大得多的虚拟内存可能会导致性能降低。  
  
 **min server memory** 和 **max server memory** 选项都是高级选项。 如果使用 **sp_configure** 系统存储过程来更改这些设置，则只有在“显示高级选项”设置为 1 时才能更改它们。 这些设置更改后会立即生效，不需要重新启动服务器。  
  
## 运行多个 SQL Server 实例  
 当运行多个 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例时，可以使用三种方法来管理内存：  
  
-   使用 **max server memory** 控制内存使用量。 为每个实例建立最大设置，注意总的允许设置值不能大于计算机上的物理总内存。 可能需要为每个实例提供与预期的工作负荷或数据库大小成正比的内存。 这种方法的优势体现在：当启动新的进程或实例时，可以立即为这些进程或实例提供可用内存。 这种方法的缺点为：如果没有运行所有实例，则所有运行中的实例都无法使用剩余的可用内存。  
  
-   使用 **min server memory** 控制内存使用量。 为每个实例建立最小设置，以使这些最小值的和比计算机上总的物理内存小 1-2 GB。 此外，可能需要建立与该实例的预期负荷成正比的最小值。 这种方法的优势体现在：如果没有同时运行所有实例，则运行中的实例可以使用剩余的可用内存。 当计算机上存在其他占用大量内存的进程时，这种方法也十分有用，因为它可确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 至少获得合理的内存量。 这种方法的缺点是：当启动新的实例（或任何其他进程）时，运行的实例可能会花费一些时间来释放内存，如果实例必须将修改后的页写回到数据库中来释放内存，则花费的时间可能会更长。  
  
-   不执行任何操作（不推荐）。 带有工作负荷的第一个实例通常分配所有的内存。 空闲实例或稍后启动的实例最终可能会只使用最少的可用内存量运行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会尝试均衡分配各个实例的内存使用量。 但是，所有实例均将响应 Windows 内存通知信号以调整它们内存需求量的大小。 Windows 不会使用内存通知 API 来平衡各个应用程序使用的内存。 它只提供有关系统内存可用性的全局反馈。  
  
 您可以在不重新启动实例的情况下更改这些设置，以便可以轻松地进行尝试以找到适合使用模式的最佳设置。  
  
## 为 SQL Server 提供最大内存量  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有版本中都可以将内存配置为最大进程虚拟地址空间限制 (8 TB)。  
  
 ***/3gb** 是一个操作系统的启动参数。 有关详细信息，请访问 [MSDN Library](http://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409)。  
  
## 示例  
  
### 示例 A  
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
  
### 示例 B. 确定当前内存分配  
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
  
## 另请参阅  
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  