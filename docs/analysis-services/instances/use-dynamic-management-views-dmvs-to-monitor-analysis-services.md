---
title: Analysis Services 中使用动态管理视图 (Dmv) |Microsoft Docs
ms.date: 09/25/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 24dd1bce8d7433f55ba64eecb1e7a08396b9e548
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209413"
---
# <a name="dynamic-management-views-dmvs"></a>动态管理视图 (DMV) 

[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

Analysis Services 动态管理视图 (DMV) 是查询，返回有关模型对象、 服务器操作和服务器运行状况的信息。 基于 SQL 的查询是接口*架构行集*。 架构行集是预设包含有关 Analysis Services 对象和服务器状态，包括数据库架构、 活动会话、 连接、 命令和在服务器执行的作业信息的表。

DMV 查询可用来代替运行 XML/A 发现命令。 对于大多数管理员，编写 DMV 查询是更简单的因为语法基于 SQL。 此外，更轻松地读取和复制以表格格式返回的结果。 
  
大多数 DMV 查询使用**选择**语句和 **$System**架构具有 XML/A 架构行集，例如：  
  
```  
SELECT * FROM $System.<schemaRowset>  
```  
  
 DMV 查询返回有关服务器和对象状态信息时运行查询。 若要监视中实时的使用应改用跟踪的操作。 若要详细了解实时监视使用跟踪信息，请参阅[使用 SQL Server Profiler 监视 Analysis services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)。  
  
## <a name="query-syntax"></a>查询语法

用于 DMV 的查询引擎是数据挖掘分析器。 DMV 查询语法基于在选择&#40;DMX&#41;语句。 尽管 DMV 查询语法基于 SQL SELECT 语句，但它并不支持 SELECT 语句的完整语法。 尤其是不支持 JOIN、GROUP BY、LIKE、CAST 和 CONVERT。  
  
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
  
对于具有限制的架构行集，该查询必须包含 SYSTEMRESTRICTSCHEMA 函数。 下面的示例返回大约 1103年兼容级别表格模型的 CSDL 元数据。 请注意 CATALOG_NAME 区分大小写：  
  
```  
Select * from SYSTEMRESTRICTSCHEMA ($System.Discover_csdl_metadata, [CATALOG_NAME] = 'Adventure Works DW')  
```  

## <a name="examples-and-scenarios"></a>示例和方案

DMV 查询可帮助您回答与活动会话和连接有关的问题，以及在特定时间点哪些对象最占用 CPU 或内存。 例如：
  
 `Select * from $System.discover_object_activity`  
此查询报告自上次启动该服务后的对象活动。 
  
 `Select * from $System.discover_object_memory_usage`  
此查询按对象报告内存使用情况。  
  
 `Select * from $System.discover_sessions`  
此查询报告活动会话，包括会话用户和持续时间。  
  
 `Select * from $System.discover_locks`   
此查询将返回时间的特定点处使用的锁的快照。  


## <a name="tools-and-permissions"></a>工具和权限

可以使用支持 MDX 或 DMX 查询的任何客户端应用程序。 在大多数情况下，最好使用 SQL Server Management Studio。 您必须具有服务器管理员权限才能查询 DMV 的实例上。  
  
 **若要从 SQL Server Management Studio 运行 DMV 查询**

1. 连接到服务器和您想要查询的模型对象。 
2. 右键单击服务器或数据库对象 >**新查询** > **MDX**。
3. 键入查询，然后依次**Execute**，或按 F5。
  
## <a name="schema-rowsets"></a>架构行集

并不是所有的架构行集都具有 DMV 接口。 若要返回可使用 DMV 查询的所有架构行集的列表，请运行以下查询。  
 
```  
SELECT * FROM $System.DBSchema_Tables   
WHERE TABLE_TYPE = 'SCHEMA'   
ORDER BY TABLE_NAME ASC  
```  
  
如果 DMV 不可用于给定行集，则服务器将返回错误：`The <schemarowset> request type was not recognized by the server.` 所有其他错误表示与语法问题。  

架构行集是在两个 SQL Server Analysis Services 协议中所述：   

[[MS-SSAS-T]:SQL Server Analysis Services 表格协议](https://msdn.microsoft.com/library/mt719260)-介绍针对 1200年及更高版本的兼容性级别的表格模型架构行集。

[[MS-SSAS]:SQL Server Analysis Services 协议](https://msdn.microsoft.com/library/ee320606)-介绍用于多维模型和表格模型 1100年和 1103年兼容级别的架构行集。

### <a name="rowsets-described-in-the-ms-ssas-t-sql-server-analysis-services-tabular-protocol"></a>行集 [MS-SSAS-T] 中所述：SQL Server Analysis Services 表格协议

|行集  |描述  |
|---------|---------|
|[TMSCHEMA_ANNOTATIONS](https://msdn.microsoft.com/library/mt704370)|提供有关批注对象模型中的信息。|
|[TMSCHEMA_ATTRIBUTE_HIERARCHIES](https://msdn.microsoft.com/library/mt704362)     |   为列提供有关 AttributeHierarchy 对象的信息。      |
|[TMSCHEMA_COLUMNS](https://msdn.microsoft.com/library/mt704373)    |  提供有关每个表中的列对象的信息。       |
|[TMSCHEMA_COLUMN_PERMISSIONS](https://msdn.microsoft.com/library/mt842440)|提供有关在每个表权限的 ColumnPermission 对象的信息。|
|[TMSCHEMA_CULTURES](https://msdn.microsoft.com/library/mt719125)|提供有关在模型中的区域性对象的信息。|
|[TMSCHEMA_DATA_SOURCES](https://msdn.microsoft.com/library/mt719191)   |   提供有关在模型中的数据源对象的信息。      |
|[TMSCHEMA_DETAIL_ROWS_DEFINITIONS](https://msdn.microsoft.com/library/mt825017)|提供有关在模型中的 DetailRowsDefinition 对象的信息。|
|[TMSCHEMA_EXPRESSIONS](https://msdn.microsoft.com/library/mt825015)|提供有关表达式对象模型中的信息。|
|[TMSCHEMA_EXTENDED_PROPERTIES](https://msdn.microsoft.com/library/mt842451)|提供有关在模型中的 ExtendedProperty 对象的信息。|
|[TMSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/mt719136)    |    提供有关每个表中的层次结构对象的信息。     |
|[TMSCHEMA_KPIS](https://msdn.microsoft.com/library/mt719002)     |    提供有关在模型中的 KPI 对象的信息。     |
|[TMSCHEMA_LEVELS](https://msdn.microsoft.com/library/mt719038)     |   提供有关每个层次结构中级别对象的信息。      |
|[TMSCHEMA_LINGUISTIC_METADATA](https://msdn.microsoft.com/library/mt719169)|提供有关同义词的对象模型中的特定区域性的信息|
|[TMSCHEMA_MEASURES](https://msdn.microsoft.com/library/mt719218)     |    提供有关每个表中的度量值对象的信息。     |
|[TMSCHEMA_MODEL](https://msdn.microsoft.com/library/mt719042)    |  在数据库中指定的模型对象。       |
|[TMSCHEMA_OBJECT_TRANSLATIONS](https://msdn.microsoft.com/library/mt719119)|区域性提供有关不同对象的翻译的信息。|
|[TMSCHEMA_PARTITIONS](https://msdn.microsoft.com/library/mt704375)     |     提供有关每个表中的分区对象的信息。    |
|[TMSCHEMA_PERSPECTIVE_COLUMNS](https://msdn.microsoft.com/library/mt719164)     |   提供有关每个 PerspectiveTable 对象中的 PerspectiveColumn 对象的信息。      |
|[TMSCHEMA_PERSPECTIVE_HIERARCHIES](https://msdn.microsoft.com/library/mt719104)     |  提供有关每个 PerspectiveTable 对象中的 PerspectiveHierarchy 对象的信息。       |
|[TMSCHEMA_PERSPECTIVE_MEASURES](https://msdn.microsoft.com/library/mt719135)     |    提供有关每个 PerspectiveTable 对象中的 PerspectiveMeasure 对象的信息。     |
|[TMSCHEMA_PERSPECTIVE_TABLES](https://msdn.microsoft.com/library/mt719272)     |    提供有关在透视表对象的信息。     |
|[TMSCHEMA_PERSPECTIVES](https://msdn.microsoft.com/library/mt704340)     |     提供有关在模型中的透视对象的信息。    |
|[TMSCHEMA_RELATIONSHIPS](https://msdn.microsoft.com/library/mt704355)     |    提供有关在模型中的关系对象的信息。     |
|[TMSCHEMA_ROLE_MEMBERSHIPS](https://msdn.microsoft.com/library/mt704584)     |  提供有关每个角色中的 RoleMembership 对象信息。      |
|[TMSCHEMA_ROLES](https://msdn.microsoft.com/library/mt719267)    |   提供有关在模型中的角色对象的信息。      |
|[TMSCHEMA_TABLE_PERMISSIONS](https://msdn.microsoft.com/library/mt704347)    |    提供有关每个角色中的 TablePermission 对象的信息。     |
|[TMSCHEMA_TABLES](https://msdn.microsoft.com/library/mt719250)     |   提供有关在模型中的表对象的信息。      |
|[TMSCHEMA_VARIATIONS](https://msdn.microsoft.com/library/mt825008)|提供有关每个列中的变体对象的信息。|

### <a name="rowsets-described-in-the-ms-ssas-sql-server-analysis-services-protocol"></a>行集 [MS-SSAS] 中所述：SQL Server Analysis Services 协议

|行集|描述|  
|------------|-----------------|  
|[DBSCHEMA_CATALOGS](https://msdn.microsoft.com/library/ee302115)|描述在服务器进行访问的目录。|  
|[DBSCHEMA_COLUMNS](https://msdn.microsoft.com/library/ee301789)|返回每个度量值、 每个多维数据集维度属性和每个架构行集列，显示为列的行。|  
|[DBSCHEMA_PROVIDER_TYPES](https://msdn.microsoft.com/library/ee301696)|标识服务器支持的 （基本） 数据类型。|  
|[DBSCHEMA_TABLES](https://msdn.microsoft.com/library/ee320843)|返回维度、 度量值组或公开为表的架构行集。|  
|[DISCOVER_CALC_DEPENDENCY](https://msdn.microsoft.com/library/hh770226)| 返回有关表格数据库中或针对表格数据库执行的 DAX 查询中指定的对象的计算依赖项信息。 |  
|[DISCOVER_COMMAND_OBJECTS](https://msdn.microsoft.com/library/ee320662)|提供引用的命令使用的对象的资源使用情况和活动信息。|  
|[DISCOVER_COMMANDS](https://msdn.microsoft.com/library/ee320715)|在服务器上提供有关当前正在执行或最后一个执行的命令打开的连接中的资源使用情况和活动信息。|  
|[DISCOVER_CONNECTIONS](https://msdn.microsoft.com/library/ee301889)|提供服务器上当前打开的连接的资源使用情况和活动信息。|  
|[DISCOVER_CSDL_METADATA](https://msdn.microsoft.com/library/gg587670)|返回有关内存中数据库的数据库元数据信息。|  
|[不应向客户端](https://msdn.microsoft.com/library/ee320285)|返回服务器可用的数据源的列表。|
|[DISCOVER_DB_CONNECTIONS](https://msdn.microsoft.com/library/ee320467)|提供当前打开的服务器到数据库连接的资源使用情况和活动信息。|  
|[DISCOVER_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320284)|返回指定维度的统计信息。|  
|[DISCOVER_ENUMERATORS](https://msdn.microsoft.com/library/ee302012)|返回枚举器的名称、数据类型和枚举值的列表，这些枚举器受特定数据源的 XMLA 访问接口支持。|  
|[DISCOVER_INSTANCES](https://msdn.microsoft.com/library/ee320541)|介绍服务器上的实例。|  
|[DISCOVER_JOBS](https://msdn.microsoft.com/library/ee320363)|提供有关在服务器上执行的活动作业的信息。 作业是命令的一部分，代表命令执行特定任务。|  
|[DISCOVER_KEYWORDS &#40;XMLA&#41;](https://msdn.microsoft.com/library/ee301719)|返回有关 XMLA 服务器保留的关键字的信息。|  
|[DISCOVER_LITERALS](https://msdn.microsoft.com/library/ee301320)|返回有关服务器支持的文本信息。|  
|[DISCOVER_LOCATIONS](https://msdn.microsoft.com/library/ee302024)|返回有关备份文件的内容的信息。 |
|[DISCOVER_LOCKS](https://msdn.microsoft.com/library/ee320398)|提供有关服务器上的当前持续锁定的信息。|  
|[DISCOVER_MASTER_KEY](https://msdn.microsoft.com/library/ee301825)|返回服务器的主加密密钥。|
|[DISCOVER_MEMORYGRANT](https://msdn.microsoft.com/library/ee320945)|返回由当前正在服务器上运行的作业占用的内部内存配额授予的列表。|  
|[DISCOVER_MEMORYUSAGE](https://msdn.microsoft.com/library/ee320910)|返回由服务器分配的各种对象的 DISCOVER_MEMORYUSAGE 统计信息。|  
|[DISCOVER_OBJECT_ACTIVITY](https://msdn.microsoft.com/library/ee320661)|提供在启动服务后每个对象的资源使用情况。|  
|[DISCOVER_OBJECT_MEMORY_USAGE](https://msdn.microsoft.com/library/ee320910)|返回由服务器分配的各种对象的 DISCOVER_MEMORYUSAGE 统计信息。|  
|[DISCOVER_PARTITION_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320268)|返回与分区关联的维度的统计信息。|  
|[DISCOVER_PARTITION_STAT](https://msdn.microsoft.com/library/ee320483)|返回特定分区中的聚合的统计信息。|  
|[DISCOVER_PERFORMANCE_COUNTERS](https://msdn.microsoft.com/library/ee320809)|返回一个或多个指定的性能计数器的值。 |  
|[DISCOVER_PROPERTIES](https://msdn.microsoft.com/library/ee320589)|返回信息和指定的数据源服务器支持的属性的值的列表。|  
|[DISCOVER_RING_BUFFERS](https://msdn.microsoft.com/library/mt719204)|在服务器上返回有关当前的 XEvent 环形缓冲区信息。|
|[DISCOVER_SCHEMA_ROWSETS](https://msdn.microsoft.com/library/ee320478)|返回名称、 限制、 说明和发现的所有请求的其他信息。|  
|[DISCOVER_SESSIONS](https://msdn.microsoft.com/library/ee301962)|提供在服务器上当前打开的会话的资源使用情况和活动信息。|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](https://msdn.microsoft.com/library/ee320710)|返回有关用于存储内存中表的数据的列段的信息。|  
|[DISCOVER_STORAGE_TABLE_COLUMNS](https://msdn.microsoft.com/library/ee302101)|包含有关用于表示内存中表的列的列信息。|  
|[DISCOVER_STORAGE_TABLES](https://msdn.microsoft.com/library/ee302014)|服务器返回有关可用的内存中表的统计信息。|  
|[DISCOVER_TRACE_COLUMNS](https://msdn.microsoft.com/library/ee301342)||  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO](https://msdn.microsoft.com/library/ee301342)|包含 DISCOVER_TRACE_COLUMNS 架构行集。|  
|[DISCOVER_TRACE_EVENT_CATEGORIES](https://msdn.microsoft.com/library/ee320442)|包含 DISCOVER_TRACE_EVENT_CATEGORIES 架构行集。|  
|[DISCOVER_TRACES](https://msdn.microsoft.com/library/ee301643)|包含 DISCOVER_TRACES 架构行集。|  
|[DISCOVER_TRANSACTIONS](https://msdn.microsoft.com/library/ee301363)|返回系统上当前挂起的一组事务。|  
|[DISCOVER_XEVENT_TRACE_DEFINITION](https://msdn.microsoft.com/library/mt704568)|提供有关在服务器当前处于活动状态的 XEvent 跟踪信息。|  
|[DISCOVER_XEVENT_PACKAGES](https://msdn.microsoft.com/library/mt704569)|在服务器上提供有关所述的 XEvent 包信息。|
|[DISCOVER_XEVENT_OBJECTS](https://msdn.microsoft.com/library/mt704543)|提供在服务器上所述的 XEvent 对象有关的信息。|
|[DISCOVER_XEVENT_OBJECT_COLUMNS](https://msdn.microsoft.com/library/mt719352)|在服务器上提供描述的 XEvent 对象的架构的信息。|
|[DISCOVER_XEVENT_SESSIONS](https://msdn.microsoft.com/library/mt704397)|在服务器上提供有关当前的 XEvent 会话的信息。|
|[DISCOVER_XEVENT_SESSION_TARGETS](https://msdn.microsoft.com/library/mt704564)|在服务器上提供有关当前的 XEvent 会话目标的信息。|
|[DISCOVER_XML_METADATA](https://msdn.microsoft.com/library/ee301560)|返回包含一行和一个列的行集。 |
|[DMSCHEMA_MINING_COLUMNS](https://msdn.microsoft.com/library/ee301664)|描述在服务器上的所有部署的所述的数据挖掘模型的各个列。|  
|[DMSCHEMA_MINING_FUNCTIONS](https://msdn.microsoft.com/library/ee320415)|介绍运行 Analysis Services 服务器上可用的数据挖掘算法支持的数据挖掘函数。|  
|[DMSCHEMA_MINING_MODEL_CONTENT](https://msdn.microsoft.com/library/ee302124)|使客户端应用程序浏览定型的数据挖掘模型的内容。|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://msdn.microsoft.com/library/ee320692)|返回挖掘模型的 XML 结构。 XML 字符串的格式遵循 PMML 2.1 标准。|  
|[DMSCHEMA_MINING_MODEL_XML](https://msdn.microsoft.com/library/ee301916)|返回挖掘模型的 XML 结构。 XML 字符串的格式遵循 PMML 2.1 标准。|  
|[DMSCHEMA_MINING_MODELS](https://msdn.microsoft.com/library/ee320603)|枚举在服务器上部署的数据挖掘模型。|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS](https://msdn.microsoft.com/library/ee320378)|提供一个参数列表，这些参数可用于配置安装在服务器上的每个数据挖掘算法的行为。|  
|[DMSCHEMA_MINING_SERVICES](https://msdn.microsoft.com/library/ee320487)|提供有关每个服务器支持的数据挖掘算法的信息。|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS](https://msdn.microsoft.com/library/ee320277)|描述在服务器上部署的所有挖掘结构的各个列。|  
|[DMSCHEMA_MINING_STRUCTURES](https://msdn.microsoft.com/library/ee320704)|枚举有关当前目录中的挖掘结构的信息。|  
|[MDSCHEMA_ACTIONS](https://msdn.microsoft.com/library/ee320890)|介绍可供客户端应用程序的操作。|
|[MDSCHEMA_CUBES](https://msdn.microsoft.com/library/ee301304)|介绍数据库中的多维数据集的结构。 透视也会返回在此架构中。|
|[MDSCHEMA_DIMENSIONS](https://msdn.microsoft.com/library/ee301366)|描述在数据库中的维度。|  
|[MDSCHEMA_FUNCTIONS](https://msdn.microsoft.com/library/mt719467)|返回有关当前可用于在 DAX 和 MDX 语言中使用的函数的信息。|
|[MDSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/ee320250)|介绍特定维度中的每个层次结构。|  
|[MDSCHEMA_INPUT_DATASOURCES](https://msdn.microsoft.com/library/ee301386)|介绍在数据库中所述的数据源对象。|  
|[MDSCHEMA_KPIS](https://msdn.microsoft.com/library/ee320406)|介绍在数据库中的 Kpi。|  
|[MDSCHEMA_LEVELS](https://msdn.microsoft.com/library/ee320746)|介绍特定层次结构中的每个级别。|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS](https://msdn.microsoft.com/library/ee320977)|枚举度量值组的维度。|  
|[MDSCHEMA_MEASUREGROUPS](https://msdn.microsoft.com/library/ee320601)|介绍数据库中的度量值组。|  
|[MDSCHEMA_MEASURES](https://msdn.microsoft.com/library/ee301871)|介绍了每个度量值。|  
|[MDSCHEMA_MEMBERS](https://msdn.microsoft.com/library/ee320960)|介绍数据库中的成员。|  
|[MDSCHEMA_PROPERTIES](https://msdn.microsoft.com/library/ee320393)|描述的成员的属性和单元属性。|  
|[MDSCHEMA_SETS](https://msdn.microsoft.com/library/ee301356)|介绍在数据库中，包括会话作用域的集目前所述的所有组。|  

> [!NOTE]
> 存储 Dmv 并没有在协议中所述的架构行集。