---
title: 访问清单架构 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- columns table
- databases table
- exported metadata
- exporting, schemas of exported metadata
- foreign keys table
- forms table
- indexes, table
- inventory schemas
- macros table
- modules table
- queries table
- reference, inventory schemas
- reports table
- schemas of exported metadata
- schemas, exported metadata
- SSMA_Access_InventoryColumns
- SSMA_Access_InventoryDatabases
- SSMA_Access_InventoryForeignKeys
- SSMA_Access_InventoryForms
- SSMA_Access_InventoryIndexes
- SSMA_Access_InventoryMacros
- SSMA_Access_InventoryModules
- SSMA_Access_InventoryQueries
- SSMA_Access_InventoryReports
- SSMA_Access_InventoryTables
- tables, inventory
ms.assetid: fdd3cff2-4d62-4395-8acf-71ea8f17f524
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 71a52a619ba2a3c16c372021181b90bae72ccfe7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653699"
---
# <a name="access-inventory-schemas-accesstosql"></a>Access 清单架构 (AccessToSQL)
以下各节介绍的表导出到 Access 架构时创建的 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="databases"></a>“数据库”  
数据库元数据导出到**SSMA_Access_InventoryDatabases**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|用于唯一标识每个数据库的 GUID。 此列也是表的主键。|  
|**DatabaseName**|**nvarchar(4000)**|访问数据库的名称。|  
|**ExportTime**|**datetime**|此元数据创建的 SSMA 的日期和时间。|  
|**文件路径**|**nvarchar(4000)**|Access 数据库完整路径和文件名称。|  
|**FileSize**|**bigint**|以 kb 为单位的 Access 数据库的大小。|  
|**FileOwner**|**nvarchar(4000)**|指定为所有者的 Access 数据库的 Windows 帐户。|  
|**DateCreated**|**datetime**|日期和时间创建的 Access 数据库中。|  
|**DateModified**|**datetime**|日期和 Access 数据库的上次修改的时间。|  
|**TablesCount**|**int**|访问数据库中的表数。|  
|**QueriesCount**|**int**|访问数据库中的查询数。|  
|**FormsCount**|**int**|Access 数据库中的窗体的数。|  
|**ModulesCount**|**int**|Access 数据库中的模块数。|  
|**ReportsCount**|**int**|Access 数据库中的报表数。|  
|**MacrosCount**|**int**|Access 数据库中的宏的数。|  
|**AccessVersion**|**nvarchar(4000)**|访问数据库的版本。|  
|**排序规则**|**nvarchar(4000)**|访问数据库的排序规则。 排序规则确定数据库如何进行排序和比较字符串。|  
|**JetVersion**|**nvarchar(4000)**|Jet 数据库引擎版本。 Access 数据库使用基础的 Jet 数据库引擎。|  
|**IsUpdatable**|**bit**|指示是否可以更新数据库。 如果值为 1，则可更新数据库。 如果值为 0，则数据库是只读的。|  
|**QueryTimeout**|**int**|配置的 ODBC 查询超时值对于数据库，以秒为单位。 默认值为 60 秒。|  
  
## <a name="tables"></a>表  
表元数据导出到**SSMA_Access_InventoryTables**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|标识包含此表的数据库。|  
|**TableId**|**uniqueidentifier**|用于唯一标识表的 GUID。 此列也是表的主键。|  
|**TableName**|**nvarchar(4000)**|表的名称。|  
|**RowsCount**|**int**|该表中的行数。|  
|**ValidationRule**|**nvarchar(4000)**|定义表的有效输入规则。 如果不存在任何验证规则，该字段将包含空字符串。|  
|**LinkedTable**|**nvarchar(4000)**|另一个表，如果有，链接的表。 链接表允许通过使用此表添加、 删除和更新到另一个表。|  
|**ExternalSource**|**nvarchar(4000)**|数据源中，如果有，与该键相关联的表。 如果链接表，它具有在此字段中指定的外部数据源。|  
  
## <a name="columns"></a>“列”  
列元数据导出到**SSMA_Access_InventoryColumns**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|标识包含此列的数据库。|  
|**TableId**|**uniqueidentifier**|标识包含此列的表。|  
|**ColumnId**|**int**|一个递增的整数，用于标识列。 **ColumnId**是表的主键。|  
|**ColumnName**|**nvarchar(4000)**|列的名称。|  
|**IsNullable**|**bit**|指定是否列可以包含 null 值。 如果值为 1，列可以包含 null 值。 如果值为 0，则列不能包含 null 值。 请注意，验证规则还可用来防止 null 值。|  
|**DataType**|**nvarchar(4000)**|访问数据类型的列，如**文本**或**长**。|  
|**IsAutoIncrement**|**bit**|指定是否该列自动递增整数值。 如果值为 1，将自动递增整数。|  
|**Ordinal**|**smallint**|在表中，从零开始的列的顺序。|  
|**DefaultValue**|**nvarchar(4000)**|列的默认值。|  
|**ValidationRule**|**nvarchar(4000)**|用于验证数据的规则添加或更新列中。|  
  
