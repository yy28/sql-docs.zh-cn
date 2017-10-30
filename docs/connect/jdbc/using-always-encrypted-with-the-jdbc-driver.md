---
title: "使用始终加密的 JDBC 驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 12/30/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: 64
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: fffb61c4c3dfa58edaf684f103046d1029895e7c
ms.openlocfilehash: cee7f5dbcf66a5357ae68192703d841ae1601a35
ms.contentlocale: zh-cn
ms.lasthandoff: 10/19/2017

---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>对 JDBC 驱动程序使用始终加密
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文提供有关如何开发使用 Java 应用程序的信息[始终加密](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7)和 Microsoft JDBC Driver 6.0 （或更高版本） for SQL Server。

始终加密允许客户端加密敏感数据，并且永远不会显示数据或 SQL Server 或 Azure SQL 数据库的加密密钥。 始终加密的 SQL Server 启用驱动程序，如 Microsoft JDBC Driver 6.0 （或更高版本），从而实现此目的以透明方式加密和解密在客户端应用程序中的敏感数据。 该驱动程序自动确定哪个查询参数对应于敏感数据库列 （使用始终加密保护），并将这些参数的值的值传递到 SQL Server 或 Azure SQL 数据库之前对加密。 同样，该驱动程序以透明方式对查询结果中从加密数据库列检索到的数据进行解密。 有关详细信息，请访问[始终加密 （数据库引擎）](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7)和[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。  


## <a name="prerequisites"></a>先决条件

- 在数据库中配置始终加密。 这涉及为选定数据库列预配始终加密密钥和设置加密。 如果还没有配置了始终加密的数据库，请按照 [始终加密入门](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_5)中的说明操作。
- 请确保 Microsoft JDBC Driver 6.0 （或更高版本） 为您的开发计算机上安装 SQL Server。 
-   下载并安装 Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files。  请确保阅读包含在 zip 文件中的自述文件，以获取有关可能的导出/导入问题的说明和相关详细信息。  
  
    -   如果使用 sqljdbc41.jar，可以从下载的策略文件[Java 加密扩展 (JCE) 不受限制的强度管辖策略文件 7 下载](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)  
  
    -   如果使用包含的 sqljdbc42.jar，可以从下载的策略文件[Java 加密扩展 (JCE) 不受限制的强度管辖策略文件 8 下载](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)   
    
## <a name="enabling-always-encrypted-for-application-queries"></a>为应用程序查询启用始终加密  
若要启用的参数，加密和解密面向加密的列中，查询结果的最简单方法是通过设置的值**columnEncryptionSetting**到连接字符串关键字**启用**。

下面是 JDBC 驱动程序中启用始终加密的连接字符串示例：
  
```  
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;"; 
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
     
```  
  
而且，以下是使用 SQLServerDataSource 对象的等效示例。  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");  
SQLServerConnection con = (SQLServerConnection) ds.getConnection(); 
```    

还可以为单个查询启用始终加密。 请参阅**控制性能影响的始终加密**下面一节。 请注意，启用始终加密不足以成功实现加密或解密。 你还需要确保：
- 应用程序具有 *查看任意列主密钥定义* 和 *查看任意列加密密钥定义* 数据库权限，这是访问数据库中始终加密密钥的相关元数据所必需的权限。 有关详细信息，请参阅 [始终加密（数据库引擎）中的“权限”一节](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7)。
- 应用程序可以访问用于保护列加密密钥的列主密钥，以便对查询到的数据库列加密。 请注意，若要使用 Java 密钥存储提供程序，你需要提供连接字符串中的其他凭据。 请参阅**使用 Java 密钥存储提供程序**有关详细信息部分。

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>配置如何将 java.sql.Time 值发送到服务器

**SendTimeAsDatetime**连接属性用于配置如何将 java.sql.Time 值发送到服务器。 当 sendTimeAsDatetime = false，SQL Server 时类型作为发送值的时间以及何时 sendTimeAsDatetime = true，值发送为 datetime 类型的时间。 请注意，当时间列已加密，sendTimeAsDatetime 属性必须为 false 因为加密的列不支持从时间转换为日期时间。 另请注意，此属性是通过默认为 true，因此在使用加密的时间列时，你将需要将其设置为 false。 否则驱动程序会引发异常。 SQLServerConnection 类具有两种方法，从版本 6.0 的驱动程序以编程方式配置此属性的值：
 
* 公共 void setSendTimeAsDatetime (布尔 sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

有关此属性的详细信息，请访问[如何配置 java.sql.Time 值发送到服务器](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx)。 

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>配置如何将字符串值发送到服务器

**SendStringParametersAsUnicode**连接属性用于配置如何将字符串值发送到 SQL Server。 如果设置为"true"，字符串参数发送到 Unicode 格式中的服务器。 如果设置为"false"，字符串参数在非 Unicode 格式，如而不是 Unicode 的 ASCII/MBCS 中发送的。 此属性的默认值为"true"。 当启用始终加密，并 char/varchar/varchar(max) 列已加密、 的值**sendStringParametersAsUnicode**必须设置为 true （或保留为默认值）。 插入到加密的 char/varchar/varchar(max) 列的数据，如果此属性设置为 false 时，Microsoft JDBC Driver for SQL Server 将引发异常。 此属性的详细信息，请访问[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。 
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>检索和修改加密列中的数据

一旦为应用程序查询启用始终加密，你可以使用标准 JDBC Api 来检索或修改加密的数据库列中的数据。 假设你的应用程序具有所需的数据库权限，并且可以访问列主密钥，Microsoft JDBC Driver for SQL Server 将加密任何面向加密的列，并将解密数据的查询参数从加密列中检索数据类型返回的 JDBC 类型，对应于 SQL Server 的纯文本值设置为数据库架构中的列。
如果未启用始终加密，具有面向加密列的参数的查询将失败。 只要查询没有面向加密列的参数，就仍然可以从加密列中检索数据。 但是，Microsoft JDBC Driver for SQL Server 不会尝试解密从加密列检索到任何值，并且应用程序将收到二进制加密的数据 （作为字节数组）。

下表概述了查询的行为，具体取决于是否启用了始终加密：

|查询特征 | 启用了始终加密，并且应用程序可以访问密钥和密钥元数据|启用了始终加密，但应用程序无法访问密钥或密钥元数据 | 禁用了始终加密|
|:---|:---|:---|:---|
| 具有面向加密列的参数的查询。 | 以透明方式加密参数值。 | 错误 | 错误|
| 从加密列中检索数据且没有面向加密列的参数的查询。| 以透明方式解密来自加密列的结果。 应用程序收到对应于为加密的列配置的 SQL Server 类型的 JDBC 数据类型的纯文本的值。 | 错误 | 不解密来自加密列的结果。 应用程序收到字节数组形式的加密值 (byte[])。
      
 
### <a name="inserting-and-retrieving-encrypted-data-examples"></a>插入和检索加密的数据示例 
以下示例说明如何检索和修改加密列中的数据。 这些示例假定目标表具有以下架构。 请注意，SSN 和 BirthDate 列已加密。

```
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1), 
 [SSN] [char](11) COLLATE Latin1_General_BIN2 
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC, 
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL, 
 [BirthDate] [date] 
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED, 
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```
 
### <a name="inserting-data-example"></a>插入数据示例

此示例向 Patients 表插入一行。 请注意以下事项：
- 对于示例代码中的加密，没有什么特定的注意事项。 Microsoft JDBC Driver for SQL Server 自动检测并加密面向加密的列的参数。 这使得加密操作对应用程序而言是透明的。 
- 插入到数据库列，包括加密的列的值作为参数使用 SQLServerPreparedStatement 传递。 使用参数时是可选的 （尽管它强烈建议，因为它有助于防止 SQL 注入），将值发送到非加密列时，它是必要条件面向加密的列的值。 如果在加密列中插入的值作为查询语句中嵌入的文本传递，查询将失败，因为 Microsoft JDBC Driver for SQL Server 将不能确定目标加密列中的值，因此它不会加密的值。 因此，服务器会因为与加密列不兼容而拒绝它们。
- 程序打印的所有值都将以纯文本形式，如 Microsoft JDBC Driver for SQL Server 将以透明方式解密从加密列检索的数据。
- 如果你正在查找使用其中子句，WHERE 子句中使用的值需要作为参数进行传递，以便 Microsoft JDBC Driver for SQL Server 可以以透明方式对其进行加密发送到数据库之前。 在下面的示例中，请注意，SSN 传递作为参数，但 LastName 传递为文本，如姓氏未加密。
- 用于面向 SSN 列的参数的 setter 方法是 setString()，映射到 char/varchar SQL Server 数据类型。 如果此参数，使用的 setter 方法已 setNString()，映射到 nchar/nvarchar，查询将失败，因为始终加密不支持从加密的 nchar/nvarchar 值转换为加密的 char/varchar 值。  

```
String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
try  
{           
     Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
     try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
     {                  
        String insertRecord="INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)";        
        try (PreparedStatement insertStatement = sourceConnection.prepareStatement(insertRecord))  
        {
            insertStatement.setString(1, "795-73-9838");  
            insertStatement.setString(2, "Catherine");   
            insertStatement.setString(3, "Abel");                   
            insertStatement.setDate(4, Date.valueOf("1996-09-10"));  
            insertStatement.executeUpdate();  
            System.out.println("1 record inserted.\n");  
        }         
     }  
}  
catch (Exception e)  
{  
    e.printStackTrace();  
}
```

### <a name="retrieving-plaintext-data-example"></a>检索纯文本数据示例

以下示例演示如何根据加密值筛选数据，以及从加密列中检索纯文本数据。 请注意以下事项：
- 用于在 WHERE 子句来筛选 SSN 列需要作为参数进行传递，以便 Microsoft JDBC Driver for SQL Server 可以以透明方式对其进行加密发送到数据库之前的值。
- 程序打印的所有值都将以纯文本形式，如 Microsoft JDBC Driver for SQL Server 将以透明方式解密从 SSN 和 BirthDate 列中检索的数据。

> [!NOTE]  
>  查询可以在列上执行相等比较（如果使用确定性加密对它们进行加密。 有关详细信息，请参阅**选择确定性或随机加密**部分[始终加密 （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)主题。  

```
String connectionString =  "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;" ;
String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;";  

