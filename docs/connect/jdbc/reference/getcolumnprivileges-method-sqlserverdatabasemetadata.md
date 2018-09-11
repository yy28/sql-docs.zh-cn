---
title: getColumnPrivileges 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getColumnPrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ab6a671-9573-4b95-8c23-364306c60d25
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16c0b0314d4e0e3b2b28e81c118ef0533ba55768
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784345"
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
 *catalog*  
  
 一个包含目录名称的字符串。  
  
 *schema*  
  
 一个包含架构名称的字符串。  
  
 *table*  
  
 一个包含表名称的字符串。  
  
 *col*  
  
 一个包含列名称模式的字符串。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getColumnPrivileges 方法由 java.sql.DatabaseMetaData 接口中的 getColumnPrivileges 方法指定。  
  
 GetColumnPrivileges 方法返回的结果集将包含以下信息：  
  
|“属性”|类型|描述|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|目录名称。|  
|TABLE_SCHEM|**String**|表架构名称。|  
|TABLE_NAME|**String**|表名称。|  
|COLUMN_NAME|**String**|列名称。|  
|GRANTOR|**String**|授予访问权限的对象。|  
|GRANTEE|**String**|获得访问权限的对象。|  
|PRIVILEGE|**String**|授予的访问权限的类型。|  
|IS_GRANTABLE|**String**|指示是否允许被授权者向其他用户授予权限。|  
  
> [!NOTE]  
>  有关 getColumnPrivileges 方法返回的数据的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“sp_column_privileges (Transact-SQL)”。  
  
## <a name="example"></a>示例  
 以下示例演示了如何使用 getColumnPrivileges 方法返回对 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库中 Person.Contact 表中的 FirstName 列的访问权限。  
  
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
  
  
