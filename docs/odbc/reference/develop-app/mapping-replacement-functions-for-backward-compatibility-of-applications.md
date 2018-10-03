---
title: 映射替换函数以应用程序-ODBC 的兼容性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cecc7fcd5ffa7234544dd0a9bc10407b1ea5cb1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626945"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>映射替换函数以实现应用程序后向兼容性
ODBC 3 *.x*应用程序使用 ODBC 3 *.x*驱动程序管理器对 ODBC 2 起作用。*x*驱动程序，只要使用的任何新功能。 复制功能和行为的更改，但是，影响的方式，ODBC 3。*x*应用程序适用于 ODBC 2。*x*驱动程序。 当使用 ODBC 2。*x*驱动程序，驱动程序管理器将映射以下 ODBC 3。*x*函数，它已替换为一个或多个 ODBC 2。*x*函数，到相应的 ODBC 2。*x*函数。  
  
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
  
 [1] 其他操作可能还会采用，具体取决于所请求的属性。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 驱动程序管理器可以将其映射到**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**根据。 以下调用到**SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 将导致在驱动程序管理器中执行以下 (概念、 错误检查) 映射：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 驱动程序管理器可以将其映射到**SQLSetPos**。 以下调用到**SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 将导致以下一系列步骤：  
  
1.  如果操作参数是 SQL_ADD，驱动程序管理器将调用**SQLSetPos** ，如下所示：  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  如果操作参数不是 SQL_ADD，驱动程序将返回 SQLSTATE HY092 （属性/选项标识符无效）。  
  
3.  如果应用程序尝试更改到的调用之间 SQL_ATTR_ROW_STATUS_PTR **SQLFetch**或**SQLFetchScroll**并**SQLBulkOperations**，驱动程序管理器将返回 SQLSTATE HY011 （属性不能立即设置）。  
  
4.  如果操作参数为 SQL_ADD，应用程序必须调用**SQLBindCol**绑定要插入的数据。 它不能调用**SQLSetDescField**或**SQLSetDescRec**绑定要插入的数据。  
  
5.  如果操作参数是 SQL_ADD 和要插入的行数不与当前行集大小，同时**SQLSetStmtAttr**必须调用以将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为要进行的行数在调用之前插入**SQLBulkOperations**。 若要恢复到以前的行集大小，该应用程序必须设置 SQL_ATTR_ROW_ARRAY_SIZE 语句属性之前**SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**调用。  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 驱动程序管理器可以将其映射到**SQLColAttributes**。 以下调用到**SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 将导致以下一系列步骤：  
  
1.  如果*FieldIdentifier*是以下之一：  
  
     SQL_DESC_PRECISION、 SQL_DESC_SCALE、 SQL_DESC_LENGTH、 SQL_DESC_OCTET_LENGTH、 SQL_DESC_UNNAMED、 SQL_DESC_BASE_COLUMN_NAME、 SQL_DESC_LITERAL_PREFIX、 SQL_DESC_LITERAL_SUFFIX 或 SQL_DESC_LOCAL_TYPE_NAME  
  
     驱动程序管理器将返回 SQL_ERROR 具有 SQLSTATE HY091 （无效的描述符字段标识符）。 本部分中没有更多规则适用。  
  
2.  驱动程序管理器将映射 SQL_COLUMN_COUNT、 SQL_COLUMN_NAME 或 SQL_COLUMN_NULLABLE 到 SQL_DESC_COUNT、 SQL_DESC_NAME 或 SQL_DESC_NULLABLE，分别。 (ODBC 2 *.x*驱动程序需要仅支持 SQL_COLUMN_COUNT、 SQL_COLUMN_NAME，和 SQL_COLUMN_NULLABLE、 不 SQL_DESC_COUNT、 SQL_DESC_NAME 和 SQL_DESC_NULLABLE。)SQLColAttribute 对映射到：  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  所有其他*FieldIdentifier*值将传递到该驱动程序，使用**SQLColAttribute**映射到**SQLColAttributes**如上所示。  
  
4.  如果*BufferLength*小于 0，驱动程序管理器返回具有 SQLSTATE HY090 SQL_ERROR （字符串或缓冲区长度无效）。 本部分中没有更多规则适用。  
  
5.  如果*FieldIdentifier* SQL_DESC_CONCISE_TYPE，则返回的类型是简洁的 datetime 数据类型，返回值的日期、 时间和时间戳的代码的驱动程序管理器映射。  
  
