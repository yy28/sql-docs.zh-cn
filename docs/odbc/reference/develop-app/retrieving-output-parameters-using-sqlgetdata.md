---
title: 检索输出参数使用 SQLGetData |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e410618b8a110cbb978f45d4ac5cf37f1a77e845
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>检索输出参数使用 SQLGetData
在 ODBC 3.8 之前应用程序只能无法检索具有绑定的输出缓冲区的查询的输出参数。 但是，很难参数值的大小是非常大 （例如，较大的图像） 时，将分配一个非常大的缓冲区。 ODBC 3.8 引入了检索部分中的输出参数的新方法。 现在，应用程序可以调用**SQLGetData**使用较小的缓冲区多次检索大型参数值。 这是类似于检索大型列数据。  
  
 若要将输出参数或输入/输出参数在部件中要检索的绑定，调用**SQLBindParameter**与*InputOutputType*参数设置为 SQL_PARAM_OUTPUT_STREAM 或 SQL_PARAM_INPUT_OUTPUT_STREAM。 借助 SQL_PARAM_INPUT_OUTPUT_STREAM，应用程序可以使用**SQLPutData**数据输入到参数，，然后使用**SQLGetData**检索输出参数。 输入的数据必须采用数据执行 (DAE) 窗体中，使用**SQLPutData**而不是将其绑定到预先分配的缓冲区。  
  
 此功能可由 ODBC 3.8 应用程序或重新编译 ODBC 3.x 和 ODBC 2.x 应用程序，这些应用程序必须具有 ODBC 3.8 支持的驱动程序检索输出参数使用**SQLGetData**和 ODBC 3.8 驱动程序管理器。 有关如何启用较旧应用程序使用 ODBC 的新功能的信息，请参阅[兼容性矩阵](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
## <a name="usage-example"></a>用法示例  
 例如，考虑执行存储的过程， **{调用 sp_f(?,?)}**，其中两个参数绑定为 SQL_PARAM_OUTPUT_STREAM，，存储的过程返回任何结果集 （本主题中稍后你将找到更复杂的方案）：  
  
1.  对于每个参数，调用**SQLBindParameter**与*InputOutputType*设置为 SQL_PARAM_OUTPUT_STREAM 和*ParameterValuePtr*设置为一个令牌，如参数数量指向数据的指针或指向应用程序用于将输入的参数绑定的结构的指针。 此示例将使用作为令牌的参数序号。  
  
2.  执行查询中的使用**SQLExecDirect**或**SQLExecute**。 将返回 SQL_PARAM_DATA_AVAILABLE，，该值指示存在可用于检索经过流处理的输出参数。  
  
3.  调用**SQLParamData**获取可用于检索参数。 **SQLParamData**将与第一个可用的参数，在中设置的令牌返回 SQL_PARAM_DATA_AVAILABLE **SQLBindParameter** （步骤 1）。 在缓冲区中返回的标记， *ValuePtrPtr*指向。  
  
4.  调用**SQLGetData**具有自变量*Col*_or\_*Param_Num*设置为参数序号以检索第一个可用参数的数据。 如果**SQLGetData**返回 SQL_SUCCESS_WITH_INFO 和 SQLState 01004 （截断的数据） 和类型为客户端和服务器上的可变长度，则从第一个可用的参数中检索的更多数据。 你可以继续调用**SQLGetData**直到返回替换为其他 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO **SQLState**。  
  
5.  重复步骤 3 和步骤 4，以检索当前参数。  
  
6.  调用**SQLParamData**试。 如果它返回 SQL_PARAM_DATA_AVAILABLE 除，没有没有更多流式处理的参数数据检索，并且返回的代码将执行的下一个语句的返回代码。  
  
7.  调用**SQLMoreResults**处理下一步的参数集，直到它返回 SQL_NO_DATA。 **SQLMoreResults**如果语句特性 SQL_ATTR_PARAMSET_SIZE 已设置为 1 将返回在此示例中的 SQL_NO_DATA。 否则为**SQLMoreResults**将返回 SQL_PARAM_DATA_AVAILABLE 用于指示可用于下一步的一组参数来检索经过流处理的输出参数。  
  
 参数中使用类似于 DAE 输入参数，该令牌*ParameterValuePtr*中**SQLBindParameter** （步骤 1） 可以是指向应用程序数据结构，其中包含的指针参数和应用程序特定的详细信息，序号如有必要。  
  
 返回经过流处理的输出或输入/输出参数的顺序是特定的驱动程序，并且不可能始终与查询中指定的顺序相同。  
  
 如果应用程序不会调用**SQLGetData**在步骤 4 中，参数值将被丢弃。 同样，如果应用程序调用**SQLParamData**之前所有参数值已都读取的**SQLGetData**、 的值的其余部分将被丢弃，和应用程序可以处理下一步参数。  
  
 如果应用程序调用**SQLMoreResults**经过流处理的所有输出参数的都处理 (**SQLParamData**仍返回 SQL_PARAM_DATA_AVAILABLE)，所有剩余的参数将被丢弃。 同样，如果应用程序调用**SQLMoreResults**之前所有参数值已都读取的**SQLGetData**，值和所有剩余的参数的其余部分将被丢弃，与应用程序可以继续对下一步的参数集进行处理。  
  
 请注意，应用程序可以在指定的 C 数据类型**SQLBindParameter**和**SQLGetData**。 使用指定的 C 数据类型**SQLGetData**重写中指定的 C 数据类型**SQLBindParameter**，除非 C 数据类型中指定**SQLGetData**是 SQL_APD_TYPE。  
  
 尽管类型 BLOB 的输出参数的数据类型时，流式处理的输出参数是更为有用，但此功能还可与任何数据类型。 支持流式处理的输出参数的数据类型指定驱动程序中。  
  
 如果没有 SQL_PARAM_INPUT_OUTPUT_STREAM 参数来处理**SQLExecute**或**SQLExecDirect**将先返回 SQL_NEED_DATA。 应用程序可以调用**SQLParamData**和**SQLPutData**发送 DAE 参数数据。 当处理所有 DAE 输入的参数时， **SQLParamData**返回 SQL_PARAM_DATA_AVAILABLE 以指示流式处理的输出参数均可用。  
  
 当存在进行流式处理输出参数和要处理的绑定的输出参数，该驱动程序将确定处理输出参数的顺序。 因此，如果输出参数绑定到的缓冲区 ( **SQLBindParameter**参数*InputOutputType*设置为 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT)，该缓冲区可能不会填充直到**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。 应用程序应阅读绑定之后才缓冲**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 别忘了流式传输输出参数进行处理。  
  
 数据源可以返回的警告和结果集，此外到流式处理的输出参数。 一般情况下，警告和结果集单独处理从流式处理的输出参数通过调用**SQLMoreResults**。 进程的警告消息和结果集在处理经过流处理的输出参数之前。  
  
 下表描述单个命令发送到在服务器和应用程序应如何工作的不同的方案。  
  
|应用场景|从 SQLExecute 或 SQLExecDirect 的返回值|下一步操作|  
|--------------|---------------------------------------------------|---------------------|  
|数据仅包含经过流处理的输出参数|SQL_PARAM_DATA_AVAILABLE|使用**SQLParamData**和**SQLGetData**检索经过流处理的输出参数。|  
|数据包括的结果集和流式处理输出参数|SQL_SUCCESS|检索结果集与**SQLBindCol**和**SQLGetData**。<br /><br /> 调用**SQLMoreResults**开始处理经过流处理的输出参数。 它应返回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**检索经过流处理的输出参数。|  
|数据包括一条警告消息和流式处理输出参数|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**处理这些警告消息。<br /><br /> 调用**SQLMoreResults**开始处理经过流处理的输出参数。 它应返回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**检索经过流处理的输出参数。|  
|数据包含一条警告消息，结果设置和流式处理输出参数|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**处理这些警告消息。 然后调用**SQLMoreResults**开始处理结果集中。<br /><br /> 检索结果集与**SQLBindCol**和**SQLGetData**。<br /><br /> 调用**SQLMoreResults**开始处理经过流处理的输出参数。 **SQLMoreResults**应返回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**检索经过流处理的输出参数。|  
|查询包含 DAE 输入参数，例如，经过流处理的输入/输出 (DAE) 参数|SQL NEED_DATA|调用**SQLParamData**和**SQLPutData**发送 DAE 输入参数数据。<br /><br /> 在处理所有 DAE 输入的参数之后， **SQLParamData**可以返回任何返回代码， **SQLExecute**和**SQLExecDirect**可以返回。 然后可以应用此表中的情况。<br /><br /> 如果返回代码，SQL_PARAM_DATA_AVAILABLE 流式处理的输出参数均可用。 应用程序必须调用**SQLParamData**以检索经过流处理的输出参数的标记，此表的第一行中所述。<br /><br /> 如果返回代码，SQL_SUCCESS 没有要处理结果集，或处理已完成。<br /><br /> 返回代码是 SQL_SUCCESS_WITH_INFO，要处理的警告消息。|  
  
 后**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**如果应用程序调用可能会造成返回 SQL_PARAM_DATA_AVAILABLE，函数序列错误不在下面的列表的函数：  
  
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
  
-   **SQLCancelHandle** （具有语句句柄）  
  
-   **SQLFreeStmt** （选项 = SQL_CLOSE、 SQL_DROP 或 SQL_UNBIND）  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** （HandleType = SQL_HANDLE_STMT）  
  
-   **SQLGetStmtAttr**  
  
 应用程序仍然可以使用**SQLSetDescField**或**SQLSetDescRec**可设置的绑定信息。 字段映射将不会更改。 但是，描述符中的字段，可能会返回新值。 例如，SQL_DESC_PARAMETER_TYPE 可能返回 SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM。  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>使用方案： 从结果集中检索部分中的图像  
 **SQLGetData**可以用于在部分中获取数据，当存储的过程返回结果集，其中包含有关映像的元数据的一个行并在大输出参数中返回映像。  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>使用方案： 发送和接收作为经过流处理的输入/输出参数的大型对象  
 **SQLGetData**可以用于获取和存储的过程将大型对象传递作为输入/输出参数，流式处理与其他数据库的值时在部件中发送数据。 不需要在内存中存储的所有数据。  
  
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
