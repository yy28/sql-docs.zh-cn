---
title: SQLPutData 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLPutData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPutData
helpviewer_keywords:
- SQLPutData function [ODBC]
ms.assetid: 9a60f004-1477-4c54-a20c-7378e1116713
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cfe33eb04b4948dcba85aa2d9549c301eb65c8a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlputdata-function"></a>SQLPutData 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLPutData**允许应用程序将参数或列的数据发送到在语句执行时驱动程序。 此函数可用来将部件中的字符或二进制数据值发送到具有字符、 binary 或数据源 – 特定数据类型 （例如，在 SQL_LONGVARBINARY 或 SQL_LONGVARCHAR 类型参数） 的列。 **SQLPutData**支持到 Unicode C 数据类型的绑定，即使基础驱动程序不支持 Unicode 数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *DataPtr*  
 [输入]指向包含的参数或列的实际数据的缓冲区的指针。 数据中指定的 C 数据类型必须为*ValueType*参数**SQLBindParameter** （用于参数数据） 或*TargetType*参数**SQLBindCol** （适用于列数据）。  
  
 *StrLen_or_Ind*  
 [输入]长度\* *DataPtr*。 指定的调用中发送的数据量**SQLPutData**。 数据量可能随每个调用中给定的参数或列。 *StrLen_or_Ind*除非它满足以下条件之一，否则将忽略：  
  
-   *StrLen_or_Ind*是 sql_nts 以、 SQL_NULL_DATA，还是 SQL_DEFAULT_PARAM。  
  
-   中指定的 C 数据类型**SQLBindParameter**或**SQLBindCol** SQL_C_CHAR 或 SQL_C_BINARY。  
  
-   C 数据类型是 SQL_C_DEFAULT，并且指定的 SQL 数据类型的默认 C 数据类型为 SQL_C_CHAR 或 SQL_C_BINARY。  
  
 对于所有其他类型的 C 数据，如果*StrLen_or_Ind* SQL_NULL_DATA 或 SQL_DEFAULT_PARAM，不是驱动程序假定的大小\* *DataPtr*缓冲区是指定的 C 数据类型的大小与*ValueType*或*TargetType*和发送的整个数据值。 有关详细信息，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)附录 d： 数据类型中。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLPutData**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLPutData**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|字符串或为输出参数返回的二进制数据导致的非空白字符或非 NULL 二进制数据截断。 如果它是一个字符串值，它是右侧被截断。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|由标识的数据值*ValueType*中的参数**SQLBindParameter**对于无法转换的绑定的参数，标识的数据类型为*ParameterType*中的参数**SQLBindParameter**。|  
