---
title: 并行数据仓库组件的分析平台系统 |Microsoft Docs
description: 此文章介绍了设备软件和分析平台系统的非设备软件组件。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: aaf90124cc7877b633a997a2c4f170057b965028
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510934"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>并行数据仓库组件的分析平台系统
此文章介绍了设备软件和分析平台系统的非设备软件组件。  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![并行数据仓库软件](media/parallel-data-warehouse-software.png "并行数据仓库软件")  
  
## <a name="sec1"></a>设备软件的查询处理和用户数据存储  
  
### <a name="control-node"></a>控制节点  
MPP 引擎  
此 MPP 引擎是整个系统中枢的大规模并行处理 (MPP) 系统。 它执行以下操作：  
  
-   创建并行查询计划和协调并行查询执行的计算节点上。  
  
-   将存储并协调所有数据库的元数据和配置数据。  
  
-   管理 SQL Server PDW 数据库身份验证和授权。  
  
-   跟踪硬件和软件的状态。  
  
### <a name="data-movement-service-dms"></a>数据移动服务 (DMS)  
数据移动服务 (DMS) 是 PDW"秘密调料"的一部分。 它执行以下操作：  
  
-   将传输到和从 SQL Server PDW 节点的数据。  
  
-   进程查询需要在节点之间的数据传输的操作。  
  
-   通过优化的数据传输速度可以提高查询性能。  
  
### <a name="admin-console"></a>管理员控制台  
管理员控制台是 web 应用程序，其中的设备状态、 运行状况和性能信息。  
  
### <a name="configuration-manager"></a>配置管理器  
配置管理器 (dwconfig.exe) 是设备管理员用于配置分析平台系统的工具。  
  
### <a name="control-node-databases"></a>控制节点数据库  
SQL Server 管理的所有数据库在控制节点上。  
  
-   Shell 数据库管理所有分布式的用户数据库的元的数据。  
  
-   TempDB 包含整个设备的所有用户的临时表的元数据。  
  
-   主机是在控制节点上 SQL Server 的主表。  
  
### <a name="compute-node"></a>计算节点  
计算节点是并行数据处理和存储单元。 它们具有直接连接的存储和 SQL Server 用于管理用户数据。  
  
### <a name="data-movement-service-dms"></a>数据移动服务 (DMS)  
数据移动服务 (DMS) 执行以下每个计算节点上运行：  
  
-   作为处理并行查询的一部分，DMS 相互传输数据从其他计算机节点和管理节点。  
  
-   DMS，每个计算节点上运行以并行形式接收数据加载。 直接从服务器加载到计算节点并行加载数据  
  
-   DMS 传输每个计算节点直接到备份服务器数据。  
  
-   使用 PolyBase，DMS 将传输数据传入和传出外部 Hadoop 集群或 Azure 存储 Blob。  
  
### <a name="compute-node-databases"></a>计算节点数据库 
每个计算节点运行要处理查询和管理用户数据的 SQL Server 实例。  
  
## <a name="appliance-fabric"></a>设备 Fabric  
设备 fabric 为设备提供操作系统、 服务和网络基础结构。  
  
### <a name="domain-controller"></a>域控制器  
Active Directory (AD) 域服务 (DS)  
分析平台系统执行分析平台系统节点之间的身份验证，并管理 SQL Server PDW Windows 身份验证登录名的身份验证。  
  
DNS 服务  
Windows 域服务 (DNS) 解析为分析平台系统设备的 IP 地址的域名。  
  
### <a name="windows-deployment-service"></a>Windows 部署服务  
Windows 部署服务 (WDS) 部署到设备上 Windows Server 操作系统。 它在设备之间的每个主机和虚拟机上部署。  
  
DHCP 服务，以便设备域内的主机可以加入设备网络而无需预先配置的 IP 地址创建 IP 地址。  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
分析平台系统使用虚拟化来实现高可用性。 Virtual Machine Manager 托管 System Center 部署物理主机上的操作系统。  
  
Windows Server Update Services (WSUS) 以应用或删除在所有主机和虚拟机上的 Windows 更新。  
  
### <a name="windows-server"></a>Windows Server  
主机和设备中的虚拟机的所有运行 Windows Server 操作系统。  
  
### <a name="failover-clustering"></a>故障转移群集  
Windows 故障转移群集提供的功能来重新启动被动主机上的进程的事件中的主机失败。  
  