try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))  
{  
    selectStatement.setString(1, "795-73-9838");  
    ResultSet rs = selectStatement.executeQuery();   
    while(rs.next()) 
    {  
    System.out.println("SSN: " +rs.getString("SSN") + 
    ", FirstName: " + rs.getString("FirstName") + 
    ", LastName:"+ rs.getString("LastName")+
     ", Date of Birth: " + rs.getString("BirthDate"));  
          }  
}
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>检索加密数据示例

如果未启用始终加密，只要查询没有面向加密列的参数，就仍然可以从加密列中检索数据。

以下示例说明如何从加密列中检索二进制加密数据。 请注意以下事项：

- 由于未在连接字符串中启用始终加密，因此，查询将以字节数组的形式返回 SSN 和 BirthDate 的加密值（程序会将值转换为字符串）。
- 如果禁用始终加密，从加密列中检索数据的查询可以有参数，但前提是所有参数均不面向加密列。 上述查询按未在数据库中加密的 LastName 进行筛选。 如果查询按 SSN 或 BirthDate 进行筛选，则将失败。

```
String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;"; 
 
try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))  
{  
    selectStatement.setString(1, "Abel");  
    ResultSet rs = selectStatement.executeQuery();   
    while(rs.next())
    {  
        System.out.println("SSN: " + rs.getString("SSN") +
         ", FirstName: " + rs.getString("FirstName") + 
        ", LastName:"+ rs.getString("LastName")+ 
        ", Date of Birth: " + rs.getString("BirthDate"));  
    } 
}  
catch (Exception e)  
{  
    e.printStackTrace();  
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免查询加密列时的常见问题

查询从 Java 应用程序和几个指导说明了如何避免它们的加密的列时，本部分介绍常见错误的类别。

### <a name="unsupported-data-type-conversion-errors"></a>不支持的数据类型转换错误

始终加密支持对加密数据类型进行若干种转换。 请参阅[始终加密 （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)有关受支持的类型转换的详细列表。 下面介绍可以执行哪些操作来避免数据类型转换错误，请确保：

- 面向加密的列的参数值，以便参数的 SQL Server 数据类型可以是完全相同将作为传递目标列或参数的 SQL Server 数据类型的转换的类型使用正确的 setter 方法到目标支持的列的类型。 请注意，新的 API 方法已添加到 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 类对应于特定的 SQL Server 数据类型的参数传递。 例如，如果未加密的列可以使用 setTimestamp() 方法将参数传递到 datetime2 或日期时间列。 但在加密列时将需要使用的具体方法表示数据库中的列的类型。 例如，使用 setTimestamp() 将值传递给加密的 datetime2 列并使用 setDateTime() 将值传递到加密的日期时间列。 请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)有关新的 Api 的完整列表。 
- 对于面向列的 decimal 和 numeric SQL Server 数据类型的参数，其精度和小数位数与为目标列配置的精度和小数位数相同。 请注意，新的 API 方法已添加到 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 类，以接受精度和小数位数以及参数/列，表示 decimal 和 numeric 数据类型的数据值。 请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)有关新/重载 Api 的完整列表。  
- 秒的小数部分精度/刻度面向列的 datetime2、 datetimeoffset 或时间 SQL Server 数据类型的参数不大于修改目标列的值的查询中的目标列。 请注意，新的 API 方法已添加到 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 类，以接受以及表示这些数据类型的参数的数据值的秒的小数部分精度/缩放。 请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)有关新/重载 Api 的完整列表。   

### <a name="errors-due-to-incorrect-connection-properties"></a>由于不正确的连接属性的错误
本部分介绍如何配置连接设置正确，若要使用始终加密数据。 由于加密的数据类型支持有限的转换，sendTimeAsDatetime 和 sendStringParametersAsUnicode 连接设置时使用加密的列需要正确配置。 请确保： 
- [sendTimeAsDatetime](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx)将数据插入加密时间列时，将连接设置设置为 false。 有关详细信息，请参阅配置如何将 java.sql.Time 值发送到服务器部分。
- [sendStringParametersAsUnicode](../../connect/jdbc/setting-the-connection-properties.md)连接设置为 true （或保留为默认值） 时将数据插入加密 char/varchar/varchar(max) 列。 有关详细信息，请参阅配置如何将字符串值发送到服务器部分。

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>由于传递纯文本而不是加密值导致的错误

面向加密列的任何值都需要在应用程序内加密。 尝试插入/修改或者按纯文本值筛选加密列将导致如下错误：


```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

