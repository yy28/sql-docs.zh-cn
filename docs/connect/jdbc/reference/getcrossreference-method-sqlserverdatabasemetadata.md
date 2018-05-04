---
title: getCrossReference 方法 (SQLServerDatabaseMetaData) |Microsoft 文档
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
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8876c49e809cf1bd941937c294d6122bb3c7d3f3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getcrossreference-method-sqlserverdatabasemetadata"></a>getCrossReference 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索给定外键表中的外键列的说明，该外键表引用给定主键表的主键列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getCrossReference(java.lang.String cat1,  
                                            java.lang.String schem1,  
                                            java.lang.String tab1,  
                                            java.lang.String cat2,  
                                            java.lang.String schem2,  
                                            java.lang.String tab2)  
```  
  
#### <a name="parameters"></a>Parameters  
 *cat1*  
  
 A**字符串**包含目录名称包含主键的表。  
  
 *schem1*  
  
 A**字符串**包含包含主键的表的架构名称。  
  
 *选项卡 1*  
  
 A**字符串**包含包含主键的表的表名。  
  
 *cat2*  
  
 A**字符串**包含包含外键的表的目录名称。  
  
 *schem2*  
  
 A**字符串**包含包含外键的表的架构名称。  
  
 *tab2*  
  
 A**字符串**包含包含外键的表的表名。  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getCrossReference 方法指定此 getCrossReference 方法。  
  
 GetCrossReference 方法所返回的结果集将包含以下信息：  
  
|名称|类型|Description|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**字符串**|包含主键表的目录名称。|  
|PKTABLE_SCHEM|**字符串**|主键表的架构名称。|  
|PKTABLE_NAME|**字符串**|主键表的名称。|  
|PKCOLUMN_NAME|**字符串**|主键的列名称。|  
|FKTABLE_CAT|**字符串**|包含外键表的目录名称。|  
|FKTABLE_SCHEM|**字符串**|外键表的架构名称。|  
|FKTABLE_NAME|**字符串**|外键表的名称。|  
|FKCOLUMN_NAME|**字符串**|外键的列名称。|  
|KEY_SEQ|**short**|多列主键中列的序列号。|  
|UPDATE_RULE|**short**|SQL 操作为更新时对外键应用的操作。 它可以是以下值之一：<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|SQL 操作为删除时对外键应用的操作。 它可以是以下值之一：<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**字符串**|外键的名称。|  
|PK_NAME|**字符串**|主键的名称。|  
|DEFERRABILITY|**short**|指示对外键约束的计算是否可以延迟到提交时。 它可以是以下值之一：<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  有关 getCrossReference 方法返回的数据的详细信息，请参阅"sp_fkeys (TRANSACT-SQL)"中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 getCrossReference 方法之间 Person.Contact 和 HumanResources.Employee 表中返回有关主键和外键关系的信息[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。  
  
```  
public static void executeGetCrossReference(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCrossReference("AdventureWorks", "Person", "Contact", null, "HumanResources", "Employee");  
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
  
  
