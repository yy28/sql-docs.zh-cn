---
title: "使用动态管理视图 (DMV) 监视 Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22b82b2d-867f-4ebf-9288-79d1cdd62f18
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 16
---
# 使用动态管理视图 (DMV) 监视 Analysis Services
  Analysis Services 动态管理视图 (DMV) 是公开与本地服务器操作和服务器运行状况有关信息的查询结构。 该查询结构是返回与 Analysis Services 实例有关的元数据和监视信息的架构行集的接口。  
  
 对于大多数 DMV 查询，你会使用 **SELECT** 语句以及具有 XML/A 架构行集的 **$System** 架构。  
  
```  
SELECT * FROM $System.<schemaRowset>  
```  
  
 DMV 查询将返回查询运行时所处的服务器状态的有关信息。 若要实时监视操作，应改用跟踪。 有关详细信息，请参阅 [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)。  
  
 本主题包含以下各节：  
  
 [使用 DMV 查询的好处](#bkmk_ben)  
  
 [示例和应用场景](#bkmk_ex)  
  
 [查询语法](#bkmk_syn)  
  
 [工具和权限](#bkmk_tools)  
  
 [DMV 参考](#bkmk_ref)  
  
##  <a name="bkmk_ben"></a> 使用 DMV 查询的好处  
 DMV 查询返回与无法通过其他方式得到的操作和资源使用有关的信息。  
  
 DMV 查询可用来代替运行 XML/A 发现命令。 对于大多数管理员，编写 DMV 查询很简单，因为查询语法基于 SQL。 此外，结果集以易于读取和复制的表格格式返回。  
  
##  <a name="bkmk_ex"></a> 示例和应用场景  
 DMV 查询可帮助您回答与活动会话和连接有关的问题，以及在特定时间点哪些对象最占用 CPU 或内存。 本节提供了最常使用 DMV 查询的应用场景示例。 您也可以查看 [SQL Server 2008 R2 Analysis Services 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409) ，了解使用 DMV 查询监视服务器实例的其他内情。  
  
 `Select * from $System.discover_object_activity` /** 此查询报告自上次启动该服务后的对象活动。 有关基于此 DMV 的查询的示例，请参阅[新的 System.Discover_Object_Activity](http://go.microsoft.com/fwlink/?linkid=221322)。  
  
 `Select * from $System.discover_object_memory_usage` /** 此查询按对象报告内存使用情况。  
  
 `Select * from $System.discover_sessions` /** 此查询报告活动会话，包括会话用户和持续时间。  
  
 `Select * from $System.discover_locks` /** 此查询返回在特定时间点使用的锁的快照。  
  
##  <a name="bkmk_syn"></a> 查询语法  
 用于 DMV 的查询引擎是数据挖掘分析器。 DMV 查询语法基于 [SELECT (DMX)](../../dmx/select-dmx.md) 语句。  
  
 尽管 DMV 查询语法基于 SQL SELECT 语句，但它并不支持 SELECT 语句的完整语法。 尤其是不支持 JOIN、GROUP BY、LIKE、CAST 和 CONVERT。  
  
```  
SELECT [DISTINCT] [TOP <n>] <select list>  
FROM $System.<schemaRowset>  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
 以下针对 DISCOVER_CALC_DEPENDENCY 的示例阐释了如何使用 WHERE 子句来向查询提供参数：  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
WHERE OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
 此外，对于具有限制的架构行集，该查询必须包含 SYSTEMRESTRICTSCHEMA 函数。 下面的示例返回与在表格模式服务器上运行的表格模型有关的 CSDL 元数据。 请注意 CATALOG_NAME 区分大小写：  
  
```  
Select * from SYSTEMRESTRICTSCHEMA ($System.Discover_csdl_metadata, [CATALOG_NAME] = 'Adventure Works DW')  
```  
  
##  <a name="bkmk_tools"></a> 工具和权限  
 您必须对 Analysis Services 实例具有系统管理员权限，才能查询 DMV。  
  
 您可以使用支持 MDX 或 DMX 查询的任何客户端应用程序，包括 SQL Server Management Studio、Reporting Services 报表和 PerformancePoint 面板。  
  
 若要从 Management Studio 运行 DMV 查询，请连接到您要查询的实例，然后单击 **“新建查询”**。 您可以从 MDX 或 DMX 查询窗口运行查询。  
  
##  <a name="bkmk_ref"></a> DMV 参考  
 并不是所有的架构行集都具有 DMV 接口。 若要返回可使用 DMV 查询的所有架构行集的列表，请运行以下查询。  
  
```  
SELECT * FROM $System.DBSchema_Tables   
WHERE TABLE_TYPE = 'SCHEMA'   
ORDER BY TABLE_NAME ASC  
```  
  
> [!NOTE]  
>  如果 DMV 不可用于某一给定行集，服务器将返回以下错误：“服务器未能识别 \<schemarowset> 请求类型。” 所有其他错误均与语法问题有关。  
  
|行集|Description|  
|------------|-----------------|  
|[DBSCHEMA_CATALOGS 行集](../../analysis-services/schema-rowsets/ole-db/dbschema-catalogs-rowset.md)|返回当前连接上 Analysis Services 数据库的列表。|  
|[DBSCHEMA_COLUMNS 行集](../../analysis-services/schema-rowsets/ole-db/dbschema-columns-rowset.md)|返回当前数据库中所有列的列表。 您可以使用此列表来构造 DMV 查询。|  
|[DBSCHEMA_PROVIDER_TYPES 行集](../../analysis-services/schema-rowsets/ole-db/dbschema-provider-types-rowset.md)|返回与 OLE DB 数据访问接口支持的基础数据类型有关的属性。|  
|[DBSCHEMA_TABLES 行集](../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md)|返回当前数据库中所有表的列表。 您可以使用此列表来构造 DMV 查询。|  
|[DISCOVER_CALC_DEPENDENCY 行集](../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)|返回在某一模型中使用的与其他列和表有依赖关系的列和表的列表。|  
|[DISCOVER_COMMAND_OBJECTS 行集](../../analysis-services/schema-rowsets/xml/discover-command-objects-rowset.md)|提供与引用的命令使用的对象有关的资源使用情况和活动信息。|  
|[DISCOVER_COMMANDS 行集](../../analysis-services/schema-rowsets/xml/discover-commands-rowset.md)|提供有关当前正在执行的命令的资源使用情况和活动信息。|  
|[DISCOVER_CONNECTIONS 行集](../../analysis-services/schema-rowsets/xml/discover-connections-rowset.md)|提供与 Analysis Services 的打开的连接有关的资源使用情况和活动信息。|  
|[DISCOVER_CSDL_METADATA 行集](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)|返回有关表格模型的信息。<br /><br /> 要求添加 SYSTEMRESTRICTSCHEMA 和附加的参数。|  
|[DISCOVER_DB_CONNECTIONS 行集](../../analysis-services/schema-rowsets/xml/discover-db-connections-rowset.md)|提供与从 Analysis Services 到外部数据源（例如在处理或导入过程中）打开的连接有关的资源使用情况和活动信息。|  
|[DISCOVER_DIMENSION_STAT 行集](../../analysis-services/schema-rowsets/xml/discover-dimension-stat-rowset.md)|根据模型类型，返回维度中的属性或表中的列。|  
|[DISCOVER_ENUMERATORS 行集](../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)|返回与支持特定数据源的枚举器有关的元数据。|  
|[DISCOVER_INSTANCES 行集](../../analysis-services/schema-rowsets/ole-db-olap/discover-instances-rowset.md)|返回有关指定的实例的信息。<br /><br /> 要求添加 SYSTEMRESTRICTSCHEMA 和附加的参数。|  
|[DISCOVER_JOBS 行集](../../analysis-services/schema-rowsets/xml/discover-jobs-rowset.md)|返回有关当前作业的信息。|  
|[DISCOVER_KEYWORDS 行集 (XMLA)](../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)|返回保留关键字的列表。|  
|[DISCOVER_LITERALS 行集](../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)|返回 XMLA 支持的文字的列表，包括数据类型和值。|  
|[DISCOVER_LOCKS 行集](../../analysis-services/schema-rowsets/xml/discover-locks-rowset.md)|返回在特定时间点使用的锁的快照。|  
|[DISCOVER_MEMORYGRANT 行集](../../analysis-services/schema-rowsets/xml/discover-memorygrant-rowset.md)|返回 Analysis Services 在启动时分配的内存的有关信息。|  
|[DISCOVER_MEMORYUSAGE 行集](../../analysis-services/schema-rowsets/xml/discover-memoryusage-rowset.md)|显示特定对象的内存使用情况。|  
|[DISCOVER_OBJECT_ACTIVITY 行集](../../analysis-services/schema-rowsets/xml/discover-object-activity-rowset.md)|报告自上次启动该服务后的对象活动。|  
|[DISCOVER_OBJECT_MEMORY_USAGE 行集](../../analysis-services/schema-rowsets/xml/discover-object-memory-usage-rowset.md)|按对象报告内存使用情况。|  
|[DISCOVER_PARTITION_DIMENSION_STAT 行集](../../analysis-services/schema-rowsets/xml/discover-partition-dimension-stat-rowset.md)|提供有关维度中的属性的信息。<br /><br /> 要求添加 SYSTEMRESTRICTSCHEMA 和附加的参数。|  
|[DISCOVER_PARTITION_STAT 行集](../../analysis-services/schema-rowsets/xml/discover-partition-stat-rowset.md)|提供有关维度、表或度量值组中的分区的信息。<br /><br /> 要求添加 SYSTEMRESTRICTSCHEMA 和附加的参数。|  
|[DISCOVER_PERFORMANCE_COUNTERS 行集](../../analysis-services/schema-rowsets/xml/discover-performance-counters-rowset.md)|列出性能计数器中使用的列。<br /><br /> 要求添加 SYSTEMRESTRICTSCHEMA 和附加的参数。|  
|[DISCOVER_PROPERTIES 行集](../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md)|返回 XMLA 支持的针对指定数据源的属性的有关信息。|  
|[DISCOVER_SCHEMA_ROWSETS 行集](../../analysis-services/schema-rowsets/xml/discover-schema-rowsets-rowset.md)|返回 XMLA 支持的针对所有枚举值的名称、限制、说明和其他信息。|  
|[DISCOVER_SESSIONS 行集](../../analysis-services/schema-rowsets/xml/discover-sessions-rowset.md)|报告活动会话，包括会话用户和持续时间。|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 行集](../../analysis-services/schema-rowsets/xml/discover-storage-table-column-segments-rowset.md)|在列级和段级提供有关在表格或 SharePoint 模式下运行的 Analysis Services 数据库使用的存储表的信息。|  
|[DISCOVER_STORAGE_TABLE_COLUMNS 行集](../../analysis-services/schema-rowsets/xml/discover-storage-table-columns-rowset.md)|允许客户端确定在表格或 SharePoint 模式下运行的 Analysis Services 数据库使用的存储表的列分配。|  
|[DISCOVER_STORAGE_TABLES 行集](../../analysis-services/schema-rowsets/xml/discover-storage-tables-rowset.md)|返回用于在表格模型数据库中存储模型的表的有关信息。|  
|[DISCOVER_TRACE_COLUMNS 行集](../../analysis-services/schema-rowsets/xml/discover-trace-columns-rowset.md)|返回可用于跟踪的列的 XML 说明。|  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO 行集](../../analysis-services/schema-rowsets/xml/discover-trace-definition-providerinfo-rowset.md)|返回访问接口的名称和版本信息。|  
|[DISCOVER_TRACE_EVENT_CATEGORIES 行集](../../analysis-services/schema-rowsets/xml/discover-trace-event-categories-rowset.md)|返回可用类别的列表。|  
|[DISCOVER_TRACES 行集](../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)|返回正在当前连接上主动运行的跟踪的列表。|  
|[DISCOVER_TRANSACTIONS 行集](../../analysis-services/schema-rowsets/xml/discover-transactions-rowset.md)|返回正在当前连接上主动运行的事务的列表。|  
|[DISCOVER_XEVENT_TRACE_DEFINITION 行集](../Topic/DISCOVER_XEVENT_TRACE_DEFINITION%20Rowset.md)|返回正在当前连接上主动运行的 xevent 跟踪的列表。|  
|[DMSCHEMA_MINING_COLUMNS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|列出在当前连接上可用的所有挖掘模型的单独列。|  
|[DMSCHEMA_MINING_FUNCTIONS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)|返回服务器上的数据挖掘算法支持的函数的列表。|  
|[DMSCHEMA_MINING_MODEL_CONTENT 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|返回由描述当前模型的列组成的行集。|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|以 PMML 格式返回由描述当前模型的列组成的行集。|  
|[DMSCHEMA_MINING_MODEL_XML 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)|以 PMML 格式返回由描述当前模型的列组成的行集。|  
|[DMSCHEMA_MINING_MODELS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|返回当前数据库中挖掘模型的列表。|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|返回服务器上算法参数的列表。|  
|[DMSCHEMA_MINING_SERVICES 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|提供可用于服务器的数据挖掘算法的列表。|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|返回在当前连接中提供的所有挖掘模型的所有列的列表。|  
|[DMSCHEMA_MINING_STRUCTURES 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|列出当前连接中可用的挖掘结构。|  
|[MDSCHEMA_CUBES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|返回有关在当前数据库中定义的多维数据集的信息。|  
|[MDSCHEMA_DIMENSIONS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|返回有关在当前数据库中定义的维度的信息。|  
|[MDSCHEMA_FUNCTIONS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)|返回可用于已连接到数据库的客户端应用程序的列表。|  
|[MDSCHEMA_HIERARCHIES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|返回有关在当前数据库中定义的层次结构的信息。|  
|[MDSCHEMA_INPUT_DATASOURCES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)|返回有关在当前数据库中定义的数据源对象的信息。|  
|[MDSCHEMA_KPIS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|返回有关在当前数据库中定义的 KPI 的信息。|  
|[MDSCHEMA_LEVELS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|返回有关在当前数据库中定义的层次结构内的级别的信息。|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)|列出度量值组的维度。|  
|[MDSCHEMA_MEASUREGROUPS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)|返回当前连接中度量值组的列表。|  
|[MDSCHEMA_MEASURES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|返回当前连接中度量值的列表。|  
|[MDSCHEMA_MEMBERS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|返回在当前连接中按数据库、多维数据集和维度列出的所有成员的列表。|  
|[MDSCHEMA_PROPERTIES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|返回每个属性的完全限定名，以及属性类型、数据类型和其他元数据。|  
|[MDSCHEMA_SETS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|返回当前连接中定义的集合的列表。|  
  
## 另请参阅  
 [SQL Server 2008 R2 Analysis Services 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409)   
 [新的 System.Discover_Object_Activity](http://go.microsoft.com/fwlink/?linkid=221322)   
 [新的 SYSTEMRESTRICTEDSCHEMA 函数，适用于受限行集和 DMV](http://go.microsoft.com/fwlink/?LinkId=231885)  
  
  