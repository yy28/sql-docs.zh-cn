---
title: "替换函数映射的兼容性应用-ODBC |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 461f41eb5f8ae7481b65d293b0c3a619b59e7f9c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>替换函数映射的向后兼容性应用程序
ODBC 3*.x*应用程序工作到 ODBC 3*.x*对 ODBC 2 起驱动程序管理器。*x*驱动程序，只要使用任何新功能。 同时复制功能和行为的更改，但是，影响的方式，ODBC 3。*x*应用程序适用于 ODBC 2。*x*驱动程序。 当使用 ODBC 2。*x*驱动程序，驱动程序管理器映射以下 ODBC 3。*x*函数，已替换一个或多个 ODBC 2。*x*函数，到相应的 ODBC 2。*x*函数。  
  
|ODBC 3。*x*函数|ODBC 2。*x*函数|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**， **SQLFreeConnect**，或**SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] 其他可能还执行操作，具体取决于所请求的属性。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 驱动程序管理器映射到**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**适当。 以下调用到**SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 将导致在驱动程序管理器执行以下 (概念，没有错误检查) 映射：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 驱动程序管理器映射到**SQLSetPos**。 以下调用到**SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 将导致下面的步骤序列：  
  
1.  如果操作参数是 SQL_ADD，驱动程序管理器调用**SQLSetPos** ，如下所示：  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  驱动程序的操作参数不是 SQL_ADD，如果返回 SQLSTATE HY092 （无效的属性/选项标识符）。  
  
3.  如果应用程序尝试更改到的调用之间 SQL_ATTR_ROW_STATUS_PTR **SQLFetch**或**SQLFetchScroll**和**SQLBulkOperations**，驱动程序管理器将返回 SQLSTATE HY011 （不能设置属性现在）。  
  
4.  如果操作参数是 SQL_ADD，应用程序必须调用**SQLBindCol**绑定要插入的数据。 它不能调用**SQLSetDescField**或**SQLSetDescRec**绑定要插入的数据。  
  
5.  如果操作参数是 SQL_ADD 而要插入的行数不是与当前的行集大小相同**SQLSetStmtAttr**必须调用将 SQL_ATTR_ROW_ARRAY_SIZE 语句特性设置为要为的行数在调用之前插入**SQLBulkOperations**。 若要还原为以前的行集大小，应用程序必须设置之前的 SQL_ATTR_ROW_ARRAY_SIZE 语句属性**SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**调用。  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 驱动程序管理器映射到**SQLColAttributes**。 以下调用到**SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 将导致下面的步骤序列：  
  
1.  如果*FieldIdentifier*是以下之一：  
  
     SQL_DESC_PRECISION、 SQL_DESC_SCALE、 SQL_DESC_LENGTH、 SQL_DESC_OCTET_LENGTH、 SQL_DESC_UNNAMED、 SQL_DESC_BASE_COLUMN_NAME、 SQL_DESC_LITERAL_PREFIX、 SQL_DESC_LITERAL_SUFFIX 或 SQL_DESC_LOCAL_TYPE_NAME  
  
     驱动程序管理器返回与 SQLSTATE HY091 SQL_ERROR （描述符字段标识符无效）。 本部分没有进一步规则适用。  
  
2.  驱动程序管理器映射 SQL_COLUMN_COUNT、 SQL_COLUMN_NAME 或 SQL_COLUMN_NULLABLE 到 SQL_DESC_COUNT、 SQL_DESC_NAME 或 SQL_DESC_NULLABLE，分别。 (ODBC 2*.x*驱动程序需要仅支持 SQL_COLUMN_COUNT、 SQL_COLUMN_NAME，和 SQL_COLUMN_NULLABLE、 不 SQL_DESC_COUNT、 SQL_DESC_NAME 和 SQL_DESC_NULLABLE。)SQLColAttribute 调用映射到：  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  所有其他*FieldIdentifier*值将传递到该驱动程序，与**SQLColAttribute**映射到**SQLColAttributes**如上所示。  
  
4.  如果*BufferLength*小于 0，则驱动程序管理器将返回与 SQLSTATE HY090 SQL_ERROR （无效字符串或缓冲区长度）。 本部分没有进一步规则适用。  
  
