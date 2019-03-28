---
title: XML 索引 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- deleting indexes
- secondary indexes [XML in SQL Server]
- xml data type [SQL Server], indexes
- dropping indexes
- PATH index
- DROP_EXISTING clause
- XML [SQL Server], indexes
- primary indexes [XML in SQL Server]
- indexes [SQL Server], XML
- XML indexes [SQL Server], secondary
- BLOBs, XML indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- XML indexes [SQL Server]
- XML indexes [SQL Server], primary
- modifying indexes
- XML indexes [SQL Server], dropping
- VALUE index
- XML indexes [SQL Server], xml data type
- PROPERTY index
- XML indexes [SQL Server], creating
ms.assetid: f5c9209d-b3f3-4543-b30b-01365a5e7333
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7004f2cae60ab69c6c4bf94ceee47d270579570b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533969"
---
# <a name="xml-indexes-sql-server"></a>XML 索引 (SQL Server)
  可以对 `xml` 数据类型列创建 XML 索引。 它们对列中 XML 实例的所有标记、值和路径进行索引，从而提高查询性能。 在下列情况下，您的应用程序可以从 XML 索引中获益：  
  
-   对 XML 列进行查询在您的工作负荷中很常见。 必须考虑数据修改过程中的 XML 索引维护开销。  
  
-   XML 值相对较大，而检索的部分相对较小。 生成索引避免了在运行时分析所有数据，并能实现高效的查询处理，从而使索引查找受益。  
  
 XML 索引分为下列类别：  
  
-   主 XML 索引  
  
-   辅助 XML 索引  
  
 `xml` 类型列的第一个索引必须是主 XML 索引。 使用主 XML 索引，支持以下类型的辅助索引：路径、 值和属性。 根据查询类型的不同，这些辅助索引可能有助于改善查询性能。  
  
> [!NOTE]  
>  除非为使用 `xml` 数据类型正确设置了数据库选项，否则无法创建或修改 XML 索引。 有关详细信息，请参阅 [结合使用具有全文搜索和 XML 列](use-full-text-search-with-xml-columns.md)。  
  
 XML 实例作为二进制大型对象 (BLOB) 存储在 `xml` 类型列中。 这些 XML 实例可以很大，并且存储的 `xml` 数据类型实例的二进制表示形式最大可以为 2 GB。 如果没有索引，则运行时将拆分这些二进制大型对象以计算查询。 此拆分可能非常耗时。 例如，请看以下查询：  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 为了选择满足 `WHERE` 子句中条件的 XML 实例，表 `Production.ProductModel` 的每行中的 XML 二进制大型对象 (BLOB) 将在运行时拆分。 然后，计算 `(/PD:ProductDescription/@ProductModelID[.="19"]`方法中的表达式 `exist()` )。 此运行时拆分有可能开销较大，这取决于存储在列中的实例的大小和数目。  
  
 如果在应用程序环境中经常查询 XML 二进制大型对象 (BLOB)，则对 `xml` 类型列创建索引很有用。 但是，在数据修改过程中维护索引会带来开销。  
  
## <a name="primary-xml-index"></a>主 XML 索引  
 主 XML 索引对 XML 列中 XML 实例内的所有标记、值和路径进行索引。 若要创建主 XML 索引，相应 XML 列所在的表必须对该表的主键创建了聚集索引。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用此主键将主 XML 索引中的行与包含此 XML 列的表中的行关联起来。  
  
 主 XML 索引是 `xml` 数据类型列中的 XML BLOB 的已拆分和持久的表示形式。 对于列中的每个 XML 二进制大型对象 (BLOB)，索引将创建数个数据行。 该索引中的行数大约等于 XML 二进制大型对象中的节点数。 当查询检索完整的 XML 实例时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会提供此 XML 列中的实例。 XML 实例中的查询使用主 XML 索引，并可以通过使用索引本身返回标量值或 XML 子树。  
  
 每行存储以下节点信息：  
  
-   标记名（如元素名称或属性名称）。  
  
-   节点值。  
  
-   节点类型（如元素节点、属性节点或文本节点）。  
  
-   文档顺序信息（由内部节点标识符表示）。  
  
-   从每个节点到 XML 树的根的路径。 搜索此列可获得查询中的路径表达式。  
  
-   基表的主键。 基表的主键将复制到主 XML 索引中，用于向后和基表进行联接，并且基表的主键中的最大列数限制为 15。  
  
 此节点信息用于计算和构造指定查询的 XML 结果。 出于优化的需要，标记名和节点类型信息编码为整数值，且 Path 列使用同样的编码。 另外，路径以相反的顺序存储，以便在仅知道路径后缀的情况下能够匹配路径。 例如：  
  