6.  驱动程序管理器执行必要的检查以查看是否 SQLSTATE HY010 （函数序列错误） 需要引发。 如果有，驱动程序管理器返回 SQL_ERROR 并且 SQLSTATE HY010 （函数序列错误）。 本部分中没有更多规则适用。  
  
## <a name="sqlendtran"></a>SQLEndTran  
 驱动程序管理器可以将其映射到**SQLTransact**。 以下调用到**SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 将导致在驱动程序管理器中执行以下 (概念、 错误检查) 映射：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 驱动程序管理器可以将其映射到**SQLExtendedFetch**与*FetchOrientation* SQL_FETCH_NEXT 的参数。 以下调用到**SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 驱动程序管理器调用将产生**SQLExtendedFetch**，按如下所示：  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 在此调用中， *pcRow*参数设置为应用程序将设置为通过调用将 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的值**SQLSetStmtAttr**。  
  
> [!NOTE]  
>  当应用程序调用**SQLSetStmtAttr** ，为了将 SQL_ATTR_ROW_STATUS_PTR 设置为指向状态数组，驱动程序管理器缓存指针。 *RowStatusArray*可以是等于 null 指针。  
  
 如果该驱动程序不支持**SQLExtendedFetch**和加载游标库、 驱动程序管理器使用游标库**SQLExtendedFetch**映射**SQLFetch**到**SQLExtendedFetch**。 如果该驱动程序不支持**SQLExtendedFetch**和游标库时未加载，驱动程序管理器将传递到调用**SQLFetch**通过向驱动程序。 如果应用程序调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器可确保填充该数组。 如果应用程序调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ROWS_FETCHED_PTR，驱动程序管理器设置此字段为 1。  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 驱动程序管理器可以将其映射到**SQLExtendedFetch**。 以下调用到**SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 将导致以下一系列步骤：  
  
1.  当应用程序调用**SQLSetStmtAttr**若要设置 SQL_ATTR_ROW_STATUS_PTR （用于在 IRD 中设置 SQL_DESC_ARRAY_STATUS_PTR 字段） 以指向状态数组，驱动程序管理器，将缓存此指针。 允许将此指针*RowStatusArray*; 否则为可让*RowStatusArray*等于 null 指针。 如果*RowStatusArray*参数设置为 null 指针，则驱动程序管理器生成的行状态数组。  
  
2.  如果*FetchOrientation*不是一个 SQL_FETCH_NEXT、 SQL_FETCH_PRIOR、 SQL_FETCH_ABSOLUTE，SQL_FETCH_RELATIVE、 SQL_FETCH_FIRST、 SQL_FETCH_LAST 或 SQL_FETCH_BOOKMARK，驱动程序管理器返回 SQL_ERROR 并且 SQLSTATEHY106 （提取类型超出了范围）。 本部分中没有更多规则适用。  
  
3.  用例：  
  
-   如果*FetchOrientation*等于 SQL_FETCH_BOOKMARK，然后：  
  
    -   如果**SQLSetStmtAttr**调用之前设置的值 SQL_ATTR_FETCH_BOOKMARK_PTR，然后让*Bmk*是通过取消引用指针 SQL_DESC_FETCH_BOOKMARK_PTR 获得的值。  
  
    -   否则，返回具有 SQLSTATE HY111 SQL_ERROR （无效的书签值）。 本部分中没有更多规则适用。  
  
     现在，驱动程序管理器调用**SQLExtendedFetch**，按如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   否则，驱动程序管理器会调用**SQLExtendedFetch**，按如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     在这些调用中， *pcRow*参数设置为应用程序将设置为通过调用将 SQL_ATTR_ROWS_FETCHED_PTR 语句属性的值**SQLSetStmtAttr**。  
  
-   SQL_ATTR_ROW_ARRAY_SIZE 映射到 SQL_ROWSET_SIZE。  
  
-   如果*rc*等于 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，并且如果*FetchOrientation*等于 SQL_FETCH_BOOKMARK 并*FetchOffset*是不等于 0，然后该驱动程序管理器会警告，SQLSTATE 01S10 （尝试提取由书签偏移量，偏移量值被忽略），并返回 SQL_SUCCESS_WITH_INFO。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 驱动程序管理器可以将其映射到**SQLFreeEnv**， **SQLFreeConnect**，或**SQLFreeStmt**根据需要。 以下调用到**SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 将导致在驱动程序管理器中执行以下 (概念、 错误检查) 映射：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 驱动程序管理器可以将其映射到**SQLGetConnectOption**。 以下调用到**SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 将导致以下一系列步骤：  
  
