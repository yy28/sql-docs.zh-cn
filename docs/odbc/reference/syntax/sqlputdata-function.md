---
title: SQLPutData 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f91799e5d484a763c23fcc132232a8a35fc6152c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63186111"
---
# <a name="sqlputdata-function"></a>SQLPutData 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLPutData** ，应用程序可以将参数或列的数据发送到在语句执行时驱动程序。 此函数可用于将部分中的字符或二进制数据值发送到字符、 二进制或数据源特定的数据类型 （例如，SQL_LONGVARBINARY 或 SQL_LONGVARCHAR 类型参数） 的列。 **SQLPutData**支持绑定到 Unicode 的 C 数据类型，即使基础驱动程序不支持 Unicode 数据。  
  
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
 [输入]指向包含参数或列的实际数据的缓冲区的指针。 中指定的 C 数据类型必须是数据*ValueType*的参数**SQLBindParameter** （适用于参数数据） 或*TargetType*自变量的**SQLBindCol** （适用于列数据）。  
  
 *StrLen_or_Ind*  
 [输入]长度\* *DataPtr*。 指定对的调用中发送的数据量**SQLPutData**。 数据量可以随每个调用中给定的参数或列。 *StrLen_or_Ind*将忽略未满足以下条件之一：  
  
-   *StrLen_or_Ind*是 SQL_NTS、 SQL_NULL_DATA 或 SQL_DEFAULT_PARAM。  
  
-   中指定的 C 数据类型**SQLBindParameter**或**SQLBindCol**为 SQL_C_CHAR 或 SQL_C_BINARY。  
  
-   C 数据类型为 SQL_C_DEFAULT，并且指定 SQL 数据类型的默认 C 数据类型为 SQL_C_CHAR 或 SQL_C_BINARY。  
  
 对于所有其他类型的 C 数据，如果*StrLen_or_Ind*不是 SQL_NULL_DATA 或 SQL_DEFAULT_PARAM，驱动程序假定的大小\* *DataPtr*缓冲区是指定的 C 数据类型的大小与*ValueType*或*TargetType* ，并将发送整个数据值。 有关详细信息，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)中附录 d:数据类型。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLPutData**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLPutData** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|字符串或二进制数据返回为输出参数时截断了非空白字符或非 NULL 的二进制数据。 如果它是一个字符串值，它是右侧被截断。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|标识的数据值*ValueType*中的参数**SQLBindParameter**无法为数据类型由标识转换绑定的参数为*ParameterType*中的参数**SQLBindParameter**。|  
