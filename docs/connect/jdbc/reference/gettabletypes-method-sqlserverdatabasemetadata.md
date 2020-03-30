---
title: getTableTypes 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTableTypes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0f5dc57-07b8-4811-ab1a-80a524bfdb42
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8da791a53d6ee25dd56f7f015ccc69947999f3b9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979155"
---
# <a name="gettabletypes-method-sqlserverdatabasemetadata"></a>getTableTypes 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索当前数据库中可用的表类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getTableTypes()  
```  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getTableTypes 方法是由 java.sql.DatabaseMetaData 接口中的 getTableTypes 方法指定的。  
  
 由 getTableTypes 方法返回的结果集将包含以下信息：  
  
|名称|类型|说明|  
|----------|----------|-----------------|  
|TABLE_TYPE|**字符串**|表类型。|  
  
> [!NOTE]  
>  有关 getTableTypes 方法返回的数据的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“sp_tables (Transact-SQL)”。  
  
## <a name="example"></a>示例  
 以下示例演示了已在连接字符串中指定了数据库的情况下如何使用 getTableTypes 方法返回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库中的表类型信息。  
  
```  
public static void executeGetTableTypes(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTableTypes();  
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
  
  
