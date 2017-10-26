---
title: "使用高级的数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
caps.latest.revision: 58
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b74ed587d91e351f91db2e3ef2a45c41edf37918
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-advanced-data-types"></a>使用高级数据类型
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]使用 JDBC 高级数据类型将转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]编程语言的数据类型为 Java 可以理解的格式。  
  
## <a name="remarks"></a>注释  
 下表列出了默认映射之间高级[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，JDBC 和 Java 编程语言的数据类型。  
  
|SQL Server 类型|JDBC 类型 (java.sql.Types)|Java 语言类型|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> 图像|LONGVARBINARY|byte []\(默认)，Blob，InputStream，字符串|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String（默认）、Clob、InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String（默认）、Clob、NClob (Java SE 6.0)|  
|xml|LONGVARCHAR<br /><br /> SQLXML (Java SE 6.0)|String（默认）、InputStream、Clob、byte[]、Blob、SQLXML (Java SE 6.0)|  
|Udt<sup>1</sup>|VARBINARY|String（默认）、byte[]、InputStream|  
  
 <sup>1</sup> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持发送和检索二进制数据作为 CLR Udt，但不支持的 CLR 元数据的操作。  
  
 以下部分提供了关于如何使用 JDBC 驱动程序和高级数据类型的示例。  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>BLOB、CLOB 和 NCLOB 数据类型  
 JDBC 驱动程序实现了 java.sql.Blob、java.sql.Clob 和 java.sql.NClob 接口的所有方法。  
  
> [!NOTE]  
>  CLOB 值可与[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]（或更高版本） 大型值数据类型。 具体而言，可以与使用 CLOB 类型**varchar （max)**和**nvarchar (max)**数据类型，可与使用 BLOB 类型**varbinary （max)**和**映像**可以用于数据类型和 NCLOB 类型**ntext**和**nvarchar (max)**。  
  
## <a name="large-value-data-types"></a>大值数据类型  
 在早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]、 使用大型值数据类型需要特殊处理。 大值数据类型是超过了 8KB 最大行大小的数据类型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]引入了最大说明符**varchar**， **nvarchar**，和**varbinary**数据类型，以允许的值存储最大为 2 ^31 个字节。 表列和[!INCLUDE[tsql](../../includes/tsql_md.md)]变量可以指定**varchar （max)**， **nvarchar (max)**，或**varbinary （max)**数据类型。  
  
 大值类型主要用于以下场合：从数据库中检索这些类型，或者将其添加到数据库。 以下部分介绍了完成这些任务的几种不同方法。  
  
