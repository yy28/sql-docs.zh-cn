---
title: 映射应用兼容性的替代功能 - ODBC |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18669fe9b6edbd39859166e382ad18d1b04a99a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301087"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>映射替换函数以实现应用程序后向兼容性
通过 ODBC *3.x*驱动程序管理器工作的 ODBC *3.x*应用程序将针对 ODBC *2.x*驱动程序，只要不使用新功能。 但是，重复的功能和行为更改都会影响 ODBC *3.x*应用程序在 ODBC *2.x*驱动程序上的工作方式。 使用 ODBC *2.x*驱动程序时，驱动程序管理器将以下 ODBC *3.x*函数（已替换一个或多个 ODBC *2.x*函数）映射到相应的 ODBC *2.x*函数中。  
  
|ODBC *3.x*功能|ODBC *2.x*功能|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv** **、SQLAllocConnect**或**SQLAllocStmt**|  
|**SQLBulk 操作**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColattributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQL 扩展获取**|  
|**SQLFetchScroll**|**SQL 扩展获取**|  
|**SQLFreeHandle**|**SQLFreeEnv** **、SQLFreeConnect**或**SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSet 连接选项**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] 也可以采取其他操作，具体取决于所请求的属性。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 驱动程序管理器将其映射到**SQLAllocEnv、SQLAllocConnect**或**SQLAllocStmt（** 视情况而定）。 **SQLAllocConnect** 以下调用**SQLAllocHandle**：  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 将导致驱动程序管理器执行以下（概念性、无错误检查）映射：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulk 操作  
 驱动程序管理器将此映射到**SQLSetPos**。 以下对**SQLBulk 操作的**调用 ：  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 将导致以下步骤序列：  
  
1.  如果操作参数SQL_ADD，驱动程序管理器将**SQLSetPos**调用如下：  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  如果未SQL_ADD操作参数，驱动程序将返回 SQLSTATE HY092（无效属性/选项标识符）。  
  
3.  如果应用程序尝试更改对**SQLFetch**或**SQLFetchScroll**和**SQLBulk 操作**的调用之间的SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器将返回 SQLSTATE HY011（现在无法设置属性）。  
  
4.  如果操作参数SQL_ADD，则应用程序必须调用**SQLBindCol**来绑定要插入的数据。 它不能调用**SQLSetDescField**或**SQLSetDescRec**来绑定要插入的数据。  
  
5.  如果操作参数SQL_ADD且要插入的行数与当前行集大小不同，则必须调用**SQLSetStmtAttr**将SQL_ATTR_ROW_ARRAY_SIZE语句属性设置为调用**SQLBulk 操作**之前要插入的行数。 要恢复到以前的行集大小，应用程序必须在调用**SQLFetch、SQLFetchScroll**或**SQLFetch** **SQLSetPos**之前设置SQL_ATTR_ROW_ARRAY_SIZE语句属性。  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 驱动程序管理器将此映射到**SQLColattributes**。 以下对**SQLColattribute 的**调用 ：  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 将导致以下步骤序列：  
  
1.  如果*字段标识符*是以下类型之一：  
  
     SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH、SQL_DESC_OCTET_LENGTH、SQL_DESC_UNNAMED、SQL_DESC_BASE_COLUMN_NAME、SQL_DESC_LITERAL_PREFIX、SQL_DESC_LITERAL_SUFFIX或SQL_DESC_LOCAL_TYPE_NAME  
  
     驱动程序管理器返回SQL_ERROR与 SQLSTATE HY091（无效描述符字段标识符）。 本条没有进一步的规则适用。  
  
2.  驱动程序管理器分别将SQL_COLUMN_COUNT、SQL_COLUMN_NAME或SQL_COLUMN_NULLABLE映射到SQL_DESC_COUNT、SQL_DESC_NAME或SQL_DESC_NULLABLE。 （ODBC *2.x*驱动程序只需要支持SQL_COLUMN_COUNT、SQL_COLUMN_NAME和SQL_COLUMN_NULLABLE，而不需要SQL_DESC_COUNT、SQL_DESC_NAME和SQL_DESC_NULLABLE。对 SQLColAttribute 的调用映射到：  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  所有其他*字段标识符*值都传递给驱动程序 **，SQLColAttribute**映射到**SQLColattributes，** 如前所示。  
  
