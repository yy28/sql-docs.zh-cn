---
title: 创建 XML 索引 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- indexes [XML in SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: 6ecac598-355d-4408-baf7-1b2e8d4cf7c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c83cf778439ed8508c3c0128d90b085ae358c60
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664596"
---
# <a name="create-xml-indexes"></a>创建 XML 索引
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主题介绍如何创建主 XML 索引和辅助 XML 索引。  
  
## <a name="creating-a-primary-xml-index"></a>创建主 XML 索引  
 若要创建主 XML 索引，请使用 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 语句。 XML 索引不完全支持可用于非 XML 索引的所有选项。  
  
 创建 XML 索引时注意下列事项：  
  
-   若要创建主 XML 索引，含有被索引的 XML 列的表（称为基表）必须具有主键的聚集索引。 这确保了在对基表进行了分区的情况下，可以使用相同的分区方案和分区函数对主 XML 索引进行分区。  
  
-   如果存在 XML 索引，则不能修改基表的聚集主键。 在修改主键之前，必须删除表的所有 XML 索引。  
  
-   您可以对单个 **xml** 类型列创建主 XML 索引。 您无法将 XML 类型列作为键列来创建任何其他类型的索引。 但是，可以在非 XML 索引中包含 **xml** L 类型列。 表中的每个 **xml** 类型列都可以有自己的主 XML 索引。 但是，一个 **xml** 类型列只允许有一个主 XML 索引。  
  
-   XML 索引和非 XML 索引存在于相同的命名空间中。 因此，同一表的 XML 索引和非 XML 索引不能具有相同的名称。  
  
-   对于 XML 索引，IGNORE_DUP_KEY 选项和 ONLINE 选项始终设置为 OFF。 您可以将这些选项的值指定为 OFF。  
  
-   将用户表的文件组和分区信息应用于 XML 索引。 用户无法单独为 XML 索引指定这些信息。  
  
-   DROP_EXISTING 索引选项可以删除主 XML 索引并创建一个新的主 XML 索引，或者删除辅助 XML 索引并创建一个新的辅助 XML 索引。 但是，此选项不能通过删除辅助 XML 索引来创建新的主 XML 索引，反之亦然。  
  
-   主 XML 索引名称与视图名称有相同的限制。  
  
 不能对视图中的 **xml** 类型列、 **xml** 类型列的  表值变量或 **xml** 类型变量创建 XML 索引。  
  
-   若要使用 ALTER TABLE ALTER COLUMN 选项将 **xml** 类型列从非类型化的 XML 更改为类型化的 XML，或者从类型化的 XML 更改为非类型化的 XML，则列不应存在 XML 索引。 如果确实存在，则在尝试更改列类型之前必须删除该索引。  
  
-   创建 XML 索引时必须将选项 ARITHABORT 设置为 ON。 若要使用 XML 数据类型方法查询、删除、更新 XML 列中的值或向 XML 列中插入值，则必须对连接设置相同的选项。 如果没有设置，则 XML 数据类型方法将会失败。  
  
    > [!NOTE]  
    >  有关 XML 索引的信息可以在目录视图中找到。 但是，不支持 **sp_helpindex** 。 本主题后面部分提供的示例说明了如何查询目录视图以查找 XML 索引信息。  
  
 如果 XML 数据类型列包含类型为 XML 架构类型 **xs:date** 或 **xs:dateTime** （或这些类型的任何子类型）的值且这些值中的年份小于 1，则在对这样的 XML 数据类型列创建或重新创建主 XML 索引时，索引创建操作在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中将失败。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 允许使用这些值，因此在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中生成的数据库中创建索引时可能会出现这种问题。 有关详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
### <a name="example-creating-a-primary-xml-index"></a>示例：创建主 XML 索引  
 在大多数示例中，使用的是包含非类型化的 XML 列的表 T (pk INT PRIMARY KEY, xCol XML)。 可以采用简单的方式将它们扩展为类型化的 XML。 为简化起见，针对 XML 数据实例说明了查询，如下所示：  
  
```  
<book genre="security" publicationdate="2002" ISBN="0-7356-1588-2">  
   <title>Writing Secure Code</title>  
   <author>  
      <first-name>Michael</first-name>  
      <last-name>Howard</last-name>  
   </author>  
   <author>  
      <first-name>David</first-name>  
      <last-name>LeBlanc</last-name>  
   </author>  
   <price>39.99</price>  
</book>  
```  
  
 下面的语句对表 T 的 XML 列 xCol 创建一个名为 idx_xCol 的 XML 索引：  
  
```  
CREATE PRIMARY XML INDEX idx_xCol on T (xCol)  
```  
  
## <a name="creating-a-secondary-xml-index"></a>创建辅助 XML 索引  
 使用 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 语句可创建辅助 XML 索引并且可指定所需的辅助 XML 索引的类型。  
  
 创建辅助 XML 索引时注意下列事项：  
  
-   除了 IGNORE_DUP_KEY 和 ONLINE 之外，允许对辅助 XML 索引使用所有适用于非聚集索引的索引选项。 对于辅助 XML 索引，这两个选项必须始终设置为 OFF。  
  
-   辅助索引的分区方式类似于主 XML 索引。  
  
-   DROP_EXISTING 可以删除用户表的辅助索引并为用户表创建其他辅助索引。  
  
 可以查询 **sys.xml_indexes** 目录视图来检索 XML 索引信息。 请注意， **sys.xml_indexes** 目录视图中的 **secondary_type_desc** 列中提供了辅助索引的类型：  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 **secondary_type_desc** 列中返回的值可以是 NULL、PATH、VALUE 或 PROPERTY。 对于主 XML 索引而言，返回的值为 NULL。  
  
### <a name="example-creating-secondary-xml-indexes"></a>示例：创建辅助 XML 索引  
 下面的示例说明了如何创建辅助 XML 索引。 此示例还显示了有关您创建的 XML 索引的信息。  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML);  
