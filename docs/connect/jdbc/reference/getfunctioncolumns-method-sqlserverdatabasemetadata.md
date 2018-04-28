---
title: getFunctionColumns 方法 (SQLServerDatabaseMetaData) |Microsoft 文档
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
ms.topic: article
ms.assetid: e2b0e0f7-717c-48e6-bcd2-a325d938a833
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e9e3d78c17b4c2fe44ce80b6baf0eb8e4294339
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getfunctioncolumns-method-sqlserverdatabasemetadata"></a>getFunctionColumns 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索关于指定目录的系统函数或用户函数参数和返回类型的说明。  
  
## <a name="syntax"></a>语法  
  
```  
  
public ResultSet getFunctionColumns(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern  
                       java.lang.String columnNamePattern)  
```  
  
#### <a name="parameters"></a>Parameters  
 *catalog*  
  
 A**字符串**，其中包含目录名称。 如果该名称为空字符串 ""，则结果将包括无目录的函数。 如果它是**null**，目录名称不用于搜索。  
  
 *schemaPattern*  
  
 A**字符串**，其中包含的架构名称模式。 如果该名称为空字符串 ""，则结果将包括无架构的函数。 如果它是**null**，架构名称不用于搜索。  
  
 *functionNamePattern*  
  
 A**字符串**包含函数的名称。  
  
 *columnNamePattern*  
  
 A**字符串**，其中包含参数的名称。  
  
## <a name="return-value"></a>返回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getFunctionColumns 方法指定此 getFunctionColumns 方法。  
  
 此方法只返回与指定目录内的指定架构、函数名称和参数名称相匹配的函数和参数。  
  
 结果集中的各行均包括针对参数说明、列说明或返回类型的以下列：  
  
|名称|类型|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**字符串**|函数所在的数据库的名称。|  
|FUNCTION_SCHEM|**字符串**|函数的架构。|  
|FUNCTION_NAME|**字符串**|函数的名称。|  
|COLUMN_NAME|**字符串**|参数或列的名称。|  
|COLUMN_TYPE|**short**|**列的类型。它可以是以下值之一：**<br /><br /> functionColumnUnknown (0)：未知类型。<br /><br /> functionColumnIn (1)：输入参数。<br /><br /> functionColumnInOut (2)：输入/输出参数。<br /><br /> functionColumnOut (3)：输出参数。<br /><br /> functionReturn (4)：函数返回值。<br /><br /> functionColumnResult (5)：参数或列是结果集中的列。|  
|DATA_TYPE|**int**|SQL 数据类型从 Java.sql.Types 的值。|  
|TYPE_NAME|**字符串**|数据类型的名称。|  
|PRECISION|**int**|有效数字总个数。|  
|LENGTH|**int**|以字节为单位的数据的长度。|  
|SCALE|**short**|小数点右侧的数字个数。|  
|RADIX|**short**|数值类型的基础。|  
|NULLABLE|**short**|指示是否参数或返回值可以包含**null**值。<br /><br /> **它可以是以下值之一：**<br /><br /> functionNoNulls (0)：不允许为 NULL 值。<br /><br /> functionNullable (1)：允许为 NULL 值。<br /><br /> functionNullableUnknown (2)：未知。|  
|REMARKS|**字符串**|有关列或参数的注释。|  
|COLUMN_DEF|**字符串**|列的默认值。<br /><br /> **注意：**此信息，同时提供[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]和是特定于驱动程序的 JDBC。|  
|SQL_DATA_TYPE|**int**|此列等同于**DATA_TYPE**列中，除**datetime**和 ISO**间隔**数据类型。<br /><br /> **注意：**此信息，同时提供[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]和是特定于驱动程序的 JDBC。|  
|SQL_DATETIME_SUB|**int**|**Datetime** ISO**间隔**如果子代码的值**SQL_DATA_TYPE**是**SQL_DATETIME**或**SQL_INTERVAL**. 数据类型以外**datetime**和 ISO**间隔**，此列为 NULL。<br /><br /> **注意：**此信息，同时提供[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]和是特定于驱动程序的 JDBC。|  
|CHAR_OCTET_LENGTH|**int**|基于二进制和字符的最大长度的参数或列。 对于其他数据类型，该值为 NULL。|  
|ORDINAL_POSITION|**int**|对于输入和输出参数，它表示从 1 开始的位置。<br /><br /> 对于结果集列，它指从 1 开始的结果集的列的位置。<br /><br /> 对于返回值，该值为 0。|  
|IS_NULLABLE|**字符串**|确定参数或列的可为 Null 性。<br /><br /> 它可以是以下值之一：<br /><br /> **是**： 参数或列可以包含 NULL 值。<br /><br /> **不**： 参数或列不能包含 NULL 值。<br /><br /> 空字符串 ("")：未知。|  
|SS_TYPE_CATALOG_NAME|**字符串**|包含用户定义类型 (UDT) 的目录名称。|  
|SS_TYPE_SCHEMA_NAME|**字符串**|包含用户定义类型 (UDT) 的架构名称。|  
|SS_UDT_CATALOG_NAME|**字符串**|采用完全限定名称的用户定义类型 (UDT)。|  
|SS_UDT_SCHEMA_NAME|**字符串**|在其中定义 XML 架构集合名称的目录的名称。 如果找不到的目录名称，此变量包含一个空字符串。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**字符串**|在其中定义 XML 架构集合名称的架构的名称。 如果找不到架构名称，则为空字符串。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**字符串**|XML 架构集合的名称。 如果找不到名称，则为空字符串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**字符串**|包含用户定义类型 (UDT) 的目录名称。|  
|SS_XML_SCHEMACOLLECTION_NAME|**字符串**|包含用户定义类型 (UDT) 的架构名称。|  
|SS_DATA_TYPE|**tinyint**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用的数据类型扩展存储的过程。<br /><br /> **请注意**有关通过返回的数据类型的详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，请参阅"数据类型 (TRANSACT-SQL)"[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]联机丛书。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
