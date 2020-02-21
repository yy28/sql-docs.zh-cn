---
title: getColumns 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f173fa5d-e114-4a37-a5c4-2baad9ff3af1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d34f5748a5a85d67754ea9a001ba1819935e53a6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67952830"
---
# <a name="getcolumns-method-sqlserverdatabasemetadata"></a>getColumns 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定目录中可用的表列的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getColumns(java.lang.String catalog,  
                                     java.lang.String schema,  
                                     java.lang.String table,  
                                     java.lang.String col)  
```  
  
#### <a name="parameters"></a>parameters  
 *catalog*  
  
 一个包含目录名称的字符串  。  
  
 *schema*  
  
 一个包含架构名称模式的字符串  。  
  
 *table*  
  
 一个包含表名称模式的字符串  。  
  
 *col*  
  
 一个包含列名称模式的字符串  。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getColumns 方法是由 java.sql.DatabaseMetaData 接口中的 getColumns 方法指定的。  
  
 由 getColumns 方法返回的结果集将包含以下信息：  
  
|名称|类型|说明|  
|----------|----------|-----------------|  
|TABLE_CAT|**字符串**|目录名称。|  
|TABLE_SCHEM|**字符串**|表架构名称。|  
|TABLE_NAME|**字符串**|表名称。|  
|COLUMN_NAME|**字符串**|列名称。|  
|DATA_TYPE|**smallint**|来自 java.sql.Types 的 SQL 数据类型。|  
|TYPE_NAME|**字符串**|数据类型的名称。|  
|COLUMN_SIZE|**int**|列的精度。|  
|BUFFER_LENGTH|**smallint**|数据的传输大小。|  
|DECIMAL_DIGITS|**smallint**|列的小数位数。|  
|NUM_PREC_RADIX|**smallint**|列的基数。|  
|NULLABLE|**smallint**|指示列是否可以为 Null。 可以为下列值之一：<br /><br /> columnNoNulls (0)<br /><br /> columnNullable (1)|  
|REMARKS|**字符串**|与列关联的注释。<br /><br /> **注意：** 对于此列，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 始终会返回 null。|  
|COLUMN_DEF|**字符串**|列的默认值。|  
|SQL_DATA_TYPE|**smallint**|SQL 数据类型在描述符的 TYPE 字段中显示的值。 该列与 DATA_TYPE 列相同，datetime 和 SQL-92 interval 数据类型除外。 该列始终返回值。|  
|SQL_DATETIME_SUB|**smallint**|datetime 及 SQL-92 interval 数据类型的子类型代码。 对于其他数据类型，该列返回 NULL。|  
|CHAR_OCTET_LENGTH|**int**|列中的最大字节数。|  
|ORDINAL_POSITION|**int**|列在表中的索引。|  
|IS_NULLABLE|**字符串**|指示列是否允许 Null 值。|  
|SS_IS_SPARSE|**smallint**|如果此列是稀疏列，它将具有值 1；否则为 0。<sup>1</sup>|  
|SS_IS_COLUMN_SET|**smallint**|如果该列是稀疏 column_set 列，它将具有值 1；否则为 0。 <sup>1</sup>|  
|SS_IS_COMPUTED|**smallint**|指示 TABLE_TYPE 中的列是否为计算所得的列。 <sup>1</sup>|  
|IS_AUTOINCREMENT|**字符串**|如果列是自动递增的，则为“是”。 如果列不是自动递增的，则为“否”。 如果驱动程序无法确定列是否为自动递增，则为 ""（空字符串）。 <sup>1</sup>|  
|SS_UDT_CATALOG_NAME|**字符串**|包含用户定义类型 (UDT) 的目录名称。 <sup>1</sup>|  
|SS_UDT_SCHEMA_NAME|**字符串**|包含用户定义类型 (UDT) 的架构名称。 <sup>1</sup>|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**字符串**|采用完全限定名称的用户定义类型 (UDT)。 <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**字符串**|在其中定义 XML 架构集合名称的目录的名称。 如果找不到目录名称，此变量则会包含一个空字符串。 <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**字符串**|在其中定义 XML 架构集合名称的架构的名称。 如果找不到架构名称，则为空字符串。 <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_NAME|**字符串**|XML 架构集合的名称。 如果找不到名称，则为空字符串。 <sup>1</sup>|  
|SS_DATA_TYPE|**tinyint**|扩展存储过程使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型。<br /><br /> **注意：** 有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 返回的数据类型的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“数据类型 (Transact-SQL)”。|  
  
 (1) 如果正连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，此列将不会出现。  
  
> [!NOTE]  
>  有关 getColumns 方法返回的数据的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“sp_columns (Transact-SQL)”。  
  
 在 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中，你将看到有别于以往 JDBC 驱动程序版本的以下行为更改：  
  
 DATA_TYPE 列具有以下更改：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型|JDBC Driver 2.0 中的返回类型（或者，如果连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]）和关联的数值常量|连接到 [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] 或更高版本时 JDBC Driver 3.0 中的返回类型|  
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|  
|大于 8 kB 的用户定义类型|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geography|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geometry|LONGVARBINARY (-4)|VARBINARY (-3)|  
|varbinary(max)|LONGVARBINARY (-4)|VARBINARY (-3)|  
|nvarchar(max)|LONGVARCHAR (-1) 或 LONGNVARCHAR (JDBC 4) (-16)|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|  
|varchar(max)|LONGVARCHAR (-1)|VARCHAR (12)|  
|time|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|TIME (-154)|  
|date|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|DATE (91)|  
|datetime2|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|TIMESTAMP (93)|  
|datetimeoffset|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|microsoft.sql.Types.DATETIMEOFFSET  (-155)|  
  
 COLUMN_SIZE 列具有以下更改：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型|返回 JDBC Driver 2.0 中的类型|返回 JDBC Driver 3.0 中的类型|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|nvarchar(max)|1073741823|2147483647（数据库元数据）|  
|xml|1073741823|2147483647（数据库元数据）|  
|小于或等于 8 kB 的用户定义类型|8 kB（结果集和参数元数据）|存储过程返回的实际大小。|  
|time||类型的字符串表示形式的字符长度，假定精度允许的最大值为秒的小数形式。|  
|date||与 time 相同|  
|datetime2||与 time 相同|  
|datetimeoffset||与 time 相同|  
  
 BUFFER_LENGTH 列具有以下更改：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型|返回 JDBC Driver 2.0 中的类型|返回 JDBC Driver 3.0 中的类型|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|大于 8 kB 的用户定义类型||2147483647|  
  
 TYPE_NAME 列具有以下更改：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型|返回 JDBC Driver 2.0 中的类型|返回 JDBC Driver 3.0 中的类型|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|varchar(max)|text|varchar|  
|varbinary(max)|image|varbinary|  
  
 DECIMAL_DIGITS 列具有以下更改：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 类型|JDBC Driver 2.0|JDBC Driver 3.0|  
|--------------------------------------------------------------|---------------------|---------------------|  
|time|Null|7（或指定的较小值）|  
|date|Null|Null|  
|datetime2|Null|7（或指定的较小值）|  
|datetimeoffset|Null|7（或指定的较小值）|  
  
 SQL_DATA_TYPE 列具有以下更改：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型|JDBC Driver 2.0 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 数据值|JDBC Driver 3.0 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 数据值|  
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|varchar(max)|-10|-9|  
|nvarchar(max)|-1|-9|  
|xml|-10|-152|  
|小于或等于 8 kB 的用户定义类型|-3|-151|  
|大于 8 kB 的用户定义类型|在 JDBC Driver 2.0 中不可用|-151|  
|geography|-4|-151|  
|geometry|-4|-151|  
|hierarchyid|-4|-151|  
|time|-9|92|  
|date|-9|91|  
|datetime2|-9|93|  
|datetimeoffset|-9|-155|  
  
## <a name="example"></a>示例  
 以下示例演示了如何使用 getColumns 方法返回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库中的 Person.Contact 表的信息。  
  
```  
import java.sql.*;  
public class c1 {  
   public static void main(String[] args) {  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedsecurity=true";  
  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         DatabaseMetaData dbmd = con.getMetaData();  
         rs = dbmd.getColumns("AdventureWorks", "Person", "Contact", "FirstName");  
  
         ResultSet r = dbmd.getColumns(null, null, "Contact", null);  
         ResultSetMetaData rm = r.getMetaData();   
         int noofcols = rm.getColumnCount();  
  
         if (r.next())  
            for (int i = 0 ; i < noofcols ; i++ )  
            System.out.println(rm.getColumnName( i + 1 ) + ": \t\t" + r.getString( i + 1 ));  
      }  
  
      catch (Exception e) {}  
      finally {}  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
