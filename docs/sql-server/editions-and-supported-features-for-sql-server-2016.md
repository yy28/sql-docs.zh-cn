---
title: "SQL Server 2016 的各版本和支持的功能 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "SQL 版本"
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 175
author: sabotta
ms.author: carlasab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b9b9db3ca911b8fd8eed6304b9d3a8f51e9e9ba2
ms.lasthandoff: 04/11/2017

---
# <a name="editions-and-supported-features-for-sql-server-2016"></a>SQL Server 2016 的各版本和支持的功能
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主题提供有关不同版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]所支持的功能的详细信息。  
  
 可在 180 天的试用期内使用 SQL Server 评估版。  
  
 有关最新的发布说明和新增功能的信息，请参阅以下内容：
- [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
- [SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)

    
 **试用 SQL Server 2016！**    
    
 > [![Download from Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Download SQL Server 2016  from the Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 虚拟机小](../analysis-services/media/azure-virtual-machine-small.png)**启动已安装 SQL Server 2016 的虚拟机[](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)**    
    
**开发人员版和评估版**  
 有关开发人员版和评估版支持的功能，请参阅下表中列出的 SQL Server Enterprise Edition 功能。
有关已添加到 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 开发人员版的功能的列表，请参阅 [SQL Server 2016 SP1 版本](https://aka.ms/uw6cw4)。   
  
##  <a name="Cross-BoxScaleLimits"></a> Scale Limits  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|单个实例使用的最大计算能力 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|操作系统支持的最大值|限制为 4 个插槽或 24 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值| 
|单个实例使用的最大计算能力 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|操作系统支持的最大值|限制为 4 个插槽或 24 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|  
|每个 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]实例的缓冲池的最大内存|操作系统支持的最大值|128 GB|64 GB|1410 MB|1410 MB|
|每个 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]实例的列存储段缓存的最大内存|不受限制的内存| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 中每个数据库的最大内存优化数据大小|不受限制的内存| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|每个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例利用的最大内存|操作系统支持的最大值|表格：16 GB<br /><br /> MOLAP：64 GB|N/A|N/A|N/A|  
|每个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]实例利用的最大内存|操作系统支持的最大值|64 GB|64 GB|4 GB|N/A|
|最大关系数据库大小|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
<sup>1</sup> 对于 Enterprise Edition 配合基于服务器 + 客户端访问许可证 (CAL) 的许可（对新协议不可用），每个 SQL Server 实例的内核数上限为 20。 基于内核的服务器许可模型没有限制。 有关详细信息，请参阅 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
<sup>2</sup> 适用于 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1。 

##  <a name="RDBMSHA"></a> RDBMS High Availability  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Server Core 支持 <sup>1</sup>|是|是|是|是|是|  
|日志传送|是|是|是|“否”|是|  
|数据库镜像|是|是<br /><br /> 仅完全安全|仅见证服务器|仅见证服务器|仅见证服务器| 
|备份压缩|是|是|“否”|“否”|是| 
|数据库快照|是|是 <sup>3</sup>|是 <sup>3</sup>|是 <sup>3</sup>|是 <sup>3</sup>|
|AlwaysOn 故障转移群集实例|是<br /><br /> 节点数是操作系统支持的最大值|是<br /><br /> 支持 2 个节点|是|“否”|是|  
|AlwaysOn 可用性组|是<br /><br /> 支持最多 8 个次要副本，包括 2 个同步次要副本|是|“否”|“否”|是|
|基本可用性组 <sup>2</sup>|是|是<br /><br /> 支持 2 个节点|是|“否”|是|
|联机页面和文件还原|是|“否”|“否”|“否”|是|
|联机索引|是|“否”|“否”|“否”|是|
|联机架构更改|是|“否”|“否”|“否”|是|
|快速恢复|是|“否”|“否”|“否”|是|
|镜像备份|是|“否”|“否”|“否”|是|
|热插拔内存和 CPU|是|“否”|“否”|“否”|是|
|数据库恢复顾问|是|是|是|是|是|
|加密备份|是|是|“否”|“否”|是|
|Microsoft Azure 的混合备份（URL 的备份）|是|是|“否”|“否”|是|  
  
 <sup>1</sup> 有关如何在 Server Core 上安装 SQL Server 2016 的详细信息，请参阅 [在 Server Core 上安装 SQL Server 2016](../database-engine/install-windows/install-sql-server-on-server-core.md)。 