GO  
-- Create primary index.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol);  
GO  
-- Create secondary indexes (PATH, VALUE, PROPERTY).  
CREATE XML INDEX PIdx_T_XmlCol_PATH ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PATH;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_VALUE ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR VALUE;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_PROPERTY ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PROPERTY;  
GO  
```  
  
 您可以查询 `sys.xml_indexes` 来检索 XML 索引信息。 `secondary_type_desc` 列提供了辅助索引类型。  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 您还可以在目录视图中查询索引信息。  
  
```  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T');  
```  
  
 您可以添加示例数据然后查看 XML 索引信息。  
  
```  
INSERT INTO T VALUES (1,  
'<doc id="123">  
<sections>  
<section num="2">  
<heading>Background</heading>  
</section>  
<section num="3">  
<heading>Sort</heading>  
</section>  
<section num="4">  
<heading>Search</heading>  
</section>  
</sections>  
</doc>');  
GO  
-- Check XML index information.  
SELECT *  
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, NULL, 'DETAILED');  
GO  
-- Space usage of primary XML index  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id  
FROM    sys.xml_indexes i   
WHERE   i.name = 'PIdx_T_XmlCol' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
--- Space usage of secondary XML index (for example PATH secondary index)  PIdx_T_XmlCol_PATH  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id   
FROM    sys.xml_indexes i   
WHERE  i.name = 'PIdx_T_XmlCol_PATH' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
  
-- Space usage of all secondary XML indexes for a particular table  
SELECT i.name, object_name(i.object_id), stats.*   
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, DEFAULT, 'DETAILED') stats  
JOIN sys.xml_indexes i ON (stats.object_id = i.object_id and stats.index_id = i.index_id)  
WHERE secondary_type is not null;  
-- Drop secondary indexes.  
DROP INDEX PIdx_T_XmlCol_PATH ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_VALUE ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_PROPERTY ON T;  
GO  
-- Drop primary index.  
DROP INDEX PIdx_T_XmlCol ON T;  
-- Drop table T.  
DROP TABLE T;  
Go  
```  
  
## <a name="see-also"></a>另请参阅  
 [XML 索引 (SQL Server)](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [XML 数据 (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