5.  如果*FieldIdentifier*是 SQL_DESC_CONCISE_TYPE 和返回的类型是简洁的 datetime 数据类型，返回值的日期、 时间和时间戳的代码的驱动程序管理器映射。  
  
6.  驱动程序管理器执行必要的检查，以查看是否 SQLSTATE HY010 （函数序列错误） 需要发出。 如果这样，驱动程序管理器返回 SQL_ERROR 和 SQLSTATE HY010 （函数序列错误）。 本部分没有进一步规则适用。  
  
## <a name="sqlendtran"></a>SQLEndTran  
 驱动程序管理器映射到**SQLTransact**。 以下调用到**SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 将导致在驱动程序管理器执行以下 (概念，没有错误检查) 映射：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 驱动程序管理器映射到**SQLExtendedFetch**与*FetchOrientation* SQL_FETCH_NEXT 自变量。 以下调用到**SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 将导致驱动程序管理器调用**SQLExtendedFetch**、，如下所示：  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 在此调用中， *pcRow*参数设置为应用程序将设置到通过调用 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的值**SQLSetStmtAttr**。  
  
> [!NOTE]  
>  在应用程序调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ROW_STATUS_PTR 以指向状态数组，驱动程序管理器缓存指针。 *RowStatusArray*可以是等于 null 指针。  
  
 如果该驱动程序不支持**SQLExtendedFetch**和加载的是光标库，驱动程序管理器使用的是光标库的**SQLExtendedFetch**映射**SQLFetch**到**SQLExtendedFetch**。 如果该驱动程序不支持**SQLExtendedFetch**和未加载的是光标库，驱动程序管理器将传递到调用**SQLFetch**通过与驱动程序。 如果应用程序调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器可确保填充数组。 如果应用程序调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ROWS_FETCHED_PTR，驱动程序管理器设置此字段为 1。  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 驱动程序管理器映射到**SQLExtendedFetch**。 以下调用到**SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 将导致下面的步骤序列：  
  
1.  在应用程序调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ROW_STATUS_PTR （其设置在 IRD SQL_DESC_ARRAY_STATUS_PTR 字段） 以指向状态数组，驱动程序管理器缓存此指针。 允许将此指针*RowStatusArray*; 否则为让*RowStatusArray*等于 null 指针。 如果*RowStatusArray*参数设置为 null 指针时，驱动程序管理器将生成的行状态数组。  
  
2.  如果*FetchOrientation*不是一个 SQL_FETCH_NEXT、 SQL_FETCH_PRIOR、 SQL_FETCH_ABSOLUTE、 SQL_FETCH_RELATIVE、 SQL_FETCH_FIRST、 SQL_FETCH_LAST 或 SQL_FETCH_BOOKMARK，驱动程序管理器返回具有 SQL_ERROR 和 SQLSTATEHY106 （提取类型超出了范围）。 本部分没有进一步规则适用。  
  
3.  情况：  
  
-   如果*FetchOrientation*等同于 SQL_FETCH_BOOKMARK，然后：  
  
    -   如果**SQLSetStmtAttr**调用以前设置的值 SQL_ATTR_FETCH_BOOKMARK_PTR，然后让*Bmk*是通过取消引用指针 SQL_DESC_FETCH_BOOKMARK_PTR 获取的值。  
  
    -   否则，返回与 SQLSTATE HY111 SQL_ERROR （无效的书签值）。 本部分没有进一步规则适用。  
  
     驱动程序管理器现在调用**SQLExtendedFetch**、，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   否则，驱动程序管理器会调用**SQLExtendedFetch**、，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     在这些调用中， *pcRow*参数设置为应用程序将设置到通过调用 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的值**SQLSetStmtAttr**。  
  
-   SQL_ATTR_ROW_ARRAY_SIZE 映射到 SQL_ROWSET_SIZE。  
  
-   如果*rc*等于 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，并且如果*FetchOrientation*等于 SQL_FETCH_BOOKMARK 和*FetchOffset*是不等于 0，然后该驱动程序管理器发布警告、 SQLSTATE 01S10 （尝试提取使用书签偏移量，偏移量值已被忽略），并返回 SQL_SUCCESS_WITH_INFO。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 驱动程序管理器映射到**SQLFreeEnv**， **SQLFreeConnect**，或**SQLFreeStmt**根据。 以下调用到**SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 将导致在驱动程序管理器执行以下 (概念，没有错误检查) 映射：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 驱动程序管理器映射到**SQLGetConnectOption**。 以下调用到**SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 将导致下面的步骤序列：  
  
