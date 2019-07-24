---
title: getIndexInfo 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8dd512236aa3070ce299756d4e4294c79ac2e94a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982788"
---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>getIndexInfo 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索给定表的索引和统计信息的说明。  
  
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
  
 一个包含目录名称的字符串  。  
  
 *schema*  
  
 一个包含架构名称的字符串  。  
  
 *table*  
  
 一个包含表名称的字符串  。  
  
 *UNIQUE*  
  
 如果只返回唯一值的索引,**则为 true** 。 如果返回所有索引, 则**为 false** 。  
  
 *approximate*  
  
 如果结果反映大致或过期值,**则为 true** 。 如果结果准确, 则**为 false** 。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getIndexInfo 方法是由 java.sql.DatabaseMetaData 接口中的 getIndexInfo 方法指定的。  
  
 由 getIndexInfo 方法返回的结果集将包含以下信息：  
  
|“属性”|类型|描述|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|指定的表所在的数据库的名称。|  
|TABLE_SCHEM|**String**|表的架构。|  
|TABLE_NAME|**String**|表的名称。|  
|NON_UNIQUE|**boolean**|指示索引值是否可以不唯一。|  
|INDEX_QUALIFIER|**String**|索引所有者的名称。 当 TYPE 为 tableIndexStatistic 时，该名称为 Null。|  
|INDEX_NAME|**String**|索引的名称。|  
|TYPE|**short**|索引的类型。 可以为下列值之一：<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**short**|列在索引中的序号位置。 索引中的第一列为 1。|  
|COLUMN_NAME|**String**|列的名称。|  
|ASC_OR_DESC|**String**|索引排序规则中所用的顺序。 可以为下列值之一：<br /><br /> A（升序）<br /><br /> D（降序）<br /><br /> NULL（不适用）<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 始终会返回“A”。|  
|CARDINALITY|**int**|表中的行数或索引中的唯一值个数。|  
|PAGES|**int**|用于存储索引或表的页数。|  
|FILTER_CONDITION|**String**|筛选条件。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 始终会返回 null。|  
  
> [!NOTE]  
>  有关 getIndexInfo 方法返回的数据的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“sp_indexes (Transact-SQL)”。  
  
## <a name="example"></a>示例  
 以下示例演示了如何使用 getIndexInfo 方法返回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库中的 Person.Contact 表的索引信息和统计信息。  
  
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
  
  
