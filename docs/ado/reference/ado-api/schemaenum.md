---
title: "SchemaEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0b17893425ea772c848b9fb20907c4e0899d1e3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="schemaenum"></a>SchemaEnum
指定的架构的类型**记录集**， [OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法检索。  
  
## <a name="remarks"></a>注释  
 为主题中找不到每个 ADO 常量返回有关函数和列的其他信息[附录 b： 架构行集](http://msdn.microsoft.com/en-us/2b5fbf03-e50d-44ee-bc57-5a57666c55f1)的 OLE DB 程序员参考。 下表的描述部分中的括号中列出的每个主题的名称。  
  
 为每个 ADO MD 常量可以找到主题中返回有关函数和列的其他信息[OLE DB for OLAP 对象和架构行集](http://msdn.microsoft.com/en-us/d20bb2a6-68bd-423f-9ec8-eb930cd0c144)的 OLE DB 中的联机分析处理 (OLAP) 文档。 下表描述列中的括号中列出的每个主题的名称。  
  
 可以通过引用的 ADO 说明列转换为 ADO 数据类型的 OLE DB 文档中的列的数据类型[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)主题。 例如，OLE DB 数据类型的**DBTYPE_WSTR**等效于的 ADO 数据类型为**adWChar**。  
  
 ADO 将会生成类似于架构的结果为常量， **adSchemaDBInfoKeywords**和**adSchemaDBInfoLiterals**。 ADO 创建**记录集**，然后以分别返回的值填充每个行**IDBInfo::GetKeywords**和**IDBInfo::GetLiteralInfo**方法。 有关这些方法的其他信息可在[IDBInfo](http://msdn.microsoft.com/en-us/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) OLE DB 程序员参考的部分。  
  
|常量|值|Description|约束列|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|返回由给定用户所拥有的断言的目录中定义。<br /><br /> （断言行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|返回与从 DBMS 可访问的目录关联的物理属性。<br /><br /> （目录行集）|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|返回定义的字符集在目录中与给定用户可访问。<br /><br /> （CHARACTER_SETS 行集）|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|返回由给定用户所拥有的 check 约束的目录中定义。<br /><br /> (CHECK_CONSTRAINTS)行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|返回字符定义的排序规则在目录中与给定用户可访问。<br /><br /> （排序规则行集）|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|在目录中定义的可指定用户或由给定的用户授权的表的列返回的权限。<br /><br /> （COLUMN_PRIVILEGES 行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|返回的表的列 （包括视图） 的目录中定义给定用户可以访问。<br /><br /> （列行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|返回目录中定义依赖于目录中定义和给定用户所拥有的域中的列。<br /><br /> （COLUMN_DOMAIN_USAGE 行集）|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|返回由引用约束、 唯一约束、 check 约束和断言、 目录中定义和给定用户所拥有的列。<br /><br /> （CONSTRAINT_COLUMN_USAGE 行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|返回由引用约束、 唯一约束、 check 约束和断言的目录中定义并由给定的用户拥有的表。<br /><br /> （CONSTRAINT_TABLE_USAGE 行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|在架构 （或目录，如果提供程序不支持架构） 中返回有关可用的多维数据集信息。<br /><br /> （多维数据集行集 *）|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|返回提供程序特定关键字的列表。<br /><br /> (IDBInfo::GetKeywords)|\<无 >|  
|**adSchemaDBInfoLiterals**|31|返回文本命令中使用的提供程序特定文本的列表。<br /><br /> (IDBInfo::GetLiteralInfo)|\<无 >|  
|**adSchemaDimensions**|33|返回给定的多维数据集中维度的信息。 它有对应的一行，每个维度。<br /><br /> （维度行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|返回由给定用户在目录中定义的外键列。<br /><br /> （FOREIGN_KEYS 行集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|返回有关可用维度中的层次结构的信息。<br /><br /> （层次结构行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|返回由给定用户所拥有的索引的目录中定义。<br /><br /> （索引行集）|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME 类型 TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|返回由给定用户约束为键的列的目录中定义。<br /><br /> （KEY_COLUMN_USAGE 行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|返回有关可用维度中的级别的信息。<br /><br /> （级别行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|返回有关可用度量值的信息。<br /><br /> （度量值行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|返回有关可用的成员信息。<br /><br /> （成员行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE 树运算符。 有关详细信息，请参阅 OLE DB 的联机分析处理 (OLAP)。|  
|**adSchemaPrimaryKeys**|28|返回由给定用户在目录中定义的主键列。<br /><br /> （PRIMARY_KEYS 行集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|返回有关由过程返回的行集中的列的信息。<br /><br /> （PROCEDURE_COLUMNS 行集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|返回有关过程的参数和返回代码的信息。<br /><br /> （PROCEDURE_PARAMETERS 行集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|返回由给定用户所拥有的过程的目录中定义。<br /><br /> （过程行集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|返回有关每个级别的维度可用的属性的信息。<br /><br /> （属性行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|如果提供程序定义其自己的非标准架构查询，使用。|\<特定于提供程序 >|  
|**adSchemaProviderTypes**|22|返回支持的数据提供程序 （基） 数据类型。<br /><br /> （PROVIDER_TYPES 行集）|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|返回由给定用户所拥有的引用约束的目录中定义。<br /><br /> （REFERENTIAL_CONSTRAINTS 行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|返回由给定用户所拥有的架构 （数据库对象）。<br /><br /> （架构行集）|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|返回一致性级别、 选项和支持的目录中定义的 SQL 实现处理数据的方言。<br /><br /> （SQL_LANGUAGES 行集）|\<无 >|  
|**adSchemaStatistics**|19|返回目录中定义由给定用户拥有的统计信息。<br /><br /> （统计信息行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|返回由给定用户所拥有的表约束的目录中定义。<br /><br /> （TABLE_CONSTRAINTS 行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|返回上可用，或由给定的用户授权的表的目录中定义的权限。<br /><br /> （TABLE_PRIVILEGES 行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|返回定义的表 （包括视图） 在目录中与给定用户可访问。<br /><br /> （表行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|返回给定的用户可以访问的字符转换的目录中定义。<br /><br /> （翻译行集）|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|保留供将来使用。||  
|**adSchemaUsagePrivileges**|15|在目录中定义的可指定用户或授予由给定用户的对象上返回的使用情况特权。<br /><br /> （USAGE_PRIVILEGES 行集）|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE 授权者被授权者|  
|**adSchemaViewColumnUsage**|24|返回所依据的列查看表、 在目录中定义并由给定用户拥有所依赖。<br /><br /> （VIEW_COLUMN_USAGE 行集）|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|返回给定的用户可以访问的视图的目录中定义。<br /><br /> （视图行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|返回在其上的表查看表、 目录中定义和归给定用户所依赖。<br /><br /> （VIEW_TABLE_USAGE 行集）|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.Schema.ASSERTS|  
|AdoEnums.Schema.CATALOGS|  
|AdoEnums.Schema.CHARACTERSETS|  
|AdoEnums.Schema.CHECKCONSTRAINTS|  
|AdoEnums.Schema.COLLATIONS|  
|AdoEnums.Schema.COLUMNPRIVILEGES|  
|AdoEnums.Schema.COLUMNS|  
|AdoEnums.Schema.COLUMNSDOMAINUSAGE|  
|AdoEnums.Schema.CONSTRAINTCOLUMNUSAGE|  
|AdoEnums.Schema.CONSTRAINTTABLEUSAGE|  
|AdoEnums.Schema.CUBES|  
|AdoEnums.Schema.DBINFOKEYWORDS|  
|AdoEnums.Schema.DBINFOLITERALS|  
|AdoEnums.Schema.DIMENSIONS|  
|AdoEnums.Schema.FOREIGNKEYS|  
|AdoEnums.Schema.HIERARCHIES|  
|AdoEnums.Schema.INDEXES|  
|AdoEnums.Schema.KEYCOLUMNUSAGE|  
|AdoEnums.Schema.LEVELS|  
|AdoEnums.Schema.MEASURES|  
|AdoEnums.Schema.MEMBERS|  
|AdoEnums.Schema.PRIMARYKEYS|  
|AdoEnums.Schema.PROCEDURECOLUMNS|  
|AdoEnums.Schema.PROCEDUREPARAMETERS|  
|AdoEnums.Schema.PROCEDURES|  
|AdoEnums.Schema.PROPERTIES|  
|AdoEnums.Schema.PROVIDERSPECIFIC|  
|AdoEnums.Schema.PROVIDERTYPES|  
|AdoEnums.Schema.REFERENTIALCONTRAINTS|  
|AdoEnums.Schema.SCHEMATA|  
|AdoEnums.Schema.SQLLANGUAGES|  
|AdoEnums.Schema.STATISTICS|  
|AdoEnums.Schema.TABLECONSTRAINTS|  
|AdoEnums.Schema.TABLEPRIVILEGES|  
|AdoEnums.Schema.TABLES|  
|AdoEnums.Schema.TRANSLATIONS|  
|AdoEnums.Schema.TRUSTEES|  
|AdoEnums.Schema.USAGEPRIVILEGES|  
|AdoEnums.Schema.VIEWCOLUMNUSAGE|  
|AdoEnums.Schema.VIEWS|  
|AdoEnums.Schema.VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>适用范围  
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)