为防止发生此类错误，请确保：
- 为面向加密的列 （为连接字符串或者为特定的查询） 的应用程序查询启用始终加密。
- 使用已准备的语句和参数以发送数据面向加密列。 下面的示例显示不正确筛选文本/常量对加密列 (SSN)，而不是作为参数传递文本内部的查询。 此查询会失败。

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");  
```

## <a name="working-with-column-master-key-stores"></a>使用列主密钥存储
若要对参数值进行加密或解密数据在查询结果中的，Microsoft JDBC Driver for SQL Server 需要获取为目标列配置的列加密密钥。 列加密密钥存储在数据库元数据中的加密形式。 每个列加密密钥都有一个用于加密列加密密钥的相应列主密钥。 数据库元数据不会存储列主密钥 — 它只包含含有特定列主密钥的密钥存储的相关信息，以及该密钥在密钥存储中的位置。

若要获取列加密密钥的纯文本值，Microsoft JDBC Driver for SQL Server，首先获取有关列加密密钥和其相应的列主密钥的元数据，然后它使用信息的元数据中联系密钥包含列主密钥，存储和解密加密的列加密密钥。 Microsoft JDBC Driver for SQL Server 通信密钥存储区中使用的列主密钥存储提供程序 – 这是一个类的实例派生自**SQLServerColumnEncryptionKeyStoreProvider**类。


### <a name="using-built-in-column-master-key-store-providers"></a>使用内置列主密钥存储提供程序
  
Microsoft JDBC Driver for SQL Server 附带以下内置列主密钥存储提供程序。 请注意，这些提供程序的一些特定的提供程序名称 （用来查找该提供程序），进行预注册，但有些需要其他凭据或显式注册。

| 类 | 说明 | 提供程序（查找）名称 |预先注册？|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| 用于 Azure 密钥保管库的密钥存储提供程序。| AZURE_KEY_VAULT|是|
|**SQLServerColumnEncryptionCertificateStoreProvider**| 用于 Windows 证书存储的提供程序。|MSSQL_CERTIFICATE_STORE|是
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| 用于 Java 密钥库的提供程序|MSSQL_JAVA_KEYSTORE|是|

对于预注册的密钥存储提供程序不需要进行任何应用程序代码更改，以使用这些提供程序，但请注意以下：

- 你（或你的 DBA）需要确保列主密钥元数据中配置的提供程序名称正确，并且列主密钥路径符合对于给定提供程序有效的密钥路径格式。 建议你使用诸如 SQL Server Management Studio 之类的工具来配置密钥，这类工具在发出 CREATE COLUMN MASTER KEY (Transact-SQL) 语句时会自动生成有效的提供程序名称和密钥路径。
- 需要确保应用程序可以访问密钥存储中的密钥。 这可能涉及向应用程序授予对密钥和/或密钥存储的访问权限（具体取决于密钥存储），或执行其他特定于密钥存储的配置步骤。 例如，对于使用 SQLServerColumnEncryptionJavaKeyStoreProvider 你需要提供位置和密钥存储的连接属性中的密码。 

所有这些密钥存储提供程序均下面更详细地有述。
  
### <a name="using-azure-key-vault-provider"></a>使用 Azure 密钥保管库提供程序
Azure 密钥保管库便于存储和管理用于始终加密的列主密钥（尤其是当应用程序在 Azure 中托管时）。 Microsoft JDBC Driver for SQL Server 包括内置的提供程序，SQLServerColumnEncryptionAzureKeyVaultProvider，具有 Azure 密钥保管库中存储的密钥的应用程序。 此提供程序的名称是 AZURE_KEY_VAULT。 若要使用 Azure 密钥保管库存储区提供程序，应用程序开发人员需要在 Azure 中创建保管库和密钥，并配置应用程序以访问密钥。 有关如何设置密钥保管库和创建列主密钥的详细信息请参阅[Azure 密钥保管库 – 有关详细信息设置密钥保管库 Step by Step](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)和[Azure 密钥保管库中创建列主密匙](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2).  
  
若要使用 Azure 密钥保管库，客户端应用程序需要实例化 SQLServerColumnEncryptionAzureKeyVaultProvider 并将其注册到该驱动程序。

此处是初始化 SQLServerColumnEncryptionAzureKeyVaultProvider 的一个示例：  
  
```  
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey); 
```

应用程序创建的 SQLServerColumnEncryptionAzureKeyVaultProvider 实例后，应用程序需要注册 Microsoft JDBC Driver 内 SQL Server 使用的实例SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 方法。 强烈建议，使用默认查找名称，AZURE_KEY_VAULT，可以通过调用 SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API 来获取注册实例。 使用默认名称，将允许你使用设置的工具，如 SQL Server Management Studio 或 PowerShell，和管理始终加密密钥 （用于工具的默认名称生成列主密钥的元数据对象）。 以下示例显示了正在注册 Azure 密钥保管库提供程序。 SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 方法的更多详细信息，请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。 

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();   
keyStoreMap.put(akvProvider.getName(), akvProvider);   
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);   
```
  
