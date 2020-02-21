---
title: getVersionColumns 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getVersionColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6dd275d3-d9b2-4db7-938a-d4406c940a7a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e2cf823a6c1cd33d647472a2e709517175ddce7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67978167"
---
# <a name="getversioncolumns-method-sqlserverdatabasemetadata"></a>getVersionColumns 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索在某行内的任何值更新时会随之自动更新的表列的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getVersionColumns(java.lang.String catalog,  
                                            java.lang.String schema,  
                                            java.lang.String table)  
```  
  
#### <a name="parameters"></a>parameters  
 *catalog*  
  
 一个包含目录名称的字符串  。  
  
 *schema*  
  
 一个包含架构名称模式的字符串  。  
  
 *table*  
  
 一个包含表名称的字符串  。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getVersionColumns 方法是由 java.sql.DatabaseMetaData 接口中的 getVersionColumns 方法指定的。  
  
 由 getVersionColumns 方法返回的结果集将包含下列信息：  
  
|名称|类型|说明|  
|----------|----------|-----------------|  
|SCOPE|**short**|JDBC 驱动程序不支持此类型。|  
|COLUMN_NAME|**字符串**|列名称。|  
|DATA_TYPE|**short**|来自 java.sql.Types 的 SQL 数据类型。|  
|TYPE_NAME|**字符串**|数据类型的名称。|  
|COLUMN_SIZE|**int**|列的精度。|  
|BUFFER_LENGTH|**int**|列的长度（字节）。|  
|DECIMAL_DIGITS|**short**|列的小数位数。|  
|PSEUDO_COLUMN|**short**|指示列是否为伪列。 可以为下列值之一：<br /><br /> versionColumnUnknown (0)<br /><br /> versionColumnNotPseudo (1)<br /><br /> versionColumnPseudo (2)|  
  
> [!NOTE]  
>  有关 getVersionColumns 方法返回的数据的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“sp_datatype_info (Transact-SQL)”。  
  
## <a name="example"></a>示例  
 以下示例演示了如何使用 getVersionColumns 方法返回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库中的 Person.Contact 表中自动更新的列的信息。  
  
```  
public static void executeGetVersionColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getVersionColumns("AdventureWorks", "Person", "Contact");  
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
  
  
