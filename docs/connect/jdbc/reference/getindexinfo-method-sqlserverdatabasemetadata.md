---
title: getIndexInfo 方法 (SQLServerDatabaseMetaData) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cdde9bb9a9b655fec98bc80e61a8e6b19869a753
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>getIndexInfo 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索的索引和给定的表的统计信息的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getIndexInfo(java.lang.String cat,  
                                       java.lang.String schema,  
                                       java.lang.String table,  
                                       boolean unique,  
                                       boolean approximate)  
```  
  
#### <a name="parameters"></a>Parameters  
 *cat*  
  
 A**字符串**，其中包含目录名称。  
  
 *schema*  
  
 A**字符串**包含架构的名称。  
  
 *table*  
  
 A**字符串**包含表的名称。  
  
 *唯一*  
  
 **true**如果只返回唯一值的索引。 **false**如果返回的所有索引。  
  
 *近似*  
  
 **true**如果结果反映近似或过期值。 **false**如果结果的准确性。  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getIndexInfo 方法指定此 getIndexInfo 方法。  
  
 GetIndexInfo 方法所返回的结果集将包含以下信息：  
  
|名称|类型|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**字符串**|在其中指定的表所在的数据库名称。|  
|TABLE_SCHEM|**字符串**|表的架构。|  
|TABLE_NAME|**字符串**|表的名称。|  
|NON_UNIQUE|**boolean**|指示索引值是否可以不唯一。|  
|INDEX_QUALIFIER|**字符串**|索引所有者的名称。 当 TYPE 为 tableIndexStatistic 时，该名称为 Null。|  
|INDEX_NAME|**字符串**|索引的名称。|  
|TYPE|**short**|索引的类型。 它可以是以下值之一：<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**short**|列在索引中的序号位置。 索引中的第一列为 1。|  
|COLUMN_NAME|**字符串**|列的名称。|  
|ASC_OR_DESC|**字符串**|索引排序规则中所用的顺序。 它可以是以下值之一：<br /><br /> A（升序）<br /><br /> D（降序）<br /><br /> NULL（不适用）<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]始终返回"A"。  |  
|CARDINALITY|**int**|表中的行数或索引中的唯一值个数。|  
|PAGES|**int**|用于存储索引或表的页数。|  
|FILTER_CONDITION|**字符串**|筛选条件。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]始终返回 null。  |  
  
> [!NOTE]  
>  有关 getIndexInfo 方法返回的数据的详细信息，请参阅"sp_indexes (TRANSACT-SQL)"中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 getIndexInfo 方法返回的索引和统计信息中的 Person.Contact 表有关的信息[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。  
  
```  
public static void executeGetIndexInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getIndexInfo("AdventureWorks", "Person", "Contact", false, true);  
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
  
  
