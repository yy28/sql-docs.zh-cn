---
title: "要求和注意事项 Analysis Services 部署 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- memory [Analysis Services]
- scalability [Analysis Services]
- space [Analysis Services]
- Analysis Services deployments, requirements
- deploying [Analysis Services], requirements
- disk space [Analysis Services]
- requirements [Analysis Services]
- processors [Analysis Services]
- system requirements [Analysis Services]
- availability [Analysis Services]
ms.assetid: ef1387a5-5137-4ef4-b731-fec347e5f5ed
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: fa49c67746a2c2e9da22e8e2b18ae9af06eb6c42
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="requirements-and-considerations-for-analysis-services-deployment"></a>Analysis Services 部署的要求和注意事项
  解决方案的性能和可用性取决于许多因素，包括基础硬件的性能、服务器部署的拓扑结构、您的解决方案特性（例如，具有跨多个服务器分布的分区或者使用要求对关系引擎的直接访问权限的 ROLAP 存储区）、服务级别协议和您的数据模型的复杂程度。  
  
## <a name="memory-and-processor-requirements"></a>内存和处理器要求  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在以下情况下需要更多的内存和处理器资源：  
  
-   处理大型或复杂多维数据集时。 与小型或简单的多维数据集相比，它们需要更多的内存和处理器资源。  
  
-   单个数据库中的多维数据集个数增加时。  
  
-   单个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中的数据库个数增加时。  
  
-   单个计算机上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例数增加时。  
  