1.  如果*属性*不是驱动程序定义的连接或语句属性并且不是在 ODBC 2 中定义属性。*x*，驱动程序管理器返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。 本部分中的没有更多规则适用。  
  
2.  如果*属性*等于 SQL_ATTR_AUTO_IPD 或 SQL_ATTR_METADATA_ID，驱动程序管理器返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。  
  
3.  驱动程序管理器执行必要的检查，以查看是否 SQLSTATE 08003 （连接未打开） 或 SQLSTATE HY010 （函数序列错误） 需要引发。 如果是这样，驱动程序管理器将返回 SQL_ERROR 和相应的错误消息发送。 本部分没有进一步规则适用。  
  
4.  驱动程序管理器调用**SQLGetConnectOption** ，如下所示：  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     请注意， *BufferLength*和*StringLengthPtr*将被忽略。  
  
## <a name="sqlgetdata"></a>SQLGetData  
 当一个 ODBC 3。*x*应用程序使用 ODBC 2*.x*驱动程序调用**SQLGetData**与*ColumnNumber*参数等于 0，ODBC 3*.x*驱动程序管理器将其映射到调用**SQLGetStmtOption**与*选项*属性设置为 SQL_GET_BOOKMARK。  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 驱动程序管理器映射到**SQLGetStmtOption**。 以下调用到**SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 将导致下面的步骤序列：  
  
1.  如果*属性*不是驱动程序定义的连接或语句属性并且不是在 ODBC 2 中定义属性。*x*，驱动程序管理器返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。 本部分中的没有更多规则适用。  
  
2.  如果*属性*是以下之一：  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     驱动程序管理器返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。 本部分没有进一步规则适用。  
  
3.  驱动程序管理器执行必要的检查，以查看是否 SQLSTATE HY010 （函数序列错误） 需要发出。 如果这样，驱动程序管理器返回 SQL_ERROR 和 SQLSTATE HY010 （函数序列错误）。 本部分没有进一步规则适用。  
  
4.  如果*属性*等于 SQL_ATTR_ROWS_FETCHED_PTR，驱动程序管理器将返回的指针到内部的驱动程序管理器变量*cRow*，它已使用或将在调用中使用**SQLExtendedFetch**。 本部分没有进一步规则适用。  
  
5.  如果*属性*等于到 SQL_DESC_FETCH_BOOKMARK_PTR，驱动程序管理器返回相应的指针，它必须在调用期间缓存**SQLSetStmtAttr**。  
  
6.  如果*属性*等于到 SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器返回相应的指针，它必须在调用期间缓存**SQLSetStmtAttr**。  
  
7.  驱动程序管理器调用**SQLGetStmtOption** ，如下所示：  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     其中*hstmt*， *fOption*，和*pvParam*将设置的值为*StatementHandle*，*属性*，和*ValuePtr*分别。 *BufferLength*和*StringLengthPtr*将被忽略。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 驱动程序管理器映射到**SQLSetConnectOption**。 以下调用到**SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 将导致下面的步骤序列：  
  
1.  如果*属性*不是驱动程序定义的连接或语句属性并且不是在 ODBC 2 中定义属性。*x*，驱动程序管理器返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。 本部分中的没有更多规则适用。  
  
2.  如果*属性*等于 SQL_ATTR_AUTO_IPD，驱动程序管理器返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。  
  
3.  驱动程序管理器执行必要的检查，以查看是否 SQLSTATE 08003 （连接未打开） 或 SQLSTATE HY010 （函数序列错误） 需要发出。 如果其中一个错误需要发出，驱动程序管理器将返回 SQL_ERROR 和相应的错误消息发送。 本部分没有进一步规则适用。  
  
4.  驱动程序管理器调用**SQLSetConnectOption** ，如下所示：  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     其中*hdbc*， *fOption*，和*vParam*将设置的值为*ConnectionHandle*，*属性*，和*ValuePtr*分别。 *StringLengthPtr*将被忽略。  
  
> [!NOTE]  
>  能够在连接级别上设置语句特性已弃用。 语句特性应永远不会设置在连接级别由 ODBC 3。*x*应用程序。  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 驱动程序管理器映射到**SQLSetStmtOption**。 以下调用到**SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 将导致下面的步骤序列：  
  
