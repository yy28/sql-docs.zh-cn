---
title: "从分析的数据源中检索元数据 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- metadata [ADOMD.NET]
- retrieving metadata
ms.assetid: 00043ebd-7164-4ceb-b945-6e44378ea00a
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 595b68b37eacf09f6cb4d327190f012207eb4286
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="retrieving-metadata-from-an-analytical-data-source"></a>从分析数据源检索元数据
  对于检索和使用分析数据的应用程序，元数据是非常重要的。 从关系数据源检索数据时，这些数据的维数是可预测的，即使对嵌套数据集也是如此。 关系数据库的结果集的结构通常是二维的或为标量。 但是，从分析数据源检索的数据的维数是可变的，组织的层次结构可能会很深。  
  
 为了应对从分析数据源检索元数据的复杂性，ADOMD.NET 提供了两种形式的元数据检索：  
  
 **对象模型**  
 ADOMD.NET 对象模型通常比架构行集更易于使用。 对于大多数应用场景，使用对象模型即可访问不同数据库对象的元数据。 ADOMD.NET 通过 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 公开对象模型。  
  
 有关详细信息：[使用 ADOMD.NET 对象模型](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-adomd-net-object-model.md)  
  
 **架构行集**  
 通过使用架构行集检索元数据是一种完备但难度较大的方式。 架构行集是一种 OLE DB 行集，其中封装了对数据库中特定类型的所有对象的说明。 分析数据源中的架构信息包括可从数据源获取的数据库或目录、数据库中的多维数据集和挖掘模型、数据源中存在的多维数据集的角色等。 此元数据可以通过使用来检索<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>方法，并传递在**GUID**或的 XML for Analysis (XMLA) 名称。  
  
 有关详细信息： [Working with Schema Rowsets in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)  
  
 上述每种元数据检索方法都可以访问不同类型的元数据。 下表介绍每种方法可检索的不同元数据以及用于访问每种元数据的方法。  
  
