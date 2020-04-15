---
title: SQLPutData 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c4e704d96924942812904ea63d0e3d4fce8748e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300037"
---
# <a name="sqlputdata-function"></a>SQLPutData 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLPutData**允许应用程序在语句执行时将参数或列的数据发送到驱动程序。 此函数可用于将零件中的字符或二进制数据值发送到具有字符、二进制或数据源特定数据类型的列（例如，SQL_LONGVARBINARY或SQL_LONGVARCHAR类型的参数）。 **SQLPutData**支持绑定到 Unicode C 数据类型，即使基础驱动程序不支持 Unicode 数据也是如此。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *数据Ptr*  
 [输入]指向包含参数或列的实际数据的缓冲区的指针。 数据必须位于**SQLBind参数***的值类型*参数（用于参数数据）或**SQLBindCol** *的目标类型*参数（用于列数据）中指定的 C 数据类型中。  
  
 StrLen_or_Ind   
 [输入]\**数据 Ptr*的长度 。 指定调用**SQLPutData**中发送的数据量。 给定参数或列的每个调用都会更改数据量。 *除非满足*以下条件之一，否则将忽略StrLen_or_Ind：  
  
-   *StrLen_or_Ind*是SQL_NTS、SQL_NULL_DATA或SQL_DEFAULT_PARAM。  
  
-   **在 SQLBind 参数**或**SQLBindCol**中指定的 C 数据类型SQL_C_CHAR或SQL_C_BINARY。  
  