-   同时访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 资源的用户数增加时。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可用的内存和处理器资源量随不同的 SQL Server 版本、操作系统、硬件功能以及是使用虚拟还是物理处理器而变化。 有关详细信息，请访问以下链接：  
  
 [安装 SQL Server 2016 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [按 SQL Server 版本划分的计算能力限制](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
 [SQL Server 2016 各个版本支持的功能](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)  
  
 [最大容量规范 (Analysis Services)](../../analysis-services/multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md)  
  
## <a name="disk-space-requirements"></a>磁盘空间要求  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安装的不同方面和与对象处理相关的任务需要不同的磁盘空间大小。 以下列表描述了这些要求。  
  
 多维数据集  
 与有小事实数据表的多维数据集相比，有大型事实数据表的多维数据集需要更多的磁盘空间。 同样，尽管是在更小的程度内，与有较少维度成员的多维数据集相比，有很多大型维度的多维数据集需要更多的磁盘空间。 通常，可以预计 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库所需的空间量是存储在基础关系数据库中的相同数据所需空间量的大约 20%。  
  
 Aggregations  
 聚合需要与所增加的聚合成比例的额外空间，即聚合越多，需要的空间越多。 如果避免创建不必要的聚合，则聚合所需要的额外磁盘空间通常不应超过存储在基础关系数据库中的数据大小的大约 10%。  
  
 数据挖掘  
 默认情况下，挖掘结构将把用它们定型的数据集缓存到磁盘。 若要从磁盘删除此缓存数据，可以对挖掘结构对象使用 **“处理清除结构”** 处理选项。 有关详细信息，请参阅[处理要求和注意事项（数据挖掘）](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 对象处理  
 在处理过程中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将它正在处理事务中进行处理的对象的副本存储在磁盘上，直到处理完成。 处理完成后，经过处理的对象副本将替换原始对象。 因此，您必须为要处理的每个对象的第二个副本提供足够的额外磁盘空间。 例如，如果计划在单个事务中处理整个多维数据集，则需要足够的硬盘空间来存储整个多维数据集的第二个副本。  
  
##  <a name="BKMK_Availability"></a> 可用性注意事项  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 环境中，由于硬件或软件故障，多维数据集或挖掘模型可能对查询不可用。 多维数据集还可能由于需要被处理而不可用。  
  
### <a name="providing-availability-in-the-event-of-hardware-or-software-failures"></a>一旦硬件或软件发生故障时提供可用性  
 硬件或软件可能由于各种原因而发生故障。 但是，维护 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安装的可用性不仅涉及排除这些故障源，而且涉及提供替代资源，以使用户能够在发生故障时继续使用系统。 通常，使用群集和负载平衡服务器来提供当硬件或软件故障发生时维护可用性所需的替代资源。  
  
 若要在发生硬件或软件故障时提供可用性，请考虑将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署到故障转移群集中。 在故障转移群集中，如果主节点由于任何原因发生故障或必须重新启动，则 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 群集将故障转移到辅助节点。 发生故障转移的速度非常快，在此之后，当用户运行查询时，他们将访问运行在辅助节点上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。 有关故障转移群集的详细信息，请参阅 [Windows Server 技术：故障转移群集](http://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)。  
  
 可用性问题的另一个解决方案是将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到两个或更多个生产服务器上。 然后，可以使用 Windows 服务器的网络负载平衡 (NLB) 功能，将生产服务器组合成单个群集。 在 NLB 群集中，如果群集中的服务器由于硬件或软件问题而不可用，NLB 服务会将用户查询引向那些仍然可用的服务器。  
  
### <a name="providing-availability-while-processing-structural-changes"></a>当处理结构更改时提供可用性  
 多维数据集的某些更改可以导致多维数据集在被处理之前不可用。 例如，如果对多维数据集中的维度进行了结构更改，那么，即使重新处理该维度，仍然必须对使用修改后的维度的每个多维数据集进行处理。 直到处理完这些多维数据集之后，用户才能查询它们，也才能查询基于有修改维度的多维数据集的任何挖掘模型。  
  
 若要在处理可能会影响 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中的一个或多个多维数据集的结构更改时提供可用性，请考虑合并临时服务器，并使用同步数据库向导。 此功能允许您更新临时服务器上的数据和元数据，然后对生产服务器和临时服务器执行联机同步。 有关详细信息，请参阅 [Synchronize Analysis Services Databases](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)。  
  
 若要透明处理对源数据的增量更新，请启用主动缓存。 主动缓存将以新的源数据更新多维数据集，而不需要手动处理，并且不会影响多维数据集的可用性。 有关详细信息，请参阅[主动缓存（分区）](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
##  <a name="BKMK_Scalability"></a> 可伸缩性注意事项  
 同一个计算机上的多个 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例可能导致性能问题。 若要解决这些问题，一个选项可能是增加服务器的处理器、内存和磁盘资源。 但是，可能还需要将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例分散到多个计算机。  
  
### <a name="scaling-analysis-services-across-multiple-computers"></a>将 Analysis Services 分散到多个计算机  
 有几种方式将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安装分散到多个计算机。 以下列表描述了这些选项。  
  
-   如果在单个计算机上有多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，可以将一个或多个实例移动到另一个计算机上。  
  
-   如果单台计算机上有多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，则可以将一个或多个数据库移动到单独计算机它自己的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中。  
  
-   如果一个或多个关系数据库为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库提供数据，则可以将这些数据库移动到单独的计算机上。 在移动数据库之前，请考虑在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库和它的基础数据库之间实际的网络速度和带宽。 如果网络缓慢或堵塞，那么，将基础数据库移到单独的计算机上将会影响处理性能。  
  
-   如果处理会影响查询性能，但在多次减少查询负载后也无法进行处理，请考虑将处理任务移动到临时服务器上，然后对生产服务器和临时服务器执行联机同步。 有关详细信息，请参阅 [Synchronize Analysis Services Databases](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)。 还可以使用远程分区将处理分散到多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中。 处理远程分区时，将使用远程服务器上的处理器和内存资源，而不是本地计算机上的资源。 有关远程分区管理的信息，请参阅[创建和管理远程分区 (Analysis Services)](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)。  
  
-   如果查询性能不足，但无法增加本地服务器的处理器和内存资源，请考虑将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到两个或更多个生产服务器上。 然后，可以使用网络负载平衡 (NLB) 将服务器组合成单个群集。 在 NLB 群集中，查询将自动分散在 NLB 群集中的所有服务器上。  
  
  