1.  如果*特性*不是驱动程序定义的连接或语句属性并不是 ODBC 2 中定义的属性。*x*，驱动程序管理器将返回 SQL_ERROR 具有 SQLSTATE HY092 （属性/选项标识符无效）。 在本部分中没有更多的规则适用。  
  
2.  如果*特性*等于 SQL_ATTR_AUTO_IPD 或 SQL_ATTR_METADATA_ID，驱动程序管理器返回具有 SQLSTATE HY092 SQL_ERROR （属性/选项标识符无效）。  
  
3.  驱动程序管理器执行必要的检查以查看是否 SQLSTATE 08003 （连接未打开） 或 SQLSTATE HY010 （函数序列错误） 需要引发。 如果是这样，驱动程序管理器将返回 SQL_ERROR，并将发布相应的错误消息。 本部分中没有更多规则适用。  
  
4.  驱动程序管理器调用**SQLGetConnectOption** ，如下所示：  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     请注意， *BufferLength*并*StringLengthPtr*将被忽略。  
  
## <a name="sqlgetdata"></a>SQLGetData  
 当 ODBC 3。*x*应用程序使用 ODBC 2 *.x*驱动程序调用**SQLGetData**与*ColumnNumber*参数等于 0，ODBC 3 *.x*驱动程序管理器将其映射到调用**SQLGetStmtOption**与*选项*属性设置为 SQL_GET_BOOKMARK。  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 驱动程序管理器可以将其映射到**SQLGetStmtOption**。 以下调用到**SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 将导致以下一系列步骤：  
  
1.  如果*特性*不是驱动程序定义的连接或语句属性并不是 ODBC 2 中定义的属性。*x*，驱动程序管理器将返回 SQL_ERROR 具有 SQLSTATE HY092 （属性/选项标识符无效）。 在本部分中没有更多的规则适用。  
  
2.  如果*特性*是以下之一：  
  
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
  
     驱动程序管理器将返回 SQL_ERROR 具有 SQLSTATE HY092 （属性/选项标识符无效）。 本部分中没有更多规则适用。  
  
3.  驱动程序管理器执行必要的检查以查看是否 SQLSTATE HY010 （函数序列错误） 需要引发。 如果有，驱动程序管理器返回 SQL_ERROR 并且 SQLSTATE HY010 （函数序列错误）。 本部分中没有更多规则适用。  
  
4.  如果*特性*等于 SQL_ATTR_ROWS_FETCHED_PTR，驱动程序管理器返回指向内部的驱动程序管理器变量*cRow*，其中具有使用或将在调用中使用它**SQLExtendedFetch**。 本部分中没有更多规则适用。  
  
5.  如果*特性*等于到 SQL_DESC_FETCH_BOOKMARK_PTR，驱动程序管理器返回其缓存在调用的相应指针**SQLSetStmtAttr**。  
  
6.  如果*特性*等于到 SQL_ATTR_ROW_STATUS_PTR，驱动程序管理器返回其缓存在调用的相应指针**SQLSetStmtAttr**。  
  
7.  驱动程序管理器调用**SQLGetStmtOption** ，如下所示：  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     其中*hstmt*， *fOption*，并*pvParam*将设为的值*StatementHandle*，*属性*，并*ValuePtr*分别。 *BufferLength*并*StringLengthPtr*将被忽略。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 驱动程序管理器可以将其映射到**SQLSetConnectOption**。 以下调用到**SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 将导致以下一系列步骤：  
  
1.  如果*特性*不是驱动程序定义的连接或语句属性并不是 ODBC 2 中定义的属性。*x*，驱动程序管理器将返回 SQL_ERROR 具有 SQLSTATE HY092 （属性/选项标识符无效）。 在本部分中没有更多的规则适用。  
  
2.  如果*特性*等于 SQL_ATTR_AUTO_IPD，驱动程序管理器返回具有 SQLSTATE HY092 SQL_ERROR （属性/选项标识符无效）。  
  
