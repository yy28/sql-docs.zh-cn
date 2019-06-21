---
title: getTablePrivileges 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 26c1630042b4f33230f37ec979de7bfa643b283b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802611"
---
# <a name="gettableprivileges-method-sqlserverdatabasemetadata"></a>getTablePrivileges 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索可用于给定目录、架构或表名称模式的各表的访问权限的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getTablePrivileges(java.lang.String catalog,  
                                             java.lang.String schema,  
                                             java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parameters  
 *catalog*  
  
 一个包含目录名称的字符串  。 对此参数提供 Null 值指示无需使用目录名称。  
  
 *schema*  
  
 一个包含架构名称模式的字符串  。 对此参数提供 Null 值指示无需使用架构名称。  
  
 *table*  
  
 一个包含表名称模式的字符串  。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getTablePrivileges 方法是由 java.sql.DatabaseMetaData 接口中的 getTablePrivileges 方法指定的。  
  
 由 getTablePrivileges 方法返回的结果集将包含以下信息：  
  
|“属性”|类型|描述|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|目录名称。|  
|TABLE_SCHEM|**String**|表架构名称。|  
|TABLE_NAME|**String**|表名称。|  
|GRANTOR|**String**|授予访问权限的对象。|  
|GRANTEE|**String**|获得访问权限的对象。|  
|PRIVILEGE|**String**|授予的访问权限的类型。|  
|IS_GRANTABLE|**String**|指示是否允许被授权者向其他用户授予权限。|  
  
> [!NOTE]  
>  有关 getTablePrivileges 方法返回的数据的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“sp_table_privileges (Transact-SQL)”。  
  
## <a name="example"></a>示例  
 以下示例演示了如何使用 getTablePrivileges 方法返回针对 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库中 Person.Contact 表的访问权限。  
  
```  
public static void executeGetTablePrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTablePrivileges("AdventureWorks", "Person", "Contact");  
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
  
  
