---
title: affinity mask 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- default affinity mask option
- reloading processor cache
- processor cache [SQL Server]
- CPU [SQL Server], licensing
- deferred process call
- affinity mask option
- processor affinity [SQL Server]
- SMP
- DPC
ms.assetid: 5823ba29-a75d-4b3e-ba7b-421c07ab3ac1
caps.latest.revision: 52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e1328851c9e11239a602d1069a72cc259b7a11eb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="affinity-mask-server-configuration-option"></a>affinity mask 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 改为使用 [ALTER SERVER CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-server-configuration-transact-sql.md)。  
  
 为了执行多任务， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 有时会在不同的处理器之间移动进程线程。 虽然从操作系统方面而言，这种活动是高效的，但是在高系统负荷的情况下，该活动会降低 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的性能，因为每个处理器缓存都会不断地重新加载数据。 如果将各个处理器分配给特定线程，则通过消除处理器的重新加载需要以及减少处理器之间的线程迁移（因而减少上下文切换），可以提高在这些条件下的性能；线程与处理器之间的这种关联称为“处理器关联”。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过以下两个关联掩码选项来支持处理器关联：affinity mask（也称为 **CPU affinity mask**）和 affinity I/O mask。 有关 affinity I/O maskoption 的详细信息，请参阅 [affinity I/O mask 服务器配置选项](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)。 对具有 33 至 64 个处理器的服务器的 CPU 和 I/O 关联支持还要求分别使用 [affinity64 mask 服务器配置选项](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) 和 [affinity64 I/O mask 服务器配置选项](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)。  
  
> [!NOTE]  
>  对具有 33 到 64 个处理器的服务器的关联支持仅在 64 位操作系统上可用。  
  
 关联掩码选项存在于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的早期版本中，用于动态控制 CPU 关联。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，可以配置关联掩码选项而无需重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 在您正在使用 sp_configure 时，必须在设置配置选项之后运行 RECONFIGURE 或 RECONFIGURE WITH OVERRIDE。 使用 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]时，更改关联掩码选项不需要重新启动。  
  
 关联掩码的更改是动态进行的，因此可以按需启动和关闭用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中绑定进程线程的 CPU 计划程序。 当服务器上的条件改变时会发生这种情况。 例如，如果向服务器上添加了新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，可能需要调整关联掩码选项以重新分配处理器负荷。  
  
 对关联位掩码进行修改需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启用新的 CPU 计划程序并禁用现有的 CPU 计划程序。 然后就可以在新的或剩余的计划程序上处理新批处理。  
  
 若要启动新的 CPU 计划程序， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 应创建新的计划程序并将其添加到标准计划程序列表中。 新的计划程序仅用于新加入的批处理。 当前批处理会继续在同一计划程序上运行。 当释放了现有工作线程或创建了新的工作线程后，它们就会迁移到新的计划程序。  
  
 若要关闭某个计划程序，需要等到该计划程序上的所有批处理都完成其活动并退出之后。 已关闭的计划程序将被标记为脱机，以防在它上面安排新的批处理。  
  
 服务器处于运行状态时，无论添加还是删除了计划程序，永久系统任务 [如锁监视器、检查点、系统任务线程（用于处理 DTC）和信号进程] 都会继续在原计划程序上运行。 这些永久系统任务不会动态迁移。 若要在各个计划程序上重新为这些系统任务分配处理器负荷，则需要重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尝试关闭与某个永久系统任务相关联的计划程序时，该任务会继续在脱机计划程序上运行（而不迁移）。 此计划程序将被绑定到修改后的关联掩码中的处理器，在修改之前，不应在其关联的处理器上添加任何负荷。 额外的脱机计划程序不会显著影响系统的负荷。 如果不是这样，则需要重新启动数据库服务器以重新配置这些任务。  
  
 I/O 关联任务（如惰性编写器和日志编写器）直接受 I/O 关联掩码的影响。 如果惰性编写器和日志编写器任务不被关联，它们将与其他永久任务（如锁监视器或检查点）遵循相同的规则。  
  
 为了确保新的关联掩码有效，RECONFIGURE 命令将验证正常 CPU 与 I/O 关联是否互相排斥。 如果不互相排斥，将向客户端会话和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志报告一条错误消息，指明不建议进行这种设置。 运行 RECONFIGURE WITH OVERRIDE 选项将允许 CPU 与 I/O 关联不互相排斥。  
  
 如果指定的关联掩码试图映射到不存在的 CPU，RECONFIGURE 命令会向客户端会话和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志报告一条错误消息。 在这种情况下，RECONFIGURE WITH OVERRIDE 选项将不起作用，并将再次报告相同的配置错误。  
  
 您也可以不在由 Windows 2000 或 Windows Server 2003 操作系统分配了特定工作负荷的处理器上执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活动。 如果将代表某个处理器的位设置为 1，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎将会选择该处理器来进行线程分配。 如果你将“关联掩码”设置为 0（默认值），则 Microsoft Windows 2000 或 Windows Server 2003 计划算法会设置线程的关联。 如果你将 **关联掩码** 设置为任一非零值，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关联会将该值解释为指定可供选择的处理器的位掩码。  
  
 通过防止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 线程在某个特定的处理器上运行，Microsoft Windows 2000 或 Windows Server 2003 可以更好地评估 Windows 专用的系统进程处理。 例如，在运行两个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例（实例 A 和实例 B）的具有 8 个 CPU 的服务器上，系统管理员可以使用关联掩码选项将第一组的 4 个 CPU 分配给实例 A，将第二组的 4 个 CPU 分配给实例 B。若要配置 32 个以上的处理器，应同时设置关联掩码和 affinity64 掩码。 **关联掩码** 值如下所示：  
  