3.  驱动程序管理器执行必要的检查以查看是否 SQLSTATE 08003 （连接未打开） 或 SQLSTATE HY010 （函数序列错误） 需要引发。 如果其中一个错误需要引发，驱动程序管理器将返回 SQL_ERROR，并将发布相应的错误消息。 本部分中没有更多规则适用。  
  
4.  驱动程序管理器调用**SQLSetConnectOption** ，如下所示：  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     其中*hdbc*， *fOption*，并*vParam*将设为的值*ConnectionHandle*，*属性*，并*ValuePtr*分别。 *StringLengthPtr*将被忽略。  
  
> [!NOTE]  
>  已弃用的功能在连接级别上设置的语句属性。 语句应该永远不会将属性设置在连接级别上的 ODBC 3。*x*应用程序。  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 驱动程序管理器可以将其映射到**SQLSetStmtOption**。 以下调用到**SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 将导致以下一系列步骤：  
  
1.  如果*特性*不是驱动程序定义的连接或语句属性并不是 ODBC 2 中定义的属性。*x*，驱动程序管理器将返回 SQL_ERROR 具有 SQLSTATE HY092 （属性/选项标识符无效）。 在本部分中没有更多的规则适用。  
  
2.  如果*特性*是以下之一：  
  
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
  
     驱动程序管理器将返回 SQL_ERROR 具有 SQLSTATE HY092 （属性/选项标识符无效）。 本部分中没有更多规则适用。  
  
3.  驱动程序管理器执行必要的检查以查看是否 SQLSTATE HY010 （函数序列错误） 需要引发。 如果有，驱动程序管理器返回 SQL_ERROR 并且 SQLSTATE HY010 （函数序列错误）。 本部分中没有更多规则适用。  
  
4.  如果*特性*本主题中后面是等于 SQL_ATTR_PARAMSET_SIZE 或 SQL_ATTR_PARAMS_PROCESSED_PTR，请参阅"映射为处理参数数组，"一节。 本部分中没有更多规则适用。  
  
5.  如果*特性*等于 SQL_ATTR_ROWS_FETCHED_PTR，指针值用于更高版本的驱动程序管理器缓存**SQLFetchScroll**。  
  
6.  如果*特性*等于 SQL_ATTR_ROW_STATUS_PTR，指针值用于更高版本的驱动程序管理器缓存**SQLFetchScroll**或**SQLSetPos**。 本部分中没有更多规则适用。  
  
7.  如果*特性*等于 SQL_ATTR_FETCH_BOOKMARK_PTR，驱动程序管理器缓存*ValuePtr*并将使用缓存的值更高版本中调用**SQLFetchScroll**。 本部分中没有更多规则适用。  
  
8.  驱动程序管理器调用**SQLSetStmtOption** ，如下所示：  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     其中*hstmt*， *fOption*，并*vParam*将设为的值*StatementHandle*，*属性*，并*ValuePtr*分别。 *StringLength*忽略参数。  
  
     如果检测到 ODBC 2。*x*驱动程序支持字符串、 特定于驱动程序的语句选项，ODBC 3。*x*应用程序应调用**SQLSetStmtOption**设置这些选项。  
  
## <a name="mappings-for-handling-parameter-arrays"></a>用于处理参数数组映射  
 当应用程序调用：  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 驱动程序管理器调用：  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 驱动程序管理器更高版本返回一个指向此变量时在应用程序调用**SQLGetStmtAttr**检索 SQL_ATTR_PARAMS_PROCESSED_PTR。 驱动程序管理器不能更改此内部变量，直到语句句柄返回到已准备好或已分配状态。  
  
 ODBC 3。*x*应用程序可以调用**SQLGetStmtAttr**即使 APD 中的 SQL_DESC_ARRAY_SIZE 字段未显式设置，它具有获取 SQL_ATTR_PARAMS_PROCESSED_PTR 的值。 这种情况下也可能会发生，例如，应用程序必须检查当前"行"的参数的通用例程时正在处理**SQLExecute**返回 SQL_NEED_DATA。 此例程调用是否 SQL_DESC_ARRAY_SIZE 为 1 或大于 1。 若要考虑到这一点，驱动程序管理器将需要定义此内部变量是否已调用应用程序**SQLSetStmtAttr**设置 APD 中的 SQL_DESC_ARRAY_SIZE 字段。 如果尚未设置 SQL_DESC_ARRAY_SIZE，驱动程序管理器必须确保此变量包含之前从返回的值 1 **SQLExecDirect**或**SQLExecute**。  
  