4.  如果*缓冲区长度*小于 0，驱动程序管理器将返回 SQL_ERROR SQLSTATE HY090（无效字符串或缓冲区长度）。 本条没有进一步的规则适用。  
  
5.  如果*FieldIdentifier*是SQL_DESC_CONCISE_TYPE并且返回的类型是简明的日期时间数据类型，则驱动程序管理器将映射日期、时间和时间戳代码的返回值。  
  
6.  驱动程序管理器执行必要的检查，以查看是否需要引发 SQLSTATE HY010（功能序列错误）。 如果是这样，驱动程序管理器将返回SQL_ERROR和 SQLSTATE HY010（函数序列错误）。 本条没有进一步的规则适用。  
  
## <a name="sqlendtran"></a>SQLEndTran  
 驱动程序管理器将此映射到**SQLTransact**。 以下调用**SQLEndTran**：  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 将导致驱动程序管理器执行以下（概念性、无错误检查）映射：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 驱动程序管理器将其映射到**SQL 扩展获取**，并*带有SQL_FETCH_NEXT的提取方向*参数。 以下调用**SQLFetch**：  
  
```  
SQLFetch (StatementHandle);  
```  
  
 将导致驱动程序管理器调用 SQL**扩展获取**，如下所示：  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 在此调用中 *，pcRow*参数设置为应用程序通过调用**SQLSetStmtAttr**将SQL_ATTR_ROWS_FETCHED_PTR语句属性设置为的值。  
  
> [!NOTE]  
>  当应用程序调用**SQLSetStmtAttr**将SQL_ATTR_ROW_STATUS_PTR设置为指向状态数组时，驱动程序管理器将缓存指针。 *行状态数组*可以等于空指针。  
  
 如果驱动程序不支持 SQL**延长获取**，并且加载了游标库，则驱动程序管理器使用光标库的**SQL 扩展获取**将**SQLFetch**映射到**SQL 扩展获取**。 如果驱动程序不支持**SQLExtendedFetch，** 并且游标库未加载，则驱动程序管理器将**SQLFetch**的调用传递给驱动程序。 如果应用程序调用**SQLSetStmtAttr**来设置SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器将确保填充阵列。 如果应用程序调用**SQLSetStmtAttr**来设置SQL_ATTR_ROWS_FETCHED_PTR，驱动程序管理器将此字段设置为 1。  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 驱动程序管理器将其映射到**SQL 扩展获取**。 以下调用**SQLFetchScroll**：  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 将导致以下步骤序列：  
  
1.  当应用程序调用**SQLSetStmtAttr**将SQL_ATTR_ROW_STATUS_PTR（将 IRD 中的SQL_DESC_ARRAY_STATUS_PTR字段设置为指向状态数组时，驱动程序管理器将缓存此指针。 让此指针成为*RowStatusArray*;否则，让*RowStatusArray*等于空指针。 如果*RowStatusArray*参数设置为空指针，则驱动程序管理器将生成行状态数组。  
  
2.  如果*Fetch 方向*不是SQL_FETCH_NEXT、SQL_FETCH_PRIOR、SQL_FETCH_ABSOLUTE、SQL_FETCH_RELATIVE、SQL_FETCH_FIRST、SQL_FETCH_LAST或SQL_FETCH_BOOKMARK之一，则驱动程序管理器返回时带有SQL_ERROR和 SQLSTATE HY106（提取类型不在范围）。 本条没有进一步的规则适用。  
  
3.  大小写：  
  
-   如果*取取方向*等于SQL_FETCH_BOOKMARK，则：  
  
    -   如果之前调用**SQLSetStmtAttr**来设置SQL_ATTR_FETCH_BOOKMARK_PTR的值，则让*Bmk*成为通过取消引用指针SQL_DESC_FETCH_BOOKMARK_PTR获得的值。  
  
    -   否则，使用 SQLSTATE HY111（无效书签值）返回SQL_ERROR。 本条没有进一步的规则适用。  
  
     驱动程序管理器现在调用**SQL 扩展获取**，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   否则，驱动程序管理器将 SQL**扩展获取**调用 ，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     在这些调用中 *，pcRow*参数设置为应用程序通过调用**SQLSetStmtAttr**将SQL_ATTR_ROWS_FETCHED_PTR语句属性设置为的值。  
  
-   SQL_ATTR_ROW_ARRAY_SIZE映射到SQL_ROWSET_SIZE。  
  
