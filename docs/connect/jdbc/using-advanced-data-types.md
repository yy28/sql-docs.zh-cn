---
title: 使用高级数据类型
description: 了解如何通过 Microsoft JDBC Driver for SQL Server 使用 JDBC 高级数据类型从 SQL Server 数据类型转换为 Java 数据类型。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70de1a4d2508a955510eb160af5622d7c1252520
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81727931"
---
# <a name="using-advanced-data-types"></a>使用高级数据类型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 使用 JDBC 高级数据类型将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型转换为 Java 编程语言所支持的格式。  
  
## <a name="remarks"></a>备注

下表列出了高级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、JDBC 和 Java 编程语言数据类型之间的默认映射。  
  
|SQL Server 类型|JDBC 类型 (java.sql.Types)|Java 语言类型|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|byte[] \(默认）、Blob、InputStream、String|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String（默认）、Clob、InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (default), Clob, NClob|  
|xml|LONGVARCHAR<br /><br /> SQLXML|String (default), InputStream, Clob, byte[], Blob, SQLXML|  
|Udt<sup>1</sup>|VARBINARY|String（默认）、byte[]、InputStream|  
|sqlvariant|SQLVARIANT|对象|  
|geometry<br /><br /> geography|VARBINARY|byte[]|  


<sup>1</sup>[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持以二进制数据的格式发送和检索 CLR UDT，但不支持操作 CLR 元数据。  
  
以下部分提供了关于如何使用 JDBC 驱动程序和高级数据类型的示例。  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>BLOB、CLOB 和 NCLOB 数据类型

JDBC 驱动程序实现了 java.sql.Blob、java.sql.Clob 和 java.sql.NClob 接口的所有方法。  
  
> [!NOTE]  
> CLOB 值可与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]（或更高版本）大值数据类型一同使用。 具体来说，CLOB 类型可以与 varchar(max)  和 nvarchar(max)  数据类型一起使用，BLOB 类型可以与 varbinary(max)  和 image  数据类型一起使用，NCLOB 类型可与 ntext  和 nvarchar(max)  一起使用。  

## <a name="large-value-data-types"></a>大值数据类型

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本中，使用大值数据类型需要特殊处理。 大值数据类型是超过了 8KB 最大行大小的数据类型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为 varchar、nvarchar 和 varbinary 数据类型引入一个 max 说明符，以允许存储最长可达 2^31 个字节的值    。 表列和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 变量可以指定 varchar(max)、nvarchar(max) 或 varbinary(max) 数据类型    。  

大值类型主要用于以下场合：从数据库中检索这些类型，或者将其添加到数据库。 以下部分介绍了完成这些任务的几种不同方法。  

### <a name="retrieving-large-value-types-from-a-database"></a>从数据库中检索大值类型

从数据库中检索非二进制大值数据类型（例如 varchar(max) 数据类型）时，一种方法是将此数据读取为字符流  。 以下实例使用了 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法从数据库中检索数据，并将其返回为结果集。 然后，使用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 类的 [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 方法从结果集读取大值数据。  

```java
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```

> [!NOTE]
> 此相同方法还可用于 text  、ntext  和 nvarchar (max)  数据类型。  

从数据库中检索二进制大值数据类型（例如 varbinary(max)）时，可采用多种方法进行操作  。 最有效的方法是将数据作为二进制流进行读取，如下所示：  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```

也可以使用 [getBytes](reference/getbytes-method-sqlserverresultset.md) 方法将数据作为字节数组进行读取，如下所示：  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```

> [!NOTE]  
> 还可以将数据作为 BLOB 进行读取。 但是，这种方法与前两种方法相比效率较低。  

### <a name="adding-large-value-types-to-a-database"></a>向数据库添加大值类型

通过 JDBC 驱动程序上载较大数据适用于内存大小合适的情况，而对于大于内存的情况，流是主要选择。 但是，最有效的上载较大数据的方法是通过流接口。  

使用字符串或字节也是一个选项，如下所示：  

```java
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```

> [!NOTE]  
> 还可以将这种方法用于存储在 text  、ntext  和 nvarchar(max)  列中的值。  

如果在服务器上具有图像库并且必须将整个二进制图像文件上传到 varbinary(max) 列，则适用于 JDBC 驱动程序的最有效方法是直接使用流，如下所示  ：  

```java
try (PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)")) { 
  File inputFile = new File("CLOBFile20mb.jpg");  
  try (FileInputStream inStream = new FileInputStream(inputFile)) {
    int id = 1;  
    pstmt.setInt(1,id);  
    pstmt.setBinaryStream(2, inStream);  
    pstmt.executeUpdate();
  }
}
```

> [!NOTE]  
> 使用 CLOB 或 BLOB 方法不是上载较大数据的有效方法。  

### <a name="modifying-large-value-types-in-a-database"></a>修改数据库中的大值类型

在大多数情况下，用于在数据库上更新或修改较大值的推荐方法是使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令（例如 `UPDATE``WRITE` 和 `SUBSTRING`）通过 [SQLServerPreparedStatement](reference/sqlserverpreparedstatement-class.md) 类和 [SQLServerCallableStatement](reference/sqlservercallablestatement-class.md) 类来传递参数。  

如果必须替换较大文本文件（例如已存档的 HTML 文件）中某个字的实例，则可以使用 Clob 对象，如下所示：  

```java
String SQL = "SELECT * FROM test1;";  
try (Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE)
     ResultSet rs = stmt.executeQuery(SQL)) {
  rs.next();

  Clob clob = rs.getClob(2);  
  long pos = clob.position("dog", 1);  
  clob.setString(pos, "cat");  
  rs.updateClob(2, clob);  
  rs.updateRow();  
}
```

此外，可以在服务器上完成全部工作，仅将参数传递到准备好的 UPDATE 语句。  

有关大值类型的详细信息，请参阅 SQL Server 联机丛书中的“使用大值类型”。  

## <a name="xml-data-type"></a>XML 数据类型

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了 xml 数据类型，该数据类型允许将 XML 文档和片段存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中  。 xml 数据类型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的内置数据类型，在某些方面类似于其他内置类型（如 int 和 varchar）    。 对于其他内置类型，在作为变量类型、参数类型、函数返回类型或在 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 和 CONVERT 函数中创建表时，可以使用 xml 数据类型作为列类型  。  
  
在 JDBC 驱动程序中，xml 数据类型可以映射为字符串、字节数组、流、CLOB、BLOB 或 SQLXML 对象  。 String 为默认值。 从 JDBC Driver 2.0 开始，JDBC 驱动程序为 JDBC 4.0 API 提供支持，后者引入了 SQLXML 接口。 SQLXML 接口定义与 XML 数据交互以及操作 XML 数据的方法。 数据类型 SQLXML  映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]xml  数据类型。 若要详细了解如何使用 SQLXML  Java 数据类型从/向关系数据库读取和写入 XML 数据，请参阅[支持 XML 数据](../../connect/jdbc/supporting-xml-data.md)。  
  
在 JDBC 驱动程序中实现 xml 数据类型为以下各项提供了支持  ：  
  
- 在大多数常见的编程场景中，对作为标准 Java UTF-16 字符串的 XML 的访问  
  
- 输入以 UTF-8 和其他 8 格式进行编码的 XML  
  
- 为了可与其他 XML 处理器和磁盘文件进行互换而以 UTF-16 进行编码时，对作为带有前导 BOM 的字节数组的 XML 的访问  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要求以 UTF-16 编码的 XML 具有前导 BOM。 当以字节数组形式提供 XML 参数值时，应用程序必须提供此前导 BOM。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 始终以 UTF-16 字符串形式输出 XML 值，而不带有 BOM 或嵌入式编码声明。 当将 XML 值作为 byte[]、BinaryStream 或 Blob 进行检索时，会为该值预置一个 UTF-16 BOM。  
  
有关 xml 数据类型的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“xml 数据类型”  。  
  
## <a name="user-defined-data-type"></a>用户定义数据类型  

通过允许在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中存储对象和自定义数据结构，在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中引入了用户定义的类型 (UDT)，从而扩展了 SQL 类型系统。 UDT 可以包含多种数据类型并且可具有行为，这使它们不同于由单一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型构成的传统别名数据类型。 可使用 Microsoft .NET 公共语言运行时 (CLR)（生成可验证的代码）所支持的任意一种语言定义 UDT。 这些语言包括 Microsoft Visual C# 和 Visual Basic .NET。 数据被公开为基于 .NET Framework 的类或结构的字段和属性，行为由类或结构的方法定义。  
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，UDT 可用作表的列定义、[!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理的变量或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数或存储过程的参数。  
  
有关用户定义的数据类型的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“使用和修改用户定义类型的实例”。  
  
## <a name="sql_variant-data-type"></a>Sql_variant 数据类型

有关 sql_variant 数据类型的信息，请参阅[使用 Sql_variant 数据类型](using-sql-variant-datatype.md)。  

## <a name="spatial-data-types"></a>空间数据类型

有关 spatial 数据类型的信息，请参阅[使用 Spatial 数据类型](use-spatial-datatypes.md)。  

## <a name="see-also"></a>另请参阅

[了解 JDBC 驱动程序数据类型](understanding-the-jdbc-driver-data-types.md)  