## <a name="error-handling"></a>错误处理  
 在 ODBC 3。*x*，则调用**SQLFetch**或**SQLFetchScroll**填充 SQL_DESC_ARRAY_STATUS_PTR IRD 和给定的诊断记录的 SQL_DIAG_ROW_NUMBER 字段中包含与此记录相关的行集中的行数。 使用此，应用程序可以与给定的行位置关联的错误消息。  
  
 ODBC 2。*x*驱动程序将不能提供此功能。 但是，它将提供具有 SQLSTATE 01S01 错误分界 （行中的错误）。 ODBC 3。*x*正在使用的应用程序**SQLFetch**或**SQLFetchScroll**时将对 ODBC 2。*x*驱动程序需要考虑这一点。 此类应用程序将不能调用另请注意**SQLGetDiagField**实际上是否仍要获取 SQL_DIAG_ROW_NUMBER 字段。 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序将能够调用**SQLGetDiagField**仅与*DiagIdentifier* SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_NATIVE、 SQL_DIAG_RETURNCODE 或 SQL_DIAG_ 的参数SQLSTATE。 ODBC 3 *.x*驱动程序管理器维护的诊断数据结构时使用的 ODBC 2。*x*驱动程序，但 ODBC 2。*x*驱动程序将返回仅这四个字段。  
  
 当 ODBC 2。*x*应用程序使用 ODBC 2。*x*驱动程序，如果某项操作可能会导致多个错误返回由驱动程序管理器中，不同的错误可能返回的 ODBC 3 *.x*比 ODBC 2 的驱动程序管理器。*x*驱动程序管理器。  
  
## <a name="mappings-for-bookmark-operations"></a>书签操作的映射  
 ODBC 3 *.x*驱动程序管理器执行以下映射时 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序执行书签操作。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用**SQLBindCol**要绑定到列 0 *fCType*等于 SQL_C_VARBOOKMARK，ODBC 3 *.x*驱动程序管理器会检查是否*BufferLength*参数小于 4 或大于 4，以及如果是这样，将返回 SQLSTATE HY090 （字符串或缓冲区长度无效）。 如果*BufferLength*参数为等于 4，驱动程序管理器调用**SQLBindCol**中的驱动程序，替换后*fCType* SQL_C_BOOKMARK 使用。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用**SQLColAttribute**与*ColumnNumber*参数设置为 0，驱动程序管理器返回*FieldIdentifier*值下表中列出。  
  
|*FieldIdentifier*|ReplTest1|  
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
 当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用**SQLDescribeCol**与*ColumnNumber*参数设置为 0，驱动程序管理器将返回下表中列出的值。  
  
|缓冲区|ReplTest1|  
|------------|-----------|  
|ColumnName|""（空字符串）|  
|* NameLengthPtr|0|  
|* DataTypePtr|SQL_BINARY|  
|* ColumnSizePtr|4|  
|* DecimalDigitsPtr|0|  
|* NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序，可以对以下调用**SQLGetData**检索书签：  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 在调用映射到**SQLGetStmtOption**与*fOption*的 SQL_GET_BOOKMARK，按如下所示：  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 其中*hstmt*并*pvParam*设置为中的值*StatementHandle*并*TargetValuePtr*分别。 指向的缓冲区中返回该书签*pvParam* (*TargetValuePtr*) 参数。 指向缓冲区中的值*StrLen_or_IndPtr*调用中的参数**SQLGetData**设置为 4。  
  
 此映射是帐户中的事例所需**SQLFetch**在调用之前调用了**SQLGetData**和 ODBC 2。*x*驱动程序不支持**SQLExtendedFetch**。 在这种情况下， **SQLFetch**将通过传递到 ODBC 2。*x*驱动程序，在其中不支持 case 书签检索。  
  
 **SQLGetData**不能在 ODBC 2 中调用多次。*x*驱动程序检索中部分，因此调用的书签**SQLGetData**与*BufferLength*参数设置为小于 4 的值和*ColumnNumber*设置为 0 的参数将返回 SQLSTATE HY090 （字符串或缓冲区长度无效）。 **SQLGetData** ，但是，可以调用多次来检索同一书签。  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 当 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序调用**SQLSetStmtAttr**若要设置到 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 属性，驱动程序管理器属性设置为在基础 ODBC 2 SQL_UB_ON。*x*驱动程序。
