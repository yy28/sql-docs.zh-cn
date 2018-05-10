---
title: 高可用性和 Analysis Services 中的可伸缩性 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3eb3d358f22c22472185c61baebc4197792f6353
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="high-availability-and-scalability-in-analysis-services"></a>Analysis Services 中的高可用性和可伸缩性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本指南介绍提高 Analysis Services 数据库可用性和可伸缩性的方法。 尽管每个目标无法单独实现，在在现实生活中，它们往往是相辅相成的：大型查询或处理工作负载的可伸缩部署通常附带高可用性的预期值。  
  
 反之亦然。 当任务关键型的中等查询工作负载存在严格的服务级别协议时，唯一的目标可能是实现高可用性而不要求可伸缩性。  
  
 为 Analysis Services 实现高可用性和可伸缩性的方法对于所有服务器模式（多维、表格和 SharePoint 集成模式）往往相同。 除非另有说明，否则假设本文中的信息适用于所有模式。  
  
## <a name="key-points"></a>要点  
 由于实现高可用性和可伸缩性的方法与适用于关系数据库引擎的方法不同，此处简要汇总了一些要点，以便有效地介绍对 Analysis Services 使用的方法：  
  
-   Analysis Services 利用 Windows 服务器平台中内置的高可用性和可伸缩性机制：网络负载平衡 (NLB) 和/或 Windows Server 故障转移群集 (WSFC)。  
  
    > [!NOTE]  
    >  关系数据库引擎的 Always On 功能未扩展到 Analysis Services。  无法将 Analysis Services 实例配置为在 Always On 可用性组中运行。  
    >   
    >  尽管 Analysis Services 无法在 Alwayson 可用性组中运行，但可以从 Always On 关系数据库检索和处理数据。 有关如何配置高可用性关系数据库以使其可用于 Analysis Services 的说明，请参阅 [含有 AlwaysOn 可用性组的 Analysis Services](../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md)。  
  
-   可以通过故障转移群集中的服务器冗余实现高可用性这个唯一目标。假设替代节点使用相同的硬件和软件配置作为活动节点。  WSFC 本身可实现高可用性，但无法实现可伸缩性。  
  
-   附带或不附带可用性的可伸缩性是通过对只读数据库使用 NLB 实现的。  当查询量较大或者经常出现突发高峰时，可伸缩性通常是一个问题。  
  
     结合多个只读数据库的负载平衡可以同时提供可伸缩性和高可用性，因为所有节点都处于活动状态，当某台服务器停机时，请求将自动在剩余节点之间重新分配。 如果你同时需要可伸缩性和可用性，NLB 群集是正确的选择。  
  
 对于处理，高可用性和可伸缩性的目标不太重要，因为你会控制操作的计时和范围。 处理可能是在模型的多个部分之间进行的不完整和增量操作，不过，在某些时候，你需要在单个服务器上处理整个模型，以确保所有索引和聚合的数据一致性。 稳健的可伸缩体系结构依赖于无论在哪种场合下，都能适应整个处理要求的硬件。 针对大型解决方案，这种工作将构建为独立的操作，并具有自身的硬件资源。  
  
##  <a name="bkmk_serverconfig"></a> 单服务器与多服务器配置  
 在常规的单服务器部署中，处理和查询工作负载并发运行（假设系统资源足以满足这两个活动）。 Analysis Services 将现有数据结构保持不变以提供查询支持，同时，更新的版本将在后台处理。 提供足够的内存和磁盘空间来处理临时数据结构所有服务器模式提出的硬件要求，不过，每种模式在系统资源方面会提出不同的需求，并附带了不同的 NUMA 感知度。  
  
 **单一服务器和可伸缩性**  
  
 一台高端多核服务器本身就能提供足够高的可伸缩性。 在具有大量核心、RAM 和磁盘空间的高端系统上，你也许可以在单个系统中扩展。  
  
 对于多维数据库，你可以调整服务器配置属性，以创建进程与处理器之间的相关性。 有关详细信息，请参阅 [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) 。  
  
 **多服务器部署**  
  
 有时，操作要求规定要使用多个服务器。 例如，根据定义，故障转移群集包含多个服务器，其每个节点以相同的硬件和软件配置运行。  
  
 同样，如果严格要求对查询工作负载实现高可用性，则通常也要用到多个服务器。 在这种情况下，Analysis Services 的建议配置是借助专用的硬件，混合使用 Analysis Services 的不同实例上运行的只读和读/写数据库。 只读数据库处理查询请求。 读/写数据库用于处理。 下一部分提供了这种常用方法的更详细说明。  
  
 **虚拟机和高可用性**  
  
 满足高可用性要求的另一种策略可能包括使用虚拟机。 如果通过部署替代服务器来实现可用性需要花费数小时而不是几分钟的时间，则你也许可以使用能够按需启动的虚拟机，并在其中加载从中心位置检索的更新数据库。  
  