> [!IMPORTANT]  
>  JDBC 驱动程序的 Azure 密钥保管库实现这些库 （GitHub) 上具有依赖关系：  
>   
>  [azure sdk 的 java](https://github.com/Azure/azure-sdk-for-java)  
>   
>  [azure activedirectory-库-为-java 库](https://github.com/AzureAD/azure-activedirectory-library-for-java)  
  
### <a name="using-windows-certificate-store-provider"></a>使用 Windows 证书存储区提供程序
SQLServerColumnEncryptionCertificateStoreProvider 可以用于在 Windows 证书存储中存储列主密钥。 使用 SQL Server Management Studio (SSMS) 始终加密向导或其他支持的工具的列主密钥和列加密密钥定义在数据库中创建。 相同的向导可以用于在将 Windows 证书存储中生成自签名的证书用作列主密钥的始终加密的数据。 有关详细信息列主密钥和列加密密钥的 T-SQL 语法访问[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)和[CREATE COLUMN ENCRPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)分别。

SQLServerColumnEncryptionCertificateStoreProvider 名称是"MSSQL_CERTIFICATE_STORE"，并且可通过提供程序对象 getName() API 查询。 它自动注册由驱动程序，并可无缝而无需任何应用程序更改。

> [!IMPORTANT]  
>  JDBC 驱动程序 SQLServerColumnEncryptionCertificateStoreProvider 实现是适用于 Windows 操作系统仅且具有可用的驱动程序包中 sqljdbc_auth.dll 的依赖关系。  若要使用此提供程序，请将 sqljdbc_auth.dll 文件复制到装有 JDBC 驱动程序的计算机上的 Windows 系统路径上的目录。 也可以设置 java.libary.path 系统属性以指定 sqljdbc_auth.dll 的目录。 如果您运行 32 位的 Java 虚拟机 (JVM)，则使用 x86 文件夹中的 sqljdbc_auth.dll 文件，即使操作系统是 x64 版本也不例外。 如果您在 x64 处理器上运行 64 位 JVM，则使用 x64 文件夹中的 sqljdbc_auth.dll 文件。 例如，如果你使用的 32 位 JVM 和 JDBC 驱动程序安装在默认目录，你可以通过使用以下虚拟机 (VM) 参数启动 Java 应用程序时指定的 DLL 的位置：  
`-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`
        
### <a name="using-java-key-store-provider"></a>使用 Java 密钥存储提供程序  
JDBC 驱动程序附带的内置密钥存储 Java 密钥存储提供程序实现。 该驱动程序自动实例化和寄存器的 Java 密钥存储提供程序，如果**keyStoreAuthentication**连接字符串属性在连接字符串中存在，并且设置为"JavaKeyStorePassword"（请参阅详见下文）。 Java 密钥存储提供程序的名称是 MSSQL_JAVA_KEYSTORE。 此名称还可通过 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() API 查询。 

进行了三个新的连接字符串关键字以允许客户端应用程序，以声明方式指定该驱动程序必须向 Java 密钥存储进行身份验证的凭据。 该驱动程序将初始化提供程序，根据特定连接的连接字符串，以下三个属性的值。 
  
 **keyStoreAuthentication:**标识要使用的密钥存储区。 SQL Server 的 Microsoft JDBC Driver 6.0，你可以进行身份验证到 Java 密钥存储只能通过此属性。 对于 Java 密钥存储，此属性的值必须是"JavaKeyStorePassword"。   
  
 **keyStoreLocation:**存储列主密钥的 Java 密钥库文件的路径。 请注意，路径包含的密钥存储区文件名。  
  
 **keyStoreSecret:**机密/密码用于 keystore 以及与该密钥。 请注意，对于使用 Java 密钥存储密钥库和密钥的密码必须相同。  

此处提供的连接字符串中的这些凭据是一个示例：

    String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
    
这些设置也可以设置/获取使用 SQLServerDataSource 对象。 请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)有关详细信息。     
  
JDBC 驱动程序自动实例化 SQLServerColumnEncryptionJavaKeyStoreProvider 连接属性中存在这些凭据时。 
  
### <a name="creating-a-column-master-key-for-the-java-key-store"></a>创建 Java 密钥存储列主密钥
SQLServerColumnEncryptionJavaKeyStoreProvider 可以用于 JKS 或 PKCS12 keystore 类型。 若要创建或导入要与此提供程序使用的密钥使用 Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html)实用程序。 请注意，该密钥必须具有的 keystore 本身的相同密码。 下面是举例说明如何创建一个公钥和使用 keytool 实用工具及其关联的私钥。

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks    

