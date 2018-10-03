---
title: 版本和 SQL Server 2017 的支持的功能 ~ Linux |Microsoft Docs
ms.custom: sql-linux
ms.date: 09/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: linux
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- default components
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 11cb2d92d0a18e837a1bf7887ddf6f7a2dfbc449
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628825"
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>版本和 Linux 上的 SQL Server 2017 的支持的功能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供了在 Linux 上的 SQL Server 2017 各个版本支持的功能的详细信息。 有关各版本和 Windows 上的 SQL Server 支持的功能，请参阅[SQL Server 2017 的 Windows](../sql-server/editions-and-components-of-sql-server-2017.md)。  
  
根据应用程序的需要，安装要求会有所不同。 不同版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 能够满足单位和个人独特的性能、运行时以及价格要求。 安装哪些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件还取决于您的具体需要。 下面各节将帮助您了解如何在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的不同版本和可用组件中做出最佳选择。  

有关最新的发布说明和新增功能的信息，请参阅以下内容：
- [SQL Server on Linux 发行说明](sql-server-linux-release-notes.md)
- [什么是 Linux 上的 SQL Server 中的新增功能](sql-server-linux-whats-new.md)

在 Linux 上不可用的 SQL Server 功能的列表，请参阅[不受支持的功能和服务](sql-server-linux-release-notes.md#Unsupported)。

### <a name="try-sql-server"></a>试用 SQL Server！    
    
[下载 SQL Server 2017](http://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] 版本  
 下表介绍 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的各个版本。 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|定义|  
|---------------------------------------|----------------|  
|Enterprise|高级版产品[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]Enterprise 版提供全面的高端数据中心功能与速度超快的快速性能，让任务关键型工作负荷的高服务级别。|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard edition 提供了使部门和小型组织能够运行其应用程序的基本数据管理和支持常用开发工具用于在本地和云 — 最少的 IT 资源的有效的数据库管理。|  
|Web|对于为从小规模至大规模 Web 资产提供可伸缩性、经济性和可管理性功能的 Web 宿主和 Web VAP 来说，[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web 版本是一项总拥有成本较低的选择。|  
|开发人员|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer 版支持开发人员基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]构建任意类型的应用程序。 它包括 Enterprise 版的所有功能，但有许可限制，只能用作开发和测试系统，而不能用作生产服务器。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer 是构建和测试应用程序的人员的理想之选。|  
|Express Edition|Express 版本是入门级的免费数据库，是学习和构建桌面及小型服务器数据驱动应用程序的理想选择。 它是独立软件供应商、开发人员和热衷于构建客户端应用程序的人员的最佳选择。 如果您需要使用更高级的数据库功能，则可以将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 无缝升级到其他更高端的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本。|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用于客户端/服务器应用程序  

在运行直接连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的客户端/服务器应用程序的计算机上，只能安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]客户端组件。 如果要在数据库服务器上管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，或者打算开发 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 应用程序，那么客户端组件安装也是一个不错的选择。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件  

Linux 上的 SQL Server 2017 支持的 SQL Server 数据库引擎。 下表介绍在数据库引擎的功能。   
  
|服务器组件|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 包括[!INCLUDE[ssDE](../includes/ssde-md.md)]，用于存储、 处理和保护数据、 复制、 全文搜索、 用于管理关系的工具和 XML 数据，并在数据库分析集成的核心服务。|  

**开发人员、 企业核心和 Evaluation 版本**  
有关支持的开发人员功能，Enterprise Core 和评估版，请参阅下表中的 SQL Server Enterprise 版本列出的功能。

开发人员版仍然仅支持一个 [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md) 客户端。 
  
##  <a name="Cross-BoxScaleLimits"></a>规模限制  
  
|功能|Enterprise|Standard|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|单个实例使用的最大计算能力 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|操作系统支持的最大值|限制为 4 个插槽或 24 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值| 
|单个实例使用的最大计算能力 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|操作系统支持的最大值|限制为 4 个插槽或 24 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|
|每个 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]实例的缓冲池的最大内存|操作系统支持的最大值|128 GB|64 GB|1410 MB|
|每个 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]实例的列存储段缓存的最大内存|不受限制的内存| 32 GB| 16 GB| 352 MB|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 中每个数据库的最大内存优化数据大小|不受限制的内存| 32 GB| 16 GB| 352 MB|
|最大关系数据库大小|524 PB|524 PB|524 PB|10 GB|  
  