-   C 数据类型SQL_C_DEFAULT，指定 SQL 数据类型的默认 C 数据类型为SQL_C_CHAR或SQL_C_BINARY。  
  
 对于所有其他类型的 C 数据，如果*StrLen_or_Ind*不是SQL_NULL_DATA或SQL_DEFAULT_PARAM，则驱动程序假定\**DataPtr*缓冲区的大小是使用*ValueType*或*TargetType*指定的 C 数据类型的大小，并发送整个数据值。 有关详细信息，请参阅在附录 D：数据类型中[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLPutData**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLPutData**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|为输出参数返回的字符串或二进制数据导致非空白字符或非 NULL 二进制数据的截断。 如果它是一个字符串值，它是右截断的。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|绑定参数的**SQLBind 参数**中*的值类型*参数标识的数据值无法转换为**SQLBind 参数**中的*参数类型*参数标识的数据类型。|  
|07S01|默认参数使用无效|使用**SQLBind 参数**设置的参数值SQL_DEFAULT_PARAM，并且相应的参数没有默认值。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|22001|字符串数据，右截断|将字符或二进制值分配给列会导致非空白（字符）或非空（二进制）字符或字节的截断。<br /><br /> **SQLGetInfo**中的SQL_NEED_LONG_DATA_LEN信息类型为"Y"，对于长参数（数据类型为SQL_LONGVARCHAR、SQL_LONGVARBINARY或长数据源特定数据类型）发送的数据比**在 SQLBind 参数**中*StrLen_or_IndPtr参数中*指定的数据多。<br /><br /> **SQLGetInfo**中的SQL_NEED_LONG_DATA_LEN信息类型为"Y"，对于长列（数据类型为SQL_LONGVARCHAR、SQL_LONGVARBINARY或长数据源特定数据类型）发送的数据比在长度缓冲区中指定的数据多，该长度缓冲区对应于使用**SQLBulk 操作**添加或更新或使用**SQLSetPos**更新的一行数据中的列。|  
|22003|数值超范围|为绑定数值参数或列发送的数据导致在分配给关联的表列时，将数字的整个部分（而不是小数）被截断。<br /><br /> 为一个或多个输入/输出或输出参数返回数值（作为数字或字符串）将导致数字的整个（而不是小数）部分被截断。|  
|22007|无效日期时间格式|为绑定到日期、时间或时间戳结构的参数或列发送的数据分别为无效的日期、时间或时间戳。<br /><br /> 输入/输出或输出参数绑定到日期、时间或时间戳 C 结构，返回参数中的值分别为无效日期、时间或时间戳。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|22008|日期时间字段溢出|为输入/输出或输出参数计算的 datetime 表达式会导致日期、时间或时间戳 C 结构无效。|  
|22012|除零|为输入/输出或输出参数计算的算术表达式导致除以零。|  
|22015|间隔字段溢出|为精确数字或间隔列或参数发送到间隔 SQL 数据类型的数据会导致重要数字丢失。<br /><br /> 发送具有多个字段的间隔列或参数的数据，转换为数字数据类型，并且在数字数据类型中没有表示形式。<br /><br /> 为列或参数数据发送的数据已分配给间隔 SQL 类型，并且间隔 SQL 类型中没有 C 类型的值表示形式。<br /><br /> 为精确数字或间隔 C 列或参数发送到间隔 C 类型的数据导致重要数字丢失。<br /><br /> 为列或参数数据发送的数据分配给间隔 C 结构，并且间隔数据结构中没有数据的表示形式。|  
|22018|强制转换规范的无效字符值|C 类型是精确或近似的数字、日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;列或参数中的值不是绑定 C 类型的有效文本。<br /><br /> SQL 类型是精确或近似的数字、日期时间或间隔数据类型;C 类型为SQL_C_CHAR;列或参数中的值不是绑定 SQL 类型的有效文本。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY009|无效使用空指针|（DM） 参数*DataPtr*是一个空指针，并且*参数StrLen_or_Ind*不是 0、SQL_DEFAULT_PARAM 或SQL_NULL_DATA。|  
|HY010|函数序列错误|（DM） 以前的函数调用不是对**SQLPutData**或**SQLParamData**的调用。<br /><br /> （DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用 SQLPutData 函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY019|分段发送的非字符和非二进制数据|**SQLPutData**被多次调用用于参数或列，它不用于将字符 C 数据发送到具有字符、二进制或数据源特定数据类型的列，或将二进制 C 数据发送到具有字符、二进制或数据源特定数据类型的列。|  
|HY020|尝试串联空值|**SQLPutData**自返回SQL_NEED_DATA的调用以来多次调用，并在其中一个调用中 *，StrLen_or_Ind*参数包含SQL_NULL_DATA或SQL_DEFAULT_PARAM。|  
|HY090|无效的字符串或缓冲区长度|参数*DataPtr*不是空指针 *，StrLen_or_Ind*参数小于 0，但不等于SQL_NTS或SQL_NULL_DATA。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
 如果在 SQL 语句中为参数发送数据时调用**SQLPutData，** 它可以返回调用执行语句 **（SQLExecute**或**SQLExecDirect**） 的函数可以返回的任何 SQLSTATE。 如果在发送使用**SQLBulk 操作**更新或添加的列的数据或使用**SQLSetPos**更新时调用它，则可以返回**SQLBulk 操作**或**SQLSetPos**可以返回的任何 SQLSTATE。  
  
## <a name="comments"></a>注释  
 **SQLPutData**可以调用提供执行时的数据，用于两个用途：参数数据用于 SQLExecute 或**SQLExecDirect**的**SQLExecDirect**调用，或者当对**SQLBulk 操作**的调用更新或添加行或通过调用**SQLSetPos**更新时使用的列数据。  
  
 当应用程序调用**SQLParamData**以确定它应该发送哪些数据时，驱动程序将返回一个指示器，应用程序可以使用该指示器来确定要发送的参数数据或可以找到列数据的位置。 它还返回SQL_NEED_DATA，这是应用程序应调用**SQLPutData**发送数据的指示器。 在**SQLPutData**的*DataPtr*参数中，应用程序传递指向包含参数或列的实际数据的缓冲区的指针。  
  
 当驱动程序返回**SQLPutData**SQL_SUCCESS 时，应用程序将再次调用**SQLParamData。** 如果需要发送更多数据 **，SQLParamData**将返回SQL_NEED_DATA，在这种情况下，应用程序将再次调用**SQLPutData。** 如果已发送所有执行数据，它将返回SQL_SUCCESS。 然后，应用程序再次调用**SQLParamData。** 如果驱动程序返回SQL_NEED_DATA和*\*ValuePtrPtr*中的另一个指标，则需要另一个参数或列的数据，并且再次调用**SQLPutData。** 如果驱动程序返回SQL_SUCCESS，则已发送所有执行时的数据数据，并可以执行 SQL 语句，也可以处理**SQLBulk 操作**或**SQLSetPos**调用。  
  
 有关如何在语句执行时传递数据执行参数数据的详细信息，请参阅[SQLBind 参数](../../../odbc/reference/syntax/sqlbindparameter-function.md)中的"传递参数值"和["发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)"。 有关如何更新或添加数据执行列数据的详细信息，请参阅 SQLSetPos 中的"使用[SQLSetPos"](../../../odbc/reference/syntax/sqlsetpos-function.md)部分[、SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)中的"使用书签执行批量更新"以及[长数据和 SQLSetPos 和 SQLBulk 操作](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
> [!NOTE]  
>  应用程序只能将字符 C 数据发送到具有字符、二进制或数据源特定数据类型的列，或者将二进制 C 数据发送到具有字符、二进制或数据源特定数据类型的列时，才能使用**SQLPutData**以零件发送数据。 如果在任何其他条件下多次调用**SQLPutData，** 它将返回SQL_ERROR和 SQLSTATE HY019（以件形式发送的非字符和非二进制数据）。  
  
## <a name="example"></a>示例  
 下面的示例假定一个数据源名称称为 Test。 关联的数据库应具有可以创建的表，如下所示：  
  
```sql  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到参数|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行准备好的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回下一个参数以发送数据|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
