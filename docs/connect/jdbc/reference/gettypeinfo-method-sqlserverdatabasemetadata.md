---
title: "getTypeInfo 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
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
- SQLServerDatabaseMetaData.getTypeInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 23208f01-c1bf-4235-b29c-9051d3df59a3
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4cce857630acc646d10da1ede7aa9139d62b6039
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="gettypeinfo-method-sqlserverdatabasemetadata"></a>getTypeInfo 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索当前数据库支持的所有标准 SQL 类型的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getTypeInfo()  
```  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getTypeInfo 方法指定此 getTypeInfo 方法。  
  
 GetTypeInfo 方法所返回的结果集将包含以下信息：  
  
|Name|类型|Description|  
|----------|----------|-----------------|  
|TYPE_NAME|**字符串**|数据类型的名称。|  
|DATA_TYPE|**短**|来自 java.sql.Types 的 SQL 数据类型。|  
|PRECISION|**int**|有效数字总个数。|  
|LITERAL_PREFIX|**字符串**|字符或字符常量前使用。|  
|LITERAL_SUFFIX|**字符串**|用于终止常量的一个或多个字符。|  
|CREATE_PARAMS|**字符串**|此数据类型的创建参数说明。|  
|NULLABLE|**短**|指示列能否包含 Null 值。 它可以是以下值之一：<br /><br /> typeNoNulls (0)<br /><br /> typeNullable (1)<br /><br /> typeNullableUnknown (2)|  
|CASE_SENSITIVE|**boolean**|指示数据类型是否区分大小写。 "**true**"如果类型是区分大小写; 否则为"**false**"。|  
|SEARCHABLE|**短**|指示是否可在 SQL WHERE 子句中使用此列。 它可以是以下值之一：<br /><br /> typePredNone (0)<br /><br /> typePredChar (1)<br /><br /> typePredBasic (2)<br /><br /> typeSeachable (3)|  
|UNSIGNED_ATTRIBUTE|**boolean**|指示数据类型的符号。 "**true**"如果类型是无符号; 否则为"**false**"。|  
|FIXED_PREC_SCALE|**boolean**|指示数据类型可以为 money 值。 "**true**"数据类型是否为 money 类型; 否则为"**false**"。|  
|AUTO_INCREMENT|**boolean**|指示数据类型可以自动递增。 "**true**"如果递增; 否则为可以自动类型"**false**"。|  
|LOCAL_TYPE_NAME|**字符串**|数据类型的本地化名称。|  
|MINIMUM_SCALE|**短**|小数点右边的最大位数。|  
|MAXIMUM_SCALE|**短**|小数点右边的最小位数。|  
|SQL_DATA_TYPE|**int**|JDBC 驱动程序不支持此类型。|  
|SQL_DATETIME_SUB|**int**|JDBC 驱动程序不支持此类型。|  
|NUM_PREC_RADIX|**int**|计算某列最大容纳数时所采用的位数或数字个数。|  
|INTERVAL_PRECISION|**int**|间隔起始精度的值。|  
|USERTYPE|**int**|**Usertype**值从**systypes**表。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 联机丛书。|  
  
> [!NOTE]  
>  有关 getTypeInfo 方法返回的数据的详细信息，请参阅"sp_datatype_info (TRANSACT-SQL)"中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 getTypeInfo 方法以返回有关中使用的数据类型信息[!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]（或更高版本） 数据库。  
  
```  
public static void executeGetTypeInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTypeInfo();  
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
  
  

