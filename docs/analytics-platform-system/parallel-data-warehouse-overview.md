---
title: 并行数据仓库组件
description: 本文介绍了分析平台系统的设备软件和非设备软件组件。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5e609585e464cb52b996f45c7d8c57aaffcd79fe
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400934"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>并行数据仓库组件-分析平台系统
本文介绍了分析平台系统的设备软件和非设备软件组件。  
  
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
  
## <a name="appliance-software---query-processing-and-user-data-storage"></a><a name="sec1"></a>设备软件-查询处理和用户数据存储  
  
### <a name="control-node"></a>控制节点  
MPP 引擎  
MPP 引擎是 (MPP) 系统的大规模并行处理的大脑。 它执行以下操作：  
  
-   在计算节点上创建并行查询计划并协调并行查询执行。  
  
-   存储并协调所有数据库的元数据和配置数据。  
  
-   管理 SQL Server PDW 数据库身份验证和授权。  
  
-   跟踪硬件和软件状态。  
  
### <a name="data-movement-service-dms"></a>数据移动服务 (DM)   
数据移动服务 (DM) 是 PDW "机密酱" 的一部分。 它执行以下操作：  
  
-   在 SQL Server PDW 节点之间传输数据。  
  
-   处理需要在节点之间传输数据的查询操作。  
  
-   优化数据传输速度，提高查询性能。  
  
### <a name="admin-console"></a>管理控制台  
管理控制台是一个 web 应用程序，用于显示设备状态、运行状况和性能信息。  
  
