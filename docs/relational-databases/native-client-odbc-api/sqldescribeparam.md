---
title: SQLDescribeParam | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
caps.latest.revision: "61"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e1f4ce5630728cb33e98f389dd1e65a02f6178c
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  若要描述参数的任何 SQL 语句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序生成并执行[!INCLUDE[tsql](../../includes/tsql-md.md)]SQLDescribeParam 调用的已准备的 ODBC 语句句柄时的 SELECT 语句。 结果集的元数据确定预定义语句中的参数的特征。 SQLDescribeParam 可以返回 SQLExecute 或 SQLExecDirect 可能会返回任何错误代码。  
  
 从数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 SQLDescribeParam 以获取更准确的预期结果的说明。 这些更准确的结果可能与在以前版本的 SQLDescribeParam 返回的值不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
 中还新增[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]， *ParameterSizePtr*现在可返回一个值，符合的大小，以字符为单位的列或表达式的相应参数标记的定义中定义[ODBC规范](http://go.microsoft.com/fwlink/?LinkId=207044)。 在以前版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client， *ParameterSizePtr*可能的相应值**SQL_DESC_OCTET_LENGTH**类型，或提供一个不相关的列大小值到类型 SQLBindParameter，应忽略的值 (**SQL_INTEGER**，例如)。  
  
 在以下情况下，该驱动程序不支持调用 SQLDescribeParam:  
  
-   对于任何 SQLExecDirect 后[!INCLUDE[tsql](../../includes/tsql-md.md)]包含 FROM 子句的 UPDATE 或 DELETE 语句。  
  
-   对于 HAVING 子句中包含参数或与 SUM 函数的结果相比较的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
-   对于依赖于包含参数的子查询的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
-   对于在比较和类似表达式中包含参数标记或包含限定谓词的 ODBC SQL 语句。  
  
-   对于其参数之一为函数参数的任何查询。  
  
-   如果有注释 (/ * \*/) 中[!INCLUDE[tsql](../../includes/tsql-md.md)]命令。  
  
 处理一批时[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，该驱动程序也不支持批处理中的第一个语句后调用语句中参数标记 SQLDescribeParam。  
  
 SQLDescribeParam 介绍准备存储的过程的参数，当使用系统存储过程[sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md)检索参数特征。 sp_sproc_columns 可以报告的当前用户数据库中的存储过程的数据。 准备一个完全限定的存储的过程名称允许 SQLDescribeParam 跨数据库执行。 例如，对于系统存储过程[sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)可以准备和执行在与任何数据库中：  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 成功准备返回空的行集时连接到任何数据库后执行 SQLDescribeParam 但**master**。 相同的调用，准备好，如下所示，将导致 SQLDescribeParam 成功而不考虑当前的用户数据库：  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 对于大型值数据类型值将返回在*DataTypePtr*是 SQL_VARCHAR、 SQL_VARBINARY，还是 SQL_NVARCHAR。 若要指示大型值数据类型参数的大小是"无限制，" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序集*ParameterSizePtr*为 0。 返回标准的实际大小值**varchar**参数。  
  
> [!NOTE]  
>  对于 SQL_VARCHAR、SQL_VARBINARY 或 SQL_WVARCHAR 参数，如果参数绑定有最大大小，则返回该参数的绑定大小，而非“无限制”。  
  
 若要绑定大小“无限制”的输入参数，必须使用执行时数据。 不能将"无限制"大小输出参数绑定 (如流数据从一个输出参数，没有方法[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)会为结果集)。  
  
 对于输出参数，必须绑定一个缓冲区，如果值过大，则填充此缓冲区，并返回 SQL_SUCCESS_WITH_INFO 消息和“字符串数据；右端被截断”的警告。 随后将放弃截断的数据。  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam 和表值函数  
 应用程序可以检索与 SQLDescribeParam 已准备的语句的表值参数信息。 有关详细信息，请参阅[准备语句的表值参数元数据](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 有关表值参数的详细信息一般情况下，请参阅[表值参数 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>SQLDescribeParam 对日期和时间增强功能的支持  
 日期/时间类型返回以下值：  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 有关详细信息，请参阅[日期和时间改进 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>SQLDescribeParam 对大型 CLR UDT 的支持  
 **SQLDescribeParam**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型 &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLDescribeParam Function](http://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
