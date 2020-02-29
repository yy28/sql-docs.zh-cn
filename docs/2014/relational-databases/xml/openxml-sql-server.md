---
title: OPENXML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ColPattern [XML in SQL Server]
- OPENXML statement, about OPENXML statement
- writing XML, OPENXML statement
- OPENXML statement, querying XML
- attribute-centric mapping
- SELECT statement [SQL Server], OPENXML keyword
- column patterns [XML in SQL Server]
- row patterns [XML in SQL Server]
- rowpattern [XML in SQL Server]
- queries [XML in SQL Server], OPENXML statement
- XML [SQL Server], OPENXML statement
- element-centric mapping [SQL Server]
ms.assetid: 060126fc-ed0f-478f-830a-08e418d410dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a40eb3451ed249cf1ac582179fbda67e04fdfb3e
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78174006"
---
# <a name="openxml-sql-server"></a>OPENXML (SQL Server)
  OPENXML 是一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 关键字，对内存中的 XML 文档提供与表或视图相似的行集。 OPENXML 允许像访问关系行集一样访问 XML 数据。 它通过提供以内部形式表示的 XML 文档的行集视图来实现这一点。 行集中的记录可以存储在数据库表中。

 无论行集提供程序（视图或 OPENROWSET）可以在何处作为源出现，都可以在 SELECT 和 SELECT INTO 语句中使用 OPENXML。 有关 OPENXML 语法的信息，请参阅 [OPENXML (Transact-SQL)](/sql/t-sql/functions/openxml-transact-sql)。

 若要使用 OPENXML 编写对 XML 文档的查询，必须先调用`sp_xml_preparedocument`。 它将分析 XML 文档并向准备使用的已分析文档返回一个句柄。 已分析文档以文档对象模型 (DOM) 树的形式说明 XML 文档中的各种节点。 该文档句柄传递给 OPENXML。 然后 OPENXML 根据传递给它的参数提供一个该文档的行集视图。

> [!NOTE]
>  `sp_xml_preparedocument`使用 MSXML 分析器的 SQL 更新版本 Msxmlsql.dll。 此版本的 MSXML 分析器设计为支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并保持与 MSXML 2.6 版的向后兼容性。

 必须通过调用 **sp_xml_removedocument** 系统存储过程从内存中删除以内部形式表示的 XML 文档来释放内存。

 下图说明了该过程。

 ![使用 OPENXML 分析 XML](../../database-engine/media/xmlsp.gif "使用 OPENXML 分析 XML")

 请注意，要理解 OPENXML，需要熟悉 XPath 查询并理解 XML。 有关 SQL Server 中 XPath 支持的详细信息，请参阅 [在 SQLXML 4.0 中使用 XPath 查询](../sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)。

> [!NOTE]
>  OPENXML 允许将行和列的 XPath 模式参数化为变量。 如果程序员向外部用户公开参数化（例如通过外部调用的存储过程提供参数），这种参数化可能会导致引入 XPath 表达式。 为了避免这种潜在的安全问题，建议切勿向外部调用方公开 XPath 参数。

## <a name="example"></a>示例
 `OPENXML` 下面的示例说明了如何在 `INSERT` 语句和 `SELECT` 语句中使用 。 `<Customers>` 示例 XML 文档包含 `<Orders>` 和  元素。

 首先， `sp_xml_preparedocument` 存储过程分析 XML 文档。 分析后的文档是 XML 文档中各节点（元素、属性、文本和注释）的树状表示形式。 `OPENXML` 然后， 引用此经过分析的 XML 文档，并提供此 XML 文档全部或部分内容的行集视图。 `INSERT` 使用 `OPENXML` 的  语句可将数据从这样的行集插入数据库表中。 `OPENXML` 可以使用多个  调用来提供 XML 文档中各部分的行集视图，并对它们进行处理，例如，将它们插入不同的表中。 此过程也称为“将 XML 拆分到表中”。

 `<Customers>` 在下面的示例中，拆分 XML 文档的方式是使用两个 `Customers` 语句，将 `<Orders>` 元素存储在 `Orders` 表中，将 `INSERT` 元素存储在  表中。 `SELECT` 另外，此例还说明了 `OPENXML` 语句如何使用 `CustomerID` 从 XML 文档中检索 `OrderDate` 和 。 `sp_xml_removedocument`该过程的最后一步是调用 。 这样做是为了释放已分配的内存，以包含在分析阶段创建的内部 XML 树表示形式。