此命令创建一个公钥，并将其包装的自签名证书，然后存储在密钥存储区 keystore.jks 以及它的关联的私钥 X.509 中。 在密钥存储区的此项都由别名 AlwaysEncryptedKey 标识。 

下面是同一个使用 PKCS12 storetype 的示例。 

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword   

请注意，如果密钥库的键入 PKCS12 keytool 实用工具不提示输入密码和密钥的密码，然后需要随附-keypass 选项，因为 SQLServerColumnEncryptionJavaKeyStoreProvider 需要具有密钥库和密钥相同的密码。

你还可以从 Windows 证书存储以.pfx 格式导出证书，然后，使用 SQLServerColumnEncryptionJavaKeyStoreProvider。 导出的证书可以还将导入 Java 密钥存储为 JKS keystore 类型。 

创建 keytool 条目后你将需要在需要密钥存储提供程序名称和密钥路径的数据库中创建列主密钥元数据。 有关如何创建列主密钥元数据的详细信息，请访问[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)。 对于 SQLServerColumnEncryptionJavaKeyStoreProvider，注册表项路径是只需密钥的别名。 并且 SQLServerColumnEncryptionJavaKeyStoreProvider 名称为 MSSQL_JAVA_KEYSTORE。 你还可以查询使用 getName() 公共 API SQLServerColumnEncryptionJavaKeyStoreProvider 类的此名称。 

