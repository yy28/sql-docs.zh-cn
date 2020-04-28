---
title: 使用 SQLGetData 检索输出参数 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c96a3f9fc81d081ce16fe8e75746aafe8962fd0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294587"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>使用 SQLGetData 检索输出参数
在 ODBC 3.8 之前，应用程序只能检索带有绑定输出缓冲区的查询的输出参数。 但是，如果参数值的大小非常大（例如，大图像），则很难分配非常大的缓冲区。 ODBC 3.8 引入了一种新方法来检索部分中的输出参数。 现在，应用程序可以多次调用带有小缓冲区的**SQLGetData** ，以检索大型参数值。 这类似于检索大列数据。  
  
 若要绑定要在部分中检索的输出参数或输入/输出参数，请调用**SQLBindParameter** ，并将*InputOutputType*参数设置为 SQL_PARAM_OUTPUT_STREAM 或 SQL_PARAM_INPUT_OUTPUT_STREAM。 使用 SQL_PARAM_INPUT_OUTPUT_STREAM，应用程序可以使用**SQLPutData**将数据输入到参数中，然后使用**SQLGetData**检索 OUTPUT 参数。 输入数据必须在执行时数据（DAE）形式中，使用**SQLPutData**而不是将其绑定到预分配的缓冲区。  
  
 此功能可由 ODBC 3.8 应用程序或重新编译的 ODBC 1.x 和 ODBC 2.x 应用程序使用，这些应用程序必须具有支持使用**SQLGetData**和 Odbc 3.8 驱动程序管理器检索输出参数的 ODBC 3.8 驱动程序。 有关如何启用较旧的应用程序以使用新的 ODBC 功能的信息，请参阅[兼容性矩阵](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
## <a name="usage-example"></a>用法示例  
 例如，请考虑执行存储过程 **{CALL sp_f （?,?）}**，其中两个参数均绑定为 SQL_PARAM_OUTPUT_STREAM，存储过程不返回结果集（稍后在本主题中，你将看到更复杂的方案）：  
  
1.  对于每个参数，请调用**SQLBindParameter** ，将*InputOutputType*设置为 SQL_PARAM_OUTPUT_STREAM，并将*ParameterValuePtr*设置为标记，如参数号、指向数据的指针或指向应用程序用于绑定输入参数的结构的指针。 此示例将使用参数序号作为标记。  
  
2.  执行具有**SQLExecDirect**或**SQLExecute**的查询。 将返回 SQL_PARAM_DATA_AVAILABLE，指示有可用于检索的流式处理输出参数。  
  
3.  调用**SQLParamData**可获取可用于检索的参数。 **SQLParamData**将返回 SQL_PARAM_DATA_AVAILABLE，其中包含第一个可用参数的标记，该参数在**SQLBindParameter**中设置（步骤1）。 在*ValuePtrPtr*指向的缓冲区中返回该令牌。  
  
4.  使用参数*列*_or\_调用**SQLGetData** *Param_Num*设置为参数序号，以检索第一个可用参数的数据。 如果**SQLGetData**返回 SQL_SUCCESS_WITH_INFO 和 SQLState 01004 （数据已截断），并且该类型在客户端和服务器上都是可变的，则从第一个可用参数检索更多数据。 你可以继续调用**SQLGetData** ，直到它返回不同**SQLState**SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
5.  重复步骤3和步骤4以检索当前参数。  
  
6.  再次调用**SQLParamData** 。 如果它返回除 SQL_PARAM_DATA_AVAILABLE 之外的任何内容，则没有更多要检索的流式处理参数数据，返回代码将是执行的下一条语句的返回代码。  
  
7.  调用**SQLMoreResults**以处理下一组参数，直到其返回 SQL_NO_DATA。 如果 SQL_ATTR_PARAMSET_SIZE 的语句属性设置为1，则**SQLMoreResults**将在此示例中返回 SQL_NO_DATA。 否则， **SQLMoreResults**将返回 SQL_PARAM_DATA_AVAILABLE，以指示有可用于要检索的下一组参数的流式处理输出参数。  
  
 类似于 DAE 输入参数，在**SQLBindParameter**中的参数*ParameterValuePtr*中使用的令牌（步骤1）可以是指向应用程序数据结构的指针，该结构包含参数的序号和应用程序特定的信息（如有必要）。  
  
 返回的流式处理输出参数或输入/输出参数的顺序是特定于驱动程序的，可能并不总是与查询中指定的顺序相同。  
  
 如果应用程序在步骤4中未调用**SQLGetData** ，则会丢弃参数值。 同样，如果应用程序在**SQLGetData**读取所有参数值之前调用**SQLParamData** ，则会丢弃该值的其余部分，应用程序可以处理下一个参数。  
  
 如果应用程序在处理所有流式处理输出参数之前调用**SQLMoreResults** （**SQLParamData**仍返回 SQL_PARAM_DATA_AVAILABLE），则丢弃所有剩余的参数。 同样，如果应用程序在**SQLGetData**读取所有参数值之前调用**SQLMoreResults** ，则会丢弃该值的其余部分和所有剩余参数，应用程序可以继续处理下一个参数集。  
  
 请注意，应用程序可以在**SQLBindParameter**和**SQLGetData**中指定 C 数据类型。 用**SQLGetData**指定的 c 数据类型将重写**SQLBindParameter**中指定的 c 数据类型，除非在**SQLGetData**中指定的 c 数据类型 SQL_APD_TYPE。  
  
 尽管输出参数的数据类型为 BLOB 类型时，流式处理输出参数更为有用，但也可以将此功能与任何数据类型一起使用。 流式处理输出参数支持的数据类型是在驱动程序中指定的。  
  
 如果有 SQL_PARAM_INPUT_OUTPUT_STREAM 参数要处理，则**SQLExecute**或**SQLExecDirect**将首先返回 SQL_NEED_DATA。 应用程序可以调用**SQLParamData**和**SQLPUTDATA**来发送 DAE 参数数据。 处理所有 DAE 输入参数时， **SQLParamData**将返回 SQL_PARAM_DATA_AVAILABLE 以指示流式输出参数可用。  
  
 当存在要处理的流式处理输出参数和绑定输出参数时，驱动程序将确定处理输出参数的顺序。 因此，如果将输出参数绑定到缓冲区（将**SQLBindParameter**参数*InputOutputType*设置为 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT），则在**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 之前，可能不会填充缓冲区。 仅当**SQLParamData**返回了所有流式处理输出参数之后 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 之后，应用程序才应读取绑定缓冲区。  
  
 除流式处理输出参数外，数据源还可以返回警告和结果集。 通常，通过调用**SQLMoreResults**，与流式处理的输出参数分别处理警告和结果集。 在处理流式处理输出参数之前处理警告和结果集。  
  
 下表描述了发送到服务器的单个命令的不同方案，以及应用程序的工作原理。  
  
|方案|从 SQLExecute 或 SQLExecDirect 返回值|下一步操作|  
|--------------|---------------------------------------------------|---------------------|  
|数据仅包含流式输出参数|SQL_PARAM_DATA_AVAILABLE|使用**SQLParamData**和**SQLGetData**检索流式处理的输出参数。|  
|数据包括结果集和流式输出参数|SQL_SUCCESS|检索包含**SQLBindCol**和**SQLGetData**的结果集。<br /><br /> 调用**SQLMoreResults**开始处理流式输出参数。 它应返回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**检索流式处理的输出参数。|  
|数据包括警告消息和流式输出参数|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**处理警告消息。<br /><br /> 调用**SQLMoreResults**开始处理流式输出参数。 它应返回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**检索流式处理的输出参数。|  
|数据包括警告消息、结果集和流式输出参数|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**处理警告消息。 然后调用**SQLMoreResults** ，开始处理结果集。<br /><br /> 使用**SQLBindCol**和**SQLGetData**检索结果集。<br /><br /> 调用**SQLMoreResults**开始处理流式输出参数。 **SQLMoreResults**应返回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**检索流式处理的输出参数。|  
|使用 DAE 输入参数（例如，流输入/输出（DAE）参数）进行查询|SQL NEED_DATA|调用**SQLParamData**和**SQLPUTDATA**以发送 DAE 输入参数数据。<br /><br /> 处理完所有 DAE 输入参数后， **SQLParamData**可以返回**SQLExecute**和**SQLExecDirect**可以返回的任何返回代码。 然后，可以应用此表中的事例。<br /><br /> 如果 SQL_PARAM_DATA_AVAILABLE 返回代码，则流输出参数可用。 应用程序必须再次调用**SQLParamData**来检索流式处理输出参数的令牌，如此表的第一行中所述。<br /><br /> 如果返回代码为 SQL_SUCCESS，则可能是要处理的结果集或处理已完成。<br /><br /> 如果 SQL_SUCCESS_WITH_INFO 返回代码，则会发出警告消息。|  
  
 在**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults**返回 SQL_PARAM_DATA_AVAILABLE 后，如果应用程序调用的函数不在以下列表中，则会导致函数序列错误：  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr**SQLGetEnvAttr / **SQLGetDescField**SQLGetDescField / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** （带有语句句柄）  
  
-   **SQLFreeStmt** （选项为 = SQL_CLOSE、SQL_DROP 或 SQL_UNBIND）  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** （带有 HandleType = SQL_HANDLE_STMT）  
  
-   **SQLGetStmtAttr**  
  
 应用程序仍可使用**SQLSetDescField**或**SQLSetDescRec**来设置绑定信息。 字段映射不会更改。 但是，描述符中的字段可能返回新值。 例如，SQL_DESC_PARAMETER_TYPE 可能返回 SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM。  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>使用方案：从结果集检索部件中的图像  
 当存储过程返回的结果集包含一个与图像有关的元数据，并且该图像在大的输出参数中返回时，可以使用**SQLGetData**在部分中获取数据。  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>使用方案：发送和接收大型对象作为流式输入/输出参数  
 当存储过程将大型对象作为输入/输出参数传递时，可以使用**SQLGetData**在部分中获取和发送数据，并将值流式传输到数据库或从数据库流式传输。 无需将所有数据存储在内存中。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [语句参数](../../../odbc/reference/develop-app/statement-parameters.md)