<sup>1</sup> Enterprise edition 配合服务器 + 客户端访问许可证 (CAL) 基于许可 （对新协议不可用），为每个 SQL Server 实例的 20 个内核的最大值。 基于内核的服务器许可模型没有限制。 有关详细信息，请参阅[版本的 SQL Server 计算能力限制](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
 
##  <a name="RDBMSHA"></a>RDBMS 高可用性  
  
|功能|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|日志传送|用户帐户控制|是|是|否|  
|备份压缩|用户帐户控制|是|否|否| 
|数据库快照|用户帐户控制|否|否|否|
|Always On 故障转移群集实例<sup>1</sup>|用户帐户控制|是|否|否| 
|Always On 可用性组<sup>2</sup>|用户帐户控制|否|否|否|
|基本可用性组<sup>3</sup>|否|是|否|否|
|最小副本提交可用性组|用户帐户控制|是|否|否|
|无群集的可用性组|用户帐户控制|是|否|否|
|联机页面和文件还原|用户帐户控制|否|否|否|
|联机索引|用户帐户控制|否|否|否|
|可恢复的联机索引重新生成|用户帐户控制|否|否|否|
|联机架构更改|用户帐户控制|否|否|否|
|快速恢复|用户帐户控制|否|否|否|
|镜像备份|用户帐户控制|否|否|否|
|热插拔内存和 CPU|用户帐户控制|否|否|否|
|加密备份|用户帐户控制|是|否|否|
|Microsoft Azure 的混合备份（URL 的备份）|用户帐户控制|是|否|否|
  
<sup>1</sup>企业版上的节点数是操作系统最大值。 Standard 版本中支持两个节点。 

<sup>2</sup>在 Enterprise edition 支持最多 8 个辅助副本，包括 2 个同步辅助副本。 

<sup>3</sup>标准版支持基本可用性组。 基本可用性组支持两个副本，一个数据库。 有关基本可用性组的详细信息，请参阅 [可用性组](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。    

##  <a name="RDBMSSP"></a>RDBMS 可伸缩性和性能  
  
|功能|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|列存储 <sup>1</sup>|用户帐户控制|是|是|用户帐户控制|  
|聚集列存储索引中的大型对象二进制文件|用户帐户控制|是|是|用户帐户控制|  
|联机非聚集列存储索引重新生成|用户帐户控制|否|否|否|
|内存中 OLTP <sup>1</sup>|用户帐户控制|是|是|用户帐户控制|
|永久性主内存|用户帐户控制|是|是|用户帐户控制|
|表和索引分区|用户帐户控制|是|是|用户帐户控制|  
|数据压缩|用户帐户控制|是|是|用户帐户控制|
|资源调控器|用户帐户控制|否|否|否|  
|已分区表并行度|用户帐户控制|否|否|否|
|NUMA 感知、大型页内存和缓冲区数组分配|用户帐户控制|否|否|否|
|IO 资源调控|用户帐户控制|否|否|否|  
|延迟持续性|用户帐户控制|是|是|用户帐户控制|
|自动优化|用户帐户控制|否|否|否|
|批处理模式自适应联接|用户帐户控制|否|否|否|
|批处理模式内存授予反馈|用户帐户控制|否|否|否|
|多语句表值函数的交错执行|用户帐户控制|是|是|用户帐户控制|
|大容量插入改进|用户帐户控制|是|是|用户帐户控制|


<sup>1</sup> 内存中 OLTP 数据大小和列存储段缓存限制为“规模限制”部分中的版本所指定的内存量。 最大并行度是有限的。 程度的索引生成的进程并行度 (DOP) 被限制为 2 DOP 标准版和 Web 和 Express edition 的 1 DOP。 这是指在基于磁盘的表和内存优化表上创建的列存储索引。

##  <a name="RDBMSS"></a>RDBMS 安全性  
  
|功能|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|行级安全性|用户帐户控制|是|是|用户帐户控制|  
|始终加密|用户帐户控制|是|是|用户帐户控制| 
|动态数据屏蔽|用户帐户控制|是|是|用户帐户控制|   
|基本审核|用户帐户控制|是|是|用户帐户控制| 
|精细审核|用户帐户控制|是|是|用户帐户控制| 
|透明数据库加密|用户帐户控制|否|否|否|   
|用户定义的角色|用户帐户控制|是|是|用户帐户控制| 
|包含的数据库|用户帐户控制|是|是|用户帐户控制| 
|备份加密|用户帐户控制|是|否|否|  

##  <a name="RDBMSM"></a>RDBMS 可管理性  
  
|功能|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|专用管理连接|用户帐户控制|是|是|支持（使用跟踪标志）|支持（使用跟踪标志）|   
|PowerShell 脚本支持|用户帐户控制|是|是|用户帐户控制| 
|支持数据层应用程序组件操作 - 提取、部署、升级、删除|用户帐户控制|是|是|用户帐户控制| 
|策略自动执行（检查计划和更改）|用户帐户控制|是|是|否|否|   
|性能数据收集器|用户帐户控制|是|是|否|否| 
|标准性能报表|用户帐户控制|是|是|否|否| 
|计划指南和计划指南的计划冻结|用户帐户控制|是|是|否|否|   
|使用 NOEXPAND 提示的索引视图的直接查询|用户帐户控制|是|是|用户帐户控制| 
|自动索引视图维护|用户帐户控制|是|是|否|否| 
|分布式分区视图|用户帐户控制|否|否|否| 
|并行索引操作|用户帐户控制|否|否|否|  
|查询优化器自动使用索引视图|用户帐户控制|否|否|否| 
|并行一致性检查|用户帐户控制|否|否|否| 
|SQL Server 实用工具控制点|用户帐户控制|否|否|否|    

##  <a name="Programmability"></a> Programmability  
  
|功能|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|用户帐户控制|是|是|用户帐户控制|   
|查询存储|用户帐户控制|是|是|用户帐户控制|   
|临时|用户帐户控制|是|是|用户帐户控制|   
|本机 XML 支持|用户帐户控制|是|是|用户帐户控制| 
|XML 索引|用户帐户控制|是|是|用户帐户控制| 
|MERGE 和 UPSERT 功能|用户帐户控制|是|是|用户帐户控制|   
|日期和时间数据类型|用户帐户控制|是|是|用户帐户控制|  
|国际化支持|用户帐户控制|是|是|用户帐户控制| 
|全文和语义搜索|用户帐户控制|是|是|是|否| 
|查询中的语言规范|用户帐户控制|是|是|是|否|   
|Service Broker（消息传递）|用户帐户控制|用户帐户控制|不支持（仅客户端）|不支持（仅客户端）|不支持（仅客户端）|   
|Transact-SQL 端点|用户帐户控制|是|是|否|否| 
|图形|用户帐户控制|是|是|用户帐户控制|  


<sup>1</sup> 具有多个计算节点的 Scale out 需要一个头节点。

## <a name="IS"></a> Integration Services

有关支持的版本的 Integration Services (SSIS) 功能的信息[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]，请参阅[Integration Services 功能的 SQL Server 各个版本支持](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)。

##  <a name="SLS"></a>空间和位置服务  
  
|功能名称|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|空间索引|用户帐户控制|是|是|用户帐户控制|   
|平面和大地测量数据类型|用户帐户控制|是|是|用户帐户控制| 
|高级空间库|用户帐户控制|是|是|用户帐户控制|   
|导入/导出业界标准的空间数据格式|用户帐户控制|是|是|用户帐户控制|   

  
## <a name="next-steps"></a>后续步骤 
 [版本和支持的 SQL Server 2017 的 Windows 功能](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [版本和 SQL Server 2016 的 Windows 支持的功能](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [版本和支持适用于 SQL Server 2014 的 Windows 功能](http://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [安装 SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [SQL Server 的产品规格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb) 

  
  
