---
title: "并行数据仓库概述"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "本主题介绍设备软件和分析平台系统的非设备软件组件。"
ms.date: 01/05/2017
ms.topic: article
ms.assetid: db0c4a43-a66d-4c44-ab91-791c5785f71c
caps.latest.revision: "20"
ms.openlocfilehash: 587b1ce6720fc07d9ac24edde2c5b8cc2b30c89f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="parallel-data-warehouse-overview"></a>并行数据仓库概述
本主题介绍设备软件和分析平台系统的非设备软件组件。  
  
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
  
## <a name="sec1"></a>设备软件-查询处理和用户数据存储  
  
### <a name="control-node"></a>控制节点  
MPP 引擎  
MPP 引擎是大脑大规模并行处理 (MPP) 系统。 它执行以下操作：  
  
-   创建并行查询计划和协调计算节点上的执行并行查询。  
  
-   存储和协调的所有数据库的元数据和配置数据。  
  
-   管理 SQL Server PDW 数据库身份验证和授权。  
  
-   跟踪硬件和软件的状态。  
  
### <a name="data-movement-service-dms"></a>数据移动服务 (DMS)  
数据移动服务 (DMS) 是"秘方"的 PDW 的一部分。 它执行以下操作：  
  
-   传输数据与其他 SQL Server PDW 节点。  
  
-   进程查询需要节点之间传输数据的操作。  
  
-   优化的数据传输速度，从而提高了查询性能。  
  
### <a name="admin-console"></a>管理控制台  
管理员控制台是一个 web 应用程序提供的设备状态、 运行状况和性能信息。  
  
### <a name="configuration-manager"></a>配置管理器  
配置管理器 (dwconfig.exe) 是设备管理员用于配置分析平台系统的工具。  
  
### <a name="control-node-databases"></a>控制节点数据库  
SQL Server 管理的所有数据库上的控件节点。  
  
-   Shell 数据库管理所有分布式的用户数据库的元数据。  
  
-   TempDB 包含跨设备的所有用户的临时表的元数据。  
  
-   主机是 SQL Server 的主表上的控件节点。  
  
### <a name="compute-node"></a>计算节点  
计算节点是并行数据处理和存储单元。 它们具有直接连接的存储器，并使用 SQL Server 来管理用户数据。  
  
### <a name="data-movement-service-dms"></a>数据移动服务 (DMS)  
数据移动服务 (DMS) 执行以下每个计算节点上运行：  
  
-   作为处理并行查询的一部分，DMS 传输数据到和从其他计算机节点和管理节点。  
  
-   DMS，在每个计算节点上，运行并行接收数据加载。 直接从服务器加载到计算节点并行加载数据  
  
-   DMS 数据从每个计算节点将直接传递给备份服务器。  
  
-   使用 PolyBase，DMS 将数据传入和传出外部的 Hadoop 群集或 HDInsight 区域传输在设备上。  
  
### <a name="compute-node-databases"></a>计算节点数据库 
每个计算节点运行要处理查询和管理用户数据的 SQL Server 实例。  
  
## <a name="appliance-fabric"></a>设备构造  
设备构造该设备提供操作系统、 服务和网络基础结构。  
  
### <a name="domain-controller"></a>域控制器  
Active Directory (AD) 域服务 (DS)  
分析平台系统执行分析平台系统节点之间的身份验证和管理 SQL Server PDW Windows 身份验证登录名的身份验证。  
  
DNS 服务  
Windows 域名服务 (DNS) 解析为针对分析平台系统设备的 IP 地址的域名。  
  
### <a name="windows-deployment-service"></a>Windows 部署服务  
Windows 部署服务 (WDS) 将部署到设备上 Windows Server 操作系统。 它跨设备上的每个主机和虚拟机部署。  
  
DHCP 服务，以便设备域内的主机可以在无预配置的 IP 地址的情况下将加入设备网络创建 IP 地址。  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
分析平台系统使用虚拟化来实现高可用性。 Virtual Machine Manager 承载 System Center 部署物理主机上的操作系统。  
  
Windows Server Update Services (WSUS) 应用或删除的所有主机和虚拟机的 Windows 更新。  
  
### <a name="windows-server"></a>Windows Server  
主机和设备中的虚拟机的所有运行 Windows Server 操作系统。  
  
### <a name="failover-clustering"></a>故障转移群集  
Windows 故障转移群集提供的事件中某个主机故障，重新启动被动主机上的进程的能力。  
  
### <a name="storage-spaces"></a>存储空间  
Windows 存储空间将小的一组计算节点的存储池作为管理用户数据。 如果计算节点失败，仍可通过组中的另一个计算节点进行访问数据。  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft HYPER-V Server 提供简单且可靠的虚拟化解决方案。 分析平台系统使用的虚拟化，以平衡 CPU 资源并为 PDW 节点和装置 fabric 组件提供高可用性。  
  