-   如果*rc*等于SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，并且*Fetch方向*等于*SQL_FETCH_BOOKMARK，FetchOffset*不等于 0，则驱动程序管理器将发布警告 SQLSTATE 01S10（尝试通过书签偏移进行提取，忽略偏移值），并返回SQL_SUCCESS_WITH_INFO。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 驱动程序管理器将其映射到**SQLFreeEnv、SQLFreeConnect**或**SQLFreeConnect** **SQLFreeStmt（** 视情况而定）。 以下调用**SQLFreeHandle**：  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 将导致驱动程序管理器执行以下（概念性、无错误检查）映射：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 驱动程序管理器将其映射到**SQLGetConnectOption**。 以下调用**SQLGetConnectAttr**：  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 将导致以下步骤序列：  
  
1.  如果*属性*不是驱动程序定义的连接或语句属性，并且不是在 ODBC *2.x*中定义的属性，则驱动程序管理器返回SQL_ERROR SQLSTATE HY092（无效属性/选项标识符）。 本节中没有进一步的规则。  
  
2.  如果*属性*等于SQL_ATTR_AUTO_IPD或SQL_ATTR_METADATA_ID，驱动程序管理器将返回SQL_ERROR SQLSTATE HY092（无效属性/选项标识符）。  
  
3.  驱动程序管理器执行必要的检查，以查看是否需要引发 SQLSTATE 08003（连接未打开）或 SQLSTATE HY010（功能序列错误）。 如果是这样，驱动程序管理器返回SQL_ERROR并发布相应的错误消息。 本条没有进一步的规则适用。  
  
4.  驱动程序管理器调用**SQLGetConnectOption**如下所示：  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     请注意，*缓冲区长度*和*字符串长度Ptr*将被忽略。  
  
## <a name="sqlgetdata"></a>SQLGetData  
 当使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序调用**SQLGetData**时，*列数*参数等于 0，ODBC *3.x*驱动程序管理器将此映射到**SQLGetStmtOption**的调用，*选项*属性设置为SQL_GET_BOOKMARK。  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 驱动程序管理器将此映射到**SQLGetStmtOption**。 以下调用**SQLGetStmtAttr**：  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 将导致以下步骤序列：  
  
1.  如果*属性*不是驱动程序定义的连接或语句属性，并且不是在 ODBC *2.x*中定义的属性，则驱动程序管理器返回SQL_ERROR SQLSTATE HY092（无效属性/选项标识符）。 本节中没有进一步的规则。  
  
2.  如果*属性*是以下属性之一：  
  
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
  
     驱动程序管理器返回SQL_ERROR与 SQLSTATE HY092（无效属性/选项标识符）。 本条没有进一步的规则适用。  
  
3.  驱动程序管理器执行必要的检查，以查看是否需要引发 SQLSTATE HY010（功能序列错误）。 如果是这样，驱动程序管理器将返回SQL_ERROR和 SQLSTATE HY010（函数序列错误）。 本条没有进一步的规则适用。  
  
4.  如果*属性*等于SQL_ATTR_ROWS_FETCHED_PTR，驱动程序管理器将返回指向内部驱动程序管理器变量*cRow*的指针 ，它已使用或将在调用**SQLExtendedFetch**中使用 。 本条没有进一步的规则适用。  
  
5.  如果*属性*等于SQL_DESC_FETCH_BOOKMARK_PTR，驱动程序管理器将返回它在调用**SQLSetStmtAttr**期间缓存的相应指针。  
  
6.  如果*属性*等于SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器将返回它在调用**SQLSetStmtAttr**期间缓存的相应指针。  
  
7.  驱动程序管理器调用**SQLGetStmtOption**如下所示：  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     *其中 hstmt、fOption*和*pvParam*将分别设置为*语句处理*、*属性*和*ValuePtr*的值。 *fOption* 将忽略*缓冲区长度*和*字符串长度 Ptr。*  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 驱动程序管理器将其映射到**SQLSetConnectOption**。 以下对**SQLSetConnectAttr 的**调用 ：  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 将导致以下步骤序列：  
  
1.  如果*属性*不是驱动程序定义的连接或语句属性，并且不是在 ODBC *2.x*中定义的属性，则驱动程序管理器返回SQL_ERROR SQLSTATE HY092（无效属性/选项标识符）。 本节中没有进一步的规则。  
  
2.  如果*属性*等于SQL_ATTR_AUTO_IPD，驱动程序管理器将返回SQL_ERROR SQLSTATE HY092（无效属性/选项标识符）。  
  
