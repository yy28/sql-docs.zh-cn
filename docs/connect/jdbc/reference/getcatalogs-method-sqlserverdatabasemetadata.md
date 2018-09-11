---
title: getCatalogs 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
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
- SQLServerDatabaseMetaData.getCatalogs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f8bd0f1-f340-4bb9-b559-0a6176124033
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84f5f8668dea2b06a6390235be315ee25a27ba80
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785060"
---
# <a name="getcatalogs-method-sqlserverdatabasemetadata"></a>getCatalogs 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索在连接的服务器中可用的目录名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getCatalogs()  
```  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getCatalogs 方法由 java.sql.DatabaseMetaData 接口中的 getCatalogs 方法指定。  
  
> [!NOTE]  
>  在 SQL Azure，则应连接到 master 数据库以调用**SQLServerDatabaseMetaData.getCatalogs**。 SQL Azure 不支持从用户数据库中返回整个目录集。 **SQLServerDatabaseMetaData.getCatalogs**使用 sys.databases 视图获取目录。 中的权限的讨论，请参阅[sys.databases （SQL Azure 数据库）](http://go.microsoft.com/fwlink/?LinkId=217396)若要了解**SQLServerDatabaseMetaData.getCatalogs** SQL Azure 上的行为。  
  
 由 getCatalogs 方法返回的结果集将包含以下信息：  
  
|“属性”|类型|描述|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|目录名称，包括 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的系统数据库。|  
  
## <a name="example"></a>示例  
 以下示例演示了如何使用 getCatalogs 方法返回 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中包含的所有数据库（包括系统数据库）的名称。  
  
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
  
  