### <a name="retrieving-large-value-types-from-a-database"></a>从数据库中检索大值类型  
 检索非二进制大型值数据类型时，如**varchar （max)**数据类型-一种方法是从数据库读取该数据作为字符流。 在下面的示例中， [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类用于从数据库中检索数据和返回作为结果集。 则[getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类用于从结果集中读取大型值数据。  
  
```  
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```  
  
> [!NOTE]  
>  这种方法还可以用于**文本**， **ntext**，和**nvarchar (max)**数据类型。  
  
 检索二进制大型值数据类型时，如**varbinary （max)**数据类型-从数据库中，有几种方法，你可以执行。 最有效的方法是将数据作为二进制流进行读取，如下所示：  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```  
  
 你还可以使用[getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)方法来读取的数据作为字节数组，如以下所示：  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```  
  
> [!NOTE]  
>  还可以将数据作为 BLOB 进行读取。 但是，这种方法与前两种方法相比效率较低。  
  
### <a name="adding-large-value-types-to-a-database"></a>向数据库中添加大值类型  
 通过 JDBC 驱动程序上载较大数据适用于内存大小合适的情况，而对于大于内存的情况，流是主要选择。 但是，最有效的上载较大数据的方法是通过流接口。  
  
 使用字符串或字节也是一个选项，如下所示：  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```  
  
> [!NOTE]  
>  此方法还可以用于存储中的值**文本**， **ntext**，和**nvarchar (max)**列。  
  
 如果在服务器上的映像库，并且必须整个二进制图像文件上载到**varbinary （max)**列中，使用 JDBC 驱动程序的最有效方法是使用流直接，如以下所示：  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)");  
File inputFile = new File("CLOBFile20mb.jpg");  
FileInputStream inStream = new FileInputStream(inputFile);  
int id = 1;  
pstmt.setInt(1,id);  
pstmt.setBinaryStream(2, inStream);  
pstmt.executeUpdate();  
inStream.close();  
```  
  
> [!NOTE]  
>  使用 CLOB 或 BLOB 方法不是上载较大数据的有效方法。  
  
### <a name="modifying-large-value-types-in-a-database"></a>修改数据库中的大值类型  
 在大多数情况下，更新或修改数据库上的较大值的建议的方法是将通过参数传递[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类通过使用[!INCLUDE[tsql](../../includes/tsql_md.md)]命令，如更新、 写入和子字符串。  
  
 如果你必须将一个大型的文本文件，例如已存档的 HTML 文件，在 word 的实例可以使用 Clob 对象，如下所示：  
  
```  
String SQL = "SELECT * FROM test1;";  
Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
ResultSet rs = stmt.executeQuery(SQL);  
rs.next();  
  
Clob clob = rs.getClob(2);  
long pos = clob.position("dog", 1);  
clob.setString(pos, "cat");  
rs.updateClob(2, clob);  
rs.updateRow();  
```  
  
 此外，可以在服务器上完成全部工作，仅将参数传递到准备好的 UPDATE 语句。  
  
 有关大值类型的详细信息，请参阅 SQL Server 联机丛书中的“使用大值类型”。  
  
## <a name="xml-data-type"></a>XML 数据类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]提供**xml** ，您可以存储 XML 文档和片段中的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 **Xml**数据类型是中的内置数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，并在某些方面类似于其他内置类型，如是**int**和**varchar**。 因为与其他内置类型，你可以使用**xml**数据类型用作列类型创建表时; 作为变量类型、 参数类型或函数返回类型; 或在[!INCLUDE[tsql](../../includes/tsql_md.md)]CAST 和 CONVERT 函数。  
  
 JDBC 驱动程序中, **xml**可以作为字符串、 字节数组、 流、 CLOB、 BLOB 或 SQLXML 对象映射数据类型。 默认值为字符串。 从 JDBC Driver 2.0 开始，JDBC 驱动程序为 JDBC 4.0 API 提供支持，后者引入了 SQLXML 接口。 SQLXML 接口定义进行交互并处理 XML 数据的方法。 **SQLXML**数据类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml**数据类型。 有关如何读取和写入 XML 数据，from 和 to 的关系数据库的详细信息**SQLXML** Java 数据类型，请参阅[支持 XML 数据](../../connect/jdbc/supporting-xml-data.md)。  
  
 实现**xml** JDBC 驱动程序中的数据类型提供对以下支持：  
  
-   在大多数常见的编程场景中，对作为标准 Java UTF-16 字符串的 XML 的访问  
  
-   输入以 UTF-8 和其他 8 格式进行编码的 XML  
  
-   为了可与其他 XML 处理器和磁盘文件进行互换而以 UTF-16 进行编码时，对作为带有前导 BOM 的字节数组的 XML 的访问  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]UTF 16 编码 xml 需要前导 BOM。 当以字节数组形式提供 XML 参数值时，应用程序必须提供此前导 BOM。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]始终输出 XML 值，如 utf-16 字符串与没有 BOM 或嵌入编码声明。 当将 XML 值作为 byte[]、BinaryStream 或 Blob 进行检索时，会为该值预置一个 UTF-16 BOM。  
  
 有关详细信息**xml**数据类型，请参阅"xml 数据类型"中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="user-defined-data-type"></a>用户定义的数据类型  
 中的用户定义类型 (Udt) 的简介[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]扩展通过让你存储对象和自定义数据结构中的 SQL 类型系统[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 UDT 可以包含多种数据类型并且可具有行为，这使它们不同于由单一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 系统数据类型构成的传统别名数据类型。 可使用 Microsoft .NET 公共语言运行时 (CLR)（生成可验证的代码）所支持的任意一种语言定义 UDT。 这些语言包括 Microsoft Visual C# 和 Visual Basic .NET。 数据被公开为基于 .NET Framework 的类或结构的字段和属性，行为由类或结构的方法定义。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，UDT 可以用作表的列定义为中的变量[!INCLUDE[tsql](../../includes/tsql_md.md)]批处理，或作为自变量的[!INCLUDE[tsql](../../includes/tsql_md.md)]函数或存储的过程。  
  
 有关用户定义的数据类型的详细信息，请参阅"使用和修改的用户定义的类型的实例"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

