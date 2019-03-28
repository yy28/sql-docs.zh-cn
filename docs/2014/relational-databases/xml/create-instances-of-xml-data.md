---
title: 创建 XML 数据的实例 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- type casting string instances [XML in SQL Server]
- XML [SQL Server], typed
- xml data type [SQL Server], generating instances
- casting string instances [XML in SQL Server]
- typed XML
- generating XML instances [SQL Server]
- XML [SQL Server], generating instances
- white space [XML in SQL Server]
ms.assetid: dbd6c06f-db6e-44a7-855a-6a55bf374907
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae842748d2d510c5c00f329f5e28cd49a0c86ef3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538619"
---
# <a name="create-instances-of-xml-data"></a>创建 XML 数据的实例
  本主题说明了如何生成 XML 实例。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，可以按照下列方式生成 XML 实例：  
  
-   对字符串实例进行类型转换。  
  
-   将 SELECT 语句与 FOR XML 子句结合使用。  
  
-   使用常量赋值。  
  
-   使用大容量加载。  
  
## <a name="type-casting-string-and-binary-instances"></a>类型转换字符串实例和二进制实例  
 你可以分析的任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符串数据类型，如 [**n**] [**var**]**char**， **[n] text**， **varbinary**，并**映像**，到`xml`数据类型转换 （强制转换） 或 （转换） 将字符串转换为`xml`数据类型。 对非类型化的 XML 进行检查以确认其格式是否正确。 如果没有与关联的架构`xml`还执行类型验证。 有关详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](compare-typed-xml-to-untyped-xml.md)。  
  
 XML 文档可以采用不同的编码方式（例如，UTF-8、UTF-16 和 windows-1252）进行编码。 下面概述了有关字符串和二进制源类型与 XML 文档编码进行交互的方式以及分析器行为方式的规则。  
  
 由于 **nvarchar** 采用为双字节 Unicode 编码（例如 UTF-16 或 UCS-2），因此 XML 分析器会将字符串值作为双字节 Unicode 编码 XML 文档或片断来处理。 这意味着该 XML 文档需要以双字节 Unicode 编码方式进行编码，同时需要与源数据类型兼容。 UTF-16 编码 XML 文档可以具有 UTF-16 字节顺序标记 (BOM)，但是它不需要，因为源类型的上下文显式指出 UTF-16 编码 XML 文档只能是双字节 Unicode 编码文档。  
  
 **varchar** 字符串的内容被 XML 分析器视为单字节编码 XML 文档/片断。 由于 **varchar** 源字符串具有相关联的代码页，因此如果 XML 本身没有明确指定编码方式，分析器将使用该代码页。如果 XML 实例具有 BOM 或编码声明，则该 BOM 或声明应当与代码页一致，否则分析器将会报告一个错误。  
  
 **varbinary** 的内容被视为码位流，它将直接被传递到 XML 分析器。 这样，XML 文档或片断就需要提供 BOM 或其他内联编码信息。 分析器将仅查看该流来确定编码方式。 这意味着 UTF-16 编码 XML 需要提供 UTF-16 BOM，不带 BOM 和编码声明的实例将被解释为 UTF-8。  
  
 如果事先不知道 XML 文档的编码方式，并且数据在转换到 XML 之前被作为字符串或二进制数据而不是 XML 数据来传递，则建议将数据作为 **varbinary**处理。 例如，当使用 OpenRowset() 从 XML 文件读取数据时，应该指定将数据作为 **varbinary(max)** 值读取：  
  
```  
select CAST(x as XML)   
from OpenRowset(BULK 'filename.xml', SINGLE_BLOB) R(x)  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在内部以一种使用 UTF-16 编码的有效二进制表示形式来表示 XML。 用户提供的编码不会保留下来，但在分析过程中会考虑。  
  
### <a name="type-casting-clr-user-defined-types"></a>类型转换 CLR 用户定义类型  
 如果 CLR 用户定义类型具有 XML 序列化，则该类型的实例可以显式转换为 XML 数据类型。 有关 CLR 用户定义类型的 XML 序列化的详细信息，请参 [从 CLR 数据库对象进行 XML 序列化](../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md)。  
  
### <a name="white-space-handling-in-typed-xml"></a>类型化的 XML 中的空格处理  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果元素内容中的空格出现在一组只有空格并由标记（如开始或结束标记）分隔的字符数据中，则认为其无关紧要，因此不对其进行实体化。 （忽略 CDATA 部分。）这种空格处理方式与万维网联盟 (W3C) 发布的 XML 1.0 规格中介绍的空格处理方式不同。 这是因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XML 分析器只识别有限数量的 DTD 子集（在 XML 1.0 中定义）。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中支持的有限 DTD 子集的详细信息，请参阅 [CAST 和 CONVERT (Transact-SQL)](/sql/t-sql/functions/cast-and-convert-transact-sql)。  
  
 默认情况下，在 XML 分析器将字符串数据转换为 XML 时，如果存在下列任何一种情况，则 XML 分析器将丢弃无关紧要的空格：  
  
-   `The xml:space` 属性。  
  
-   某元素或其某一祖先元素上有效的 `xml:space` 属性具有默认值。  
  
 例如：  
  
```  
declare @x xml  
set @x = '<root>      <child/>     </root>'  
select @x   
```  
  
 下面是结果：  
  
```  
<root><child/></root>  
```  
  
 不过，您可以更改此行为。 若要为 xml DT 实例保留空格，请使用 CONVERT 运算符，并将其可选的 *style* 参数的值设置为 1。 例如：  
  
```  
SELECT CONVERT(xml, N'<root>      <child/>     </root>', 1)  
```  
  
 如果未使用 *style* 参数，或将其值设置为 0，则转换 xml DT 实例时不保留无关紧要的空格。 有关在将字符串数据转换为 xml DT 实例时如何使用 CONVERT 运算符及其 *style* 参数的详细信息，请参阅 [CAST 和 CONVERT (Transact-SQL)](/sql/t-sql/functions/cast-and-convert-transact-sql)。  
  
### <a name="example-cast-a-string-value-to-typed-xml-and-assign-it-to-a-column"></a>例如：将字符串值转换为类型化的 xml 并将其分配到的列  
 下面的示例将包含 XML 片段的字符串变量转换`xml`数据类型，然后将其存储在`xml`类型列：  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
go  
DECLARE  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
```  
  
 下面的插入操作隐式转换从字符串到`xml`类型：  
  
