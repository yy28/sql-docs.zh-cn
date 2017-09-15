---
title: "getTables 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bbf35aeec7b5626b380fc654995d181fe124811
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="gettables-method-sqlserverdatabasemetadata"></a>getTables 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索可用于给定目录、架构或表名称模式的各表的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getTables(java.lang.String catalog,  
                                    java.lang.String schema,  
                                    java.lang.String table,  
                                    java.lang.String[] types)  
```  
  
#### <a name="parameters"></a>Parameters  
 *目录*  
  
 A**字符串**，其中包含目录名称。 对此参数提供 Null 值指示无需使用目录名称。  
  
 *架构*  
  
 A**字符串**，其中包含的架构名称模式。 对此参数提供 Null 值指示无需使用架构名称。  
  
 *表名*  
  
 A**字符串**，其中包含的表名称模式。  
  
 *类型*  
  
 含有要包含的表类型的字符串数组。 Null 指示应包含所有表类型。  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getTables 方法指定此 getTables 方法。  
  
 GetTables 方法所返回的结果集将包含以下信息：  
  
|Name|类型|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**字符串**|在其中指定的表所在的数据库名称。|  
|TABLE_SCHEM|**字符串**|表架构名称。|  
|TABLE_NAME|**字符串**|表名称。|  
|TABLE_TYPE|**字符串**|表类型。|  
|REMARKS|**字符串**|表的说明。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]不返回此列的值。  |  
|TYPE_CAT|**字符串**|JDBC 驱动程序不支持此类型。|  
|TYPE_SCHEM|**字符串**|JDBC 驱动程序不支持此类型。|  
|TYPE_NAME|**字符串**|JDBC 驱动程序不支持此类型。|  
|SELF_REFERENCING_COL_NAME|**字符串**|JDBC 驱动程序不支持此类型。|  
|REF_GENERATION|**字符串**|JDBC 驱动程序不支持此类型。|  
  
> [!NOTE]  
>  有关 getTables 方法返回的数据的详细信息，请参阅"sp_tables (TRANSACT-SQL)"中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 getTables 方法返回的 Person.Contact 表中的表描述信息[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。  
  
```  
public static void executeGetTables(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTables("AdventureWorks", "Person", "Contact", null);  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
