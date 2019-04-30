---
title: 正在检索输出参数，使用 SQLGetData |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ebb09b3118c2d16041d4ca60bf738d0fda561346
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199083"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>使用 SQLGetData 检索输出参数
ODBC 3.8 之前应用程序可以仅检索具有绑定的输出缓冲区的查询的输出参数。 但是，很难参数值的大小非常大 （例如，一个大图像） 时分配非常大的缓冲区。 ODBC 3.8 引入了检索输出参数部分中的新方法。 应用程序现在可以调用**SQLGetData**用小缓冲区多次来检索大型参数值。 这是类似于检索大型列数据。  
  
 若要将绑定的输出参数或输入/输出参数来检索部分中，调用**SQLBindParameter**与*InputOutputType*参数设置为 SQL_PARAM_OUTPUT_STREAM 或 SQL_PARAM_INPUT_OUTPUT_STREAM。 与 SQL_PARAM_INPUT_OUTPUT_STREAM，应用程序可以使用**SQLPutData**参数中输入数据，然后使用**SQLGetData**检索输出参数。 输入的数据必须在执行时数据-(DAE) 窗体中，使用**SQLPutData**而不是绑定到的预先分配的缓冲区。  
  
 此功能可由 ODBC 3.8 应用程序或重新编译 ODBC 3.x 和 ODBC 2.x 应用程序，以及这些应用程序必须有支持检索输出参数使用的 ODBC 3.8 驱动程序**SQLGetData**和 ODBC 3.8 驱动程序管理器。 有关如何启用旧的应用程序使用 ODBC 的新功能的信息，请参阅[兼容性矩阵](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
## <a name="usage-example"></a>用法示例  
 例如，请考虑执行存储的过程， **{调用 sp_f(?,?)}**，其中两个参数绑定为 SQL_PARAM_OUTPUT_STREAM，而存储的过程未返回结果集 （本主题中稍后您会发现更复杂的方案）：  
  
1.  对于每个参数，调用**SQLBindParameter**与*InputOutputType*设置为 SQL_PARAM_OUTPUT_STREAM 并*ParameterValuePtr*设置为的令牌，如参数数目指向数据的指针或指向应用程序用于绑定输入的参数的结构的指针。 此示例将使用的标记为参数序号。  
  
2.  执行与查询**SQLExecDirect**或**SQLExecute**。 将返回 SQL_PARAM_DATA_AVAILABLE，指示可检索用于流式处理的输出参数。  
  
3.  调用**SQLParamData**若要获取可供检索的参数。 **SQLParamData**将与令牌中设置的第一个可用参数返回 SQL_PARAM_DATA_AVAILABLE **SQLBindParameter** （步骤 1）。 在缓冲区中返回的标记的*ValuePtrPtr*指向。  
  
4.  调用**SQLGetData**带有参数*Col*_or\_*Param_Num*设置为参数序号以检索第一个可用参数的数据。 如果**SQLGetData**返回 SQL_SUCCESS_WITH_INFO 和 SQLState 01004 （数据被截断） 和类型为客户端和服务器上的可变长度，则更多的数据检索的第一个可用参数。 你可以继续调用**SQLGetData**直到其与其他返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO **SQLState**。  
  
5.  重复步骤 3 和步骤 4，以检索当前参数。  
  
6.  调用**SQLParamData**试。 如果它返回 SQL_PARAM_DATA_AVAILABLE 以外，没有更多流式处理的参数数据检索，并返回代码将执行的下一个语句的返回代码。  
  
7.  调用**SQLMoreResults**进行处理下一步的参数集，直到其返回 sql_no_data 为止。 **SQLMoreResults**将语句特性则 SQL_ATTR_PARAMSET_SIZE 设置为 1 在此示例中返回 sql_no_data 为止。 否则为**SQLMoreResults**将返回 SQL_PARAM_DATA_AVAILABLE 指示可用于下一组参数来检索经过流处理的输出参数。  
  
 参数中使用类似于 DAE 输入参数，该令牌*ParameterValuePtr*中**SQLBindParameter** （步骤 1） 可以是指向应用程序数据结构，其中包含的指针序号对参数和特定于应用程序的详细信息，如有必要。  
  
 返回经过流处理的输出或输入/输出参数的顺序是特定的驱动程序，可能无法始终在查询中指定的顺序相同。  
  
 如果应用程序不会调用**SQLGetData**在步骤 4 中，参数值将被丢弃。 同样，如果应用程序调用**SQLParamData**之前所有参数的值由都读取**SQLGetData**、 值的其余部分将被放弃，和应用程序可以处理下一步参数。  
  
 如果应用程序调用**SQLMoreResults**经过流处理的所有输出参数的都处理 (**SQLParamData**仍返回 SQL_PARAM_DATA_AVAILABLE)，所有剩余的参数将被丢弃。 同样，如果应用程序调用**SQLMoreResults**之前所有参数的值由都读取**SQLGetData**，其余的值、 所有剩余参数将被丢弃，和应用程序可以继续处理下一步的参数集。  
  
 请注意，应用程序可以在这种指定的 C 数据类型**SQLBindParameter**并**SQLGetData**。 使用指定的 C 数据类型**SQLGetData**重写中指定的 C 数据类型**SQLBindParameter**除非中指定的 C 数据类型，否则**SQLGetData**是 SQL_APD_TYPE。  
  
 尽管 BLOB 类型的输出参数的数据类型时，流式处理的输出参数是更有用，但此功能还可与任何数据类型。 支持流的输出参数的数据类型指定驱动程序中。  
  
 如果要处理的 SQL_PARAM_INPUT_OUTPUT_STREAM 参数**SQLExecute**或**SQLExecDirect**将先返回 SQL_NEED_DATA。 应用程序可以调用**SQLParamData**并**SQLPutData**发送 DAE 参数数据。 当处理所有 DAE 输入的参数时， **SQLParamData**返回 SQL_PARAM_DATA_AVAILABLE 以指示可以使用流式处理的输出参数。  
  
 当存在已流式传输输出参数和绑定的输出参数，以进行处理，该驱动程序将确定处理输出参数的顺序。 因此，如果输出参数绑定到一个缓冲区 ( **SQLBindParameter**参数*InputOutputType*设置为 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT)，该缓冲区可能不会填充直到**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。 应用程序应读取绑定之后才缓冲**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 毕竟流式输出参数进行处理。  
  
 数据源可以返回的警告和结果集，此外到流式处理的输出参数。 一般情况下，警告和结果集单独处理从流式处理的输出参数通过调用**SQLMoreResults**。 处理警告和结果集处理经过流处理的输出参数之前。  
  
 下表描述单个命令发送到服务器和应用程序的工作方式的不同方案。  
  
|应用场景|从 SQLExecute 或 SQLExecDirect 的返回值|下一步操作|  
|--------------|---------------------------------------------------|---------------------|  
|数据仅包含流的输出参数|SQL_PARAM_DATA_AVAILABLE|使用**SQLParamData**并**SQLGetData**检索流式处理的输出参数。|  
|数据包括结果集，流式输出参数|SQL_SUCCESS|检索结果集与**SQLBindCol**并**SQLGetData**。<br /><br /> 调用**SQLMoreResults**开始处理经过流处理的输出参数。 它应返回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**并**SQLGetData**检索流式处理的输出参数。|  
|数据包括一条警告消息，流式输出参数|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**并**SQLGetDiagField**处理警告消息。<br /><br /> 调用**SQLMoreResults**开始处理经过流处理的输出参数。 它应返回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**并**SQLGetData**检索流式处理的输出参数。|  
|数据包括一条警告消息、 结果集和流式输出参数|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**并**SQLGetDiagField**处理警告消息。 然后调用**SQLMoreResults**开始处理结果集。<br /><br /> 检索结果集与**SQLBindCol**并**SQLGetData**。<br /><br /> 调用**SQLMoreResults**开始处理经过流处理的输出参数。 **SQLMoreResults**应返回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**并**SQLGetData**检索流式处理的输出参数。|  
|查询使用 DAE 输入参数，例如，经过流处理的输入/输出 (DAE) 参数|SQL NEED_DATA|调用**SQLParamData**并**SQLPutData**发送 DAE 输入参数数据。<br /><br /> 所有 DAE 输入的参数的都处理后， **SQLParamData**任何返回代码，可以返回**SQLExecute**并**SQLExecDirect**可以返回。 然后可以应用此表中的情况。<br /><br /> 如果返回代码为 SQL_PARAM_DATA_AVAILABLE，可以使用流式处理的输出参数。 应用程序必须调用**SQLParamData**再次以检索流式处理的输出参数的令牌，此表的第一行中所述。<br /><br /> 如果返回代码为 SQL_SUCCESS，没有要处理的结果集，或处理已完成。<br /><br /> 如果返回代码，SQL_SUCCESS_WITH_INFO 有要处理的警告消息。|  
  
 之后**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**如果应用程序调用，将会导致返回 SQL_PARAM_DATA_AVAILABLE，函数序列错误以下列表中的函数：  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** （与语句句柄）  
  
-   **SQLFreeStmt** （选项 = SQL_CLOSE、 SQL_DROP 或 SQL_UNBIND）  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** （HandleType = SQL_HANDLE_STMT）  
  
-   **SQLGetStmtAttr**  
  
 应用程序仍可以使用**SQLSetDescField**或**SQLSetDescRec**若要设置的绑定信息。 字段映射将不会更改。 但是，描述符中的字段，可能会返回新值。 例如，SQL_DESC_PARAMETER_TYPE 可能会返回 SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM。  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>使用方案：从结果集中检索部分中的图像  
 **SQLGetData**可用于在部件中获取数据时存储的过程将返回包含有关某个映像的元数据的行的结果集和大型输出参数中返回图像。  
  
```  
// CREATE PROCEDURE SP_TestOutputPara  
//      @ID_of_picture   as int,  
//      @Picture         as varbinary(max) out  
// AS  
//     output the image data through streamed output parameter  
// GO  
BOOL displayPicture(SQLUINTEGER idOfPicture, SQLHSTMT hstmt) {  
   SQLLEN      lengthOfPicture;    // The actual length of the picture.  
   BYTE        smallBuffer[100];   // A very small buffer.  
   SQLRETURN   retcode, retcode2;  
  
   // Bind the first parameter (input parameter)  
   SQLBindParameter(  
         hstmt,  
         1,                         // The first parameter.   
         SQL_PARAM_INPUT,           // Input parameter: The ID_of_picture.  
         SQL_C_ULONG,               // The C Data Type.  
         SQL_INTEGER,               // The SQL Data Type.  
         0,                         // ColumnSize is ignored for integer.  
         0,                         // DecimalDigits is ignored for integer.  
         &idOfPicture,              // The Address of the buffer for the input parameter.  
         0,                         // BufferLength is ignored for integer.  
         NULL);                     // This is ignored for integer.  
  
   // Bind the streamed output parameter.  
   SQLBindParameter(  
         hstmt,   
         2,                         // The second parameter.  
         SQL_PARAM_OUTPUT_STREAM,   // A streamed output parameter.   
         SQL_C_BINARY,              // The C Data Type.    
         SQL_VARBINARY,             // The SQL Data Type.  
         0,                         // ColumnSize: The maximum size of varbinary(max).  
         0,                         // DecimalDigits is ignored for binary type.  
         (SQLPOINTER)2,             // ParameterValuePtr: An application-defined  
                                    // token (this will be returned from SQLParamData).  
                                    // In this example, we used the ordinal   
                                    // of the parameter.  
         0,                         // BufferLength is ignored for streamed output parameters.  
         &lengthOfPicture);         // StrLen_or_IndPtr: The status variable returned.   
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestOutputPara(?, ?)}", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Assume that the retrieved picture exists.  Use SQLBindCol or SQLGetData to retrieve the result-set.  
  
   // Process the result set and move to the streamed output parameters.  
   retcode = SQLMoreResults( hstmt );  
  
   // SQLGetData retrieves and displays the picture in parts.  
   // The streamed output parameter is available.  
   while (retcode == SQL_PARAM_DATA_AVAILABLE) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;      // #bytes remained  
      retcode = SQLParamData(hstmt, &token);   // returned token is 2 (according to the binding)  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         // A do-while loop retrieves the picture in parts.  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }  
  
   return TRUE;  
}  
```  
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>使用方案：发送和接收经过流处理的输入/输出参数作为大型对象  
 **SQLGetData**可以用于获取和存储的过程将作为输入/输出参数，流式处理与数据库的值传递大型对象时部分中的发送数据。 无需在内存中存储的所有数据。  
  
```  
// CREATE PROCEDURE SP_TestInOut  
//       @picture as varbinary(max) out  
// AS  
//    output the image data through output parameter   
// go  
  
BOOL displaySimilarPicture(BYTE* image, ULONG lengthOfImage, SQLHSTMT hstmt) {  
   BYTE smallBuffer[100];   // A very small buffer.  
   SQLRETURN retcode, retcode2;  
   SQLLEN statusOfPicture;  
  
   // First bind the parameters, before preparing the statement that binds the output streamed parameter.  
   SQLBindParameter(  
      hstmt,   
      1,                                 // The first parameter.  
      SQL_PARAM_INPUT_OUTPUT_STREAM,     // I/O-streamed parameter: The Picture.  
      SQL_C_BINARY,                      // The C Data Type.  
      SQL_VARBINARY,                     // The SQL Data Type.  
      0,                                 // ColumnSize: The maximum size of varbinary(max).  
      0,                                 // DecimalDigits is ignored.   
      (SQLPOINTER)1,                     // An application defined token.   
      0,                                 // BufferLength is ignored for streamed I/O parameters.  
      &statusOfPicture);                 // The status variable.  
  
   statusOfPicture = SQL_DATA_AT_EXEC;   // Input data in parts (DAE parameter at input).  
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestInOut(?) }", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Execute the statement.  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   if ( retcode == SQL_NEED_DATA ) {  
      // Use SQLParamData to loop through DAE input parameters.  For  
      // each, use SQLPutData to send the data to database in parts.  
  
      // This example uses an I/O parameter with streamed output.  
      // Therefore, the last call to SQLParamData should return  
      // SQL_PARAM_DATA_AVAILABLE to indicate the end of the input phrase   
      // and report that a streamed output parameter is available.  
  
      // Assume retcode is set to the return value of the last call to  
      // SQLParamData, which is equal to SQL_PARAM_DATA_AVAILABLE.  
   }  
  
   // Start processing the streamed output parameters.  
   while ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;     // #bytes remained  
      retcode = SQLParamData(hstmt, &token);  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }   
  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [语句参数](../../../odbc/reference/develop-app/statement-parameters.md)