3.  驱动程序管理器执行必要的检查，以查看是否需要引发 SQLSTATE 08003（连接未打开）或 SQLSTATE HY010（功能序列错误）。 如果需要引发这些错误之一，驱动程序管理器将返回SQL_ERROR并发布相应的错误消息。 本条没有进一步的规则适用。  
  
4.  驱动程序管理器调用**SQLSetConnectOption**如下所示：  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     *其中 hdbc、fOption*和*vParam*将分别*fOption*设置为*连接句柄*、*属性*和*ValuePtr*的值。 *字符串长度Ptr*将被忽略。  
  
> [!NOTE]  
>  在连接级别上设置语句属性的能力已被弃用。 声明属性绝不应由 ODBC *3.x*应用程序在连接级别设置。  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 驱动程序管理器将此映射到**SQLSetStmtOption**。 以下调用**SQLSetStmtAttr**：  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 将导致以下步骤序列：  
  
1.  如果*属性*不是驱动程序定义的连接或语句属性，并且不是在 ODBC *2.x*中定义的属性，则驱动程序管理器返回SQL_ERROR SQLSTATE HY092（无效属性/选项标识符）。 本节中没有进一步的规则。  
  
2.  如果*属性*是以下属性之一：  
  
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
  
     驱动程序管理器返回SQL_ERROR与 SQLSTATE HY092（无效属性/选项标识符）。 本条没有进一步的规则适用。  
  
3.  驱动程序管理器执行必要的检查，以查看是否需要引发 SQLSTATE HY010（功能序列错误）。 如果是这样，驱动程序管理器将返回SQL_ERROR和 SQLSTATE HY010（函数序列错误）。 本条没有进一步的规则适用。  
  
4.  如果*属性*等于SQL_ATTR_PARAMSET_SIZE或SQL_ATTR_PARAMS_PROCESSED_PTR，请参阅本主题后面的"处理参数数组映射"部分。 本条没有进一步的规则适用。  
  
5.  如果*属性*等于SQL_ATTR_ROWS_FETCHED_PTR，驱动程序管理器将缓存指针值，以便以后与**SQLFetchScroll**一起使用。  
  
6.  如果*属性*等于SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器将缓存指针值，以便以后与**SQLFetchScroll**或**SQLSetPos**一起使用。 本条没有进一步的规则适用。  
  
7.  如果*属性*等于SQL_ATTR_FETCH_BOOKMARK_PTR，驱动程序管理器将缓存*ValuePtr，* 并在调用**SQLFetchScroll**时稍后使用缓存的值。 本条没有进一步的规则适用。  
  
8.  驱动程序管理器调用**SQLSetStmtOption**如下所示：  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     *其中 hstmt、fOption*和*vParam*将分别设置为*语句处理*、*属性*和*ValuePtr*的值。 *fOption* 将忽略*字符串长度*参数。  
  
     如果 ODBC *2.x*驱动程序支持字符字符串、特定于驱动程序的语句选项，则 ODBC *3.x*应用程序应调用**SQLSetStmtOption**来设置这些选项。  
  
## <a name="mappings-for-handling-parameter-arrays"></a>处理参数数组的映射  
 当应用程序调用时：  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 驱动程序管理器调用：  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 当应用程序调用**SQLGetStmtAttr**以检索SQL_ATTR_PARAMS_PROCESSED_PTR时，驱动程序管理器稍后返回指向此变量的指针。 在语句句柄返回到准备或分配状态之前，驱动程序管理器无法更改此内部变量。  
  
 ODBC *3.x*应用程序可以调用**SQLGetStmtAttr**以获取SQL_ATTR_PARAMS_PROCESSED_PTR的值，即使它尚未在 APD 中显式设置SQL_DESC_ARRAY_SIZE字段。 例如，如果应用程序具有一个泛型例程，用于检查**SQLExecute**返回SQL_NEED_DATA时正在处理的当前"行"参数，则可能会出现这种情况。 无论SQL_DESC_ARRAY_SIZE是 1 还是大于 1，都调用此例程。 为了考虑到这一点，驱动程序管理器将需要定义此内部变量，无论应用程序是否调用**SQLSetStmtAttr**来设置 APD 中的SQL_DESC_ARRAY_SIZE字段。 如果未设置SQL_DESC_ARRAY_SIZE，驱动程序管理器必须确保此变量在从**SQLExecDirect**或**SQLExecute**返回之前包含值 1。  
  
