---
title: SQLDescribeParam 函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be6d076ca121923a4b6769c7dad5269c3fd642ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301157"
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLDescribeParam**返回与准备好的 SQL 语句关联的参数标记的说明。 此信息也可在 IPD 领域提供。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *参数编号*  
 [输入]参数标记编号按增加参数顺序顺序排序，从 1 开始。  
  
 *数据类型Ptr*  
 [输出]指向要返回参数的 SQL 数据类型的缓冲区的指针。 此值从 IPD 的SQL_DESC_CONCISE_TYPE记录字段中读取。 这将是附录[D：](../../../odbc/reference/appendixes/sql-data-types.md)数据类型或特定于驱动程序的 SQL 数据类型的 SQL 数据类型中的值之一。  
  
 在 ODBC 3 中。*x*x、SQL_TYPE_DATE、SQL_TYPE_TIME或SQL_TYPE_TIMESTAMP将分别在*\*DataTypePtr*中返回日期、时间或时间戳数据;在 ODBC 2 中。*x*x、SQL_DATE、SQL_TIME或SQL_TIMESTAMP将返回。 当 ODBC 2 时，驱动程序管理器执行所需的映射。*x*应用程序使用 ODBC 3。*x*驱动程序或当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序。  
  
 当*列数*等于 0（对于书签列），SQL_BINARY在*\*DataTypePtr*中返回，用于可变长度书签。 （如果 ODBC 3 使用书签，则返回SQL_INTEGER。*x*应用程序使用 ODBC 2。*x*驱动程序或 ODBC 2。*x*使用 ODBC 3 的应用程序。*x*驱动程序。  
  
 有关详细信息，请参阅附录 D 中的[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)：数据类型。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。  
  
 *参数SizePtr*  
 [输出]指向缓冲区的指针，其中用于返回数据源定义的相应参数标记的列或表达式的大小（以字符表示）。 有关列大小的详细信息，请参阅[列大小、十进制数字、传输八点长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *十进制数字Ptr*  
 [输出]指向缓冲区的指针，其中用于返回数据源定义的列或相应参数的表达式的十进制数字数。 有关十进制数字的详细信息，请参阅[列大小、十进制数字、传输八进制长度和显示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *空可点*  
 [输出]指向缓冲区的指针，其中要返回指示参数是否允许 NULL 值的值。 此值从 IPD 的SQL_DESC_NULLABLE字段中读取。 下列类型作之一：  
  
-   SQL_NO_NULLS：参数不允许 NULL 值（这是默认值）。  
  
-   SQL_NULLABLE：参数允许 NULL 值。  
  
-   SQL_NULLABLE_UNKNOWN：驱动程序无法确定参数是否允许 NULL 值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLDescribeParam**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有*Handle*SQL_HANDLE_STMT的*句柄类型*和*语句句柄*。 下表列出了**SQLDescribeParam**通常返回的 SQLSTATE 值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07009|无效描述符索引|（DM） 为参数*参数编号*指定的值小于 1。<br /><br /> 为参数*参数编号*指定的值大于关联的 SQL 语句中的参数数。<br /><br /> 参数标记是非 DML 语句的一部分。<br /><br /> 参数标记是**SELECT**列表的一部分。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|21S01|插入值列表与列列表不匹配|**INSERT**语句中的参数数与语句中命名的表中的列数不匹配。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY010|函数序列错误|（DM） 在调用**SQLPrepare**或**SQLExecDirect**进行*语句句柄*之前调用了函数。<br /><br /> （DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLDescribeParam**函数时，此异步函数仍在执行。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
 参数标记按增加参数顺序编号，以 1 开头，按它们在 SQL 语句中显示的顺序进行编号。  
  
 **SQLDescribeParam**不会返回 SQL 语句中参数的类型（输入、输入/输出或输出）。 除了对过程的调用中，SQL 语句中的所有参数都是输入参数。 要确定对过程调用中的每个参数的类型，应用程序调用**SQLAE 列**。  
  
 有关详细信息，请参阅[描述参数](../../../odbc/reference/develop-app/describing-parameters.md)。  
  
## <a name="code-example"></a>代码示例  
 下面的示例提示用户使用 SQL 语句，然后准备该语句。 接下来，它将调用**SQLNumParams**以确定该语句是否包含任何参数。 如果语句包含参数，它将调用**SQLDescribeParam**来描述这些参数 **，SQLBind参数**将它们绑定。 最后，它提示用户输入任何参数的值，然后执行语句。  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到参数|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|准备执行语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
