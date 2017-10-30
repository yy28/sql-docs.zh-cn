---
title: "getColumnPrivileges 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
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
- SQLServerDatabaseMetaData.getColumnPrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ab6a671-9573-4b95-8c23-364306c60d25
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1db7a72e555114711151e82281a4890f34d75fe6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getcolumnprivileges-method-sqlserverdatabasemetadata"></a>getColumnPrivileges 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索关于表中各列的访问权限的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getColumnPrivileges(java.lang.String catalog,  
                                              java.lang.String schema,  
                                              java.lang.String table,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parameters  
 *目录*  
  
 A**字符串**，其中包含目录名称。  
  
 *架构*  
  
 A**字符串**包含架构的名称。  
  
 *table*  
  
 A**字符串**包含表的名称。  
  
 *列*  
  
 A**字符串**，其中包含的列名称模式。  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getColumnPrivileges 方法指定此 getColumnPrivileges 方法。  
  
 GetColumnPrivileges 方法所返回的结果集将包含以下信息：  
  
|Name|类型|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**字符串**|目录名称。|  
|TABLE_SCHEM|**字符串**|表架构名称。|  
|TABLE_NAME|**字符串**|表名称。|  
|COLUMN_NAME|**字符串**|列名称。|  
|GRANTOR|**字符串**|授予访问权限的对象。|  
|GRANTEE|**字符串**|获得访问权限的对象。|  
|PRIVILEGE|**字符串**|授予的访问权限的类型。|  
|IS_GRANTABLE|**字符串**|指示是否允许被授权者向其他用户授予权限。|  
  
> [!NOTE]  
>  有关 getColumnPrivileges 方法返回的数据的详细信息，请参阅"sp_column_privileges (TRANSACT-SQL)"中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 getColumnPrivileges 方法中的 Person.Contact 表中返回的名字列的访问权限[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。  
  
```  
public static void executeGetColumnPrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getColumnPrivileges("AdventureWorks", "Person", "Contact", "FirstName");  
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
  
  