-   `//ContactRecord/PhoneNumber` ，其中只有最后两个步骤是已知的  
  
 或  
  
-   `/Book/*/Title` 其中，通配符 (`*`) 是指定在表达式中间的。  
  
 对于涉及 [xml Data Type Methods](/sql/t-sql/xml/xml-data-type-methods) 的查询，查询处理器使用主 XML 索引，并返回主索引自身中的标量值或 XML 子树。 （此索引存储重新构造 XML 实例所需的所有信息。）  
  
 例如，以下查询将返回存储的摘要信息`CatalogDescription``xml`类型列中的`ProductModel`表。 只有当产品型号的目录说明中还存储 <`Features`> 说明时，该查询才会返回 <`Summary`> 信息。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")SELECT CatalogDescription.query('  /PD:ProductDescription/PD:Summary') as ResultFROM Production.ProductModelWHERE CatalogDescription.exist ('/PD:ProductDescription/PD:Features') = 1  
```  
  
 关于主 XML 索引，为 `exist()` 方法中指定的表达式按顺序搜索与每个 XML 二进制大型对象相对应的索引中的行，而不是拆分基表中的每个 XML 二进制大型对象实例。 如果路径是在索引中的 Path 列中找到的，则从主 XML 索引检索 <`Summary`> 元素及其子树，并将它们转换为 XML 二进制大型对象以作为 `query()` 方法的结果。  
  
 注意，检索完整的 XML 实例时不使用主 XML 索引。 例如，下面的查询从表中检索描述了特定产品型号的生产说明的整个 XML 实例。  
  
```  
USE AdventureWorks2012;SELECT InstructionsFROM Production.ProductModel WHERE ProductModelID=7;  
```  
  
## <a name="secondary-xml-indexes"></a>辅助 XML 索引  
 为了增强搜索性能，可以创建辅助 XML 索引。 必须有了主 XML 索引才能创建辅助索引。 辅助索引的类型如下：  
  
-   PATH 辅助 XML 索引  
  
-   VALUE 辅助 XML 索引  
  
-   PROPERTY 辅助 XML 索引  
  
 以下为创建一个或多个辅助索引的一些准则：  
  
-   如果工作负荷对 XML 列大量使用路径表达式，则 PATH 辅助 XML 索引可能会提高工作负荷的处理速度。 最常见的情况是在 Transact-SQL 的 WHERE 子句中对 XML 列使用 **exist()** 方法。  
  
-   如果工作负荷通过使用路径表达式从单个 XML 实例中检索多个值，则在 PROPERTY 索引中聚集各个 XML 实例中的路径可能会很有用。 这种情况通常出现在属性包方案中，此时提取对象的属性并且已知其主键值。  
  
-   如果工作负荷涉及查询 XML 实例中的值，但不知道包含那些值的元素名称或属性名称，则您可能希望创建 VALUE 索引。 这通常出现在 descendant 轴查找中，例如 //author[last-name="Howard"]，其中 \<author> 元素可以出现在层次结构的任何级别上。 这种情况也出现在通配符查询中，例如 /book [@* = "novel"]，其中查询将查找具有某个值为“novel”的属性的 \<book> 元素。  
  
### <a name="path-secondary-xml-index"></a>PATH 辅助 XML 索引  
 如果查询通常对 `xml` 类型列指定路径表达式，则 PATH 辅助索引可以提高搜索的速度。 如本主题前面所述，当查询在 WHERE 子句中指定 **exist()** 方法时主索引非常有用。 如果添加 PATH 辅助索引，则您还可以改善此类查询的搜索性能。  
  
 虽然主 XML 索引避免了在运行时拆分 XML 二进制大型对象，但是它不会为基于路径表达式的查询提供最好的性能。 由于是按顺序在与 XML 二进制大型对象相对应的主 XML 索引中的所有行中搜索大 XML 实例，所以按顺序搜索可能会很慢。 这种情况下，对主索引中的路径值和节点值生成辅助索引可以有效地提高索引搜索的速度。 在 PATH 辅助索引中，路径值和节点值是允许在搜索路径时使用更高效的查找功能的键列。 查询优化器可以将 PATH 索引用于如下所示的表达式：  
  
-   `/root/Location` ，仅指定一个路径  
  
 或  
  
-   `/root/Location/@LocationID[.="10"]` ，其中路径和节点值均指定。  
  
 以下查询介绍了适用 PATH 索引的情形：  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 在该查询中， `/PD:ProductDescription/@ProductModelID` 方法中的路径表达式 `"19"` 和值 `exist()` 对应于 PATH 索引的键字段。 这便允许在 PATH 索引中直接查找，并为主索引中的路径值提供优于顺序搜索的搜索性能。  
  
### <a name="value-secondary-xml-index"></a>VALUE 辅助 XML 索引  
 如果查询是基于值的查询，例如 `/Root/ProductDescription/@*[. = "Mountain Bike"]` 或 `//ProductDescription[@Name = "Mountain Bike"]`，且没有完全指定路径或路径包含有通配符，则生成基于主 XML 索引中的节点值所创建的辅助 XML 索引可以更快地获得结果。  
  
 VALUE 索引的键列是主 XML 索引的节点值和路径。 如果您的工作负荷涉及到查询 XML 实例中的值，但不知道包含这些值的元素名称或属性名称，则 VALUE 索引可能会很有用。 例如，以下表达式受益于 VALUE 索引：  
  