## <a name="error-handling"></a>错误处理  
 在 ODBC *3.x*中，调用**SQLFetch**或**SQLFetchScroll**填充 IRD 中SQL_DESC_ARRAY_STATUS_PTR，并且给定诊断记录的SQL_DIAG_ROW_NUMBER字段包含此记录相关的行集中的行数。 使用此，应用程序可以将错误消息与给定的行位置相关联。  
  
 ODBC *2.x*驱动程序将无法提供此功能。 但是，它将提供 SQLSTATE 01S01（行中的错误）的错误划分。 与 ODBC *2.x*驱动程序对抗时使用**SQLFetch**或**SQLFetchScroll 的**ODBC *3.x*应用程序需要注意这一事实。 另请注意，这样的应用程序将无法调用**SQLGetDiagField**来实际获取SQL_DIAG_ROW_NUMBER字段。 使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序只能使用 SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_RETURNCODE或SQL_DIAG_SQLSTATE*的 Diag标识符*参数调用**SQLGetDiagField。** 使用 ODBC *2.x*驱动程序时，ODBC *3.x*驱动程序管理器维护诊断数据结构，但 ODBC *2.x*驱动程序仅返回这四个字段。  
  
 当 ODBC *2.x*应用程序使用 ODBC *2.x*驱动程序时，如果操作可能导致驱动程序管理器返回多个错误，则 ODBC 3.x 驱动程序管理器可能会返回与 ODBC *2.x* *2.x*驱动程序管理器不同的错误。  
  
## <a name="mappings-for-bookmark-operations"></a>书签操作的映射  
 当使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序执行书签操作时，ODBC *3.x*驱动程序管理器执行以下映射。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 当使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序调用**SQLBindCol**以*fCType*等于SQL_C_VARBOOKMARK绑定到列 0 时，ODBC *3.x*驱动程序管理器将检查*缓冲区长度*参数是否小于 4 或大于 4，如果是，则返回 SQLSTATE HY090（无效字符串或缓冲区长度）。 如果*缓冲区长度*参数等于 4，则驱动程序管理器在用SQL_C_BOOKMARK替换*fCType*后，在驱动程序中调用**SQLBindCol。**  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 当使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序调用**SQLColAttribute，***其中列编号*参数设置为 0 时，驱动程序管理器将返回下表中列出的*字段标识符*值。  
  
|*FieldIdentifier*|“值”|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|""（空字符串）|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|**SQLNumResultCols**返回的相同值|  
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
 当使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序调用**SQLDescribeCol，***其中列号*参数设置为 0 时，驱动程序管理器将返回下表中列出的值。  
  
|Buffer|“值”|  
|------------|-----------|  
|ColumnName|""（空字符串）|  
|*名称长度|0|  
|*数据类型Ptr|SQL_BINARY|  
|*柱大小|4|  
|*十进制数字Ptr|0|  
|*可空的Ptr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 当使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序对**SQLGetData**进行以下调用以检索书签时：  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 调用映射到**SQLGetStmtOption，fOption**为*fOption*SQL_GET_BOOKMARK，如下所示：  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 *其中 hstmt*和*pvParam*分别设置为*语句处理*和*目标ValuePtr*中的值。 书签在*pvParam* （*目标值Ptr*） 参数指向的缓冲区中返回。 调用**SQLGetData**中*StrLen_or_IndPtr*参数指向的缓冲区中的值设置为 4。  
  
 此映射是必须考虑在调用**SQLGetData**之前调用**SQLFetch**和 ODBC *2.x*驱动程序不支持**SQLAgetFetch**的情况。 在这种情况下 **，SQLFetch**将传递到 ODBC *2.x*驱动程序，在这种情况下不支持书签检索。  
  
 **SQLGetData**不能在 ODBC *2.x*驱动程序中多次调用以检索零件中的书签，因此使用*缓冲区长度*参数设置为小于 4 的值调用**SQLGetData，** 而将*列数*参数设置为 0 将返回 SQLSTATE HY090（无效字符串或缓冲区长度）。 但是 **，SQLGetData**可以多次调用以检索同一个书签。  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 当使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序调用**SQLSetStmtAttr**将SQL_ATTR_USE_BOOKMARKS属性设置为SQL_UB_VARIABLE时，驱动程序管理器将该属性设置为基础 ODBC *2.x*驱动程序中的SQL_UB_ON。
