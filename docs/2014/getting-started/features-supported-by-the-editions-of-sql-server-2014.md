---
title: SQL Server 2014 的各个版本支持的功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caae4212e2182ae6afde29b0fed1aaee4f05645a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289285"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>SQL Server 2014 各个版本支持的功能


  本主题提供有关不同版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]所支持的功能的详细信息。 

 > **请注意：** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在180天试用期内的评估版中可用。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [试用软件网站](https://go.microsoft.com/fwlink/?LinkId=190955)。  
> 
> **注意：** 对于评估版和开发人员版支持的功能[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，请参阅企业功能集。  
  
 若要导航到某种 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 技术相应的表，请单击其链接：  
  
 [跨框规模限制](#CrossBoxScale)  
  
 [高可用性](#High_availability)  
  
 [可伸缩性和性能](#Scalability)  
  
 [安全性](#Enterprise_security)  
  
 [复制](#Replication)  
  
 [管理工具](#Mgmt_Tools)  
  
 [RDBMS 可管理性](#RDBMS_mgmt)  
  
 [开发工具](#Dev_tools)  
  
 [实现](#Programmability)  
  
 [Integration Services](#SSIS)  
  
 [Integration Services - 高级适配器](#SSIS_AA)  
  
 [Integration Services - 高级转换](#SSIS_AT)  
  
 [Master Data Services](#MDS)  
  
 [数据仓库](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [BI 语义模型（多维）](#BISemModel_multi)  
  
 [BI 语义模型（表格）](#BISemModel_tabular)  
  
 [PowerPivot for SharePoint](#PowerPivot)  
  
 [数据挖掘](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [Business Intelligence 客户端](#BIClients)  
  
 [空间和位置服务](#Spatial)  
  
 [其他数据库服务](#Add_DBServices)  
  
 [其他组件](#Other_Components)  
  
##  <a name="cross-box-scale-limits"></a><a name="CrossBoxScale"></a>转换箱规模限制  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|单个实例使用的最大计算能力（[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库引擎）<sup>1</sup>|操作系统支持的最大值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|  
|单个实例使用的最大计算能力（Analysis Services，Reporting Services） <sup>1</sup>|操作系统支持的最大值|操作系统支持的最大值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|  
|利用的最大内存（每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库引擎实例）|操作系统支持的最大值|128 GB|128 GB|64 GB|1 GB|1 GB|1 GB|  
|利用的最大内存（每个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例）|操作系统支持的最大值|操作系统支持的最大值|64 GB|不适用|不适用|不适用|不适用|  
|利用的最大内存（每个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]实例）|操作系统支持的最大值|操作系统支持的最大值|64 GB|64 GB|4 GB|不适用|不适用|  
|最大关系数据库大小|524 PB|524 PB|524 PB|524 PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup>使用基于服务器 + 客户端访问许可证（CAL）的许可（对新协议不可用）的 Enterprise Edition 最多只能为每个[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例20个核心。 基于内核的服务器许可模型没有限制。 有关详细信息，请参阅 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
##  <a name="high-availability"></a><a name="High_availability"></a>高可用性  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Server Core 支持<sup>1</sup>|是|是|是|是|是|是|是|  
|日志传送|是|是|是|是||||  
|数据库镜像|是|支持（仅支持“完全”安全级别）|支持（仅支持“完全”安全级别）|仅见证服务器|仅见证服务器|仅见证服务器|仅见证服务器|  
|备份压缩|是|是|是|||||  
|数据库快照|是|||||||  
|AlwaysOn 故障转移群集实例|支持（节点支持：操作系统最大值）|支持（节点支持：2）|支持（节点支持：2）|||||  
|AlwaysOn 可用性组|支持（最多 8 个辅助副本，包括 2 个同步辅助副本）|||||||  
|连接控制器|是|||||||  
|联机页面和文件还原|是|||||||  
|联机索引|是|||||||  
|联机架构更改|是|||||||  
|快速恢复|是|||||||  
|镜像备份|是|||||||  
|热添加内存和 CPU<sup>2</sup>|是|||||||  
|数据库恢复顾问|是|是|是|是|是|是|是|  
|加密备份|是|是|是|||||  
|智能备份|是|是|是|否||||  
  
 <sup>1</sup>有关在 Server Core 上[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]安装的详细信息，请参阅在[Server core 上安装 SQL Server 2014](../database-engine/install-windows/install-sql-server-on-server-core.md)。  
  
 <sup>2</sup>此功能仅适用于64位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
##  <a name="scalability-and-performance"></a><a name="Scalability"></a>可伸缩性和性能  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|多实例支持|50|50|50|50|50|50|50|  
|表和索引分区|是|||||||  
|数据压缩|是|||||||  
|Resource Governor|是|||||||  
|分区表并行度|是|||||||  
|多个 Filestream 容器|是|||||||  
|可识别 NUMA 的大型页内存和缓冲区数组分配|是|||||||  
|缓冲池扩展<sup>1</sup>|是|是|是|||||  
|IO 资源调控|是|||||||  
|内存中 OLTP <sup>1</sup>|是|||||||  
|延迟持续性|是|是|是|是|是|是|是|  
  
 <sup>1</sup>此功能仅适用于64位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
##  <a name="security"></a><a name="Enterprise_security"></a> Security  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|基本审核|是|是|是|是|是|是|是|  
|精细审核|是|||||||  
|透明数据库加密|是|||||||  
|可扩展的密钥管理|是|||||||  
|用户定义的角色|是|是|是|是|是|是|是|  
|包含的数据库|是|是|是|是|是|是|是|  
|备份加密|是|是|是|||||  
  
##  <a name="replication"></a><a name="Replication"></a> Replication  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 更改跟踪|是|是|是|是|是|是|是|  
|合并复制|是|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|  
|事务复制|是|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|  
|快照复制|是|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|  
|异类订阅服务器|是|是|是|||||  
|Oracle 发布|是|||||||  
|对等事务复制|是|||||||  
  
##  <a name="management-tools"></a><a name="Mgmt_Tools"></a>管理工具  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|SQL 管理对象 (SMO)|是|是|是|是|是|是|是|  
|SQL 配置管理器|是|是|是|是|是|是|是|  
|SQL CMD（命令提示工具）|是|是|是|是|是|是|是|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio|是|是|是|是|是|是||  
|Distributed Replay - 管理工具|是|是|是|是|是|是||  
|分布式重播 - 客户端|是|否|是|是||||  
|分布式重播 - 控制器|支持（Enterprise 版支持最多 16 个客户端、Developer 版仅支持 1 个客户端）|否|支持（仅支持 1 个客户端）|支持（仅支持 1 个客户端）||||  
|SQL Profiler|是|是|是|否<sup>2</sup>|否<sup>2</sup>|否<sup>2</sup>|否<sup>2</sup>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理|是|是|是|是||||  
|Microsoft System Center Operations Manager 管理包|是|是|是|是||||  
|数据库优化顾问 (DTA)|是|是|是<sup>3</sup>|是<sup>3</sup>||||  
|将[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库部署到 Azure VM 向导|是|是|是|是|是|是|是|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Azure 中的数据文件|是|是|是|是|是|是|是|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]可[!INCLUDE[ssExpress](../includes/ssexpress-md.md)]使用[!INCLUDE[ssExpress](../includes/ssexpress-md.md)] [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard edition 和 Enterprise edition 分析2个 Web、with Tools 和 with Advanced Services。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 <sup>3</sup>仅对 Standard edition 功能启用优化。  
  
##  <a name="rdbms-manageability"></a><a name="RDBMS_mgmt"></a>RDBMS 可管理性  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|用户实例|||||是|是|是|  
|LocalDB|||||是|是||  
|专用管理连接|是|是|是|是|支持（受跟踪标志控制）|支持（受跟踪标志控制）|支持（受跟踪标志控制）|  
|PowerShell 脚本支持|是|是|是|是|是|是|是|  
|SysPrep 支持<sup>1</sup>|是|是|是|是|是|是|是|  
|支持数据层应用程序组件操作-提取、部署、升级、删除|是|是|是|是|是|是|是|  
|策略自动执行（检查计划和更改）|是|是|是|是||||  
|性能数据收集器|是|是|是|是||||  
|能够作为多实例管理中的托管实例注册|是|是|是|是||||  
|标准性能报表|是|是|是|是||||  
|计划指南和计划指南的计划冻结|是|是|是|是||||  
|使用 NOEXPAND 提示的索引视图的直接查询|是|是|是|是||||  
|自动的索引视图维护|是|是|是|是||||  
|分布式分区视图|是|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|  
|并行索引操作|是|||||||  
|查询优化器自动使用索引视图|是|||||||  
|并行一致性检查|是|||||||  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具控制点|是|||||||  
|包含的数据库|是|是|是|是|是|是|是|  
|缓冲池扩展<sup>2</sup>|是|是|是|||||  
  
 <sup>1</sup> 有关详细信息，请参阅 [使用 SysPrep 安装 SQL Server 的注意事项](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)。  
  
 <sup>2</sup>此功能仅适用于64位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
##  <a name="development-tools"></a><a name="Dev_tools"></a>开发工具  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio 集成|是|是|是|是|是|是|是|  
|Intellisense（[!INCLUDE[tsql](../includes/tsql-md.md)] 和 MDX）|是|是|是|是|是|是|是|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|是|是|是|是|是|||  
|SQL 查询编辑和设计工具<sup>1</sup>|是|是|是|||||  
|版本控制支持<sup>1</sup>|是|是|是|||||  
|MDX 编辑、调试和设计工具<sup>1</sup>|是|是|是|||||  
  
 <sup>1</sup>此功能不适用于64位版本的 Standard edition。  
  
##  <a name="programmability"></a><a name="Programmability"></a> Programmability  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|公共语言运行时 (CLR) 集成|是|是|是|是|是|是|是|  
|本机 XML 支持|是|是|是|是|是|是|是|  
|XML 索引|是|是|是|是|是|是|是|  
|MERGE & UPSERT 功能|是|是|是|是|是|是|是|  
|FILESTREAM 支持|是|是|是|是|是|是|是|  
|FileTable|是|是|是|是|是|是|是|  
|日期和时间数据类型|是|是|是|是|是|是|是|  
|国际化支持|是|是|是|是|是|是|是|  
|全文和语义搜索|是|是|是|是|是|||  
|查询中的语言规范|是|是|是|是|是|||  
|Service Broker（消息传递）|是|是|是|不支持（仅客户端）|不支持（仅客户端）|不支持（仅客户端）|不支持（仅客户端）|  
|[!INCLUDE[tsql](../includes/tsql-md.md)] 端点|是|是|是|是||||  
  
##  <a name="integration-services"></a><a name="SSIS"></a> Integration Services  
  
|Feature|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导|是|是|是|是|是|是|是|  
|内置数据源连接器|是|是|是|是|是|是|是|  
|SSIS 设计器和运行时|是|是|是|||||  
|基本转换|是|是|是|||||  
|基本数据探查工具|是|是|是|||||  
|Change Data Capture Service for Oracle by Attunity|是|||||||  
|Change Data Capture Designer for Oracle by Attunity|是|||||||  
  
###  <a name="integration-services---advanced-adapters"></a><a name="SSIS_AA"></a>Integration Services-高级适配器  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|高性能 Oracle 目标|是|||||||  
|高性能 Teradata 目标|是|||||||  
|SAP BW 源和目标|是|||||||  
|数据挖掘模型定型目标适配器|是|||||||  
|维度处理目标适配器|是|||||||  
|分区处理目标适配器|是|||||||  
|Attunity 提供的变更数据捕获组件|是|||||||  
|Attunity 提供的开放式数据库连接 (ODBC)|是|||||||  
  
###  <a name="integration-services---advanced-transforms"></a><a name="SSIS_AT"></a>Integration Services-高级转换  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|持续性（高性能）查找|是|||||||  
|数据挖掘查询转换|是|||||||  
|模糊分组和查找转换|是|||||||  
|术语提取和查找转换|是|||||||  
  
##  <a name="master-data-services"></a><a name="MDS"></a>Master Data Services  
  
> [!NOTE]  
>  -   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 仅适用于 Business Intelligence 版和 Enterprise 版的 64 位版本。  
  
|Feature|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库|是|是||||||  
|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序|是|是||||||  
  
##  <a name="data-warehouse"></a><a name="Data_warehouse"></a>数据仓库  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|在无需数据库的情况下创建多维数据集|是|是|是|||||  
|自动生成临时和数据仓库架构|是|是|是|||||  
|更改数据捕获|是|||||||  
|星型联接查询优化|是|||||||  
|可扩展的只读 Analysis Services 配置|是|||||||  
|针对已分区表和索引的并行查询处理|是|||||||  
|xVelocity 内存优化的列存储索引|是|||||||  
|全局批处理集成|是|||||||  
  
##  <a name="analysis-services"></a><a name="SSAS"></a>Analysis Services  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|可扩展的共享数据库（附加/分离，只读数据库）|是|是||||||  
|备份/还原、附加/分离数据库|是|是|是|||||  
|同步数据库|是|是||||||  
|高可用性|是|是|是|||||  
|可编程性（AMO、ADOMD.Net、OLEDB、XML/A、ASSL）|是|是|是|||||  
  
###  <a name="bi-semantic-model-multidimensional"></a><a name="BISemModel_multi"></a>BI 语义模型（多维）  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|半累加性度量值|是|是|否<sup>1</sup>|||||  
|层次结构|是|是|是|||||  
|KPI|是|是|是|||||  
|透视|是|是||||||  
|操作|是|是|是|||||  
|帐户智能|是|是|是|||||  
|时间智能|是|是|是|||||  
|自定义汇总|是|是|是|||||  
|写回多维数据集|是|是|是|||||  
|写回维度|是|是||||||  
|写回单元|是|是|是|||||  
|钻取|是|是|是|||||  
|高级层次结构类型（父子、不规则层次结构）|是|是|是|||||  
|高级维度（引用维度、多对多维度）|是|是|是|||||  
|链接度量值和维度|是|是||||||  
|翻译|是|是|是|||||  
|Aggregations|是|是|是|||||  
|多个分区|是|是|支持，最多 3 个|||||  
|主动缓存|是|是||||||  
|自定义程序集（存储过程）|是|是|是|||||  
|MDX 查询和脚本|是|是|是|||||  
|DAX 查询|是|是||||||  
|基于角色的安全模型|是|是|是|||||  
|维度和单元级别的安全性|是|是|是|||||  
|可扩展字符串存储|是|是|是|||||  
|MOLAP、ROLAP、HOLAP 存储模式|是|是|是|||||  
|二进制和压缩的 XML 传输|是|是|是|||||  
|推送模式处理|是|是||||||  
|直接写回|是|是||||||  
|度量值表达式|是|是||||||  
  
 <sup>1</sup>Standard edition 支持 LastChild 半累加性度量值，但不支持其他半累加性度量值，例如 None、FirstChild、FirstNonEmpty、LastNonEmpty、AverageOfChildren 和 ByAccount。 在所有版本上都支持累加性度量值（如 Sum、Count、Min 和 Max）和非累加性度量值 (DistinctCount)。  
  
###  <a name="bi-semantic-model-tabular"></a><a name="BISemModel_tabular"></a>BI 语义模型（表格）  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|层次结构|是|是||||||  
|KPI|是|是||||||  
|透视|是|是||||||  
|翻译|是|是||||||  
|DAX 计算、DAX 查询、MDX 查询|是|是||||||  
|行级安全性|是|是||||||  
|分区|是|是||||||  
|内存中和 DirectQuery 存储模式（仅限表格）|是|是||||||  
  
###  <a name="powerpivot-for-sharepoint"></a><a name="PowerPivot"></a> PowerPivot for SharePoint  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|基于共享服务体系结构的 SharePoint 场集成|是|是||||||  
|使用情况报告|是|是||||||  
|运行状况监视规则|是|是||||||  
|PowerPivot 库|是|是||||||  
|PowerPivot 数据刷新|是|是||||||  
|PowerPivot 数据馈送|是|是||||||  
  
###  <a name="data-mining"></a><a name="DataMining"></a>数据挖掘  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|标准算法|是|是|是|||||  
|数据挖掘工具（向导、编辑器、查询生成器）|是|是|是|||||  
|交叉验证|是|是||||||  
|挖掘结构数据的筛选子集的模型|是|是||||||  
|时序：ARTXP 和 ARIMA 方法之间的自定义混和|是|是||||||  
|时序：使用新数据的预测|是|是||||||  
|无限制并发数据挖掘查询|是|是||||||  
|用于数据挖掘算法的高级配置 & 优化选项|是|是||||||  
|支持插件算法|是|是||||||  
|并行模型处理|是|是||||||  
|时序：跨序列预测|是|是||||||  
|关联规则的无限制属性|是|是||||||  
|序列预测|是|是||||||  
|Naïve Bayes、神经网络和逻辑回归的多个预测目标|是|是||||||  
  
##  <a name="reporting-services"></a><a name="Reporting"></a>Reporting Services  
  
###  <a name="reporting-services-features"></a><a name="Reporting_features"></a>Reporting Services 功能  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|支持的目录 DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Standard 或更高版本|Standard 或更高版本|Standard 或更高版本|Web|Express|||  
|支持的数据源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Web|Express|||  
|报表服务器|是|是|是|是|是|||  
|报表设计器|是|是|是|是|是|||  
|报表管理器|是|是|是|是|是|||  
|基于角色的安全性|是|是|是|是|是|||  
|Word 导出和 RTF 格式支持|是|是|是|是|是|||  
|增强的仪表和图表|是|是|是|是|是|||  
|导出到 Excel、PDF 和图像|是|是|是|是|是|||  
|自定义身份验证|是|是|是|是|是|||  
|作为数据馈送的报表|是|是|是|是|是|||  
|模型支持|是|是|是|是||||  
|为基于角色的安全性创建自定义角色|是|是|是|||||  
|模型项安全性|是|是|是|||||  
|无限制链接点击|是|是|是|||||  
|共享组件库|是|是|是|||||  
|电子邮件和文件共享订阅和计划|是|是|是|||||  
|报表历史记录、执行快照和缓存|是|是|是|||||  
|SharePoint 集成|是|是|是|||||  
|远程和非 SQL 数据源支持<sup>1</sup>|是|是|是|||||  
|数据源、传递和呈现、RDCE 可扩展性|是|是|是|||||  
|数据驱动报表订阅|是|是||||||  
|扩展部署（Web 场）|是|是||||||  
|警报<sup>2</sup>|是|是||||||  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]<sup>2</sup>|是|是||||||  
  
 <sup>1</sup>有关中[!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]支持的数据源的详细信息，请参阅[Reporting Services &#40;SSRS 支持的数据源&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
 <sup>2</sup>需要[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]在 SharePoint 模式下运行。 有关详细信息，请参阅[sharepoint 2010 和 sharepoint 2013&#41;&#40;Reporting Services Sharepoint 模式安装](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
### <a name="report-server-database-server-edition-requirements"></a>报表服务器数据库的服务器版本要求  
 创建报表服务器数据库时，并非所有版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 均可用来承载数据库。 下表显示了可用于特定 [!INCLUDE[ssDE](../includes/ssde-md.md)] 版本的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]版本。  
  
|对于此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services 版本|使用此版本的数据库引擎实例来承载数据库|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Standard Edition、Business Intelligence Enterprise Edition（本地或远程）|  
|商业智能|Standard Edition、Business Intelligence Enterprise Edition（本地或远程）|  
|标准|Standard Edition、Enterprise Edition（本地或远程）|  
|Web|Web Edition（仅用于本地）|  
|Express with Advanced Services|Express with Advanced Services（仅用于本地）。|  
|评估|评估|  
  
##  <a name="business-intelligence-clients"></a><a name="BIClients"></a>商业智能客户端  
 以下软件客户端应用程序在 Microsoft 下载中心提供，它们旨在帮助您创建在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上运行的商业智能文档。 当您在某一服务器环境中承载这些文档时，请使用支持该文档类型的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 下表标识哪一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本包含承载在这些客户端应用程序中创建的文档所需的服务器功能。  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|是|是|是|||||  
|用于 Excel 和 Visio 2010 的数据挖掘外接程序|是|是|是|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010|是|是||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|是|是||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)]是 Excel 外接程序，不依赖于[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 但是，在 SharePoint 中与 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 工作簿共享和协作需要 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 。此功能在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 和 Business Intelligence 版本中提供。  
> 2.  上表标识了仅启用这些客户端工具所需的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本；但是，这些功能可以访问在任何版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上承载的数据。  
  
##  <a name="spatial-and-location-services"></a><a name="Spatial"></a>空间和位置服务  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|空间索引|是|是|是|是|是|是|是|  
|平面和大地测量数据类型|是|是|是|是|是|是|是|  
|高级空间库|是|是|是|是|是|是|是|  
|导入/导出业界标准的空间数据格式|是|是|是|是|是|是|是|  
  
##  <a name="additional-database-services"></a><a name="Add_DBServices"></a> Additional Database Services  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 迁移助手|是|是|是|是|是|是|是|  
|数据库邮件|是|是|是|是||||  
  
##  <a name="other-components"></a><a name="Other_Components"></a>其他组件  
  
|功能名称|Enterprise|商业智能|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|数据库引擎服务|是|是||||||  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|StreamInsight Standard Edition||||  
|StreamInsight HA|StreamInsight Premium Edition|||||||  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2014 的产品规格](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [安装 SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [SQL Server 2014 安装快速入门](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