```
-- Create tables for later population using OPENXML.
CREATE TABLE Customers (CustomerID varchar(20) primary key,
                ContactName varchar(20), 
                CompanyName varchar(20));
GO
CREATE TABLE Orders( CustomerID varchar(20), OrderDate datetime);
GO
DECLARE @docHandle int;
DECLARE @xmlDocument nvarchar(max); -- or xml type
SET @xmlDocument = N'<ROOT>
<Customers CustomerID="XYZAA" ContactName="Joe" CompanyName="Company1">
<Orders CustomerID="XYZAA" OrderDate="2000-08-25T00:00:00"/>
<Orders CustomerID="XYZAA" OrderDate="2000-10-03T00:00:00"/>
</Customers>
<Customers CustomerID="XYZBB" ContactName="Steve"
CompanyName="Company2">No Orders yet!
</Customers>
</ROOT>';
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument;
-- Use OPENXML to provide rowset consisting of customer data.
INSERT Customers 
SELECT * 
FROM OPENXML(@docHandle, N'/ROOT/Customers') 
  WITH Customers;
-- Use OPENXML to provide rowset consisting of order data.
INSERT Orders 
SELECT * 
FROM OPENXML(@docHandle, N'//Orders') 
  WITH Orders;
-- Using OPENXML in a SELECT statement.
SELECT * FROM OPENXML(@docHandle, N'/ROOT/Customers/Orders') WITH (CustomerID nchar(5) '../@CustomerID', OrderDate datetime);
-- Remove the internal representation of the XML document.
EXEC sp_xml_removedocument @docHandle; 
```

 下图显示了使用 sp_xml_preparedocument 创建的上述 XML 文档的 XML 分析树。

 ![经过分析的 XML 树](../../database-engine/media/xmlparsedtree.gif "经过分析的 XML 树")

## <a name="openxml-parameters"></a>OPENXML 参数
 OPENXML 的参数包括：

-   XML 文档句柄 (*idoc*)

-   标识要映射到行的节点的 XPath 表达式 (*rowpattern*)

-   对要生成的行集的说明

-   行集列和 XML 节点之间的映射

### <a name="xml-document-handle-idoc"></a>XML 文档句柄 (idoc)
 该`sp_xml_preparedocument`存储过程返回该文档句柄。

### <a name="xpath-expression-to-identify-the-nodes-to-be-processed-rowpattern"></a>标识要处理的节点的 XPath 表达式 (rowpattern)
  指定为 rowpattern 的 XPath 表达式标识 XML 文档中的一组节点。 *rowpattern* 标识的每个节点对应于 OPENXML 所生成的行集中的一行。

 XPath 表达式标识的节点可以是 XML 文档中的任何 XML 节点。  如果 rowpattern 标识 XML 文档中的一组元素，则所标识的每个元素节点在行集中都占一行。 例如，如果 *rowpattern*以属性结束，则将为 *rowpattern* 选择的每个属性节点创建一行。

### <a name="description-of-the-rowset-to-be-generated"></a>对要生成的行集的说明
 OPENXML 使用行集架构来生成结果行集。 指定行集架构时，可以使用下列选项。

