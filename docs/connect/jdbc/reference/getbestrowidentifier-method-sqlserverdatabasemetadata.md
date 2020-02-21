---
title: getBestRowIdentifier 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getBestRowIdentifier
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c19e9ca6-2a53-4a0c-91ab-80090c3f7229
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9a19bd01a8ebf54eb3e819bd4a82400b8107e382
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954026"
---
# <a name="getbestrowidentifier-method-sqlserverdatabasemetadata"></a>getBestRowIdentifier 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索表中唯一标识一行的最佳列集的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getBestRowIdentifier(java.lang.String catalog,  
                                               java.lang.String schema,  
                                               java.lang.String table,  
                                               int scope,  
                                               boolean nullable)  
```  
  
#### <a name="parameters"></a>parameters  
 *catalog*  
  
 一个包含目录名称的字符串  。  
  
 *schema*  
  
 一个包含架构名称的字符串  。  
  
 *table*  
  
 一个包含表名称的字符串  。  
  
 *作用域*  
  
 指示相关范围的 int  。 可以包括下列值：  
  
 bestRowTemporary (0)  
  
 bestRowTransaction (1)  
  
 bestRowSession (2)  
  
 *nullable*  
  
 true  可包含可为 Null 的列。 否则为 **false**。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getBestRowIdentifier 方法是由 java.sql.DatabaseMetaData 接口中的 getBestRowIdentifier 方法指定的。  
  
 由 getBestRowIdentifier 方法返回的结果集将包含以下信息：  
  
|名称|类型|说明|  
|----------|----------|-----------------|  
|SCOPE|short|返回结果的范围。 可以为下列值之一：<br /><br /> bestRowTemporary (0)<br /><br /> bestRowTransaction (1)<br /><br /> bestRowSession (2)|  
|COLUMN_NAME|String|列的名称。|  
|DATA_TYPE|short|来自 java.sql.Types 的 SQL 数据类型。|  
|TYPE_NAME|String|数据类型的名称。|  
|COLUMN_SIZE|int|列的精度。|  
|BUFFER_LENGTH|int|缓冲区长度。|  
|DECIMAL_DIGITS|short|列的小数位数。|  
|PSEUDO_COLUMN|short|指示列是否为伪列。 可以为下列值之一：<br /><br /> bestRowUnknown (0)<br /><br /> bestRowNotPseudo (1)<br /><br /> bestRowPseudo (2)|  
  
## <a name="example"></a>示例  
 下例演示了如何使用 getBestRowIdentifier 方法返回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库中的 Person.Contact 表的最佳行标识符的信息。  
  
```  
public static void executeGetBestRowIdentifier(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getBestRowIdentifier(null, "Person", "Contact", 0, true);  
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
  
  
