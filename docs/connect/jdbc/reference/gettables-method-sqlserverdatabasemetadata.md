---
title: getTables 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8dfd7f14d6006f5a41a7cd2a9b0cae4933804fe
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979210"
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
  
#### <a name="parameters"></a>parameters  
 *catalog*  
  
 一个包含目录名称的字符串  。 对此参数提供 Null 值指示无需使用目录名称。  
  
 *schema*  
  
 一个包含架构名称模式的字符串  。 对此参数提供 Null 值指示无需使用架构名称。  
  
 *tableName*  
  
 一个包含表名称模式的字符串  。  
  
 *types*  
  
 含有要包含的表类型的字符串数组。 Null 指示应包含所有表类型。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getTables 方法是由 java.sql.DatabaseMetaData 接口中的 getTables 方法指定的。  
  
 由 getTables 方法返回的结果集将包含以下信息：  
  
|名称|类型|说明|  
|----------|----------|-----------------|  
|TABLE_CAT|**字符串**|指定的表所在的数据库的名称。|  
|TABLE_SCHEM|**字符串**|表架构名称。|  
|TABLE_NAME|**字符串**|表名称。|  
|TABLE_TYPE|**字符串**|表类型。|  
|REMARKS|**字符串**|表的说明。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不返回此列的值。|  
|TYPE_CAT|**字符串**|JDBC 驱动程序不支持此类型。|  
|TYPE_SCHEM|**字符串**|JDBC 驱动程序不支持此类型。|  
|TYPE_NAME|**字符串**|JDBC 驱动程序不支持此类型。|  
|SELF_REFERENCING_COL_NAME|**字符串**|JDBC 驱动程序不支持此类型。|  
|REF_GENERATION|**字符串**|JDBC 驱动程序不支持此类型。|  
  
> [!NOTE]  
>  有关 getTables 方法返回的数据的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“sp_tables (Transact-SQL)”。  
  
## <a name="example"></a>示例  
 以下示例演示了如何使用 getTables 方法返回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库中的 Person.Contact 表的表说明信息。  
  
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
  
  
