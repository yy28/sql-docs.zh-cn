---
title: "getCatalogs 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getCatalogs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f8bd0f1-f340-4bb9-b559-0a6176124033
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f78577e4f2698966afccba5f1f97855076434e9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getcatalogs-method-sqlserverdatabasemetadata"></a>getCatalogs 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索在连接的服务器中可用的目录名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getCatalogs()  
```  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getCatalogs 方法指定此 getCatalogs 方法。  
  
> [!NOTE]  
>  在 SQL Azure 上，你应连接到 master 数据库才能调用**SQLServerDatabaseMetaData.getCatalogs**。 SQL Azure 不支持从用户数据库中返回整个集的目录。 **SQLServerDatabaseMetaData.getCatalogs**使用 sys.databases 视图来获取目录。 中的权限的讨论，请参阅[sys.databases （SQL Azure 数据库）](http://go.microsoft.com/fwlink/?LinkId=217396)了解**SQLServerDatabaseMetaData.getCatalogs** SQL Azure 上的行为。  
  
 GetCatalogs 方法所返回的结果集将包含以下信息：  
  
|Name|类型|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**字符串**|目录，其中包括系统数据库的名称[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。|  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 getCatalogs 方法返回的名称中包含的所有数据库[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，包括系统数据库。  
  
```  
public static void executeGetCatalogs(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCatalogs();  
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
  
  