## <a name="scalability-using-read-only-and-read-write-databases"></a>使用只读和读/写数据库实现可伸缩性  
 建议对大规模或升级查询和处理工作负载使用网络负载平衡。 将 NLB 解决方案中的 Analysis Services 数据库定义为只读数据库，以确保查询的一致性。  
  
 尽管 [Scale-out querying for Analysis Services using read-only databases](https://technet.microsoft.com/library/ff795582\(v=sql.100\).aspx) （使用只读数据库对 Analysis Services 进行扩展查询）（发布于 2008 年）中的指导已有些年头，但一般来说仍有价值。 尽管服务器操作系统和计算机硬件不断演进，有关特定平台和 CPU 限制的参考信息已过时，但是，使用只读和读/写数据库进行大规模查询的基本方法仍保持不变。  
  
 方法汇总如下：  
  
-   使用专用硬件和 Analysis Services 的实例来处理数据库。 处理完成后，将数据库设为只读。 有关说明，请参阅 [Switch an Analysis Services database between ReadOnly and ReadWrite modes](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) 。  
  
-   使用多个相同的查询服务器来运行同一个只读 Analysis Services 数据库的副本。 将服务器部署在 NLB 群集中，通过一个充当群集单一入口点的虚拟服务器名称来访问该群集。  
  
-   使用 robocopy 将整个数据目录从处理服务器复制到每个查询服务器，并将处于只读模式的相同数据库附加到所有查询服务器。 还可以使用用于移动生产数据库的 SAN 快照、同步或任何其他工具或方法。  
  
## <a name="resource-demands-for-tabular-and-multidimensional-workloads"></a>表格和多维工作负载的资源需求  
 下表全面汇总了 Analysis Services 如何为查询和处理使用系统资源，内容已按服务器模式和存储进行区分。 此摘要可以帮助你了解要重视多服务器部署中处理分布式工作负载的哪些组件。  
  
|||  
|-|-|  
|**服务器和存储模式**|**对系统资源的影响**|  
|内存中表格模型（默认），其中的查询以内存中数据结构的表扫描形式执行。|重视具有高速时钟速度的 RAM 和 CPU。|  
|DirectQuery 模式下表格的模型，其中的查询将卸载到后端关系数据库服务器，处理限制为在模型中构造元数据。|注重关系数据库性能、降低网络延迟和最大化吞吐量。 更快的 CPU 还可以提高 Analysis Services 查询处理器的性能。|  
|使用 MOLAP 存储的多维模型|选择可适应磁盘 IO 的平衡配置，以便快速加载数据并为缓存数据提供足够的 RAM。|  
|使用 ROLAP 存储的多维模型|最大化磁盘 IO，最小化网络延迟。|  
  
## <a name="highly-availability-and-redundancy-through-wsfc"></a>通过 WSFC 实现高可用性和冗余  
 可将 Analysis Services 安装到现有 Windows Server 故障转移群集 (WSFC) 以实现高可用性，在尽量最短的时间内还原服务。  
  
 故障转移群集提供对数据库的完全访问权限（读取和写回），但一次只能访问一个节点。 如果第一个节点关闭，辅助数据库将在群集中的其他节点上以替代服务器的形式运行。  
  
 故障转移群集的主要优势是能够在发生服务故障后快速恢复。 不过，这种优势也附带了一定的局限性。 首先，如果永远不需要故障转移，则群集中的专用资源将一直处于闲置状态。 其次，如果发生故障转移，所有连接都会断开，未提交的工作会出现相应的损失。 多数客户端应用程序应该能够处理这种情况；通常，点击应用程序中的刷新按钮就可以恢复结果。 
 
 在考虑 WSFC 时，请记住以下几点：

- 当前不支持主动/主动。 对于 Analysis Services 而言，主动/被动（故障转移）是唯一支持的 WSFC 配置。
- 当聚类分析 Analysis Services 时，请确保参与群集的任何节点都运行在完全相同或高度相似的硬件上，且每个节点的操作上下文在操作系统版本和 Service Pack、Analysis Services 版本和 Service Pack（或累积更新）以及服务器模式方面都是相同的。
- 请避免将一个被动节点作为另一个工作负荷的主动节点重新使用。 如果节点无法同时处理两个工作负荷，倘若发生实际的故障转移情况，那么计算机利用率的任何短期增益都将丢失。
 
 白皮书 [如何安装群集 SQL Server Analysis Services](https://msdn.microsoft.com/library/dn736073.aspx)中提供了有关在故障转移群集中部署 Analysis Services 的深入说明和背景信息。 此指南虽然是针对 SQL Server 2012 编写的，但同样适用于更高版本的 Analysis Services。  
  
## <a name="see-also"></a>另请参阅  
 [同步 Analysis Services 数据库](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [强制对 Analysis Services 表格数据库的 NUMA 关联](https://blogs.msdn.microsoft.com/sqlcat/2013/11/05/forcing-numa-node-affinity-for-analysis-services-tabular-databases/)   
 [Analysis Services 案例研究： 使用表格模型中大规模商业解决方案](https://msdn.microsoft.com/library/dn751533.aspx)  
  
  
