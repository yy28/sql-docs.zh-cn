---
title: SchemaEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c064120e3c658cafd88a96953ff00e18fbaa9b88
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931113"
---
# <a name="schemaenum"></a>SchemaEnum
指定的架构的类型**记录集**的[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法检索。  
  
## <a name="remarks"></a>备注  
 为每个 ADO 常量，可以找到主题中的函数和列有关的其他信息返回[附录 b:架构行集](https://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1)的 OLE DB 程序员参考。 下表描述部分中的括号中列出每个主题的名称。  
  
 为每个 ADO MD 常量可以找到主题中返回的函数和列有关的其他信息[OLE DB for OLAP 对象和架构行集](https://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144)OLE DB 中的联机分析处理 (OLAP) 文档。 下表描述列中的括号中列出每个主题的名称。  
  
 可以通过引用 ADO 的说明列转换到 ADO 数据类型的 OLE DB 文档中的列的数据类型[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)主题。 例如，类型为 OLE DB 数据类型**DBTYPE_WSTR**到 ADO 数据类型的等效**adWChar**。  
  
 ADO 将会生成常数，类似于架构的结果**adSchemaDBInfoKeywords**并**adSchemaDBInfoLiterals**。 创建 ADO**记录集**，然后以分别返回的值填充的每一行**IDBInfo::GetKeywords**并**IDBInfo::GetLiteralInfo**方法。 中可以找到有关这些方法的更多信息[IDBInfo](https://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3)的 OLE DB 程序员参考的部分。  
  
|常量|值|描述|约束列|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|返回在目录中定义的由给定用户拥有的断言。<br /><br /> （断言行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|返回与 DBMS 从可访问的目录关联的物理属性。<br /><br /> （行集目录）|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|返回在目录中定义的、 给定用户可访问字符集。<br /><br /> （CHARACTER_SETS 行集）|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|返回在目录中定义的、 给定用户拥有的 check 约束。<br /><br /> (CHECK_CONSTRAINTS)行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|返回的字符排序规则在目录中定义的给定用户可访问。<br /><br /> （排序规则行集）|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|返回列的表在目录中定义的可使用或负责授予的给定用户的特权。<br /><br /> （COLUMN_PRIVILEGES 行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|返回的表 （包括视图） 在目录中定义的给定用户可以访问的列。<br /><br /> （列行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|返回在目录中定义的列依赖于在目录中定义并由给定用户拥有的域。<br /><br /> （COLUMN_DOMAIN_USAGE 行集）|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|返回由引用约束、 唯一约束、 check 约束和断言、 在目录中定义并由给定用户拥有的列。<br /><br /> （CONSTRAINT_COLUMN_USAGE 行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|返回由引用约束、 唯一约束、 check 约束和断言在目录中定义并由给定用户拥有的表。<br /><br /> （CONSTRAINT_TABLE_USAGE 行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|架构 （或在目录中，如果提供程序不支持架构） 中返回有关可用的多维数据集的信息。<br /><br /> （多维数据集行集 *）|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|返回特定于提供程序的关键字的列表。<br /><br /> (IDBInfo::GetKeywords)|\<无 >|  
|**adSchemaDBInfoLiterals**|31|返回特定于提供程序的文字文本命令中使用的列表。<br /><br /> (IDBInfo::GetLiteralInfo)|\<无 >|  
|**adSchemaDimensions**|33|返回在给定的多维数据集中的维度的信息。 它具有每个维度的一个行。<br /><br /> （维度行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|返回由给定用户在目录中定义的外键列。<br /><br /> （FOREIGN_KEYS 行集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|返回有关可用维度中的层次结构的信息。<br /><br /> （层次结构行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|返回在目录中定义的由给定用户拥有的索引。<br /><br /> （索引行集）|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME 类型 TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|返回在目录中定义的由给定用户约束为键的列。<br /><br /> （KEY_COLUMN_USAGE 行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|返回有关可用维度中的级别的信息。<br /><br /> （级别行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|返回有关可用度量值的信息。<br /><br /> （度量值行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|返回有关可用的成员的信息。<br /><br /> （成员行集）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE 树运算符。 有关详细信息，请参阅 OLE DB 的联机分析处理 (OLAP)。|  
|**adSchemaPrimaryKeys**|28|返回由给定用户在目录中定义的主键列。<br /><br /> （PRIMARY_KEYS 行集）|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|返回有关由过程返回的行集中的列的信息。<br /><br /> （PROCEDURE_COLUMNS 行集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|返回有关过程的参数和返回代码的信息。<br /><br /> （PROCEDURE_PARAMETERS 行集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|返回在目录中定义的由给定用户拥有的过程。<br /><br /> （过程行集）|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|返回有关维度的每个级别的可用属性的信息。<br /><br /> （行集属性）|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|如果提供程序定义其自己使用了非标准架构的查询，使用。|\<特定于提供程序 >|  
|**adSchemaProviderTypes**|22|返回支持的数据提供程序 （基本） 数据类型。<br /><br /> （PROVIDER_TYPES 行集）|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|返回在目录中定义的由给定用户拥有的引用约束。<br /><br /> （REFERENTIAL_CONSTRAINTS 行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|返回由给定用户拥有的架构 （数据库对象）。<br /><br /> （架构行集）|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|返回一致性级别、 选项和方言支持在目录中定义的 SQL 实现处理数据。<br /><br /> （SQL_LANGUAGES 行集）|\<无 >|  
|**adSchemaStatistics**|19|返回在目录中定义的由给定用户拥有的统计信息。<br /><br /> （统计信息行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|返回在目录中定义的、 由给定用户拥有的表约束。<br /><br /> （TABLE_CONSTRAINTS 行集）|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|返回在目录中定义的可使用或负责授予的给定用户的表上的特权。<br /><br /> （TABLE_PRIVILEGES 行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|返回的表 （包括视图） 在目录中定义的、 给定用户可访问。<br /><br /> （表行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|返回在目录中定义的、 给定用户可访问的字符转换。<br /><br /> （转换行集）|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|保留供将来使用。||  
|**adSchemaUsagePrivileges**|15|返回在目录中定义的可使用或负责授予的给定用户的对象的使用情况特权。<br /><br /> （USAGE_PRIVILEGES 行集）|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE 授权者被授权者|  
|**adSchemaViewColumnUsage**|24|返回在其中的列中查看表、 在目录中定义并由给定用户拥有所依赖。<br /><br /> （VIEW_COLUMN_USAGE 行集）|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|返回给定用户可以访问的视图在目录中定义。<br /><br /> （视图行集）|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|返回在其上的表中查看表、 在目录中定义和由给定用户拥有所依赖。<br /><br /> （VIEW_TABLE_USAGE 行集）|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
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