|07S01|不允许使用默认参数|参数值，设置**SQLBindParameter**、 SQL_DEFAULT_PARAM，以及相应的参数没有默认值。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|22001|字符串数据，右截断|字符或二进制值的列分配导致非空白 （字符） 或非 null （二进制） 字符或字节数的截断。<br /><br /> 中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**被"Y"，并更多的数据已发送 （数据类型不 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源 – 特定数据类型） 的长参数不是指定与*StrLen_or_IndPtr*中的参数**SQLBindParameter**。<br /><br /> 中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**被"Y"，并不是中已指定，更多的数据已发送长列 （数据类型不 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源 – 特定数据类型）对应于已添加或更新的数据的行中的列的长度缓冲区**SQLBulkOperations**或更新与**SQLSetPos**。|  
|22003|数值超出范围|为绑定的数值参数发送数据或列导致整个 （而不是小数部分组成） 的部分将被截断时分配给关联的表的列。<br /><br /> 返回一个或多个输入/输出参数或输出参数的数字值 （为数字或字符串） 可能会导致整个 （而不是小数部分组成） 的部分将被截断。|  
|22007|无效的日期时间格式|为参数或列已绑定到日期、 时间或时间戳结构发送的数据时，分别无效的日期、 时间戳。<br /><br /> 一个输入/输出或输出参数绑定到日期、 时间或时间戳 C 结构中返回的参数, 的值，分别无效的日期、 时间戳。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22008|Datetime 字段溢出|日期时间表达式计算的输入/输出或输出参数导致日期、 时间或时间戳 C 结构无效。|  
|22012|被零除|输出参数导致被零的除法或算术表达式计算的输入/输出。|  
|22015|间隔字段溢出|为精确数字或间隔列发送的数据或为间隔 SQL 数据类型参数导致重要数字丢失。<br /><br /> 数据发送间隔列或参数与多个字段，已转换为数值数据类型，并且拥有的数值数据类型中的没有表示形式。<br /><br /> 发送列的数据或参数数据已分配给间隔 SQL 类型，并且没有任何值的表示形式的 C 类型在时间间隔内 SQL 类型。<br /><br /> 发送精确数字或间隔 C 列或参数间隔 C 类型的数据导致重要数字丢失。<br /><br /> 发送有关列的数据或参数数据已分配给间隔 C 结构，并且没有没有间隔数据结构中的数据的表示形式。|  
|22018|转换指定的的无效字符值|C 类型已准确或近似数字、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;并且中的列或参数的值不是有效的文本的绑定的 C 类型。<br /><br /> SQL 类型已准确或近似数字、 日期时间或间隔数据类型;C 类型为 SQL_C_CHAR;并且中的列或参数的值不是有效的文本的绑定的 SQL 类型。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY009|不允许使用 null 指针|(DM) 自变量*DataPtr*是 null 指针和的自变量*StrLen_or_Ind*不是 0、 SQL_DEFAULT_PARAM 或 SQL_NULL_DATA。|  
|HY010|函数序列错误|(DM) 前面的函数调用不是调用**SQLPutData**或**SQLParamData**。<br /><br /> (DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 调用 SQLPutData 函数时仍在执行此异步函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY019|分段发送非字符和非二进制数据|**SQLPutData**调用不止一次为参数或列中，但它不使用将字符 C 数据发送到具有字符、 binary 或数据源 – 特定数据类型的列，或将二进制 C 数据发送到具有一个字符的列二进制文件中或数据源 – 特定数据类型。|  
|HY020|尝试连接空值|**SQLPutData**由于调用返回 SQL_NEED_DATA，且这些调用之一不止一次调用*StrLen_or_Ind*自变量包含 SQL_NULL_DATA 或 SQL_DEFAULT_PARAM。|  
|HY090|字符串或缓冲区长度无效|自变量*DataPtr*不是 null 指针和的自变量*StrLen_or_Ind*小于 0，但不是等于 sql_nts 以或 SQL_NULL_DATA。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
 如果**SQLPutData**称为时发送 SQL 语句中的参数的数据，它可能会返回任何可通过调用执行语句的函数返回的 SQLSTATE (**SQLExecute**或**SQLExecDirect**)。 如果发送的列的数据时调用正在更新或添加与**SQLBulkOperations**或与正在更新**SQLSetPos**，它可返回可以由任何 SQLSTATE **SQLBulkOperations**或**SQLSetPos**。  
  
## <a name="comments"></a>注释  
 **SQLPutData**可以调用来提供数据在执行数据的两个用途： 对的调用中使用的参数数据**SQLExecute**或**SQLExecDirect**，或更新行时使用的列数据或通过调用添加**SQLBulkOperations**或通过调用更新**SQLSetPos**。  
  
 在应用程序调用**SQLParamData**以便确定哪些数据应发送，该驱动程序返回应用程序可用于确定要发送的参数数据或可找到列数据的位置的指示器。 它还返回 SQL_NEED_DATA，是对应用程序应调用指示器**SQLPutData**发送数据。 在*DataPtr*参数**SQLPutData**，应用程序将指针传递到包含的参数或列的实际数据的缓冲区。  
  
 驱动程序时返回有关 SQL_SUCCESS **SQLPutData**，应用程序调用**SQLParamData**试。 **SQLParamData**返回 SQL_NEED_DATA 更多的数据需要发送，如果在此情况下应用程序调用**SQLPutData**试。 如果已发送所有数据在执行数据，则返回 SQL_SUCCESS。 然后，应用程序调用**SQLParamData**试。 如果该驱动程序返回 SQL_NEED_DATA 和中的另一个指示器 *\*ValuePtrPtr*，它需要进行另一个参数或列的数据和**SQLPutData**会再次调用。 如果该驱动程序的返回 SQL_SUCCESS，则所有数据在执行发送数据，并且可以执行的 SQL 语句或**SQLBulkOperations**或**SQLSetPos**可处理调用。  
  
 在语句执行时传递数据在执行参数数据的详细信息，请参阅"将传递参数值"中[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)和[发送长整型数据](../../../odbc/reference/develop-app/sending-long-data.md)。 更新或添加对数据在执行的列数据的详细信息，请参阅"使用 SQLSetPos"一节中[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)，"执行大容量更新使用中的书签" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，和[长数据、 SQLSetPos 和 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
> [!NOTE]  
>  应用程序可以使用**SQLPutData**发送部分仅当将字符 C 数据发送到具有字符、 binary 或数据源 – 特定数据类型的列或将二进制 C 数据发送到字符，二进制，列中的数据源 – 特定的数据类型。 如果**SQLPutData**调用一次以上任何其他情况下它将返回 SQL_ERROR 和 SQLSTATE HY019 （分段发送非字符和非二进制数据）。  
  
## <a name="example"></a>示例  
 下面的示例假定名为 Test 的数据源名称。 关联的数据库应具有一个表，其中你可以创建，，如下所示：  
  
```  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```  
// SQLPutData.cpp  
// compile with: odbc32.lib user32.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define TEXTSIZE  12000  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // SQLBindParameter variables.  
   SQLLEN cbTextSize, lbytes;  
  
   // SQLParamData variable.  
   PTR pParmID;  
  
   // SQLPutData variables.  
   UCHAR  Data[] =   
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyz";  
  
   SDWORD cbBatch = (SDWORD)sizeof(Data) - 1;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set parameters based on total data to send.  
   lbytes = (SDWORD)TEXTSIZE;  
   cbTextSize = SQL_LEN_DATA_AT_EXEC(lbytes);  
  
   // Bind the parameter marker.  
   retcode = SQLBindParameter (hstmt1,           // hstmt  
                               1,                // ipar  
                               SQL_PARAM_INPUT,  // fParamType  
                               SQL_C_CHAR,       // fCType  
                               SQL_LONGVARCHAR,  // FSqlType  
                               lbytes,           // cbColDef  
                               0,                // ibScale  
                               (VOID *)1,        // rgbValue  
                               0,                // cbValueMax  
                               &cbTextSize);     // pcbValue  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.  
   retcode =   
      SQLExecDirect(hstmt1, (UCHAR*)"INSERT INTO emp4 VALUES('Paul Borm', 46,'1950-11-12 00:00:00', ?)", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_NEED_DATA) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Check to see if NEED_DATA; if yes, use SQLPutData.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if (retcode == SQL_NEED_DATA) {  
      while (lbytes > cbBatch) {  
         SQLPutData(hstmt1, Data, cbBatch);  
         lbytes -= cbBatch;  
      }  
      // Put final batch.  
      retcode = SQLPutData(hstmt1, Data, lbytes);   
   }  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Make final SQLParamData call.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("Final SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clean up.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到参数的缓冲区|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回下一个参数发送数据|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