1.  如果*属性*不是驱动程序定义的连接或语句属性并且不是在 ODBC 2 中定义属性。*x*，驱动程序管理器返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。 本部分中的没有更多规则适用。  
  
2.  如果*属性*是以下之一：  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     驱动程序管理器返回与 SQLSTATE HY092 SQL_ERROR （无效的属性/选项标识符）。 本部分没有进一步规则适用。  
  
3.  驱动程序管理器执行必要的检查，以查看是否 SQLSTATE HY010 （函数序列错误） 需要发出。 如果这样，驱动程序管理器返回 SQL_ERROR 和 SQLSTATE HY010 （函数序列错误）。 本部分没有进一步规则适用。  
  
4.  如果*属性*本主题中后面是等于 SQL_ATTR_PARAMSET_SIZE 或 SQL_ATTR_PARAMS_PROCESSED_PTR，请参阅"映射为处理参数数组，"一节。 本部分没有进一步规则适用。  
  
5.  如果*属性*等于 SQL_ATTR_ROWS_FETCHED_PTR，指针值用于更高版本的驱动程序管理器缓存**SQLFetchScroll**。  
  
6.  如果*属性*等于 SQL_ATTR_ROW_STATUS_PTR，指针值用于更高版本的驱动程序管理器缓存**SQLFetchScroll**或**SQLSetPos**。 本部分没有进一步规则适用。  
  
7.  如果*属性*等于 SQL_ATTR_FETCH_BOOKMARK_PTR，驱动程序管理器缓存*ValuePtr*和更高版本中对的调用将使用缓存的值**SQLFetchScroll**。 本部分没有进一步规则适用。  
  
8.  驱动程序管理器调用**SQLSetStmtOption** ，如下所示：  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     其中*hstmt*， *fOption*，和*vParam*将设置的值为*StatementHandle*，*属性*，和*ValuePtr*分别。 *StringLength*忽略自变量。  
  
     如果检测到 ODBC 2。*x*驱动程序支持字符串、 特定于驱动程序的语句选项，ODBC 3。*x*应用程序应调用**SQLSetStmtOption**设置这些选项。  
  
## <a name="mappings-for-handling-parameter-arrays"></a>处理参数数组的映射  
 在应用程序调用：  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 驱动程序管理器调用：  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 驱动程序管理器稍后将指针返回到此变量时在应用程序调用**SQLGetStmtAttr**检索 SQL_ATTR_PARAMS_PROCESSED_PTR。 驱动程序管理器不能更改此内部变量，直到语句句柄返回到已准备或已分配状态。  
  
 一个 ODBC 3。*x*应用程序可以调用**SQLGetStmtAttr**以获取 SQL_ATTR_PARAMS_PROCESSED_PTR 的值，即使在 APD 的 SQL_DESC_ARRAY_SIZE 字段未显式设置，它具有也是如此。 这种情况下可能会发生，例如，如果应用程序检查当前"行"的参数的泛型例程时正在处理**SQLExecute**返回 SQL_NEED_DATA。 此例程将调用是否 SQL_DESC_ARRAY_SIZE 为 1 或大于 1。 若要考虑到这一点，驱动程序管理器将需要定义此内部变量是否应用程序调用**SQLSetStmtAttr**在 APD 中设置 SQL_DESC_ARRAY_SIZE 字段。 如果尚未设置 SQL_DESC_ARRAY_SIZE，驱动程序管理器必须确保此变量包含之前从返回的值 1 **SQLExecDirect**或**SQLExecute**。  
  