### <a name="configuration-manager"></a>Configuration Manager  
Configuration Manager ( # A0) 是设备管理员用于配置分析平台系统的工具。  
  
### <a name="control-node-databases"></a>控制节点数据库  
SQL Server 管理控制节点上的所有数据库。  
  
-   Shell 数据库管理所有分布式用户数据库的元数据。  
  
-   TempDB 包含跨设备的所有用户临时表的元数据。  
  
-   Master 是控制节点上 SQL Server 的主表。  
  
### <a name="compute-node"></a>计算节点  
计算节点是并行数据处理和存储单元。 它们具有直接连接的存储，并使用 SQL Server 来管理用户数据。  
  
### <a name="data-movement-service-dms"></a>数据移动服务 (DM)   
数据移动服务 (DM) 在每个计算节点上运行，以执行以下操作：  
  
-   作为处理并行查询的一部分，DMS 将数据传入和传出其他计算机节点和控制节点。  
  
-   DM 在每个计算节点上运行，同时接收数据加载。 数据直接从加载服务器直接加载到计算节点  
  
-   DMS 将数据从每个计算节点直接传输到备份服务器。  
  
-   使用 PolyBase，DMS 将数据传入或传出外部 Hadoop 群集或 Azure 存储 Blob。  
  
### <a name="compute-node-databases"></a>计算节点数据库 
每个计算节点都运行一个实例，用于处理查询和管理用户数据 SQL Server。  
  
## <a name="appliance-fabric"></a>设备结构  
设备结构提供设备的操作系统、服务和网络基础结构。  
  
### <a name="domain-controller"></a>域控制器  
Active Directory (AD) 域服务 (DS)   
分析平台系统在分析平台系统节点之间执行身份验证，并管理 SQL Server PDW Windows 身份验证登录名的身份验证。  
  
DNS 服务  
Windows 域名服务 (DNS) 将域名解析为分析平台系统设备的 IP 地址。  
  
### <a name="windows-deployment-service"></a>Windows 部署服务  
Windows 部署服务 (WDS) 将 Windows Server 操作系统部署到设备上。 它部署在设备上的每个主机和虚拟机上。  
  
DHCP 服务将创建 IP 地址，以便设备域中的主机无需预配置的 IP 地址即可加入设备网络。  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
分析平台系统使用虚拟化实现高可用性。 Virtual Machine Manager 托管 System Center，以将操作系统部署到物理主机上。  
  
Windows Server Update Services (WSUS) ，以便在所有主机和虚拟机上应用或删除 Windows 更新。  
  
### <a name="windows-server"></a>Windows Server  
设备中的所有主机和虚拟机都运行 Windows Server 操作系统。  
  
### <a name="failover-clustering"></a>故障转移群集  
Windows 故障转移群集提供了在主机出现故障时，可以在被动主机上重新启动进程的能力。  
  
### <a name="storage-spaces"></a>存储空间  
Windows 存储空间将用户数据管理为一小组计算节点的存储池。 如果计算节点发生故障，仍可通过组中的另一个计算节点访问数据。  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V Server 提供简单且可靠的虚拟化解决方案。 分析平台系统使用 virtualizations 来平衡 CPU 资源并为 PDW 节点和设备 fabric 组件提供高可用性。  
  
## <a name="non-relational-data"></a><a name="sec2"></a>非关系数据
PolyBase 技术将 SQL Server PDW 数据与外部 Hadoop 数据集成。 Hadoop 数据可存储在任何这些 Hadoop 数据源中：  
  
-   Hortonworks Hadoop 分发  
  
-   Hadoop 的 Cloudera 分发  
  
-   存储在 Azure 存储 Blob 上的 HDInsight 数据  
  
## <a name="query-tools"></a>查询工具   
  
查询通过修改的 Transact-sql \- 来编写，以适合查询的 MPP 特性。 所有查询都将提交到控制节点，该节点会生成并行查询计划，以便跨计算节点运行查询。  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools 在 Visual Studio 中运行，是我们建议用于将查询提交到 SQL Server PDW 的 GUI 工具。 它类似于通过使用对象资源管理器导航来 SQL Server Management Studio。  
  
如果尚未安装 Visual Studio，可以免费下载所需的工具。 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 命令行查询工具  
sqlcmd 是用于运行 Transact-sql \- 语句和系统命令的 SQL Server 命令行工具。 它与 SQL Server PDW 一起使用，是我们建议用于查询 SQL Server PDW 的命令行工具。 使用 sqlcmd，你可以 \- 从命令行以批处理文件或从 Windows PowerShell 以交互方式运行 transact-sql 语句。  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
您可以使用 Integration Services 来查询 SQL Server PDW。 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>链接服务器  
通过使用 SQL Server 链接服务器连接，可以使用 SQL Server 将 Transact-sql \- 语句提交给 SQL Server PDW。 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>商业智能工具
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW 是 Analysis Services 数据库和 Excel PowerPivot 模型的有效数据源。 使用 OLE DB 提供程序，您可以将 Analysis Services 多维数据集配置为使用多维联机分析处理 (MOLAP) 或关系联机分析处理 (ROLAP) 存储。  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>报表生成器  
您可以使用 SQL Server PDW 作为 SQL Server 数据源，用于使用 SQL Server 报表生成器为 Reporting Services 开发的报表。 您还可以将 SQL Server PDW 用作报表模型的 SQL Server 源。 通过使用报表管理器或 Report Server API，你可以从 SQL Server PDW 数据库生成模型。  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
您可以使用 PowerPivot for Excel 连接到 SQL Server PDW，这是一个可显著扩展 Excel 的数据分析功能的免费下载。  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>正在加载工具 
  
### <a name="integration-services"></a>Integration Services  
安装 PDW 特定的目标适配器，该适配器允许使用 SQL ServerIntegration Services 将数据加载到 SQL Server PDW 中。  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 命令行加载器  
dwloader 是一个命令行加载工具，它将数据从加载服务器并行加载到 SQL Server PDW 计算节点。 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>适用于 Hadoop 集成的 PolyBase  
使用 PolyBase 技术，可以将非关系数据从 Hadoop 群集加载到 SQL Server PDW 中的关系表。 Hadoop 数据可以位于外部 Hadoop 群集或 Azure 存储 Blob 中。  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>数据库备份和还原  
SQL Server PDW 使用 Transact-sql 数据库备份和还原命令与备份服务器并行备份和还原用户数据库。 SQL Server PDW 将备份写入 Windows 文件共享中的目录，然后同样还原 Windows 文件共享中的数据。  
  
有关详细信息，请参阅 [规划备份和加载硬件](backup-and-loading-hardware.md) 以及 [备份和还原概述](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>远程表复制  
通过远程表复制功能，可以将表从 SQL Server PDW 数据库复制到远程 (非设备) SMP SQL Server 数据库。 这为 SQL Server PDW 提供了中心辐射型方案。  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>监视  
分析平台系统有多种方法可监视设备活动  
  
### <a name="admin-console"></a>管理控制台  
管理员控制台允许您查看有关设备运行状况的当前状态。 这将作为 web 应用程序在控制节点上运行，并且可通过 https 进行访问。  
  
有关详细信息，请参阅 [使用管理控制台监视设备 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>系统视图  
管理控制台基于系统视图查询。 您可以单独查询系统视图以获取所需的特定信息。  

有关详细信息，请参阅 [使用系统视图监视设备 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
SQL Server PDW System Center Operations Manager (SCOM) 管理包。 

若要为 SCOM 配置设备，请参阅 [使用 System Center Operations Manager &#40;Analytics 平台系统监视设备&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