## <a name="indexes"></a>索引  
索引的元数据导出到**SSMA_Access_InventoryIndexes**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|标识包含此索引的数据库。|  
|**TableId**|**uniqueidentifier**|标识包含此索引的表。|  
|**IndexId**|**int**|一个用于标识索引递增整数。 此列是表的主键。|  
|**IndexName**|**nvarchar(4000)**|索引的名称。|  
|**ColumnsIncluded**|**nvarchar(4000)**|列出索引中包含的列。 由分号分隔的列名称。|  
|**IsUnique**|**bit**|指定是否在索引中的每个项必须是唯一的。 对多列索引值的组合必须是唯一的。 如果值为 1，该索引强制使用唯一值。|  
|**IsPK**|**bit**|指定是否定义的主键的一部分自动创建索引。|  
|**IsClustered**|**bit**|指定对索引进行聚集。 聚集的索引重新排序数据的物理的存储。 表可以有一个聚集的索引。|  
  
## <a name="foreign-keys"></a>外键  
外键元数据导出到**SSMA_Access_InventoryForeignKeys**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|标识包含该外键的数据库。|  
|**TableId**|**uniqueidentifier**|标识包含此外键的表。|  
|**ForeignKeyId**|**int**|一个用于标识外键的递增整数。 此列是表的主键。|  
|**ForeignKeyName**|**nvarchar(4000)**|索引的名称。|  
|**ReferencedTableId**|**uniqueidentifier**|标识包含源列的表。|  
|**SourceColumns**|**nvarchar(4000)**|列出了外键列。|  
|**ReferencedColumns**|**nvarchar(4000)**|列出所引用的外键列或主键列。|  
|**IsCascadeForUpdate**|**bit**|指定是否更新的主键值，还更新引用该键值的所有行。|  
|**IsCascadeForDelete**|**bit**|指定是否删除主键值，则也删除引用该键值的所有行。|  
|**IsEnforced**|**bit**|指定外键约束强制执行。|  
  
## <a name="queries"></a>查询  
查询元数据导出到**SSMA_Access_InventoryQueries**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|标识包含此查询的数据库。|  
|**QueryId**|**int**|一个递增的整数，用于标识查询。 此列是表的主键。|  
|**QueryName**|**nvarchar(4000)**|查询的名称。|  
|**QueryText**|**nvarchar(4000)**|SQL 查询代码，如 SELECT 语句。|  
|**IsUpdateable**|**bit**|指定查询是否可更新或只读的。|  
|**QueryType**|**nvarchar(4000)**|指定类型的查询，例如**选择**或**SetOperation**。|  
|**ExternalSource**|**nvarchar(4000)**|如果查询引用了外部数据源，这是查询所使用的连接字符串。|  
  
## <a name="forms"></a>窗体  
表格元数据导出到**SSMA_Access_InventoryForms**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|标识包含此窗体的数据库。|  
|**FormId**|**int**|一个用于标识窗体的递增整数。 此列是表的主键。|  
|**FormName**|**nvarchar(4000)**|窗体的名称。|  
  
## <a name="macros"></a>宏  
宏元数据导出到**SSMA_Access_InventoryMacros**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|标识包含宏的数据库。|  
|**MacroId**|**int**|一个用于标识该宏的递增整数。 此列是表的主键。|  
|**MacroName**|**nvarchar(4000)**|宏的名称。|  
  
## <a name="reports"></a>报表  
报表元数据导出到**SSMA_Access_InventoryReports**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|标识包含该报表的数据库。|  
|**报表 Id**|**int**|一个用于标识报表的递增整数。 此列是表的主键。|  
|**ReportName**|**nvarchar(4000)**|报表的名称。|  
  
## <a name="modules"></a>模块  
模块元数据导出到**SSMA_Access_InventoryModules**表。 此表包含以下列：  
  
|列名|数据类型|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|标识包含该模块的数据库。|  
|**ModuleId**|**int**|一个用于标识模块的递增整数。 此列是表的主键。|  
|**模块名称**|**nvarchar(4000)**|模块的名称。|  
  
## <a name="see-also"></a>请参阅  
[导出 Access 清单](exporting-an-access-inventory-accesstosql.md)  
  