|07S01|默认参数的使用无效|参数值，设置**SQLBindParameter**、 是 SQL_DEFAULT_PARAM，并且相应参数没有默认值。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|22001|字符串数据，右截断|字符或二进制值的列分配导致非空白 （字符） 或非 null （二进制） 字符或字节数的截断。<br /><br /> 中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**为"Y"，而且更多的数据已发送 （数据类型为 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源特定的数据类型） 的长参数不是指定了与*StrLen_or_IndPtr*中的参数**SQLBindParameter**。<br /><br /> 中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**为"Y"，而且比中指定了更多的数据已发送长列 （数据类型为 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的长整型数据源特定的数据类型）对应于已添加或使用更新的数据行中的列长度的缓冲区**SQLBulkOperations**或更新，它**SQLSetPos**。|  
|22003|数值超出范围|数据将发送有关绑定的数值参数或列导致数字被截断时分配给关联的表的列的整个 （而不是小数） 部分。<br /><br /> 返回一个数字值 （数值或字符串） 的一个或多个输入/输出参数或输出参数将导致要截断的数字的整个 （而不是小数） 部分。|  
|22007|日期时间格式无效|发送参数或已绑定到日期、 时间或时间戳结构的列的数据时，分别，无效的日期、 时间戳。<br /><br /> 输入/输出或输出参数绑定到日期、 时间或时间戳 C 结构，返回的参数中的值时，分别，无效的日期、 时间戳。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22008|日期时间字段溢出|日期时间表达式计算的输入/输出或输出参数导致了日期、 时间或时间戳 C 结构无效。|  
|22012|被零除|算术表达式计算的输入/输出或输出参数导致除零。|  
|22015|间隔字段溢出|为确切的数值或时间间隔列发送数据或间隔 SQL 数据类型的参数时导致重要数字丢失。<br /><br /> 数据已发送间隔列或多个字段参数、 已转换为数值数据类型，和的数值数据类型中有没有表示形式。<br /><br /> 列发送数据或参数数据分配到的时间间隔的 SQL 类型，并且没有在时间间隔内 SQL 类型的 C 类型的值没有表示形式。<br /><br /> 精确数字或时间间隔 C 列或参数 C 间隔类型发送的数据时导致重要数字丢失。<br /><br /> 列发送数据或参数数据已分配给一个 C 间隔结构，没有间隔数据结构中的数据的表示形式。|  
|22018|转换指定的字符值无效|C 类型为精确或近似数值、 日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;和中的列或参数的值不是有效的绑定 C 类型的文本。<br /><br /> SQL 类型是精确或近似数值、 日期时间或间隔数据类型;C 类型为 SQL_C_CHAR;和中的列或参数的值不是绑定的 SQL 类型的有效文本。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY009|使用空指针无效|(DM) 参数*DataPtr*是空指针和参数*StrLen_or_Ind*不是 0，SQL_DEFAULT_PARAM 或 SQL_NULL_DATA。|  
|HY010|函数序列错误|(DM) 以前的函数调用不是调用**SQLPutData**或**SQLParamData**。<br /><br /> (DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行调用 SQLPutData 函数时。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY019|分段发送非字符和非二进制数据|**SQLPutData**已被调用超过一次参数或列中，并且从未被使用它将字符 C 数据发送到包含的字符、 二进制或数据源特定的数据类型的列，或将二进制 C 数据发送到具有一个字符的列二进制文件或数据源特定的数据类型。|  
|HY020|尝试连接 null 值|**SQLPutData**以来的调用返回 SQL_NEED_DATA，和一个这些调用中多次调用*StrLen_or_Ind*参数包含 SQL_NULL_DATA 或 SQL_DEFAULT_PARAM。|  
|HY090|字符串或缓冲区长度无效|自变量*DataPtr*不是 null 指针和参数*StrLen_or_Ind*小于 0，但不是等于 SQL_NTS 或 SQL_NULL_DATA。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
 如果**SQLPutData**调用时发送参数数据中的 SQL 语句，它可以返回任何可由函数调用以执行该语句返回的 SQLSTATE (**SQLExecute**或**SQLExecDirect**)。 如果发送数据的列时调用正在进行更新或添加具有**SQLBulkOperations**或使用更新**SQLSetPos**，它可以返回任何可由返回的 SQLSTATE **SQLBulkOperations**或**SQLSetPos**。  
  
## <a name="comments"></a>注释  
 **SQLPutData**可以调用来提供这两种用法的数据执行时数据： 对的调用中使用的参数数据**SQLExecute**或**SQLExecDirect**，或更新行时使用的列数据或通过调用添加**SQLBulkOperations**或通过调用更新**SQLSetPos**。  
  
 当应用程序调用**SQLParamData**来确定哪些数据应发送，该驱动程序返回的应用程序可用于确定要发送的参数数据或列数据所在的指示器。 它还会返回 SQL_NEED_DATA，这是一个指示符，则应调用的应用程序**SQLPutData**发送数据。 在中*DataPtr*自变量**SQLPutData**，应用程序将指针传递到包含实际数据的参数或列的缓冲区。  
  
 当驱动程序返回 SQL_SUCCESS 有关**SQLPutData**，应用程序调用**SQLParamData**试。 **SQLParamData**返回 sql_need_data，这更多数据需要发送，如果在此情况下应用程序调用**SQLPutData**试。 如果已发送所有数据执行时数据，它将返回 SQL_SUCCESS。 然后，应用程序调用**SQLParamData**试。 如果驱动程序将返回 SQL_NEED_DATA 和中的另一个指示器 *\*ValuePtrPtr*，它需要另一个参数或列的数据并**SQLPutData**再次调用。 如果驱动程序将返回 SQL_SUCCESS，然后所有数据在执行发送数据，并可以执行 SQL 语句或**SQLBulkOperations**或**SQLSetPos**调用可以进行处理。  
  
 在语句执行时传递的数据在执行参数数据的详细信息，请参阅"传递参数值"中[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)并[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)。 有关如何执行时的数据列数据的详细信息更新或添加，请参阅"使用 SQLSetPos"一节中[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)，"执行大容量更新使用中的书签" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，和[Long 数据和 SQLSetPos 及 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
> [!NOTE]  
>  应用程序可以使用**SQLPutData**发送部分仅当将字符 C 数据发送到特定于源的数据类型为字符、 二进制文件或数据列，或将二进制 C 数据发送到具有二进制文件，一个字符的列中的数据特定于源的数据类型。 如果**SQLPutData**调用一次以上任何其他情况下，它将返回 SQL_ERROR 和 SQLSTATE hy019 分段 （分段发送非字符和非二进制数据）。  
  
## <a name="example"></a>示例  
 下面的示例假定名为 Test 的数据源名称。 关联的数据库应具有您可以创建，按如下所示的表：  
  
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
|返回下一个参数将数据发送用于|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