|GUID（用于架构行集）|XMLA 名称（用于架构行集）|ADOMD.NET 对象模型|  
|-------------------------------------|------------------------------------------|----------------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Actions>|[MDSCHEMA_ACTIONS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Catalogs>|[DBSCHEMA_CATALOGS 行集](../../analysis-services/schema-rowsets/ole-db/dbschema-catalogs-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Columns>|[DBSCHEMA_COLUMNS 行集](../../analysis-services/schema-rowsets/ole-db/dbschema-columns-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Connections>|**DISCOVER_CONNECTIONS**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Cubes>|[MDSCHEMA_CUBES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|AdomdConnection.Cubes|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.DataSources>|[DISCOVER_DATASOURCES 行集](../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.DBConnections>|**DISCOVER_DB_CONNECTIONS**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Dimensions>|[MDSCHEMA_DIMENSIONS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|AdomdConnection.Cubes[].Dimensions|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.DimensionStat>|**DISCOVER_DIMENSION_STAT**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Enumerators>|[DISCOVER_ENUMERATORS 行集](../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Functions>|[MDSCHEMA_FUNCTIONS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Hierarchies>|[MDSCHEMA_HIERARCHIES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|AdomdConnection.Cubes[].Dimensions[].Hierarchies|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.InputDataSources>|[MDSCHEMA_INPUT_DATASOURCES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Instances>|[DISCOVER_INSTANCES 行集](../../analysis-services/schema-rowsets/ole-db-olap/discover-instances-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Jobs>|**DISCOVER_JOBS**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Keywords>|[DISCOVER_KEYWORDS 行集 &#40; OLE DB for OLAP &#41;](../../analysis-services/schema-rowsets/ole-db-olap/discover-keywords-rowset-ole-db-for-olap.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Kpis>|[MDSCHEMA_KPIS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|AdomdConnection.Cubes[].KPIs|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Levels>|[MDSCHEMA_LEVELS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|AdomdConnection.Cubes[].Dimensions[].Hierarchies[].Levels|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Literals>|[DISCOVER_LITERALS 行集](../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Locations>|**DISCOVER_LOCATIONS**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Locks>|**DISCOVER_LOCKS**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MasterKey>|**DISCOVER_MASTER_KEY**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MeasureGroupDimensions>|[MDSCHEMA_MEASUREGROUP_DIMENSIONS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MeasureGroups>|[MDSCHEMA_MEASUREGROUPS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Measures>|[MDSCHEMA_MEASURES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|AdomdConnection.Cubes[].Measures|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MemberProperties>|[MDSCHEMA_PROPERTIES 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|可从大多数主要 ADOMD.NET 对象获得的 PropertyCollection。|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Members>|[MDSCHEMA_MEMBERS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|AdomdConnection.Cubes[].Dimensions[].Hierarchies[].Levels[].GetMembers()|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MemoryGrant>|**DISCOVER_MEMORYGRANT**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MemoryUsage>|**DISCOVER_MEMORYUSAGE**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningColumns>|[DMSCHEMA_MINING_COLUMNS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|AdomdConnection.MiningModels[].MiningModelColumns|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningFunctions>|[DMSCHEMA_MINING_FUNCTIONS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningModelContent>|[DMSCHEMA_MINING_MODEL_CONTENT 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|AdomdConnection.MiningModels[].MiningContentNodes|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningModelContentPmml>|[DMSCHEMA_MINING_MODEL_CONTENT_PMML 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningModels>|[DMSCHEMA_MINING_MODELS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|AdomdConnection.MiningModels|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningModelXml>|[DMSCHEMA_MINING_MODEL_XML 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningServiceParameters>|[DMSCHEMA_MINING_SERVICE_PARAMETERS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|AdomdConnection.MiningServices[].MiningServiceParameters|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningServices>|[DMSCHEMA_MINING_SERVICES 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|AdomdConnection.MiningServices|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningStructureColumns>|[DMSCHEMA_MINING_STRUCTURE_COLUMNS 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|AdomdConnection.MiningStructures[].MiningStructureColumns|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.MiningStructures>|[DMSCHEMA_MINING_STRUCTURES 行集](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|AdomdConnection.MiningStructures|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.PartitionDimensionStat>|**DISCOVER_PARTITION_DIMENSION_STAT**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.PartitionStat>|**DISCOVER_PARTITION_STAT**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.PerformanceCounters>|**DISCOVER_PERFORMANCE_COUNTERS**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.ProviderTypes>|[DBSCHEMA_PROVIDER_TYPES 行集](../../analysis-services/schema-rowsets/ole-db/dbschema-provider-types-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.SchemaRowsets>|[DISCOVER_SCHEMA_ROWSETS 行集](../../analysis-services/schema-rowsets/xml/discover-schema-rowsets-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Sessions>|**DISCOVER_SESSIONS**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Sets>|[MDSCHEMA_SETS 行集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|AdomdConnection.Cubes[].NamedSets|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Tables>|[DBSCHEMA_TABLES 行集](../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.TablesInfo>|**DBSCHEMA_TABLES_INFO**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.TraceColumns>|**DISCOVER_TRACE_COLUMNS**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.TraceDefinitionProviderInfo>|**DISCOVER_TRACE_DEFINITION_PROVIDERINFO**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.TraceEventCategories>|**DISCOVER_TRACE_EVENT_CATEGORIES**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Traces>|**DISCOVER_TRACES**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.Transactions>|**DISCOVER_TRANSACTIONS**||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.XmlaProperties>|[DISCOVER_PROPERTIES 行集](../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md)||  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid.XmlMetadata>|[DISCOVER_XML_METADATA 行集](../../analysis-services/schema-rowsets/xml/discover-xml-metadata-rowset.md)||  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET 客户端编程](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [ADOMD.NET 客户端编程](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [Analysis Services 架构行集](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