#### <a name="using-the-edge-table-format"></a>使用边缘表格式
 应使用边缘表格式来指定行集架构。 请勿使用 WITH 子句。

 否则，OPENXML 将以边缘表格式返回行集。 边缘表这种称谓源于已分析的 XML 文档树中的每个边缘都映射到行集中的一行。

 边缘表在单个表中表示 XML 文档的细密结构。 此结构包括元素名称和属性名称、文档层次结构、命名空间和处理指令。 通过边缘表格式可以获得无法通过元属性表现的其他信息。 [Specify Metaproperties in OPENXML](../xml/specify-metaproperties-in-openxml.md)有关元数据属性的详细信息，请参阅。

 通过边缘表提供的其他信息可以存储和查询元素和属性的数据类型以及节点类型，另外还可以存储和查询有关 XML 文档结构的信息。 有了这些其他信息，还可以创建您自己的 XML 文档管理系统。

 通过使用边缘表，可以编写这样一些存储过程：将 XML 文档作为二进制大型对象 (BLOB) 输入，生成边缘表，然后以更为详细的级别提取和分析文档。 此详细级别可以包括查找文档层次结构、元素名称和属性名称、命名空间和处理指令。

 当映射到其他关系格式不合逻辑且 ntext 字段没有提供足够的结构信息时，边缘表还可以用作 XML 文档的存储格式。

 在可以使用 XML 分析器检查 XML 文档的情况下，使用边缘表也可以获得相同的信息。

 下表介绍了边缘表的结构。

|列名称|数据类型|说明|
|-----------------|---------------|-----------------|
|**id**|**bigint**|文档节点的唯一 ID。<br /><br /> 根元素具有的 ID 值为 0。 保留负的 ID 值。|
|**parentid**|**bigint**|标识节点的父节点。 此 ID 标识的父节点不一定是父元素。 但具体情况取决于此 ID 所标识节点的子节点的节点类型。 例如，如果节点为文本节点，则其父节点可能是一个属性节点。<br /><br />  如果节点位于 XML 文档的顶层，则其 ParentID 为 NULL。|
|**节点类型**|**int**|标识节点类型，是对应于 XML 对象模型 (DOM) 节点类型编号的一个整数。<br /><br /> 下列值是可以显示在此列中以指明节点类型的值：<br /><br /> **1** = 元素节点<br /><br /> **2** = 属性节点<br /><br /> **3** = 文本节点<br /><br /> **4** = CDATA 部分节点<br /><br /> **5** = 实体引用节点<br /><br /> **6** = 实体节点<br /><br /> **7** = 处理指令节点<br /><br /> **8** = 注释节点<br /><br /> **9** = 文档节点<br /><br /> **10** = 文档类型节点<br /><br /> **11** = 文档片段节点<br /><br /> **12** = 表示法节点<br /><br /> 有关详细信息，请参阅 Microsoft XML (MSXML) SDK 中的“节点类型属性”主题。|
|**localname**|**nvarchar(max)**|给出元素或属性的本地名称。 如果 DOM 对象没有名称，则为 NULL。|
|**prefix**|**nvarchar(max)**|节点名称的命名空间前缀。|
|**namespaceuri**|**nvarchar(max)**|节点的命名空间 URI。 如果值为 NULL，则命名空间不存在。|
|**datatype**|**nvarchar(max)**|元素或属性行的实际数据类型，否则是 NULL。 数据类型是从内联 DTD 中或从内联架构中推断得出。|
|**prev**|**bigint**|前一个同级元素的 XML ID。 如果前面没有同级元素，则为 NULL。|
|**text**|**ntext**|包含文本形式的属性值或元素内容。 如果边缘表项不需要值则为 NULL。|

#### <a name="using-the-with-clause-to-specify-an-existing-table"></a>使用 WITH 子句指定现有表
 可以使用 WITH 字句指定现有表的名称。 若要执行此操作，只需指定现有的表名称，OPENXML 可以使用该表的架构生成行集。