```  
INSERT INTO T VALUES (3, @s)   
```  
  
 可以使用显式 cast 的字符串`xml`类型：  
  
```  
INSERT INTO T VALUES (3, cast (@s as xml))  
```  
  
 另外，也可以使用 convert()，如下所示：  
  
```  
INSERT INTO T VALUES (3, convert (xml, @s))   
```  
  
### <a name="example-convert-a-string-to-typed-xml-and-assign-it-to-a-variable"></a>例如：将字符串转换为类型化的 xml 并将其分配给一个变量  
 在以下示例中，字符串转换为`xml`类型并赋给的变量`xml`数据类型：  
  
```  
declare @x xml  
declare  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
set @x =convert (xml, @s)  
select @x  
```  
  
## <a name="using-the-select-statement-with-a-for-xml-clause"></a>将 SELECT 语句与 FOR XML 子句结合使用  
 可以在 SELECT 语句中使用 FOR XML 子句以返回 XML 形式的结果。 例如：  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = (SELECT Column1, Column2  
               FROM   Table1, Table2  
               WHERE   Some condition  
               FOR XML AUTO)  
 ...  
```  
  
 SELECT 语句将返回到赋值的过程中进行分析的文本 XML 片段`xml`数据类型的变量。  
  
 此外可以使用[TYPE 指令](type-directive-in-for-xml-queries.md)直接返回 FOR XML 查询结果作为在 FOR XML 子句中`xml`类型：  
  
```  
Declare @xmlDoc xml  
SET @xmlDoc = (SELECT ProductModelID, Name  
               FROM   Production.ProductModel  
               WHERE  ProductModelID=19  
               FOR XML AUTO, TYPE)  
SELECT @xmlDoc  
```  
  
 下面是结果：  
  
```  
<Production.ProductModel ProductModelID="19" Name="Mountain-100" />...  
```  
  
 在以下示例中，类型化`xml`FOR XML 查询的结果插入到`xml`类型列：  
  
```  
CREATE TABLE T1 (c1 int, c2 xml)  
go  
INSERT T1(c1, c2)  
SELECT 1, (SELECT ProductModelID, Name  
           FROM Production.ProductModel  
           WHERE ProductModelID=19  
           FOR XML AUTO, TYPE)  
SELECT * FROM T1  
go  
```  
  
 有关 FOR XML 的详细信息，请参阅 [FOR XML (SQL Server)](for-xml-sql-server.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 `xml` 数据类型实例作为不同服务器构造（例如使用 TYPE 指令或在其中使用 `xml` 数据类型从 SQL 列、变量和输出参数返回 XML 的 FOR XML 查询）的结果返回到客户端。 在客户端应用程序代码中，ADO.NET 访问接口请求以二进制编码形式从服务器发送此 `xml` 数据类型信息。 但是，如果使用的是不带 TYPE 指令的 FOR XML，则 XML 数据将作为字符串类型返回。 在任何情况下，客户端访问接口都始终能够处理其中任一种形式的 XML 内容。  
  
## <a name="using-constant-assignments"></a>使用常量赋值  
 可以使用一个字符串常量，其中的一个实例`xml`预期数据类型。 这与将字符串隐式 CAST 为 XML 相同。 例如：  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
-- Or  
SET @xmlDoc = N'<?xml version="1.0" encoding="ucs-2"?><doc/>'  
```  
  
 前面的示例将字符串隐式转换`xml`数据类型，并将它分配给`xml`类型的变量。  
  
 下面的示例将常量字符串插入`xml`类型列：  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
INSERT INTO T VALUES (3, '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>')   
```  
  
> [!NOTE]  
>  对于类型化的 XML，是针对指定的架构来验证 XML。 有关详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="using-bulk-load"></a>使用大容量加载  
 通过增强的 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql) 功能，可以在数据库中大容量加载 XML 文档。 您可以将大容量加载到的文件中的 XML 实例`xml`类型列中的数据库。 有关工作示例，请参阅[批量导入和导出 XML 文档的示例 (SQL Server);](../import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)。 有关加载 XML 文档的详细信息，请参阅[加载 XML 数据](load-xml-data.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[检索和查询 XML 数据](retrieve-and-query-xml-data.md)|介绍了当 XML 实例存储在数据库中时未保留的部分。|  
  
## <a name="see-also"></a>请参阅  
 [类型化的 XML 与非类型化的 XML 的比较](compare-typed-xml-to-untyped-xml.md)   
 [XML 数据类型方法](/sql/t-sql/xml/xml-data-type-methods)   
 [XML 数据修改语言 (XML DML)](/sql/t-sql/xml/xml-data-modification-language-xml-dml)   
 [XML 数据 (SQL Server)](xml-data-sql-server.md)  
  
  