### <a name="storage-spaces"></a>存储空间  
Windows 存储空间作为一组较小的计算节点的存储池来管理用户数据。 如果计算节点发生故障，则仍可通过在组中的另一个计算节点访问数据。  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft HYPER-V Server 提供简单且可靠的虚拟化解决方案。 分析平台系统使用虚拟化，以平衡 CPU 资源并为 PDW 节点和设备 fabric 组件提供高可用性。  
  
## <a name="sec2"></a>非关系数据
PolyBase 技术集成 SQL Server PDW 数据与外部 Hadoop 数据。 Hadoop 数据可以存储在任何这些 Hadoop 数据源上：  
  
-   Hortonworks Hadoop 分发版  
  
-   Cloudera Hadoop 的分布情况  
  
-   存储在 Azure 存储 Blob 上的 HDInsight 数据  
  
## <a name="query-tools"></a>查询工具   
  
使用 Transact 编写查询\-SQL 修改以满足查询的 MPP 性质。 所有查询都提交到控制节点，将生成并行查询计划以运行跨计算节点的查询。  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools 在 Visual Studio 内部运行，并且是我们推荐的 GUI 工具，用于提交到 SQL Server PDW 查询。 它是类似于 SQL Server Management Studio 通过允许您在对象资源管理器中导航。  
  
如果还没有 Visual Studio，可以下载需要免费的工具。 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 命令行查询工具  
sqlcmd 是 SQL Server 命令行工具，用于运行 Transact\-SQL 语句和系统命令。 它适用于 SQL Server PDW，我们建议的命令行工具，用于查询 SQL Server PDW。 使用 sqlcmd，您可以运行 Transact\-以交互方式从命令行中，为批处理文件，或从 Windows PowerShell 的 SQL 语句。  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
您可以使用查询 SQL Server PDW Integration Services。 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>链接服务器  
通过使用 SQL Server 链接服务器连接，您可以使用 SQL Server 提交 Transact\-SQL 语句与 SQL Server PDW。 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>商业智能工具
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW 是 Analysis Services 数据库和 Excel 的 PowerPivot 模型的有效数据源。 使用 OLE DB 访问接口，可以配置的 Analysis Services 多维数据集使用多维联机分析处理 (MOLAP) 或关系联机分析处理 (ROLAP) 存储。  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>报表生成器  
对于您为 Reporting Services 开发使用 SQL Server 报表生成器的报表，可以作为 SQL Server 数据源中使用 SQL Server PDW。 此外可以为报表模型作为 SQL Server 源使用 SQL Server PDW。 通过使用报表管理器或报表服务器 API，可以从 SQL Server PDW 数据库生成模型。  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
对于 Excel，显著扩展了 Excel 的数据分析功能的免费下载，您可以连接到使用 PowerPivot 的 SQL Server PDW。  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>正在加载工具 
  
### <a name="integration-services"></a>Integration Services  
安装允许您使用 SQL ServerIntegration 服务将数据加载到 SQL Server PDW 的 PDW 特定于目标适配器。  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 命令行加载程序  
dwloader 是从加载服务器的数据并行加载到 SQL Server PDW 计算节点的命令行加载工具。 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase Hadoop 集成  
使用 PolyBase 技术可以载入非关系数据从 Hadoop 群集 SQL Server PDW 中的关系表。 Hadoop 数据可以位于外部的 Hadoop 群集中，也可以在 Azure 存储 Blob 中。  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>数据库备份和还原  
SQL Server PDW 使用 Transact-SQL database 备份和还原到备份命令并还原用户数据库，并行情况下，与备份服务器。 SQL Server PDW 将备份写入 Windows 文件共享中的目录，然后从 Windows 文件共享同样还原数据。  
  
有关详细信息，请参阅[规划备份和加载硬件](backup-and-loading-hardware.md)和[备份和还原概述](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>远程表复制  
远程表复制功能，可将表从 SQL Server PDW 的数据库复制到远程的 （非设备） SMP SQL Server 数据库。 这可以实现中心辐射的 SQL Server PDW。  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>监视  
分析平台系统提供几种方式来监视设备活动  
  
### <a name="admin-console"></a>管理员控制台  
在管理控制台，可查看有关设备运行状况的当前状态。 这在控制节点上运行的 web 应用程序，并可通过 https 进行访问。  
  
有关详细信息，请参阅[通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>系统视图  
在管理控制台基于系统视图查询。 您可以查询系统视图分别以获取特定的所需的信息。  

有关详细信息，请参阅[监视使用系统视图按设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
没有针对 SQL Server PDW 的 System Center Operations Manager (SCOM) 管理包。 

若要配置 SCOM 设备，请参阅[监视使用 System Center Operations Manager 通过设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
