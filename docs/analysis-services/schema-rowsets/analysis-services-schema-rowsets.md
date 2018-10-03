---
title: Analysis Services 架构行集 |Microsoft Docs
ms.date: 10/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4ec9d6c75ef1d3cdc8effdc44861eed5971ced60
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116677"
---
# <a name="analysis-services-schema-rowsets"></a>Analysis Services 架构行集
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  架构行集是预定义的表，其中包含有关 Analysis Services 对象和服务器状态（包括在服务器上执行的数据库架构、活动的会话、连接、命令和作业）的信息。 您可以在 SQL Server Management Studio 的 XML/A 脚本窗口中查询架构行集表、对架构行集运行 DMV 查询，或创建包含架构行集信息的自定义应用程序（例如，检索可用于创建报表的可用维度列表的报表应用程序）。  
  
> [!NOTE]  
>  如果使用架构行集在 XML/A 脚本，在返回的信息*结果*的参数[Discover](../../analysis-services/xmla/xml-elements-methods-discover.md)方法根据在此介绍的行集列布局进行构建部分。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持 XML for Analysis 规范所需的行集。 XMLA 访问接口还支持 OLE DB、OLE DB for OLAP 和 OLE DB for Data Mining 数据源提供程序的某些标准架构行集。 下列主题介绍了支持的行集。  

架构行集是在两个 SQL Server Analysis Services 协议中所述：   

[[MS-SSAS-T]: SQL Server Analysis Services 表格协议](https://msdn.microsoft.com/library/mt719260)-介绍针对 1200年及更高版本的兼容性级别的表格模型架构行集。

[[MS-SSAS]: SQL Server Analysis Services 协议](https://msdn.microsoft.com/library/ee320606)-介绍用于多维模型和表格模型 1100年和 1103年兼容级别的架构行集。

## <a name="rowsets-described-in-the-ms-ssas-t-sql-server-analysis-services-tabular-protocol"></a>[MS-SSAS-T] 中所述的行集： SQL Server Analysis Services 表格协议

|行集  |Description  |
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

## <a name="rowsets-described-in-the-ms-ssas-sql-server-analysis-services-protocol"></a>在 [MS-SSAS] 中所述的行集： SQL Server Analysis Services 协议

|行集|Description|  
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
|[DISCOVER_KEYWORDS &AMP;#40;XMLA&AMP;#41;](https://msdn.microsoft.com/library/ee301719)|返回有关 XMLA 服务器保留的关键字的信息。|  
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
|[DISCOVER_TRACE_COLUMNS]()||  
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

  
  
