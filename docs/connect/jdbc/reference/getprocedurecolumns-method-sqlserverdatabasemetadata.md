---
title: getProcedureColumns 方法 (SQLServerDatabaseMetaData) |Microsoft 文档
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
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d323f4ba70e439eb5ec6ee1ec6178c8d8ec69dc1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getprocedurecolumns-method-sqlserverdatabasemetadata"></a>getProcedureColumns 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索存储过程参数和结果列的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.ResultSet getProcedureColumns(java.lang.String sCatalog,  
                                              java.lang.String sSchema,  
                                              java.lang.String proc,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCatalog*  
  
 A**字符串**，其中包含目录名称。 对此参数提供 Null 值指示无需使用目录名称。  
  
 *sSchema*  
  
 A**字符串**，其中包含的架构名称模式。 对此参数提供 Null 值指示无需使用架构名称。  
  
 *proc*  
  
 A**字符串**包含过程名称模式。  
  
 *列*  
  
 A**字符串**，其中包含的列名称模式。 对此参数提供 Null 值将为每一列返回一行。  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getProcedureColumns 方法指定此 getProcedureColumns 方法。  
  
 GetProcedureColumns 方法所返回的结果集将包含以下信息：  
  
|名称|类型|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**字符串**|指定的存储过程所在数据库的名称。|  
|PROCEDURE_SCHEM|**字符串**|存储过程的架构。|  
|PROCEDURE_NAME|**字符串**|存储过程的名称。|  
|COLUMN_NAME|**字符串**|列的名称。|  
|COLUMN_TYPE|**short**|列的类型。 它可以是以下值之一：<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**int**|来自 java.sql.Types 的 SQL 数据类型。|  
|TYPE_NAME|**字符串**|数据类型的名称。|  
|PRECISION|**int**|有效数字总个数。|  
|LENGTH|**int**|以字节为单位的数据的长度。|  
|SCALE|**short**|小数点右侧的数字个数。|  
|RADIX|**short**|数值类型的基础。|  
|NULLABLE|**short**|指示列能否包含 Null 值。 它可以是以下值之一：<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|REMARKS|**字符串**|过程列的说明。<br /><br /> <br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]不返回此列的值。|  
|COLUMN_DEF|**字符串**|列的默认值。|  
|SQL_DATA_TYPE|**int**|此列等同于**DATA_TYPE**列中，除**datetime**和 ISO**间隔**数据类型。|  
|SQL_DATETIME_SUB|**int**|**Datetime** ISO**间隔**如果子代码的值**SQL_DATA_TYPE**是**SQL_DATETIME**或**SQL_INTERVAL**. 数据类型以外**datetime**和 ISO**间隔**，此列为 NULL。|  
|CHAR_OCTET_LENGTH|**int**|列中的最大字节数。|  
|ORDINAL_POSITION|**int**|列在表中的索引。|  
|IS_NULLABLE|**字符串**|指示列是否允许 Null 值。|  
|SS_TYPE_CATALOG_NAME|**字符串**|包含用户定义类型 (UDT) 的目录名称。|  
|SS_TYPE_SCHEMA_NAME|**字符串**|包含用户定义类型 (UDT) 的架构名称。|  
|SS_UDT_CATALOG_NAME|**字符串**|采用完全限定名称的用户定义类型 (UDT)。|  
|SS_UDT_SCHEMA_NAME|**字符串**|在其中定义 XML 架构集合名称的目录的名称。 如果找不到的目录名称，此变量包含一个空字符串。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**字符串**|在其中定义 XML 架构集合名称的架构的名称。 如果找不到架构名称，则为空字符串。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**字符串**|XML 架构集合的名称。 如果找不到名称，则为空字符串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**字符串**|包含用户定义类型 (UDT) 的目录名称。|  
|SS_XML_SCHEMACOLLECTION_NAME|**字符串**|包含用户定义类型 (UDT) 的架构名称。|  
|SS_DATA_TYPE|**tinyint**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用的数据类型扩展存储的过程。<br /><br /> <br /><br /> **注意：**有关通过返回的数据类型的详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，请参阅"数据类型 (TRANSACT-SQL)"[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]联机丛书。|  
  
> [!NOTE]  
>  有关 getProcedureColumns 方法返回的数据的详细信息，请参阅"sp_sproc_columns (TRANSACT-SQL)"中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 getProcedureColumns 方法来返回有关中的 uspGetBillOfMaterials 存储过程的信息[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]示例数据库。  
  
```  
public static void executeGetProcedureColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedureColumns(null, null, "uspGetBillOfMaterials", null);  
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
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
