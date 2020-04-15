---
title: 使用 SQLGetData 检索输出参数 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294587"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>使用 SQLGetData 检索输出参数
在 ODBC 3.8 之前，应用程序只能检索具有绑定输出缓冲区的查询的输出参数。 但是，当参数值的大小非常大（例如，大图像）时，很难分配非常大的缓冲区。 ODBC 3.8 引入了一种检索零件输出参数的新方法。 应用程序现在可以多次使用小缓冲区调用**SQLGetData**来检索大型参数值。 这类似于检索大型列数据。  
  
 要绑定要在零件中检索的输出参数或输入/输出参数，请调用**SQLBind 参数**，并将*输入输出类型*参数设置为SQL_PARAM_OUTPUT_STREAM或SQL_PARAM_INPUT_OUTPUT_STREAM。 使用SQL_PARAM_INPUT_OUTPUT_STREAM，应用程序可以使用**SQLPutData**将数据输入到参数中，然后使用**SQLGetData**检索输出参数。 输入数据必须采用执行时的数据 （DAE） 窗体，使用**SQLPutData**而不是将其绑定到预分配的缓冲区。  
  
 此功能可用于 ODBC 3.8 应用程序或重新编译的 ODBC 3.x 和 ODBC 2.x 应用程序，并且这些应用程序必须具有一个 ODBC 3.8 驱动程序，支持使用**SQLGetData**和 ODBC 3.8 驱动程序管理器检索输出参数。 有关如何启用较旧的应用程序使用新的 ODBC 功能的信息，请参阅[兼容性矩阵](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
## <a name="usage-example"></a>用法示例  
 例如，请考虑执行存储过程 **[CALL sp_f（?,?）]，** 其中两个参数都绑定为SQL_PARAM_OUTPUT_STREAM，并且存储过程不会返回任何结果集（在本主题的后面部分，您将发现更复杂的方案）：  
  
1.  对于每个参数，调用**SQLBind参数**，其中*输入输出类型*设置为*SQL_PARAM_OUTPUT_STREAM，参数ValuePtr*设置为令牌，如参数编号、指向数据的指针或指向应用程序用于绑定输入参数的结构的指针。 此示例将使用参数代数作为令牌。  
  
2.  使用**SQLExecDirect**或**SQLExecute 执行**查询。 将返回SQL_PARAM_DATA_AVAILABLE，指示有流输出参数可供检索。  
  
3.  调用**SQLParamData**获取可供检索的参数。 **SQLParamData**将返回SQL_PARAM_DATA_AVAILABLE，该参数将在**SQLBind 参数**（步骤 1）中设置，该参数的令牌。 令牌在*ValuePtrPtr*指向的缓冲区中返回。  
  
4.  使用参数*Col*_or\_*Param_Num*将**SQLGetData**设置为参数 ddinal 以检索第一个可用参数的数据。 如果**SQLGetData**返回SQL_SUCCESS_WITH_INFO和 SQLState 01004（数据截断），并且该类型在客户端和服务器上都是可变长度，则从第一个可用参数中检索的数据更多。 您可以继续调用**SQLGetData，** 直到它返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO使用不同的**SQLState**。  
  
5.  重复步骤 3 和步骤 4 以检索当前参数。  
  
6.  再次调用**SQLParamData。** 如果它返回除SQL_PARAM_DATA_AVAILABLE以外的任何内容，则没有要检索的流式处理参数数据，并且返回代码将是执行的下一个语句的返回代码。  
  
7.  调用**SQLMore 结果**来处理下一组参数，直到返回SQL_NO_DATA。 如果语句属性SQL_ATTR_PARAMSET_SIZE设置为 1，**则 SQLMore 结果**将返回此示例中的SQL_NO_DATA。 否则 **，SQLMore结果**将返回SQL_PARAM_DATA_AVAILABLE，以指示有流输出参数可用于下一组要检索的参数。  
  
 与 DAE 输入参数类似 **，SQLBind参数**（步骤 1） 中参数*参数ValuePtr*中使用的令牌可以是指向应用程序数据结构的指针，该结构包含参数的表位和更多特定于应用程序的信息（如有必要）。  
  
 返回的流输出或输入/输出参数的顺序特定于驱动程序，可能并不总是与查询中指定的顺序相同。  
  
 如果应用程序在步骤 4 中不调用**SQLGetData，** 则将丢弃参数值。 同样，如果应用程序在 SQLGetData 读取所有参数值之前调用**SQLParamData，** 则将丢弃该值的其余部分，并且应用程序可以处理下一个参数。 **SQLParamData**  
  
 如果应用程序在处理所有流输出参数之前调用**SQLMore 结果****（SQLParamData**仍返回SQL_PARAM_DATA_AVAILABLE），则将丢弃所有剩余的参数。 同样，如果应用程序在**SQLGetData**读取所有参数值之前调用**SQLMore结果**，则将丢弃该值的剩余部分和所有剩余参数，并且应用程序可以继续处理下一个参数集。  
  
 请注意，应用程序可以在**SQLBind 参数**和**SQLGetData**中指定 C 数据类型。 使用**SQLGetData**指定的 C 数据类型覆盖**SQLBind 参数**中指定的 C 数据类型，除非**在 SQLGetData**中指定的 C 数据类型SQL_APD_TYPE。  
  
 尽管当输出参数的数据类型为 BLOB 类型时，流式输出参数更有用，但此功能也可以与任何数据类型一起使用。 流式输出参数支持的数据类型在驱动程序中指定。  
  
 如果有要处理SQL_PARAM_INPUT_OUTPUT_STREAM参数 **，SQLExecute**或**SQLExecDirect**将首先返回SQL_NEED_DATA。 应用程序可以调用**SQLParamData**和**SQLPutData**来发送 DAE 参数数据。 处理所有 DAE 输入参数时 **，SQLParamData**将返回SQL_PARAM_DATA_AVAILABLE以指示流输出参数可用。  
  
 当有要处理的流式输出参数和绑定输出参数时，驱动程序确定处理输出参数的顺序。 因此，如果输出参数绑定到缓冲区 **（SQLBind参数**参数*InputOutputType*设置为SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_OUTPUT），则在**SQLParamData**返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO之前可能无法填充缓冲区。 只有在**SQLParamData**返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO后，应用程序才能读取绑定缓冲区，该缓冲区是处理所有流输出参数之后。  
  
 数据源除了流式输出参数外，还可以返回警告和结果集。 通常，通过调用**SQLMoreResult，** 将警告和结果集与流式输出参数分开处理。 在处理流输出参数之前，处理警告和结果集。  
  
 下表描述了发送到服务器的单个命令的不同方案，以及应用程序应如何工作。  
  
|场景|从 SQLExecute 或 SQLExecDirect 返回值|下一步操作|  
|--------------|---------------------------------------------------|---------------------|  
|数据仅包括流输出参数|SQL_PARAM_DATA_AVAILABLE|使用**SQLParam 数据和** **SQLGetData**检索流式输出参数。|  
|数据包括结果集和流输出参数|SQL_SUCCESS|使用**SQLBindCol**和**SQLGetData**检索结果集。<br /><br /> 调用**SQLMore 结果**开始处理流式处理输出参数。 它应该返回SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParam 数据和** **SQLGetData**检索流式输出参数。|  
|数据包括警告消息和流输出参数|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**处理警告消息。<br /><br /> 调用**SQLMore 结果**开始处理流式处理输出参数。 它应该返回SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParam 数据和** **SQLGetData**检索流式输出参数。|  
|数据包括警告消息、结果集和流输出参数|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**处理警告消息。 然后调用**SQLMore 结果**开始处理结果集。<br /><br /> 使用**SQLBindCol**和**SQLGetData**检索结果集。<br /><br /> 调用**SQLMore 结果**开始处理流式处理输出参数。 **SQLMore 结果**应返回SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParam 数据和** **SQLGetData**检索流式输出参数。|  
|使用 DAE 输入参数的查询，例如流式输入/输出 （DAE） 参数|SQL NEED_DATA|调用**SQLParamData**和**SQLPutData**发送 DAE 输入参数数据。<br /><br /> 处理完所有 DAE 输入参数后 **，SQLParamData**可以返回**SQLExecute**和**SQLExecDirect**可以返回的任何返回代码。 然后可以应用此表中的案例。<br /><br /> 如果返回代码SQL_PARAM_DATA_AVAILABLE，则流式输出参数可用。 应用程序必须再次调用**SQLParamData**以检索流式输出参数的令牌，如此表的第一行所述。<br /><br /> 如果返回代码SQL_SUCCESS，则有要处理的结果集或处理已完成。<br /><br /> 如果返回代码SQL_SUCCESS_WITH_INFO，则有要处理的警告消息。|  
  
 在**SQLExecute、SQLExecDirect**或**SQLMoreResult**返回SQL_PARAM_DATA_AVAILABLE后，如果应用程序调用不在以下列表中的函数，则将导致函数序列错误： **SQLExecute**  
  
-   **SQLAllocHandle** / **SQLallocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGet 函数**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescfield** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle（** 带语句句柄）  
  
-   **SQLFreeStmt（** 带选项 = SQL_CLOSE、SQL_DROP或SQL_UNBIND）  
  
-   **SQLCloseCursor**  
  
-   **SQL 断开**  
  
-   **SQLFreeHandle（** 带手柄类型 = SQL_HANDLE_STMT）  
  
-   **SQLGetStmtAttr**  
  
 应用程序仍可以使用**SQLSetDescField**或**SQLSetDescRec**来设置绑定信息。 字段映射不会更改。 但是，描述符中的字段可能会返回新值。 例如，SQL_DESC_PARAMETER_TYPE可能会返回SQL_PARAM_INPUT_OUTPUT_STREAM或SQL_PARAM_OUTPUT_STREAM。  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>使用方案：从结果集中检索零件中的映像  
 当存储过程返回包含一行有关图像的元数据的结果集并在大型输出参数中返回图像时 **，SQLGetData**可用于获取部分数据。  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>使用方案：作为流式输入/输出参数发送和接收大型对象  
 当存储过程将大型对象作为输入/输出参数传递，并将值流式传输到数据库或从数据库中流出时 **，SQLGetData**可用于分段获取和发送数据。 您不必将所有数据存储在内存中。  
  
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