用于创建列主密钥的 T-SQL 语法是：

```  
CREATE COLUMN MASTER KEY [<CMK_name>]  
WITH  
(  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',  
    KEY_PATH = N'<key_alias>'  
)  
```  

对于 AlwaysEncryptedKey 上述步骤中创建，将为列主密钥定义：

```  
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```  
    
> [!NOTE]  
>  内置在 SQL Server management Studio 功能无法创建列主密钥定义，则为 Java 密钥存储，你必须为其使用 T-SQL 命令。  
  
### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>创建 Java 密钥存储区的列加密密钥
请注意，SQL Server management Studio 或任何其他工具可以不用于创建使用 Java 密钥存储中的列主密钥的加密密钥的列。 客户端应用程序必须创建使用 SQLServerColumnEncryptionJavaKeyStoreProvider 类以编程方式的列加密密钥。 有关详细信息，请访问节使用列主密钥存储提供程序进行编程密钥预配。 

  
### <a name="implementing-a-custom-column-master-key-store-provider"></a>实现自定义列主密钥存储提供程序
如果你想要在现有提供程序不支持的密钥存储中存储列主密钥，则可以通过扩展 SQLServerColumnEncryptionKeyStoreProvider 类并注册使用的提供程序实现自定义提供程序SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 方法。
  
```  
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";
    
    public void setName(String name)
    {
        this.name = name;
    }
    
    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)  
    {  
        // Logic for encrypting the column encryption key  
    }  
    
    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)  
    {  
        // Logic for decrypting the column encryption key  
    }  
}  
  
```  
  
 注册提供程序：  
  
```  
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();  
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();  
keyStoreMap.put(storeProvider.getName(), storeProvider);  
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);  
  
```  
  
## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>使用列主密钥存储提供程序进行编程密钥预配