## <a name="sec2"></a>非关系数据
若要将 SQL Server PDW 数据集成与外部 Hadoop 数据的 PolyBase 技术。 Hadoop 数据可以存储在任何这些 Hadoop 数据源：  
  
-   用于 Linux 或 Windows Server 的 Hortonworks  
  
-   在 Linux 上的 Cloudera  
  
-   在 AP 上运行的 HDInsight  
  
-   存储在 Azure 存储 Blob 上的 HDInsight 数据  
  
## <a name="query-tools"></a>查询工具   
  
查询是否编写使用 Transact\-SQL 修改以满足查询的 MPP 性质。 所有查询会都提交对生成并行查询计划跨计算节点运行查询的控件节点。  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools 在 Visual Studio 内运行，并且是我们推荐使用的 GUI 工具，用于提交到 SQL Server PDW 的查询。 它是类似于 SQL Server Management Studio，它允许你在对象资源管理器中导航。  
  
如果你还没有 Visual Studio，你可以下载免费需要的工具。 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 命令行查询工具  
sqlcmd 是用于运行 Transact SQL Server 命令行工具\-SQL 语句和系统命令。 它适用于 SQL Server PDW，并且是用于查询 SQL Server PDW 我们推荐使用的命令行工具。使用 sqlcmd，您可以运行 Transact\-SQL 语句以交互方式从命令行中，作为批处理文件，或从 Windows PowerShell。  
  
<!-- MISSING LINKS

If you don’t have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
你可以使用查询 SQL Server PDW Integration Services。 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>链接服务器  
通过使用链接的 SQL Server 服务器连接，你可以使用 SQL Server 以提交 Transact\-向 SQL Server PDW 的 SQL 语句。 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>商业智能工具
  
Analysis Services  
SQL Server PDW 是 Analysis Services 数据库和 Excel PowerPivot 模型的有效数据源。 使用 OLE DB 提供程序，你可以配置的 Analysis Services 多维数据集，以使用多维联机分析处理 (MOLAP) 或关系的联机分析处理 (ROLAP) 存储。  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>报表生成器  
作为 SQL Server 数据源提供 SQL Server PDW 可用于通过使用 SQL Server 报表生成器的 Reporting services 开发的报表。 你还可以为报表模型作为 SQL Server 源中使用 SQL Server PDW。 通过使用报表管理器或报表服务器 API，你可以从 SQL Server PDW 数据库生成模型。  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
你可以连接到 SQL Server PDW 使用 PowerPivot for Excel，免费下载显著扩展的 Excel 的数据分析功能。  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>加载工具 
  
### <a name="integration-services"></a>Integration Services  
安装允许你使用 SQL ServerIntegration 服务将数据载入 SQL Server PDW 的 PDW 特定目标适配器。  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 命令行加载程序  
dwloader 是一个命令行加载工具，将数据并行加载服务器加载到 SQL Server PDW 计算节点。 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase Hadoop 集成  
使用 PolyBase 技术，可以到 SQL Server PDW 中的关系表加载从 Hadoop 群集的非关系数据。 可以位于 Hadoop 数据，外部 Hadoop 群集上 AP 的 HDI 区域或 Azure 存储 Blob 中。  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>数据库备份和还原  
SQL Server PDW 使用 Transact\-SQL 数据库备份和还原命令来备份和还原用户数据库，请在并行，与其他备份服务器。 SQL Server PDW 将备份写入 Windows 文件共享中的目录，然后从 Windows 文件共享同样还原数据。  
  
有关详细信息，请参阅[规划备份和加载硬件](backup-and-loading-hardware.md)和[备份和还原概述](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>远程表复制  
远程表复制功能可用于将表从 SQL Server PDW 数据库复制到远程的 （非设备） SMP SQL Server 数据库。 这样可以中心辐射方案的 SQL Server PDW。  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>监视  
分析平台系统有多种方式监视设备活动  
  
### <a name="admin-console"></a>管理控制台  
管理员控制台允许你查看有关设备运行状况的当前状态。 这在管理节点上作为 web 应用程序运行并能够通过 https 进行访问。  
  
有关详细信息，请参阅[使用管理控制台 &#40; 监视设备分析平台系统 &#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>系统视图  
管理控制台基于系统视图查询。 您可以查询单独要获取所需的信息的特定部分的系统视图。  

有关详细信息，请参阅[监视通过使用系统视图 &#40; 设备分析平台系统 &#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
没有为 SQL Server PDW 的 System Center Operations Manager (SCOM) 管理包。 

若要为 SCOM 中配置设备，请参阅[监视通过使用 System Center Operations Manager &#40; 设备分析平台系统 &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
