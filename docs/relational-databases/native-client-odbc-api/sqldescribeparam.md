---
title: SQLDescribeParam |微软文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efe1fdccbef4f5c4a393083f6eb81efee759be5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302569"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  为了描述任何 SQL 语句的参数，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序在准备在 ODBC 语句句柄上调用 SQLDescribeParam 时生成并执行[!INCLUDE[tsql](../../includes/tsql-md.md)]SELECT 语句。 结果集的元数据确定预定义语句中的参数的特征。 SQLDescribeParam 可以返回 SQLExecute 或 SQLExecDirect 可能返回的任何错误代码。  
  
 数据库引擎的改进从 SQLDescribeParam 开始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，可以更精确地描述预期结果。 这些更准确的结果可能与 SQLDescribeParam 在 以前的版本中返回的值不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
 中[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]还新增了*参数SizePtr*现在返回一个值，该值与[ODBC 规范](https://go.microsoft.com/fwlink/?LinkId=207044)中定义的相应参数标记的列或表达式的大小（以字符）的定义一致。 在本机客户端的早期版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，*参数SizePtr*可以是该类型的**SQL_DESC_OCTET_LENGTH**的相应值，也可以是提供给 SQLBindParameter 的类型的不相关的列大小值，该值应忽略该值（例如**SQL_INTEGER）。**  
  
 在以下情况下，驱动程序不支持调用 SQLDescribeParam：  
  
-   SQLExecDirect 后，[!INCLUDE[tsql](../../includes/tsql-md.md)]用于包含 FROM 子句的任何更新或删除语句。  
  
-   对于 HAVING 子句中包含参数或与 SUM 函数的结果相比较的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
-   对于依赖于包含参数的子查询的任何 ODBC 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
-   对于在比较和类似表达式中包含参数标记或包含限定谓词的 ODBC SQL 语句。  
  
-   对于其参数之一为函数参数的任何查询。  
  
-   当\*[!INCLUDE[tsql](../../includes/tsql-md.md)]命令中有注释 （/* /） 时。  
  
 处理一批[!INCLUDE[tsql](../../includes/tsql-md.md)]语句时，驱动程序也不支持在批处理中的第一个语句之后调用 SQLDescribeParam 作为语句中的参数标记。  
  
 在描述准备好的存储过程的参数时，SQLDescribeParam 使用系统存储过程[sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md)检索参数特征。 sp_sproc_columns可以报告当前用户数据库中存储过程的数据。 准备完全限定的存储过程名称允许 SQLDescribeParam 跨数据库执行。 例如，系统存储过程[sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)可以在任何数据库中准备和执行，如：  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 成功准备后执行 SQLDescribeParam 返回一个空行集，当连接到任何数据库但**主**数据库 。 相同的调用（如下）使 SQLDescribeParam 成功，而不考虑当前用户数据库：  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 对于较大的值数据类型 *，DataTypePtr*中返回的值SQL_VARCHAR、SQL_VARBINARY或SQL_NVARCHAR。 为了指示大值数据类型参数的大小为"无限制"，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序将*参数SizePtr*设置为 0。 为标准**varchar**参数返回实际大小值。  
  
> [!NOTE]  
>  对于 SQL_VARCHAR、SQL_VARBINARY 或 SQL_WVARCHAR 参数，如果参数绑定有最大大小，则返回该参数的绑定大小，而非“无限制”。  
  
 若要绑定大小“无限制”的输入参数，必须使用执行时数据。 无法绑定"无限制"大小输出参数（没有从输出参数流式传输数据的方法，就像[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)对结果集所做的那样）。  
  
 对于输出参数，必须绑定一个缓冲区，如果值过大，则填充此缓冲区，并返回 SQL_SUCCESS_WITH_INFO 消息和“字符串数据；右端被截断”的警告。 随后将放弃截断的数据。  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam 和表值函数  
 应用程序可以使用 SQLDescribeParam 检索已准备好语句的表值参数信息。 有关详细信息，请参阅[已准备的语句的表值参数元数据](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 有关一般表值参数的详细信息，请参阅[&#40;ODBC &#40;的表值参数&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>SQLDescribeParam 对日期和时间增强功能的支持  
 日期/时间类型返回以下值：  
  
||*数据类型Ptr*|*参数SizePtr*|*十进制数字Ptr*|  
|-|-------------------|------------------------|------------------------|  
|datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19、21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26、28..34|0..7|  
  
 有关详细信息，请参阅[&#40;ODBC&#41;的日期和时间改进](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>SQLDescribeParam 对大型 CLR UDT 的支持  
 **SQLDescribeParam**支持大型 CLR 用户定义类型 （UDT）。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL描述参数函数](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