-   `//author[LastName="someName"]`，其中 <`LastName`> 元素的值已知，但是 <`author`> 父级可以出现在任何地方。  
  
-   `/book[@* = "someValue"]`，其中查询将查找包含值为 `"someValue"` 的属性的 <`book`> 元素。  
  
 以下查询从 `ContactID` 表中返回 `Contact` 。 `WHERE`子句中指定筛选器中的值看起来`AdditionalContactInfo``xml`类型列。 只有当相应的其他联系信息 XML 二进制大型对象包含具体的电话号码时，才会返回联系 ID。 由于 <`telephoneNumber`> 元素可以显示在 XML 中的任意位置，因而路径表达式指定 descendent-or-self 轴。  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS CI,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.exist('//ACT:telephoneNumber/ACT:number[.="111-111-1111"]') = 1  
```  
  
 在这种情况下，<`number`> 的搜索值是已知的，但是它可以作为 <`telephoneNumber`> 元素的子级在 XML 实例中的任意位置出现。 这种查询可能受益于基于特定值的索引查找。  
  
### <a name="property-secondary-index"></a>PROPERTY 辅助索引  
 从单个 XML 实例检索一个或多个值的查询适用 PROPERTY 索引。 通过检索对象属性时，会发生这种**value （)** 方法的`xml`类型并且知道对象的主键值。  
  
 PROPERTY 索引是对主 XML 索引的列（PK、Path 和节点值）创建的，其中 PK 是基表的主键。  
  
 例如，对于产品样式 `19`，以下查询使用 `ProductModelID` 方法检索 `ProductModelName` 属性值和 `value()` 属性值。 使用 PROPERTY 索引代替主 XML 索引或其他辅助 XML 索引可以使执行速度更快。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.value('(/PD:ProductDescription/@ProductModelID)[1]', 'int') as ModelID,  
       CatalogDescription.value('(/PD:ProductDescription/@ProductModelName)[1]', 'varchar(30)') as ModelName          
FROM Production.ProductModel     
WHERE ProductModelID = 19  
```  
  
 本主题后面介绍的区别，除了创建 XML 索引上`xml`类型列是类似于创建索引对非`xml`类型列。 可以使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 语句创建和管理 XML 索引：  
  
-   [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)  
  
-   [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)  
  
## <a name="getting-information-about-xml-indexes"></a>获取有关 XML 索引的信息  
 XML 索引项位于目录视图 sys.indexes 中，索引“type”为 3。 名称列包含 XML 索引的名称。  
  
 另外，XML 索引还记录在目录视图 sys.xml_indexes 中。 此视图包含 sys.indexes 的所有列以及对 XML 索引有用的某些特定列。 secondary_type 列中的值 NULL 表示主 XML 索引；值“P”、“R”和“V”分别表示 PATH、PROPERTY 和 VALUE 辅助 XML 索引。  
  
 可以在表值函数 [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)中找到 XML 索引的空间使用情况。 它提供了所有索引类型的相关信息，例如，占用的磁盘页数、平均行大小（字节）和记录数。 其中也包括 XML 索引。 对于每个数据库分区，都提供此信息。 XML 索引使用基表的相同分区方案和分区函数。  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_db_index_physical_stats (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)   
 [XML 数据 (SQL Server)](../xml/xml-data-sql-server.md)  
  
  