<sup>2</sup> 有关基本可用性组的详细信息，请参阅 [基本可用性组](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。  

<sup>3</sup> 适用于 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。
  
##  <a name="RDBMSSP"></a> RDBMS Scalability and Performance  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|列存储 <sup>1</sup>|是|是 <sup>2</sup>|是 <sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|  
|内存中 OLTP <sup>1</sup>|是|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>， <sup>3</sup>|是 <sup>2</sup>|
|Stretch Database|是|是|是|是|是|
|永久性主内存|是|是|是|是|是|
|多实例支持|50|50|50|50|50|
|表和索引分区|是|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|  
|数据压缩|是|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|
|资源调控器|是|“否”|“否”|“否”|是|  
|分区表并行度|是|“否”|“否”|“否”|是|
|多个 Filestream 容器|是|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|
|NUMA 感知、大型页内存和缓冲区数组分配|是|“否”|“否”|“否”|是|
|缓冲池扩展|是|是|“否”|“否”|是|
|IO 资源调控|是|“否”|“否”|“否”|是|  
|延迟持续性|是|是|是|是|是|

<sup>1</sup> 内存中 OLTP 数据大小和列存储段缓存限制为“规模限制”部分中的版本所指定的内存量。 最大并行度是有限的。 对于 Standard Edition，索引生成的进程并行度 (DOP) 限制为 2 DOP，对于 Web 和 Express Edition，索引生成的进程并行度 (DOP) 限制为 1 DOP。 这是指在基于磁盘的表和内存优化表上创建的列存储索引。

<sup>2</sup> 适用于 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1。 

<sup>3</sup> LocalDB 安装选项中不包括此功能。
##  <a name="RDBMSS"></a> RDBMS Security  
  
|功能|Enterprise|Standard|Web|Express|Express with Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|行级安全性|是|是|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|  
|始终加密|是|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>| 
|动态数据屏蔽|是|是|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|   
|基本审核|是|是|是|是|是| 
|细化审核|是|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>| 
|透明数据库加密|是|“否”|“否”|“否”|是|   
|可扩展的密钥管理|是|“否”|“否”|“否”|是| 
|用户定义的角色|是|是|是|是|是| 
|包含的数据库|是|是|是|是|是| 
|备份加密|是|是|“否”|“否”|是|  

<sup>1</sup> 适用于 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。  
##  <a name="Replication"></a> Replication  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|异类订阅服务器|是|是|“否”|“否”|是|  
|合并复制|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|   
|Oracle 发布|是|“否”|“否”|“否”|是| 
|对等事务复制|是|“否”|“否”|“否”|是|   
|快照复制|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|   
|SQL Server 变更跟踪|是|是|是|是|是| 
|事务复制|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|   
|事务复制到 Azure|是|是|“否”|“否”|是|   
|事务复制可更新的订阅|是|“否”|“否”|“否”|是|  
  
##  <a name="SSMS"></a> Management Tools  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL 管理对象 (SMO)|是|是|是|是|是|  
|SQL 配置管理器|是|是|是|是|是|   
|SQL CMD（命令提示工具）|是|是|是|是|是|      
|Distributed Replay - 管理工具|是|是|是|是|是|  
|Distributed Replay - 客户端|是|是|是|“否”|是|  
|分布式重播 - 控制器|支持（最多 16 个客户端）|支持（1 个客户端）|支持（1 个客户端）|是|是|   
|SQL Profiler|是|是|否 <sup>1</sup>|否 <sup>1</sup>|否 <sup>1</sup>|  
|SQL Server 代理|是|是|是|“否”|是| 
|Microsoft System Center Operations Manager 管理包|是|是|是|“否”|是|  
|数据库优化顾问 (DTA)|是|是 <sup>2</sup>|是 <sup>2</sup>|是|是|      
  
 <sup>1</sup> 可以使用 SQL Server Standard 和 SQL Server Enterprise 版本探查 SQL Server Web、SQL Server Express、SQL Server Express with Tools 和 SQL Server Express with Advanced Services。  
  
 <sup>2</sup> 仅对 Standard 版本功能启用优化  
  
##  <a name="RDBMSM"></a> RDBMS Manageability  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|用户实例|是|“否”|是|是|是| 
|LocalDB|是|“否”|是|是|是| 
|专用管理连接|是|是|是|支持（使用跟踪标志）|支持（使用跟踪标志）|   
|PowerShell 脚本支持|是|是|是|是|是| 
|SysPrep 支持 <sup>1</sup>|是|是|是|是|是| 
|支持数据层应用程序组件操作 - 提取、部署、升级、删除|是|是|是|是|是| 
|策略自动执行（检查计划和更改）|是|是|是|“否”|是|   
|性能数据收集器|是|是|是|“否”|是| 
|能够作为多实例管理中的托管实例注册|是|是|是|“否”|是|   
|标准性能报表|是|是|是|“否”|是| 
|计划指南和计划指南的计划冻结|是|是|是|“否”|是|   
|使用 NOEXPAND 提示的索引视图的直接查询|是|是|是|是|是| 
|自动索引视图维护|是|是|是|“否”|是| 
|分布式分区视图|是|“否”|“否”|“否”|是| 
|并行索引操作|是|“否”|“否”|“否”|是|  
|查询优化器自动使用索引视图|是|“否”|“否”|“否”|是| 
|并行一致性检查|是|“否”|“否”|“否”|是| 
|SQL Server 实用工具控制点|是|“否”|“否”|“否”|是|    
|缓冲池扩展|是|是|“否”|“否”|是| 
  
 <sup>1</sup> 有关详细信息，请参阅 [使用 SysPrep 安装 SQL Server 的注意事项](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)。  
 
<sup>2</sup> 适用于 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。 
  
##  <a name="DevTools"></a> Development Tools  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Microsoft Visual Studio 集成|是|是|是|是|是| 
|Intellisense（Transact-SQL 和 MDX）|是|是|是|是|是| 
|SQL Server Data Tools (SSDT)|是|是|是|是|是|    
|MDX 编辑、调试和设计工具|是|是|“否”|“否”|是|   
  
##  <a name="Programmability"></a> Programmability  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|基本 R 集成|是|是|是|是|是|   
|高级 R 集成|是|“否”|“否”|“否”|是| 
|R Server (Standalone)|是|“否”|“否”|“否”|是|   
|Polybase 计算节点|是|是 <sup>1</sup>|是 <sup>1</sup>, <sup>2</sup>|是 <sup>1</sup>, <sup>2</sup>|是 <sup>1</sup>, <sup>2</sup>| 
|Polybase 头节点|是|“否”|“否”|“否”|是| 
|JSON|是|是|是|是|是|   
|查询存储|是|是|是|是|是|   
|临时|是|是|是|是|是|   
|公共语言运行时 (CLR) 集成|是|是|是|是|是|   
|本机 XML 支持|是|是|是|是|是| 
|XML 索引|是|是|是|是|是| 
|MERGE 和 UPSERT 功能|是|是|是|是|是|   
|FILESTREAM 支持|是|是|是|是|是| 
|FileTable|是|是|是|是|是| 
|日期和时间数据类型|是|是|是|是|是|  
|国际化支持|是|是|是|是|是| 
|全文和语义搜索|是|是|是|是|是| 
|查询中的语言规范|是|是|是|是|是|   
|Service Broker（消息传递）|是|是|不支持（仅客户端）|不支持（仅客户端）|不支持（仅客户端）|   
|Transact-SQL 端点|是|是|是|“否”|是| 

<sup>1</sup> 具有多个计算节点的 Scale out 需要一个头节点。

<sup>2</sup> 适用于 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。
  
## <a name="IS"></a> Integration Services

有关 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 各个版本支持的 Integration Services (SSIS) 功能的信息，请参阅 [SQL Server 各个版本支持的 Integration Services 功能](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)。

##  <a name="MDS"></a> Master Data Services  
 有关 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 各个版本支持的 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]和 Data Quality Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Master Data Services 和 Data Quality Services 功能](../master-data-services/master-data-services-and-data-quality-services-features-support.md)。 

  