## <a name="error-handling"></a>错误处理  
 在 ODBC 3。*x*，则调用**SQLFetch**或**SQLFetchScroll**填充 IRD 和给定的诊断记录的 SQL_DIAG_ROW_NUMBER 字段中 SQL_DESC_ARRAY_STATUS_PTR包含与此记录的行集中的行数。 使用此，应用程序可以使用给定的行位置关联一条错误消息。  
  
 一个 ODBC 2。*x*驱动程序将无法提供此功能。 不过，它将提供与 SQLSTATE 01S01 错误分界 （行中的错误）。 一个 ODBC 3。*x*正在使用应用程序**SQLFetch**或**SQLFetchScroll**同时针对 ODBC 2 逐渐。*x*驱动程序必须考虑这一点。 此类应用程序将不能调用另请注意**SQLGetDiagField**实际是否仍要获取 SQL_DIAG_ROW_NUMBER 字段。 一个 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序将能够调用**SQLGetDiagField**只用*DiagIdentifier* SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_NATIVE、 SQL_DIAG_RETURNCODE 或 SQL_DIAG_ 自变量SQLSTATE。 ODBC 3*.x*驱动程序管理器使用 ODBC 2 时维护的诊断数据结构。*x*驱动程序，但 ODBC 2。*x*驱动程序返回仅这四个字段。  
  
 当一个 ODBC 2。*x*应用程序使用 ODBC 2。*x*驱动程序，如果操作可能会导致多个错误，要返回的驱动程序管理器中，不同的错误可能会返回由 ODBC 3*.x*比通过 ODBC 2 的驱动程序管理器。*x*驱动程序管理器。  
  
## <a name="mappings-for-bookmark-operations"></a>映射的书签操作  
 ODBC 3*.x*驱动程序管理器执行以下映射时 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序执行书签操作。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 当一个 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用**SQLBindCol**将绑定到列 0 与*fCType*等于 SQL_C_VARBOOKMARK，ODBC 3*.x*驱动程序管理器检查是否*BufferLength*参数小于 4 或大于 4，并如果是这样，返回 SQLSTATE HY090 （无效字符串或缓冲区长度）。 如果*BufferLength*参数等于 4，驱动程序管理器调用**SQLBindCol**驱动程序，替换后中*fCType*与 SQL_C_BOOKMARK。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 当一个 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用**SQLColAttribute**与*ColumnNumber*自变量设置为 0，驱动程序管理器返回*FieldIdentifier*值下表中列出。  
  
|*FieldIdentifier*|值|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|""（空字符串）|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|返回的相同值**SQLNumResultCols**|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|""（空字符串）|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|""（空字符串）|  
|SQL_DESC_LITERAL_SUFFIX|""（空字符串）|  
|SQL_DESC_LOCAL_TYPE_NAME|""（空字符串）|  
|SQL_DESC_NAME|""（空字符串）|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|""（空字符串）|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|""（空字符串）|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|""（空字符串）|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 当一个 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用**SQLDescribeCol**与*ColumnNumber*参数设置为 0，驱动程序管理器会返回下表中列出的值。  
  
|缓冲区|值|  
|------------|-----------|  
|ColumnName|""（空字符串）|  
|* NameLengthPtr|0|  
|* DataTypePtr|SQL_BINARY|  
|* ColumnSizePtr|4|  
|* DecimalDigitsPtr|0|  
|* NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 当一个 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序，可以对的以下调用**SQLGetData**检索书签：  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 调用映射到**SQLGetStmtOption**与*fOption*的 SQL_GET_BOOKMARK，如下所示：  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 其中*hstmt*和*pvParam*设置中的值为*StatementHandle*和*TargetValuePtr*分别。 在通过指向的缓冲区中返回书签*pvParam* (*TargetValuePtr*) 自变量。 缓冲区中的值指向的*StrLen_or_IndPtr*对的调用中的自变量**SQLGetData**设置为 4。  
  
 此映射是必需来应对这种情况在其中**SQLFetch**在调用之前调用了**SQLGetData**和 ODBC 2。*x*驱动程序不支持**SQLExtendedFetch**。 在这种情况下， **SQLFetch**将通过传递到 ODBC 2。*x*驱动程序，在其中不支持区分大小的书签检索。  
  
 **SQLGetData**无法 ODBC 2 中多次调用。*x*驱动程序以检索在部件中，因此调用的书签**SQLGetData**与*BufferLength*参数设置为小于 4 的值与*ColumnNumber*自变量设置为 0 将返回 SQLSTATE HY090 （无效字符串或缓冲区长度）。 **SQLGetData** ，但是，可以检索相同的书签的多次调用。  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 当一个 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用**SQLSetStmtAttr**将 SQL_ATTR_USE_BOOKMARKS 属性设置为 SQL_UB_VARIABLE，驱动程序管理器将该属性设置在基础 ODBC 2 SQL_UB_ON。*x*驱动程序。
