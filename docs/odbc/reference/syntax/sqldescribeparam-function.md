---
title: SQLDescribeParam 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62d61d43638c0ca6e3e43da83367dff461033463
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982295"
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLDescribeParam**返回与已准备的 SQL 语句相关联的参数标记的说明。 在 IPD 字段中，此信息是也可用。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *ParameterNumber*  
 [输入]参数标记号订购，按顺序在不断增加的参数顺序，从 1 开始。  
  
 *DataTypePtr*  
 [输出]指向用于返回参数的 SQL 数据类型的缓冲区。 从 IPD SQL_DESC_CONCISE_TYPE 记录字段读取此值。 这将是中的值之一[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)部分的附录 d:数据类型或特定于驱动程序的 SQL 数据类型。  
  
 在 ODBC 3。*x*，将中返回 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP  *\*DataTypePtr*日期、 时间或时间戳数据的 ODBC 2 中分别;。*x*，将返回 SQL_DATE、 SQL_TIME 或 SQL_TIMESTAMP。 驱动程序管理器执行所需的映射时 ODBC 2。*x*应用程序使用 ODBC 3。*x*驱动程序或当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序。  
  
 当*ColumnNumber*等于 SQL_BINARY 中为 0 （表示书签列），则返回 *\*DataTypePtr*长度可变的书签。 （如果书签由 ODBC 3，则返回 SQL_INTEGER。*x*应用程序使用 ODBC 2。*x*驱动程序或通过 ODBC 2。*x*应用程序使用 ODBC 3。*x*驱动程序。)  
  
 有关详细信息，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)中附录 d:数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。  
  
 *ParameterSizePtr*  
 [输出]指向用于返回大小，以字符为单位的列或表达式的相应参数标记的数据源定义的缓冲区。 有关列大小的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *DecimalDigitsPtr*  
 [输出]指向在其中定义的数据源返回十进制数字的列或表达式的相应参数的数量的缓冲区的指针。 十进制数字的详细信息，请参阅[列的大小、 十进制数字、 传输八位字节长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *NullablePtr*  
 [输出]指向用于返回一个值，指示参数是否允许 NULL 值的缓冲区。 从 IPD SQL_DESC_NULLABLE 字段读取此值。 可以是以下类型之一：  
  
-   SQL_NO_NULLS:参数不允许 NULL 值 （这是默认值）。  
  
-   SQL_NULLABLE:该参数允许 NULL 值。  
  
-   SQL_NULLABLE_UNKNOWN:该驱动程序无法确定参数是否允许 NULL 值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDescribeParam**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLDescribeParam** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07009|描述符索引无效|(DM) 的参数指定的值*ParameterNumber*小于 1。<br /><br /> 为参数指定的值*ParameterNumber*大于相关联的 SQL 语句中的参数数量。<br /><br /> 参数标记是一个非 DML 语句的一部分。<br /><br /> 参数标记为属于**选择**列表。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|21S01|插入值列表与列列表不匹配|中的参数数目**插入**语句与名为语句中的表中的列数不匹配。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 之前，先调用函数**SQLPrepare**或**SQLExecDirect**有关*StatementHandle*。<br /><br /> (DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLDescribeParam**调用函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 参数标记是以不断增加的参数顺序，以它们在 SQL 语句中出现的顺序 1 开始编号。  
  
 **SQLDescribeParam**不在 SQL 语句中返回参数的类型 （输入、 输入/输出或输出）。 但在调用过程中，在 SQL 语句中的所有参数都是输入的参数。 若要确定在调用过程中每个参数的类型，应用程序调用**SQLProcedureColumns**。  
  
 有关详细信息，请参阅[描述参数](../../../odbc/reference/develop-app/describing-parameters.md)。  
  
## <a name="code-example"></a>代码示例  
 以下示例将提示用户输入的 SQL 语句，并随后将准备该语句。 接下来，调用**SQLNumParams**以确定该语句是否包含任何参数。 如果语句包含参数，则会调用**SQLDescribeParam**来描述这些参数和**SQLBindParameter**以将其绑定。 最后，它提示用户输入任何参数的值，然后执行该语句。  
  
```  
SQLCHAR       Statement[100];  
SQLSMALLINT   NumParams, i, DataType, DecimalDigits, Nullable;  
SQLUINTEGER   ParamSize;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement and prepare it.  
GetSQLStatement(Statement);  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Check to see if there are any parameters. If so, process them.  
SQLNumParams(hstmt, &NumParams);  
if (NumParams) {  
   // Allocate memory for three arrays. The first holds pointers to buffers in which  
   // each parameter value will be stored in character form. The second contains the  
   // length of each buffer. The third contains the length/indicator value for each  
   // parameter.  
   SQLPOINTER * PtrArray = (SQLPOINTER *) malloc(NumParams * sizeof(SQLPOINTER));  
   SQLINTEGER * BufferLenArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
   SQLINTEGER * LenOrIndArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
  
   for (i = 0; i < NumParams; i++) {  
   // Describe the parameter.  
   SQLDescribeParam(hstmt, i + 1, &DataType, &ParamSize, &DecimalDigits, &Nullable);  
  
   // Call a helper function to allocate a buffer in which to store the parameter  
   // value in character form. The function determines the size of the buffer from  
   // the SQL data type and parameter size returned by SQLDescribeParam and returns  
   // a pointer to the buffer and the length of the buffer.  
   AllocParamBuffer(DataType, ParamSize, &PtrArray[i], &BufferLenArray[i]);  
  
   // Bind the memory to the parameter. Assume that we only have input parameters.  
   SQLBindParameter(hstmt, i + 1, SQL_PARAM_INPUT, SQL_C_CHAR, DataType, ParamSize,  
         DecimalDigits, PtrArray[i], BufferLenArray[i],  
         &LenOrIndArray[i]);  
  
   // Prompt the user for the value of the parameter and store it in the memory  
   // allocated earlier. For simplicity, this function does not check the value  
   // against the information returned by SQLDescribeParam. Instead, the driver does  
   // this when the statement is executed.  
   GetParamValue(PtrArray[i], BufferLenArray[i], &LenOrIndArray[i]);  
   }  
}  
  
// Execute the statement.  
SQLExecute(hstmt);  
  
// Process the statement further, such as retrieving results (if any) and closing the  
// cursor (if any). Code not shown.  
  
// Free the memory allocated for each parameter and the memory allocated for the arrays  
// of pointers, buffer lengths, and length/indicator values.  
for (i = 0; i < NumParams; i++) free(PtrArray[i]);  
free(PtrArray);  
free(BufferLenArray);  
free(LenOrIndArray);  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到参数的缓冲区|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|准备执行的语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