##  <a name="DW"></a> Data Warehouse  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|在无需数据库的情况下创建多维数据集|是|是|“否”|“否”|是 |   
|自动生成临时和数据仓库架构|是|是|“否”|“否”|是| 
|变更数据捕获|是|是 <sup>1</sup>|是|“否”|是| 
|星型联接查询优化|是|“否”|“否”|“否”|是| 
|可扩展的只读 Analysis Services 配置|是|“否”|“否”|“否”|是| 
|针对已分区表和索引的并行查询处理|是|“否”|“否”|“否”|是|   
|全局批处理集成|是|“否”|“否”|“否”|是| 

<sup>1</sup> 适用于 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1。  
##  <a name="SSAS"></a> Analysis Services  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]各个版本支持的 Analysis Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。 
  
##  <a name="BIMD"></a> BI Semantic Model (Multi Dimensional)  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]各个版本支持的 Analysis Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
   
##  <a name="BIT"></a> BI Semantic Model (Tabular)  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]各个版本支持的 Analysis Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]各个版本支持的 Power Pivot for SharePoint 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="DM"></a> Data Mining  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]各个版本支持的数据挖掘功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="SSRS"></a> Reporting Services  
  
有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]各个版本支持的 Reporting Services 功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。

##  <a name="BIC"></a> Business Intelligence Clients  

有关 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]各个版本支持的商业智能客户端功能的信息，请参阅 [SQL Server 2016 各个版本支持的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) 或 [SQL Server 2016 各个版本支持的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="SLS"></a> Spatial and Location Services  
  
|功能名称|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|空间索引|是|是|是|是|是|   
|平面和大地测量数据类型|是|是|是|是|是| 
|高级空间库|是|是|是|是|是|   
|导入/导出业界标准的空间数据格式|是|是|是|是|是|   
  
##  <a name="ADS"></a> Additional Database Services  
  
|功能名称|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 迁移助手|是|是|是|是|是|   
|数据库邮件|是|是|是|“否”|是| 
  
##  <a name="Other"></a> Other Components  
  
|功能名称|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|是|是| 
|StreamInsight HA|StreamInsight Premium Edition|是|“否”|“否”|是|   
  
> [![Download SSMS](../analysis-services/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) **[Download the latest version of SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**    
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2016 的产品规格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [安装 SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  
  
  

