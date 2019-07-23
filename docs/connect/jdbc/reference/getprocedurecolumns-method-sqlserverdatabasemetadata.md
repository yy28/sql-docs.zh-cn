---
title: getProcedureColumns 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1767519cc2f36bac4a70da84efeb8da9e2a1ec3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980750"
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
 sCatalog   
  
 一个包含目录名称的字符串  。 对此参数提供 Null 值指示无需使用目录名称。  
  
 sSchema   
  
 一个包含架构名称模式的字符串  。 对此参数提供 Null 值指示无需使用架构名称。  
  
 *proc*  
  
 一个包含过程名称模式的字符串  。  
  
 *col*  
  
 一个包含列名称模式的字符串  。 对此参数提供 Null 值将为每一列返回一行。  
  
## <a name="return-value"></a>返回值  
 一个 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getProcedureColumns 方法由 getProcedureColumns 方法在 Java.sql.databasemetadata 接口中指定。  
  
 由 getProcedureColumns 方法返回的结果集将包含以下信息：  
  
|“属性”|类型|描述|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|指定的存储过程所在数据库的名称。|  
|PROCEDURE_SCHEM|**String**|存储过程的架构。|  
|PROCEDURE_NAME|**String**|存储过程的名称。|  
|COLUMN_NAME|**String**|列的名称。|  
|COLUMN_TYPE|**short**|列的类型。 可以为下列值之一：<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|来自 java.sql.Types 的 SQL 数据类型。|  
|TYPE_NAME|**String**|数据类型的名称。|  
|PRECISION|**int**|有效数字总个数。|  
|LENGTH|**int**|数据的长度 (以字节为单位)。|  
|SCALE|**short**|小数点右边的数字位数。|  
|RADIX|**short**|数值类型的基数。|  
|NULLABLE|**short**|指示列能否包含 Null 值。 可以为下列值之一：<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|REMARKS|**String**|过程列的说明。<br /><br /> <br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会为此列返回值。|  
|COLUMN_DEF|**String**|列的默认值。|  
|SQL_DATA_TYPE|**smallint**|此列与 DATA_TYPE 列相同，datetime 和 ISO interval 数据类型除外    。|  
|SQL_DATETIME_SUB|**smallint**|如果 SQL_DATA_TYPE 的值为 SQL_DATETIME 或 SQL_INTERVAL，则为 datetime ISO interval 子代码      。 对于**datetime**和 ISO **interval**以外的数据类型, 此列为 NULL。|  
|CHAR_OCTET_LENGTH|**int**|列中的最大字节数。|  
|ORDINAL_POSITION|**int**|列在表中的索引。|  
|IS_NULLABLE|**String**|指示列是否允许 Null 值。|  
|SS_TYPE_CATALOG_NAME|**String**|包含用户定义类型 (UDT) 的目录名称。|  
|SS_TYPE_SCHEMA_NAME|**String**|包含用户定义类型 (UDT) 的架构名称。|  
|SS_UDT_CATALOG_NAME|**String**|采用完全限定名称的用户定义类型 (UDT)。|  
|SS_UDT_SCHEMA_NAME|**String**|在其中定义 XML 架构集合名称的目录的名称。 如果找不到目录名称，此变量则会包含一个空字符串。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|在其中定义 XML 架构集合名称的架构的名称。 如果找不到架构名称，则为空字符串。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|XML 架构集合的名称。 如果找不到名称，则为空字符串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|包含用户定义类型 (UDT) 的目录名称。|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|包含用户定义类型 (UDT) 的架构名称。|  
|SS_DATA_TYPE|**tinyint**|扩展存储过程使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型。<br /><br /> <br /><br /> **注意：** 有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 返回的数据类型的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“数据类型 (Transact-SQL)”。|  
  
> [!NOTE]  
>  有关 getProcedureColumns 方法返回的数据的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书中的“sp_sproc_columns (Transact-SQL)”。  
  
## <a name="example"></a>示例  
 以下示例演示了如何使用 getProcedureColumns 方法返回有关 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 示例数据库中的 uspGetBillOfMaterials 存储过程的信息。  
  
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
  
  