在访问加密的列时，Microsoft JDBC Driver for SQL Server 将以透明方式查找，并调用正确的列主密钥存储提供程序来解密列加密密钥。 通常情况下，普通的应用程序代码不会直接调用列主密钥存储提供程序。 不过，你可以显式实例化并调用一个提供程序，以编程方式预配和管理始终加密密钥：以便生成加密列加密密钥以及对列加密密钥解密（例如，在列主密钥轮替过程中）。 有关详细信息，请参阅 [Always Encrypted 密钥管理概述](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。
请注意，仅当使用自定义密钥存储提供程序时，才有可能需要实现你自己的密钥管理工具。 使用密钥存储在 Windows 证书存储或 Azure 密钥保管库中时，你可以使用现有工具，如 SQL Server Management Studio 或 PowerShell，管理和预配密钥。 使用 Java 密钥存储中存储的密钥时，你需要以编程方式预配密钥。 下面的示例，演示如何使用 SQLServerColumnEncryptionJavaKeyStoreProvider 类与 Java 密钥存储中存储的密钥的密钥进行加密。

```  
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programatically for the Java Key Store.
 */
public class AlwaysEncrypted
{
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<proide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore. 
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of
     * the column encryption key. The algorithm for the system providers must be RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args)
    {
        String connectionString = GetConnectionString();
        try
        {
            // Note: if you are not using try-with-resources statements (as here),
            // you must remember to call close() on any Connection, Statement,
            // ResultSet objects that you create.

            // Open a connection to the database.
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))
            {
                // Instantiate the Java Key Store provider.
                SQLServerColumnEncryptionKeyStoreProvider storeProvider = 
                        new SQLServerColumnEncryptionJavaKeyStoreProvider(
                                keyStoreLocation,
                                keyStoreSecret);

                byte [] encryptedCEK=getEncryptedCEK(storeProvider);

                /**
                 * Create column encryption key 
                 * For more details on the syntax refer: 
                 * https://msdn.microsoft.com/library/mt146372.aspx
                 * Encrypted column encryption key first needs to be converted into varbinary_literal from bytes, 
                 * for which DatatypeConverter.printHexBinary is used
                 */
                String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY " 
                        + columnEncryptionKey
                        + " WITH VALUES ( "
                        + " COLUMN_MASTER_KEY = " 
                        + columnMasterKeyName
                        + " , ALGORITHM =  '" 
                        + algorithm
                        + "' , ENCRYPTED_VALUE =  0x" 
                        + DatatypeConverter.printHexBinary(encryptedCEK)
                        + " ) ";

                try (Statement cekStatement = sourceConnection.createStatement())
                {
                    cekStatement.executeUpdate(createCEKSQL);
                    System.out.println("Column encryption key created with name : " + columnEncryptionKey);
                }
            }
        }
        catch (Exception e)
        {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    // To avoid storing the sourceConnection String in your code,
    // you can retrieve it from a configuration file.
    private static String GetConnectionString()
    {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +
                "databaseName=ae2;user=sa;password=********;";

        return connectionUrl;
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException
    {
        /**
         * Following arguments needed by  SQLServerColumnEncryptionJavaKeyStoreProvider
         * 1) keyStoreLocation : 
         *      Path where keystore is located, including the keystore file name. 
         * 2) keyStoreSecret : 
         *      Password of the keystore and the key.  
         */
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(
                keyAlias,
                algorithm,
                plainCEK);

        return encryptedCEK;
    }
}

```  
  
## <a name="force-encryption-on-input-parameters"></a>在输入参数上强制加密
  
使用始终加密时，强行加密功能强制实施参数加密。 如果使用强制加密，并且 SQL Server 通知驱动程序参数不需要进行加密，使用参数则查询将失败。 此属性提供针对安全攻击的额外保护，这些攻击涉及受损 SQL Server 向客户端提供不正确的加密元数据，这可能会导致数据泄漏。 SQLServerPreparedStatement 和 SQLServerCallableStatement 类和更新中的组 * 方法\*SQLServerResultSet 类中的方法重载以接受布尔参数来指定强制加密设置。 如果此参数的值为 false，该驱动程序不会强制对参数加密。 如果强制加密设置为 true，查询参数也只发送如果目标列已加密，并且针对连接还是的语句上启用始终加密。 这样一层额外的安全，确保不发送任何数据是错误地到 SQL Server 以纯文本形式时这预计可以进行加密。  
  
 使用强制的加密设置都重载方法的 SQLServerPreparedStatement 和 SQLServerCallableStatement 方法详细信息，请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-performance-impact-of-always-encrypted"></a>控制始终加密对性能的影响

始终加密是一种客户端加密技术，因此，大部分性能开销发生在客户端，而不是数据库中。 除加密和解密操作的成本之外，客户端上的其他性能开销来源包括：
- 额外往返数据库以检索查询参数的元数据。
- 调用列主密钥存储以访问列主密钥。

本部分介绍在 Microsoft JDBC Driver for SQL Server 和可以如何控制上述两个因素对性能的影响的内置性能优化。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制为了检索查询参数的元数据而往返的次数

如果启用始终加密对于连接，默认情况下，将调用 Microsoft JDBC Driver for SQL Server [sys.sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396)每个参数化查询，将传递 （不带任何查询语句参数值） 到 SQL Server。 [sys.sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396)分析查询语句，以找出，如果任何参数需要加密，并因此，对于每个此类，它返回将允许 Microsoft JDBC Driver for SQL Server 的与加密相关的信息若要对参数值加密。 以上行为可确保实现针对客户端应用程序的高级别透明性。 应用程序 （和应用程序开发人员） 不会不需要，只要面向加密的列的值 Microsoft JDBC Driver for SQL Server 作为参数传递到需要注意的哪些查询在访问加密的列。


#### <a name="setting-always-encrypted-at-the-query-level"></a>在查询级别设置始终加密

若要控制检索参数化查询的加密元数据时对性能的影响，可以为单个查询启用始终加密，而不是为连接设置始终加密。 这样一来，就可以确保仅针对你知道具有面向加密列的参数的查询调用 sys.sp_describe_parameter_encryption。 但请注意，这样做会降低加密的透明度：如果更改数据库列的加密属性，可能需要更改应用程序代码，使其与架构更改保持一致。


若要控制单个查询的始终加密行为，你需要配置单独的语句对象通过传递枚举，SQLServerStatementColumnEncryptionSetting，指定将如何发送和接收时读取和写入数据适用于该特定语句的加密的列。 下面是一些有用的指导原则：
- 如果客户端应用程序通过数据库连接发送的大多数查询访问的是加密列，则可执行以下操作：
    - 将 columnEncryptionSetting 连接字符串关键字设置为已启用。
    - 设置 SQLServerStatementColumnEncryptionSetting.Disabled 不访问任何加密的列的单个查询。 这将禁止调用 sys.sp_describe_parameter_encryption，同时禁止尝试对结果集中的任何值解密。
    - 设置 SQLServerStatementColumnEncryptionSetting.ResultSet 的单个查询，没有任何参数需要加密但会从加密列检索数据。 这将禁止调用 sys.sp_describe_parameter_encryption 和参数加密。 查询将能够解密来自加密列的结果。
- 如果客户端应用程序通过数据库连接发送的大多数查询不访问加密列，则可执行以下操作：
    - ColumnEncryptionSetting 连接字符串关键字设置为禁用。
    - 设置 SQLServerStatementColumnEncryptionSetting.Enabled 的单个查询，具有需要加密任何参数。 这将允许调用 sys.sp_describe_parameter_encryption，同时允许对从加密列中检索到的任何查询结果解密。
    - 没有任何参数需要进行加密，但从加密列检索数据的查询，设置 SQLServerStatementColumnEncryptionSetting.ResultSet。 这将禁止调用 sys.sp_describe_parameter_encryption 和参数加密。 查询将能够解密来自加密列的结果。

请注意，SQLServerStatementColumnEncryptionSetting 设置不能用于绕过加密以及获取纯文本数据的访问权限。 有关如何在一个语句上配置列加密的详细信息，请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。  

在以下示例中，将对数据库连接禁用始终加密。 应用程序发出的查询有一个面向未加密的 LastName 列的参数。 该查询从已加密的 SSN 和 BirthDate 列中检索数据。 在这种情况下，不需要调用 sys.sp_describe_parameter_encryption 来检索加密元数据。 但是，需要启用查询结果解密，以便应用程序从两个加密列接收纯文本值。 SQLServerStatementColumnEncryptionSetting.ResultSet 设置用于确保。

```
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://localhost;databaseName=ae;user=sa;password=******;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=" + keyStoreLocation + ";"
        + "keyStoreSecret=******;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);

String filterRecord="SELECT FirstName, LastName, SSN, BirthDate FROM " + tblName + " WHERE LastName = ?";  
PreparedStatement selectStatement = connection.prepareStatement(
        filterRecord, 
        ResultSet.TYPE_FORWARD_ONLY, 
        ResultSet.CONCUR_READ_ONLY, 
        connection.getHoldability(), 
        SQLServerStatementColumnEncryptionSetting.ResultSetOnly);
selectStatement.setString(1, "Abel");  
ResultSet rs = selectStatement.executeQuery();  
while(rs.next()) {  
    System.out.println("First name: " + rs.getString("FirstName"));  
    System.out.println("Last name: " + rs.getString("LastName"));  
    System.out.println("SSN: " + rs.getString("SSN"));  
    System.out.println("Date of Birth: " + rs.getDate("BirthDate"));  
}  
rs.close();
selectStatement.close();
connection.close();
```


### <a name="column-encryption-key-caching"></a>列加密密钥缓存

若要减少的列主密钥存储的调用，以解密列加密密钥数，Microsoft JDBC Driver for SQL Server 将缓存在内存中的纯文本列加密密钥。 从数据库元数据收到加密列的加密密钥值之后，驱动程序首先会尝试查找与加密密钥值对应的纯文本列加密密钥。 仅当在缓存中找不到加密列的加密密钥值时，驱动程序才会调用包含列主密钥的密钥存储。

你可以在 SQLServerConnection 类中使用的 API，setColumnEncryptionKeyCacheTtl()，缓存中配置列加密密钥条目的生存时间值。 在缓存中的列加密密钥条目的默认生存时间值是 2 小时。 若要关闭缓存使用值为 0。 若要设置任何生存时间值使用以下 API:
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
   
例如，若要设置 10 分钟的生存时间值，使用
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)

请注意，作为时间单位支持仅天、 小时、 分钟和秒。  


## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>使用 SQLServerBulkCopy 复制加密数据

使用 SQLServerBulkCopy，你可以将复制数据，这已加密，并存储在一个表中，到另一个表，而无需解密数据。 为此：

- 请确保目标表的加密配置与源表的配置完全相同。 特别是，两个表必须对相同的列加密，并且必须使用相同的加密类型和相同的加密密钥对列加密。 注意：如果任何目标列的加密方式与其相应的源列不同，你都不能在复制操作完成后对目标表中的数据进行解密。 数据将损坏。
- 配置数据库到源表和目标表的连接，而不启用始终加密。 
- 设置 allowEncryptedValueModifications 选项。 请参阅[使用 JDBC 驱动程序使用大容量复制](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)有关详细信息。
 
注意： 这可能会导致损坏数据库，因为 Microsoft JDBC Driver for SQL Server 不会检查数据确实已加密，是否正确加密使用相同的加密指定 AllowEncryptedValueModifications 时要格外小心类型、 算法和密钥与目标列。

## <a name="see-also"></a>另请参阅  
 [始终加密（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  

