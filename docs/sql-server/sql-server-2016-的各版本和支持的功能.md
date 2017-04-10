---
title: "SQL Server 2016 的各版本和支持的功能 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "SQL 版本"
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 175
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
---
# SQL Server 2016 的各版本和支持的功能
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主题提供有关不同版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]所支持的功能的详细信息。  
  
 可在 180 天的试用期内使用 SQL Server 评估版。  
  
 有关最新的发布说明和新增功能的信息，请参阅以下内容：
- [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
- [SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)

    
 **试用 SQL Server 2016！**    
    
 > [![从评估中心下载](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[从评估中心下载 SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 虚拟机小](../analysis-services/media/azure-virtual-machine-small.png)**启动已安装 SQL Server 2016 的虚拟机[](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    
    
  
 有关评估版和开发人员版支持的功能，请参阅 SQL Server 企业版。  
  
##  <a name="a-namecross-boxscalelimitsa-scale-limits"></a><a name="Cross-BoxScaleLimits"></a>规模限制  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|单个实例使用的最大计算能力 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|操作系统支持的最大值|限制为 4 个插槽或 24 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值| 
|单个实例使用的最大计算能力 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|操作系统支持的最大值|限制为 4 个插槽或 24 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|  
|每个 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 实例的缓冲池的最大内存|操作系统支持的最大值|128 GB|64 GB|1410 MB|1410 MB|
|每个 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 实例的列存储段缓存的最大内存|不受限制的内存| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 中每个数据库的最大内存优化数据大小|不受限制的内存| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|每个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例利用的最大内存|操作系统支持的最大值|表格：16 GB<br /><br /> MOLAP：64 GB|N/A|N/A|N/A|  
|每个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 实例利用的最大内存|操作系统支持的最大值|64 GB|64 GB|4 GB|N/A|
|最大关系数据库大小|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
 1. 对于 Enterprise Edition 配合基于服务器 + 客户端访问许可证 (CAL) 的许可（对新协议不可用），每个 SQL Server 实例的内核数上限为 20。 基于内核的服务器许可模型没有限制。 有关详细信息，请参阅 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
<sup>2</sup> 适用于 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1。 

##  <a name="a-namerdbmshaa-rdbms-high-availability"></a><a name="RDBMSHA"></a>RDBMS 高可用性  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Server Core 支持<sup>1</sup>|是|用户帐户控制|用户帐户控制|用户帐户控制|是|  
|日志传送|是|用户帐户控制|用户帐户控制|是|“否”|  
|数据库镜像|是|是<br /><br /> 仅完全安全|仅见证服务器|仅见证服务器|仅见证服务器| 
|备份压缩|是|用户帐户控制|是|“否”|是| 
|数据库快照|是|是<sup>3</sup>|是<sup>3</sup>|是<sup>3</sup>|是<sup>3</sup>|
|AlwaysOn 故障转移群集实例|是<br /><br /> 节点数是操作系统支持的最大值|是<br /><br /> 支持 2 个节点|否|“否”|否|  
|AlwaysOn 可用性组|是<br /><br /> 支持最多 8 个次要副本，包括 2 个同步次要副本|否|“否”|“否”|否|
|基本可用性组 <sup>2</sup>|否|是<br /><br /> 支持 2 个节点|否|“否”|否|
|连接控制器|是|是|“否”|“否”|否|
|联机页面和文件还原|是|是|“否”|“否”|否|
|联机索引|是|是|“否”|“否”|否|
|联机架构更改|是|是|“否”|“否”|否|
|快速恢复|是|是|“否”|“否”|否|
|镜像备份|是|是|“否”|“否”|否|
|热插拔内存和 CPU|是|是|“否”|“否”|否|
|数据库恢复顾问|是|用户帐户控制|用户帐户控制|用户帐户控制|是|
|加密备份|是|用户帐户控制|是|“否”|否|
|Microsoft Azure 的混合备份（URL 的备份）|是|用户帐户控制|是|“否”|否|  
  
 <sup>1</sup> 有关如何在 Server Core 上安装 SQL Server 2016 的详细信息，请参阅[在 Server Core 上安装 SQL Server 2016](../database-engine/install-windows/install-sql-server-2016-on-server-core.md)。 

<sup>2</sup> 有关基本可用性组的详细信息，请参阅[基本可用性组](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。  

<sup>3</sup> 适用于 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。
  
##  <a name="a-namerdbmsspa-rdbms-scalability-and-performance"></a><a name="RDBMSSP"></a>RDBMS 可伸缩性和性能  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|列存储<sup>1</sup>|是|是<sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|  
|内存中 OLTP<sup>1</sup>|是|是<sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>，<sup>3</sup>|是<sup>2</sup>|
|Stretch Database|是|用户帐户控制|用户帐户控制|用户帐户控制|是|
|永久性主内存|是|用户帐户控制|用户帐户控制|用户帐户控制|是|
|多实例支持|50|50|50|50|50|
|表和索引分区|是|是<sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|  
|数据压缩|是|是<sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|
|资源调控器|是|是|“否”|“否”|否|  
|分区表并行度|是|是|“否”|“否”|否|
|多个 Filestream 容器|是|是<sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|
|NUMA 感知、大型页内存和缓冲区数组分配|是|是|“否”|“否”|否|
|缓冲池扩展|是|用户帐户控制|是|“否”|否|
|IO 资源调控|是|是|“否”|“否”|否|  
|延迟持续性|是|用户帐户控制|用户帐户控制|用户帐户控制|是|

<sup>1</sup> 内存中 OLTP 数据大小和列存储段缓存限制为“规模限制”部分中的版本所指定的内存量。 最大并行度是有限的。 对于 Standard Edition，索引生成的进程并行度 (DOP) 限制为 2 DOP，对于 Web 和 Express Edition，索引生成的进程并行度 (DOP) 限制为 1 DOP。 这是指在基于磁盘的表和内存优化表上创建的列存储索引。

<sup>2</sup> 适用于 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1。 

<sup>3</sup> LocalDB 安装选项中不包括此功能。
##  <a name="a-namerdbmssa-rdbms-security"></a><a name="RDBMSS"></a>RDBMS 安全  
  
|功能|Enterprise|Standard|Web|Express|Express with Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|行级安全性|是|是|是<sup>1</sup>|是<sup>1</sup>|是<sup>1</sup>|  
|始终加密|是|是<sup>1</sup>|是<sup>1</sup>|是<sup>1</sup>|是<sup>1</sup>| 
|动态数据屏蔽|是|是|是<sup>1</sup>|是<sup>1</sup>|是<sup>1</sup>|   
|基本审核|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|细化审核|是|是<sup>1</sup>|是<sup>1</sup>|是<sup>1</sup>|是<sup>1</sup>| 
|透明数据库加密|是|是|“否”|“否”|否|   
|可扩展的密钥管理|是|是|“否”|“否”|否| 
|用户定义的角色|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|包含的数据库|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|备份加密|是|用户帐户控制|是|“否”|否|  

<sup>1</sup> 适用于 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。  
##  <a name="a-namereplicationa-replication"></a><a name="Replication"></a> 复制  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|异类订阅服务器|是|用户帐户控制|是|“否”|否|  
|合并复制|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|   
|Oracle 发布|是|是|“否”|“否”|否| 
|对等事务复制|是|是|“否”|“否”|否|   
|快照复制|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|   
|SQL Server 变更跟踪|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|事务复制|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|   
|事务复制到 Azure|是|用户帐户控制|用户帐户控制|是|否|   
|事务复制可更新的订阅|是|是|“否”|“否”|否|  
  
##  <a name="a-namessmsa-management-tools"></a><a name="SSMS"></a>管理工具  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL 管理对象 (SMO)|是|用户帐户控制|用户帐户控制|用户帐户控制|是|  
|SQL 配置管理器|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
|SQL CMD（命令提示工具）|是|用户帐户控制|用户帐户控制|用户帐户控制|是|      
|Distributed Replay - 管理工具|是|用户帐户控制|用户帐户控制|用户帐户控制|否|  
|Distributed Replay - 客户端|是|用户帐户控制|用户帐户控制|是|否|  
|分布式重播 - 控制器|支持（最多 16 个客户端）|支持（1 个客户端）|支持（1 个客户端）|否|否|   
|SQL Profiler|是|是|否<sup>1</sup>|否<sup>1</sup>|否<sup>1</sup>|  
|SQL Server 代理|是|用户帐户控制|用户帐户控制|是|否| 
|Microsoft System Center Operations Manager 管理包|是|用户帐户控制|用户帐户控制|是|否|  
|数据库优化顾问 (DTA)|是|是<sup>2</sup>|是<sup>2</sup>|否|否|      
  
 <sup>1</sup> 可以使用 SQL Server Standard 和 SQL Server Enterprise 版本探查 SQL Server Web、SQL Server Express、SQL Server Express with Tools 和 SQL Server Express with Advanced Services。  
  
 <sup>2</sup> 仅对 Standard 版本功能启用优化  
  
##  <a name="a-namerdbmsma-rdbms-manageability"></a><a name="RDBMSM"></a>RDBMS 可管理性  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|用户实例|否|“否”|“否”|用户帐户控制|是| 
|LocalDB|否|“否”|“否”|是|否| 
|专用管理连接|是|用户帐户控制|是|支持（使用跟踪标志）|支持（使用跟踪标志）|   
|PowerShell 脚本支持|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|SysPrep 支持 <sup>1</sup>|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|支持数据层应用程序组件操作 - 提取、部署、升级、删除|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|策略自动执行（检查计划和更改）|是|用户帐户控制|用户帐户控制|是|否|   
|性能数据收集器|是|用户帐户控制|用户帐户控制|是|否| 
|能够作为多实例管理中的托管实例注册|是|用户帐户控制|用户帐户控制|是|否|   
|标准性能报表|是|用户帐户控制|用户帐户控制|是|否| 
|计划指南和计划指南的计划冻结|是|用户帐户控制|用户帐户控制|是|否|   
|使用 NOEXPAND 提示的索引视图的直接查询|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|自动索引视图维护|是|用户帐户控制|用户帐户控制|是|否| 
|分布式分区视图|是|是|“否”|“否”|否| 
|并行索引操作|是|是|“否”|“否”|否|  
|查询优化器自动使用索引视图|是|是|“否”|“否”|否| 
|并行一致性检查|是|是|“否”|“否”|否| 
|SQL Server 实用工具控制点|是|是|“否”|“否”|否|    
|缓冲池扩展|是|用户帐户控制|是|“否”|否| 
  
 <sup>1</sup> 有关详细信息，请参阅[使用 SysPrep 安装 SQL Server 的注意事项](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)。  
 
<sup>2</sup> 适用于 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。 
  
##  <a name="a-namedevtoolsa-development-tools"></a><a name="DevTools"></a>开发工具  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Microsoft Visual Studio 集成|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|Intellisense（Transact-SQL 和 MDX）|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|SQL Server Data Tools (SSDT)|是|用户帐户控制|用户帐户控制|用户帐户控制|否|    
|MDX 编辑、调试和设计工具|是|用户帐户控制|是|“否”|否|   
  
##  <a name="a-nameprogrammabilitya-programmability"></a><a name="Programmability"></a>可编程性  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|基本 R 集成|是|用户帐户控制|用户帐户控制|用户帐户控制|否|   
|高级 R 集成|是|是|“否”|“否”|否| 
|R Server (Standalone)|是|是|“否”|“否”|否|   
|Polybase 计算节点|是|是<sup>1</sup>|是<sup>1</sup>, <sup>2</sup>|是<sup>1</sup>, <sup>2</sup>|是<sup>1</sup>, <sup>2</sup>| 
|Polybase 头节点|是|是|“否”|“否”|“否”| 
|JSON|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
|查询存储|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
|临时|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
|公共语言运行时 (CLR) 集成|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
|本机 XML 支持|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|XML 索引|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|MERGE 和 UPSERT 功能|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
|FILESTREAM 支持|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|FileTable|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|日期和时间数据类型|是|用户帐户控制|用户帐户控制|用户帐户控制|是|  
|国际化支持|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|全文和语义搜索|是|用户帐户控制|用户帐户控制|用户帐户控制|否| 
|查询中的语言规范|是|用户帐户控制|用户帐户控制|用户帐户控制|否|   
|Service Broker（消息传递）|是|是|不支持（仅客户端）|不支持（仅客户端）|不支持（仅客户端）|   
|Transact-SQL 端点|是|用户帐户控制|用户帐户控制|是|否| 

<sup>1</sup> 具有多个计算节点的 Scale out 需要一个头节点。

<sup>2</sup> 适用于 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。
  
## <a name="a-nameisa-integration-services"></a><a name="IS"></a> Integration Services

有关 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 各个版本支持的 Integration Services (SSIS) 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Integration Services 功能](Integration%20Services%20Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)。

##  <a name="a-namemdsa-master-data-services"></a><a name="MDS"></a> Master Data Services  
 有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 各个版本支持的 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 和 Data Quality Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Master Data Services 和 Data Quality Services 功能](../master-data-services/master data services and data quality services features support.md)。 

  
##  <a name="a-namedwa-data-warehouse"></a><a name="DW"></a>数据仓库  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|在无需数据库的情况下创建多维数据集|是|用户帐户控制|是|“否”|否 |   
|自动生成临时和数据仓库架构|是|用户帐户控制|是|“否”|否| 
|变更数据捕获|是|是<sup>1</sup>|是<sup>1</sup>|否|否| 
|星型联接查询优化|是|是|“否”|“否”|否| 
|可扩展的只读 Analysis Services 配置|是|是|“否”|“否”|否| 
|针对已分区表和索引的并行查询处理|是|是|“否”|“否”|否|   
|全局批处理集成|是|是|“否”|“否”|否| 

<sup>1</sup> 适用于 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1。  
##  <a name="a-namessasa-analysis-services"></a><a name="SSAS"></a> Analysis Services  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 各个版本支持的 Analysis Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。 
  
##  <a name="a-namebimda-bi-semantic-model-multi-dimensional"></a><a name="BIMD"></a>BI 语义模型（多维）  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 各个版本支持的 Analysis Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
   
##  <a name="a-namebita-bi-semantic-model-tabular"></a><a name="BIT"></a>BI 语义模型（表格）  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 各个版本支持的 Analysis Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="a-nameppspa-power-pivot-for-sharepoint"></a><a name="PPSP"></a>PowerPivot for SharePoint  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 各个版本支持的 Power Pivot for SharePoint 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="a-namedma-data-mining"></a><a name="DM"></a>数据挖掘  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 各个版本支持的数据挖掘功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="a-namessrsa-reporting-services"></a><a name="SSRS"></a> Reporting Services  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 各个版本支持的 Reporting Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。

##  <a name="a-namebica-business-intelligence-clients"></a><a name="BIC"></a>商业智能客户端  

有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] 各个版本支持的商业智能客户端功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)或 [SQL Server 2016 各个版本支持的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="a-nameslsa-spatial-and-location-services"></a><a name="SLS"></a>空间和位置服务  
  
|功能名称|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|空间索引|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
|平面和大地测量数据类型|是|用户帐户控制|用户帐户控制|用户帐户控制|是| 
|高级空间库|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
|导入/导出业界标准的空间数据格式|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
  
##  <a name="a-nameadsa-additional-database-services"></a><a name="ADS"></a>其他数据库服务  
  
|功能名称|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]迁移助手|是|用户帐户控制|用户帐户控制|用户帐户控制|是|   
|数据库邮件|是|用户帐户控制|用户帐户控制|是|否| 
  
##  <a name="a-nameothera-other-components"></a><a name="Other"></a>其他组件  
  
|功能名称|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|否|否| 
|StreamInsight HA|StreamInsight Premium Edition|否|“否”|“否”|否|   
  
> [![下载 SSMS](../analysis-services/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) **[下载 SQL Server Management Studio 的最新版本](https://msdn.microsoft.com/library/mt238290.aspx)**    
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2016 的产品规格](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [安装 SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  
  
  