#### <a name="using-the-with-clause-to-specify-a-schema"></a>使用 WITH 子句指定架构
 可以使用 WITH 子句指定完整架构。 在指定行集架构时，可指定列名、它们的数据类型，以及它们到 XML 文档的映射。

 可以使用 SchemaDeclaration 中的 ColPattern 参数来指定列模式。 指定的列模式用于将行集列映射到 rowpattern 标识的 XML 节点并确定映射类型。

 *flags* 如果没有为列指定 ColPattern，则行集列根据  参数指定的映射来映射到具有相同名称的 XML 节点。 *flags* 但是，如果在 WITH 子句中将 ColPattern 指定为架构描述的一部分，则它将覆盖在  参数中指定的映射。

### <a name="mapping-between-the-rowset-columns-and-the-xml-nodes"></a>行集列和 XML 节点之间的映射
 在 OPENXML 语句中，可以选择指定行集列和 *rowpattern*标识的 XML 节点之间的映射类型（如以属性为中心或以元素为中心）。 此信息用于 XML 节点和行集列之间的转换。

 可以采用下列两种方式之一来指定映射，也可以同时采用来指定映射：

-    通过使用 flags 参数

      由 flags 参数指定的映射采用名称对应，即 XML 节点映射到具有相同名称的对应行集列。

-    通过使用 ColPattern 参数

     *ColPattern*是 XPath 表达式，被指定为 WITH 子句中的 *SchemaDeclaration* 的一部分。 在 *ColPattern* 中指定的映射覆盖 *flags* 参数指定的映射。

     *ColPattern* 可以用于指定映射类型（如以属性为中心或以元素为中心），以覆盖或增强 *flags*指定的默认映射。

      在下列情况下指定 ColPattern：

    -   行集中的列名不同于它映射到的元素名称或属性名称。  在这种情况下，ColPattern 用于标识行集列映射到的 XML 元素名称和属性名称。

    -   希望将元属性特性映射到列。  在这种情况下，ColPattern 用于标识行集列映射到的元属性。 有关如何使用元属性的详细信息，请参阅 [在 OPENXML 中指定元属性](../xml/specify-metaproperties-in-openxml.md)。

 *flags* 和 *ColPattern* 参数都是可选的。 如果未指定映射，则采用以属性为中心的映射。 以属性为中心的映射是 *flags* 参数的默认值。

#### <a name="attribute-centric-mapping"></a>以属性为中心的映射
 将 OPENXML 中的 *flags* 参数设置为 1 (XML_ATTRIBUTES) 将指定“**以属性为中心**”的映射。 如果 *flags* 包含 XML_ATTRIBUTES，则显示的行集提供或使用其中每个 XML 元素都表示为一行的那些行。 XML 属性根据名称对应映射到 SchemaDeclaration 中定义的属性，或 WITH 子句的 Tablename 提供的属性。 名称对应表示具有特定名称的 XML 属性都以相同名称存储在行集中的列内。

  如果列名不同于它映射到的属性名称，则必须指定 ColPattern。

 如果 XML 属性具有命名空间限定符，则行集中的列名也必须有该限定符。

#### <a name="element-centric-mapping"></a>以元素为中心的映射
 将 OPENXML 中的 *flags* 参数设置为 2 (XML_ELEMENTS) 将指定“**以元素为中心**”的映射。  除了下列差异外，它与“以属性为中心”的映射相似：

-   除非指定列级模式，否则映射的名称对应（例如，映射到具有相同名称的 XML 元素的列）选择不复杂的子元素。 在检索过程中，如果子元素复杂（因为它包含其他子元素），则将列设置为 NULL。 然后忽略子元素的属性值。

-   对于具有相同名称的多个子元素，将返回第一个节点。

## <a name="see-also"></a>另请参阅
 [sp_xml_preparedocument &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql) [sp_xml_removedocument &#40;](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql) Transact-sql&#41;[OPENXML &#40;transact-sql](/sql/t-sql/functions/openxml-transact-sql)&#41;[xml 数据 &#40;SQL Server](../xml/xml-data-sql-server.md)&#41;


