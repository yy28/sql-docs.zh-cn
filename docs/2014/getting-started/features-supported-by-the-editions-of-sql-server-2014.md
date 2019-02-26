---
title: SQL Server 2014 的版本支持的功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- data-quality-services
- database-engine
- integration-services
- master-data-services
- reporting-services-native
- reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0652a2545f0b1e9d591777f0bcabe6395cf4feaa
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2019
ms.locfileid: "56802651"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>SQL Server 2014 各个版本支持的功能


  本主题提供有关不同版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]所支持的功能的详细信息。 

 > **注意：** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]是评估版具有 180 天试用期。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [试用软件网站](https://go.microsoft.com/fwlink/?LinkId=190955)。  
> 
> **注意**：有关 SQL Server Evaluation 版和 SQL Server Developer 版支持的功能，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 功能集。  
  
 若要导航到某种 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 技术相应的表，请单击其链接：  
  
 [转换箱规模限制](#CrossBoxScale)  
  
 [高可用性](#High_availability)  
  
 [可伸缩性和性能](#Scalability)  
  
 [安全性](#Enterprise_security)  
  
 [复制](#Replication)  
  
 [管理工具](#Mgmt_Tools)  
  
 [RDBMS 可管理性](#RDBMS_mgmt)  
  
 [开发工具](#Dev_tools)  
  
 [可编程性](#Programmability)  
  
 [Integration Services](#SSIS)  
  
 [Integration Services-高级适配器](#SSIS_AA)  
  
 [Integration Services-高级转换](#SSIS_AT)  
  
 [Master Data Services](#MDS)  
  
 [数据仓库](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [BI 语义模型 （多维）](#BISemModel_multi)  
  
 [BI 语义模型（表格）](#BISemModel_tabular)  
  
 [PowerPivot for SharePoint](#PowerPivot)  
  
 [数据挖掘](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [Business Intelligence 客户端](#BIClients)  
  
 [空间和位置服务](#Spatial)  
  
 [其他数据库服务](#Add_DBServices)  
  
 [其他组件](#Other_Components)  
  
##  <a name="CrossBoxScale"></a>转换箱规模限制  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|单个实例使用的最大计算能力 ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库引擎)<sup>1</sup>|操作系统支持的最大值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|  
|使用单个实例 (Analysis Services、 Reporting Services) 的最大计算能力<sup>1</sup>|操作系统支持的最大值|操作系统支持的最大值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|  
|利用的最大内存（每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库引擎实例）|操作系统支持的最大值|128 GB|128 GB|64 GB|1 GB|1 GB|1 GB|  
|利用的最大内存（每个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例）|操作系统支持的最大值|操作系统支持的最大值|64 GB|不可用|不可用|不可用|不可用|  
|利用的最大内存（每个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]实例）|操作系统支持的最大值|操作系统支持的最大值|64 GB|64 GB|4 GB|不可用|不可用|  
|最大关系数据库大小|524 PB|524 PB|524 PB|524 PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup> Enterprise Edition 配合服务器 + 客户端访问许可证 (CAL) 基于许可 （对新协议不可用），限制为最多 20 个内核，每个[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例。 基于内核的服务器许可模型没有限制。 有关详细信息，请参阅 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
##  <a name="High_availability"></a> 高可用性  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Server Core 支持<sup>1</sup>|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|日志传送|用户帐户控制|是|是|用户帐户控制||||  
|数据库镜像|用户帐户控制|支持（仅支持“完全”安全级别）|支持（仅支持“完全”安全级别）|仅见证服务器|仅见证服务器|仅见证服务器|仅见证服务器|  
|备份压缩|用户帐户控制|是|用户帐户控制|||||  
|数据库快照|用户帐户控制|||||||  
|AlwaysOn 故障转移群集实例|是（节点支持：操作系统支持的最大值|是（节点支持：2)|是（节点支持：2)|||||  
|AlwaysOn 可用性组|支持（最多 8 个辅助副本，包括 2 个同步辅助副本）|||||||  
|连接控制器|用户帐户控制|||||||  
|联机页面和文件还原|用户帐户控制|||||||  
|联机索引|用户帐户控制|||||||  
|联机架构更改|用户帐户控制|||||||  
|快速恢复|用户帐户控制|||||||  
|镜像备份|用户帐户控制|||||||  
|热添加内存和 CPU<sup>2</sup>|用户帐户控制|||||||  
|数据库恢复顾问|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|加密备份|用户帐户控制|是|用户帐户控制|||||  
|智能备份|用户帐户控制|是|是|否||||  
  
 <sup>1</sup>有关安装的详细信息[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]Server core，请参阅[Server Core 上安装 SQL Server 2014](../database-engine/install-windows/install-sql-server-on-server-core.md)。  
  
 <sup>2</sup>此功能功能仅适用于 64 位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
##  <a name="Scalability"></a> 可伸缩性和性能  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|多实例支持|50|50|50|50|50|50|50|  
|表和索引分区|用户帐户控制|||||||  
|数据压缩|用户帐户控制|||||||  
|Resource Governor|用户帐户控制|||||||  
|分区表并行度|用户帐户控制|||||||  
|多个 Filestream 容器|用户帐户控制|||||||  
|可识别 NUMA 的大型页内存和缓冲区数组分配|用户帐户控制|||||||  
|缓冲池扩展<sup>1</sup>|用户帐户控制|是|用户帐户控制|||||  
|IO 资源调控|用户帐户控制|||||||  
|内存中 OLTP <sup>1</sup>|用户帐户控制|||||||  
|延迟持续性|用户帐户控制|是|是|是|是|是|用户帐户控制|  
  
 <sup>1</sup>此功能功能仅适用于 64 位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
##  <a name="Enterprise_security"></a> 安全性  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|基本审核|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|精细审核|用户帐户控制|||||||  
|透明数据库加密|用户帐户控制|||||||  
|可扩展的密钥管理|用户帐户控制|||||||  
|用户定义的角色|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|包含的数据库|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|备份加密|用户帐户控制|是|用户帐户控制|||||  
  
##  <a name="Replication"></a> Replication  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 更改跟踪|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|合并复制|用户帐户控制|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|  
|事务复制|用户帐户控制|是|是|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|  
|快照复制|用户帐户控制|是|用户帐户控制|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|支持（仅订阅服务器）|  
|异类订阅服务器|用户帐户控制|是|用户帐户控制|||||  
|Oracle 发布|用户帐户控制|||||||  
|对等事务复制|用户帐户控制|||||||  
  
##  <a name="Mgmt_Tools"></a> Management Tools  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|SQL 管理对象 (SMO)|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|SQL 配置管理器|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|SQL CMD（命令提示工具）|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio|用户帐户控制|是|是|是|是|用户帐户控制||  
|Distributed Replay - 管理工具|用户帐户控制|是|是|是|是|用户帐户控制||  
|分布式重播 - 客户端|用户帐户控制|否|是|用户帐户控制||||  
|分布式重播 - 控制器|支持（Enterprise 版支持最多 16 个客户端、Developer 版仅支持 1 个客户端）|否|支持（仅支持 1 个客户端）|支持（仅支持 1 个客户端）||||  
|SQL Profiler|用户帐户控制|是|用户帐户控制|不<sup>2</sup>|不<sup>2</sup>|不<sup>2</sup>|不<sup>2</sup>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理|用户帐户控制|是|是|用户帐户控制||||  
|Microsoft System Center Operations Manager 管理包|用户帐户控制|是|是|用户帐户控制||||  
|数据库优化顾问 (DTA)|用户帐户控制|用户帐户控制|是<sup>3</sup>|是<sup>3</sup>||||  
|将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库部署到 Windows Azure VM 向导|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Windows Azure 中的数据文件|用户帐户控制|是|是|是|是|是|用户帐户控制|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] web [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]， [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Tools 和[!INCLUDE[ssExpress](../includes/ssexpress-md.md)]具有高级服务可以使用探查[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]标准和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Enterprise edition。  
  
 <sup>3</sup>仅对 Standard 版本功能启用优化。  
  
##  <a name="RDBMS_mgmt"></a> RDBMS Manageability  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|用户实例|||||用户帐户控制|是|用户帐户控制|  
|LocalDB|||||用户帐户控制|用户帐户控制||  
|专用管理连接|用户帐户控制|是|是|用户帐户控制|支持（受跟踪标志控制）|支持（受跟踪标志控制）|支持（受跟踪标志控制）|  
|PowerShell 脚本支持|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|SysPrep 支持<sup>1</sup>|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|支持数据层应用程序组件操作-提取、 部署、 升级和删除|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|策略自动执行（检查计划和更改）|用户帐户控制|是|是|用户帐户控制||||  
|性能数据收集器|用户帐户控制|是|是|用户帐户控制||||  
|能够作为多实例管理中的托管实例注册|用户帐户控制|是|是|用户帐户控制||||  
|标准性能报表|用户帐户控制|是|是|用户帐户控制||||  
|计划指南和计划指南的计划冻结|用户帐户控制|是|是|用户帐户控制||||  
|使用 NOEXPAND 提示的索引视图的直接查询|用户帐户控制|是|是|用户帐户控制||||  
|自动的索引视图维护|用户帐户控制|是|是|用户帐户控制||||  
|分布式分区视图|用户帐户控制|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|部分支持。 不能更新分布式分区视图|  
|并行索引操作|用户帐户控制|||||||  
|查询优化器自动使用索引视图|用户帐户控制|||||||  
|并行一致性检查|用户帐户控制|||||||  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具控制点|用户帐户控制|||||||  
|包含的数据库|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|缓冲池扩展<sup>2</sup>|用户帐户控制|是|用户帐户控制|||||  
  
 <sup>1</sup> 有关详细信息，请参阅 [使用 SysPrep 安装 SQL Server 的注意事项](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)。  
  
 <sup>2</sup>此功能功能仅适用于 64 位[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
##  <a name="Dev_tools"></a> Development Tools  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio 集成|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|Intellisense（[!INCLUDE[tsql](../includes/tsql-md.md)] 和 MDX）|用户帐户控制|是|是|是|是|是|是|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|是|是|是|是|用户帐户控制|||  
|SQL 查询编辑和设计工具<sup>1</sup>|用户帐户控制|是|用户帐户控制|||||  
|版本控制支持<sup>1</sup>|用户帐户控制|是|用户帐户控制|||||  
|MDX 编辑、 调试和设计工具<sup>1</sup>|用户帐户控制|是|用户帐户控制|||||  
  
 <sup>1</sup>此功能不适用于 Standard 版的 64 位版本。  
  
##  <a name="Programmability"></a> Programmability  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|公共语言运行时 (CLR) 集成|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|本机 XML 支持|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|XML 索引|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|MERGE 和 UPSERT 功能|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|FILESTREAM 支持|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|FileTable|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|日期和时间数据类型|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|国际化支持|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|全文和语义搜索|用户帐户控制|是|是|是|用户帐户控制|||  
|查询中的语言规范|用户帐户控制|是|是|是|用户帐户控制|||  
|Service Broker（消息传递）|用户帐户控制|是|用户帐户控制|不支持（仅客户端）|不支持（仅客户端）|不支持（仅客户端）|不支持（仅客户端）|  
|[!INCLUDE[tsql](../includes/tsql-md.md)] 端点|用户帐户控制|是|是|用户帐户控制||||  
  
##  <a name="SSIS"></a> Integration Services  
  
|功能|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|内置数据源连接器|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|SSIS 设计器和运行时|用户帐户控制|是|用户帐户控制|||||  
|基本转换|用户帐户控制|是|用户帐户控制|||||  
|基本数据探查工具|用户帐户控制|是|用户帐户控制|||||  
|Change Data Capture Service for Oracle by Attunity|用户帐户控制|||||||  
|Change Data Capture Designer for Oracle by Attunity|用户帐户控制|||||||  
  
###  <a name="SSIS_AA"></a> Integration Services - 高级适配器  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|高性能 Oracle 目标|用户帐户控制|||||||  
|高性能 Teradata 目标|用户帐户控制|||||||  
|SAP BW 源和目标|用户帐户控制|||||||  
|数据挖掘模型定型目标适配器|用户帐户控制|||||||  
|维度处理目标适配器|用户帐户控制|||||||  
|分区处理目标适配器|用户帐户控制|||||||  
|Attunity 提供的变更数据捕获组件|用户帐户控制|||||||  
|Attunity 提供的开放式数据库连接 (ODBC)|用户帐户控制|||||||  
  
###  <a name="SSIS_AT"></a> Integration Services - 高级转换  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|持续性（高性能）查找|用户帐户控制|||||||  
|数据挖掘查询转换|用户帐户控制|||||||  
|模糊分组和查找转换|用户帐户控制|||||||  
|术语提取和查找转换|用户帐户控制|||||||  
  
##  <a name="MDS"></a> Master Data Services  
  
> [!NOTE]  
>  -   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 仅适用于 Business Intelligence 版和 Enterprise 版的 64 位版本。  
  
|功能|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库|用户帐户控制|用户帐户控制||||||  
|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序|用户帐户控制|用户帐户控制||||||  
  
##  <a name="Data_warehouse"></a> Data Warehouse  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|在无需数据库的情况下创建多维数据集|用户帐户控制|是|用户帐户控制|||||  
|自动生成临时和数据仓库架构|用户帐户控制|是|用户帐户控制|||||  
|变更数据捕获|用户帐户控制|||||||  
|星型联接查询优化|用户帐户控制|||||||  
|可扩展的只读 Analysis Services 配置|用户帐户控制|||||||  
|针对已分区表和索引的并行查询处理|用户帐户控制|||||||  
|xVelocity 内存优化的列存储索引|用户帐户控制|||||||  
|全局批处理集成|用户帐户控制|||||||  
  
##  <a name="SSAS"></a> Analysis Services  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|可扩展的共享数据库（附加/分离，只读数据库）|用户帐户控制|用户帐户控制||||||  
|备份/还原、附加/分离数据库|用户帐户控制|是|用户帐户控制|||||  
|同步数据库|用户帐户控制|用户帐户控制||||||  
|高可用性|用户帐户控制|是|用户帐户控制|||||  
|可编程性（AMO、ADOMD.Net、OLEDB、XML/A、ASSL）|用户帐户控制|是|用户帐户控制|||||  
  
###  <a name="BISemModel_multi"></a> BI 语义模型 （多维）  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|半累加性度量值|用户帐户控制|用户帐户控制|不<sup>1</sup>|||||  
|层次结构|用户帐户控制|是|用户帐户控制|||||  
|KPI|用户帐户控制|是|用户帐户控制|||||  
|透视|用户帐户控制|用户帐户控制||||||  
|操作|用户帐户控制|是|用户帐户控制|||||  
|帐户智能|用户帐户控制|是|用户帐户控制|||||  
|时间智能|用户帐户控制|是|用户帐户控制|||||  
|自定义汇总|用户帐户控制|是|用户帐户控制|||||  
|写回多维数据集|用户帐户控制|是|用户帐户控制|||||  
|写回维度|用户帐户控制|用户帐户控制||||||  
|写回单元|用户帐户控制|是|用户帐户控制|||||  
|钻取|用户帐户控制|是|用户帐户控制|||||  
|高级层次结构类型（父子、不规则层次结构）|用户帐户控制|是|用户帐户控制|||||  
|高级维度（引用维度、多对多维度）|用户帐户控制|是|用户帐户控制|||||  
|链接度量值和维度|用户帐户控制|用户帐户控制||||||  
|翻译|用户帐户控制|是|用户帐户控制|||||  
|Aggregations|用户帐户控制|是|用户帐户控制|||||  
|多个分区|用户帐户控制|用户帐户控制|支持，最多 3 个|||||  
|主动缓存|用户帐户控制|用户帐户控制||||||  
|自定义程序集（存储过程）|用户帐户控制|是|用户帐户控制|||||  
|MDX 查询和脚本|用户帐户控制|是|用户帐户控制|||||  
|DAX 查询|用户帐户控制|用户帐户控制||||||  
|基于角色的安全模型|用户帐户控制|是|用户帐户控制|||||  
|维度和单元级别的安全性|用户帐户控制|是|用户帐户控制|||||  
|可扩展字符串存储|用户帐户控制|是|用户帐户控制|||||  
|MOLAP、ROLAP、HOLAP 存储模式|用户帐户控制|是|用户帐户控制|||||  
|二进制和压缩的 XML 传输|用户帐户控制|是|用户帐户控制|||||  
|推送模式处理|用户帐户控制|用户帐户控制||||||  
|直接写回|用户帐户控制|用户帐户控制||||||  
|度量值表达式|用户帐户控制|用户帐户控制||||||  
  
 <sup>1</sup>standard edition 支持 LastChild 半累加性度量值，但其他半累加性度量值，例如 None、 FirstChild、 FirstNonEmpty、 LastNonEmpty、 AverageOfChildren 和 ByAccount。 在所有版本上都支持累加性度量值（如 Sum、Count、Min 和 Max）和非累加性度量值 (DistinctCount)。  
  
###  <a name="BISemModel_tabular"></a> BI Semantic Model (Tabular)  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|层次结构|用户帐户控制|用户帐户控制||||||  
|KPI|用户帐户控制|用户帐户控制||||||  
|透视|用户帐户控制|用户帐户控制||||||  
|翻译|用户帐户控制|用户帐户控制||||||  
|DAX 计算、DAX 查询、MDX 查询|用户帐户控制|用户帐户控制||||||  
|行级安全性|用户帐户控制|用户帐户控制||||||  
|“度量值组”|用户帐户控制|用户帐户控制||||||  
|内存中和 DirectQuery 存储模式（仅限表格）|用户帐户控制|用户帐户控制||||||  
  
###  <a name="PowerPivot"></a> PowerPivot for SharePoint  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|基于共享服务体系结构的 SharePoint 场集成|用户帐户控制|用户帐户控制||||||  
|用量报告|用户帐户控制|用户帐户控制||||||  
|运行状况监视规则|用户帐户控制|用户帐户控制||||||  
|PowerPivot 库|用户帐户控制|用户帐户控制||||||  
|PowerPivot 数据刷新|用户帐户控制|用户帐户控制||||||  
|PowerPivot 数据馈送|用户帐户控制|用户帐户控制||||||  
  
###  <a name="DataMining"></a> 数据挖掘  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|标准算法|用户帐户控制|是|用户帐户控制|||||  
|数据挖掘工具（向导、编辑器、查询生成器）|用户帐户控制|是|用户帐户控制|||||  
|交叉验证|用户帐户控制|用户帐户控制||||||  
|挖掘结构数据的筛选子集的模型|用户帐户控制|用户帐户控制||||||  
|时序：ARTXP 和 ARIMA 方法之间的自定义混和|用户帐户控制|用户帐户控制||||||  
|时序：用新数据进行预测|用户帐户控制|用户帐户控制||||||  
|无限制并发数据挖掘查询|用户帐户控制|用户帐户控制||||||  
|数据挖掘算法的高级配置和优化选项|用户帐户控制|用户帐户控制||||||  
|支持插件算法|用户帐户控制|用户帐户控制||||||  
|并行模型处理|用户帐户控制|用户帐户控制||||||  
|时序：跨序列预测|用户帐户控制|用户帐户控制||||||  
|关联规则的无限制属性|用户帐户控制|用户帐户控制||||||  
|序列预测|用户帐户控制|用户帐户控制||||||  
|Naïve Bayes、神经网络和逻辑回归的多个预测目标|用户帐户控制|用户帐户控制||||||  
  
##  <a name="Reporting"></a> Reporting Services  
  
###  <a name="Reporting_features"></a> Reporting Services 功能  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|支持的目录 DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Standard 或更高版本|Standard 或更高版本|Standard 或更高版本|Web|Express|||  
|支持的数据源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|Web|Express|||  
|报表服务器|用户帐户控制|是|是|是|用户帐户控制|||  
|报表设计器|用户帐户控制|是|是|是|用户帐户控制|||  
|报表管理器|用户帐户控制|是|是|是|用户帐户控制|||  
|基于角色的安全性|用户帐户控制|是|是|是|用户帐户控制|||  
|Word 导出和 RTF 格式支持|用户帐户控制|是|是|是|用户帐户控制|||  
|增强的仪表和图表|用户帐户控制|是|是|是|用户帐户控制|||  
|导出到 Excel、PDF 和图像|用户帐户控制|是|是|是|用户帐户控制|||  
|自定义身份验证|用户帐户控制|是|是|是|用户帐户控制|||  
|作为数据馈送的报表|用户帐户控制|是|是|是|用户帐户控制|||  
|模型支持|用户帐户控制|是|是|用户帐户控制||||  
|为基于角色的安全性创建自定义角色|用户帐户控制|是|用户帐户控制|||||  
|模型项安全性|用户帐户控制|是|用户帐户控制|||||  
|无限制链接点击|用户帐户控制|是|用户帐户控制|||||  
|共享组件库|用户帐户控制|是|用户帐户控制|||||  
|电子邮件和文件共享订阅和计划|用户帐户控制|是|用户帐户控制|||||  
|报表历史记录、执行快照和缓存|用户帐户控制|是|用户帐户控制|||||  
|SharePoint 集成|用户帐户控制|是|用户帐户控制|||||  
|远程和非 SQL 数据源支持<sup>1</sup>|用户帐户控制|是|用户帐户控制|||||  
|数据源、传递和呈现、RDCE 可扩展性|用户帐户控制|是|用户帐户控制|||||  
|数据驱动报表订阅|用户帐户控制|用户帐户控制||||||  
|扩展部署（Web 场）|用户帐户控制|用户帐户控制||||||  
|警报<sup>2</sup>|用户帐户控制|用户帐户控制||||||  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|用户帐户控制|用户帐户控制||||||  
  
 <sup>1</sup>有关详细信息中支持的数据源[!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]，请参阅[支持的 Reporting Services 数据源&#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
 <sup>2</sup>需要[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]在 SharePoint 模式下。 有关详细信息，请参阅[Reporting Services SharePoint 模式下安装&#40;SharePoint 2010 和 SharePoint 2013&#41;](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)。  
  
### <a name="report-server-database-server-edition-requirements"></a>报表服务器数据库的服务器版本要求  
 创建报表服务器数据库时，并非所有版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 均可用来承载数据库。 下表显示了可用于特定 [!INCLUDE[ssDE](../includes/ssde-md.md)] 版本的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]版本。  
  
|对于此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services 版本|使用此版本的数据库引擎实例来承载数据库|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Standard Edition、Business Intelligence Enterprise Edition（本地或远程）|  
|Business Intelligence|Standard Edition、Business Intelligence Enterprise Edition（本地或远程）|  
|标准|Standard Edition、Enterprise Edition（本地或远程）|  
|Web|Web Edition（仅用于本地）|  
|Express with Advanced Services|Express with Advanced Services（仅用于本地）。|  
|Evaluation|Evaluation|  
  
##  <a name="BIClients"></a> Business Intelligence 客户端  
 以下软件客户端应用程序在 Microsoft 下载中心提供，它们旨在帮助您创建在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上运行的商业智能文档。 当您在某一服务器环境中承载这些文档时，请使用支持该文档类型的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 下表标识哪一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本包含承载在这些客户端应用程序中创建的文档所需的服务器功能。  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|用户帐户控制|是|用户帐户控制|||||  
|用于 Excel 和 Visio 2010 的数据挖掘外接程序|用户帐户控制|是|用户帐户控制|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010|用户帐户控制|用户帐户控制||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|用户帐户控制|用户帐户控制||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 是 Excel 外接程序，而不依赖于[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 但是，在 SharePoint 中与 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 工作簿共享和协作需要 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 。此功能在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 和 Business Intelligence 版本中提供。  
> 2.  上表标识了仅启用这些客户端工具所需的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本；但是，这些功能可以访问在任何版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上承载的数据。  
  
##  <a name="Spatial"></a> Spatial and Location Services  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|空间索引|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|平面和大地测量数据类型|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|高级空间库|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|导入/导出业界标准的空间数据格式|用户帐户控制|是|是|是|是|是|用户帐户控制|  
  
##  <a name="Add_DBServices"></a> Additional Database Services  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 迁移助手|用户帐户控制|是|是|是|是|是|用户帐户控制|  
|数据库邮件|用户帐户控制|是|是|用户帐户控制||||  
  
##  <a name="Other_Components"></a>其他组件  
  
|功能名称|Enterprise|Business Intelligence|标准|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Data Quality Services|用户帐户控制|用户帐户控制||||||  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|StreamInsight Standard Edition||||  
|StreamInsight HA|StreamInsight Premium Edition|||||||  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 的产品规格](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [SQL Server 2014 安装](../database-engine/install-windows/installation-for-sql-server.md)   
 [SQL Server 2014 安装快速入门](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