-   在多处理器计算机中，单字节 **关联掩码** 最多可以涵盖 8 个 CPU。  
  
-   在多处理器计算机中，双字节 **关联掩码** 最多可以涵盖 16 个 CPU。  
  
-   在多处理器计算机中，3 字节 **关联掩码** 最多可以涵盖 24 个 CPU。  
  
-   在多处理器计算机中，4 字节 **关联掩码** 最多可以涵盖 32 个 CPU。  
  
-   若要涵盖 32 个以上的 CPU，可为前 32 个 CPU 配置一个 4 字节关联掩码，为其余的 CPU 配置一个最多 4 字节的 affinity64 掩码。  
  
 因为设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处理器关联是一种专用操作，所以建议只在需要时使用。 大多数情况下，Windows 2000 或 Windows Server 2003 的默认关联可提供最佳性能。 在设置关联掩码时还应考虑其他应用程序对 CPU 的需求。 有关详细信息，请参阅 Windows 操作系统文档。  
  
> [!NOTE]  
>  可以使用 Windows 系统监视器来查看和分析单个处理器的使用情况。  
  
 在指定 affinity I/O mask 选项时，必须将其与关联掩码配置选项结合使用。 请勿在 **affinity mask** 开关和 affinity I/O mask 选项中启用相同的 CPU。 与每个 CPU 对应的位应处于以下三种状态之一：  
  
-   在 affinity mask 选项和 affinity I/O mask 选项中均为 0。  
  
-   在 affinity mask 选项中为 1，在 affinity I/O mask 选项中为 0。  
  
-   在 affinity mask 选项中为 0，在 affinity I/O mask 选项中为 1。  
  
> [!CAUTION]  
>  请不要在 Windows 操作系统中配置 CPU 关联后，还在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中配置关联掩码。 这些设置实现的效果相同，如果配置不一致，则可能会得到意外的结果。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最好使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的 sp_configure 选项配置 CPU 关联。  
  
## <a name="example"></a>示例  
 例如，设置关联掩码选项时，如果选择处理器 1、2 和 5 作为可用的处理器，并将位 1、2 和 5 设置为 1，位 0、3、4、6 和 7 设置为 0，则将指定十六进制值 0x26 或等于 `38` 的十进制值。 从右至左对位进行编号。 关联掩码选项按从 0 到 31 的方式来计算处理器，这样在以下示例中，计数器 `1` 表示服务器上的第二个处理器。  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'affinity mask', 38;  
RECONFIGURE;  
GO  
```  
  
 以下是具有 8 个 CPU 的系统的 **关联掩码** 值。  
  
|十进制值|二进制位掩码|允许 SQL Server 线程在哪些处理器上运行|  
|-------------------|---------------------|--------------------------------------------|  
|@shouldalert|00000001|0|  
|3|00000011|0 和 1|  
|7|00000111|0、1 和 2|  
|15|00001111|0、1、2 和 3|  
|31|00011111|0、1、2、3 和 4|  
|63|00111111|0、1、2、3、4 和 5|  
|127|01111111|0、1、2、3、4、5 和 6|  
|255|11111111|0、1、2、3、4、5、6 和 7|  
  
 affinity mask 选项是一个高级选项。 如果使用 sp_configure 系统存储过程来更改该设置，则仅当“显示高级选项”设置为 1 时，才可以更改 **affinity mask**。 执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE 命令后，新的设置将立即生效，且不需要重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
## <a name="non-uniform-memory-access-numa"></a>非一致性内存访问 (NUMA)  
 当使用基于硬件的非一致性内存访问 (NUMA) 并设置了关联掩码时，节点中的每个计划程序都将关联到它自己的 CPU。 未设置关联掩码时，每个计划程序都关联到 NUMA 节点内的 CPU 组，映射到 NUMA 节点 N1 的计划程序可对节点中的任何 CPU 计划工作，但是不能对与其他节点关联的 CPU 计划工作。  
  
 针对单个 NUMA 节点执行的任何操作都只能使用该节点中的缓冲区页。 当针对多个节点上的 CPU 以并行方式执行操作时，可以使用所涉及的任何节点中的内存。  
  
## <a name="licensing-issues"></a>许可问题  
 动态关联受 CPU 许可的严格约束。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许对关联掩码选项进行任何违反许可策略的配置。  
  
### <a name="startup"></a>启动  
 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动期间或在数据库附加期间，指定的关联掩码违反了许可策略，则引擎层将会完成启动进程或数据库附加/还原操作，然后将关联掩码的 sp_configure 运行值重置为零，并向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志发出一条错误消息。  
  
### <a name="reconfigure"></a>重新配置  
 如果在运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE 命令时，指定的关联掩码违反了许可策略，则系统将向客户端会话和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志报告错误消息，要求数据库管理员重新配置关联掩码。 在这种情况下，不接受任何 RECONFIGURE WITH OVERRIDE 命令。  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [ALTER SERVER CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  
