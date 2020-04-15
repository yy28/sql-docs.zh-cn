---
title: SQLBulk 操作函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f4f294a6d84856bc3065b599a370bb5658e3ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301327"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 函数
**一致性**  
 版本介绍： ODBC 3.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLBulk操作**执行批量插入和批量书签操作，包括按书签更新、删除和提取。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *操作*  
 [输入]操作以执行：  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARKSQL_DELETE_BY_BOOKMARKSQL_DELETE_BY_BOOKMARKSQL_ADDSQL_FETCH_BY_BOOKMARK  
  
 有关详细信息，请参阅"注释"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBulk 操作**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLBulk 操作**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
 对于可以返回SQL_SUCCESS_WITH_INFO或SQL_ERROR的所有 SQLSTAT（01xxx SQLSTATEs 除外），如果多行操作的一个或多个行发生错误（但不是全部）发生错误，则返回SQL_SUCCESS_WITH_INFO，如果单行操作发生错误，则返回SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据右截断|*SQL_FETCH_BY_BOOKMARK操作*参数，为数据类型为SQL_C_CHAR或SQL_C_BINARY的列返回的字符串或二进制数据会导致非空白字符或非 NULL 二进制数据的截断。|  
|01S01|行中的错误|*操作*参数SQL_ADD，在执行操作时，一个或多个行中发生错误，但至少已成功添加一行。 （函数返回SQL_SUCCESS_WITH_INFO。<br /><br /> （仅当应用程序使用 ODBC 2 时，才会引发此错误。*x*驱动程序。|  
|01S07|分数截断|*操作*参数SQL_FETCH_BY_BOOKMARK，应用程序缓冲区的数据类型未SQL_C_CHAR或SQL_C_BINARY，返回到一个或多个列的应用程序缓冲区的数据被截断。 （对于数字 C 数据类型，数字的小数部分被截断。 对于包含时间组件的时间、时间戳和间隔 C 数据类型，时间的小数部分被截断。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|*操作*参数SQL_FETCH_BY_BOOKMARK，并且结果集中列的数据值无法转换为对**SQLBindCol**调用中*的目标类型*参数指定的数据类型。<br /><br /> *操作*参数SQL_UPDATE_BY_BOOKMARK或SQL_ADD，并且应用程序缓冲区中的数据值无法转换为结果集中列的数据类型。|  
|07009|无效描述符索引|参数*操作*SQL_ADD，并且对列绑定的列数大于结果集中的列数。|  
|21S02|派生表的程度与列列表不匹配|参数*操作*是SQL_UPDATE_BY_BOOKMARK;并且没有列是可向上的，因为所有列都是未绑定的或只读的，或者绑定长度/指示器缓冲区中的值SQL_COLUMN_IGNORE。|  
|22001|字符串数据右截断|将字符或二进制值分配给结果集中的列会导致截断非空白（对于字符）或非空字符（二进制字符或字节）。|  
|22003|数值超范围|*操作*参数SQL_ADD或SQL_UPDATE_BY_BOOKMARK，并将数值分配给结果集中的列会导致数字的整个（而不是小数）部分被截断。<br /><br /> 参数*操作*SQL_FETCH_BY_BOOKMARK，返回一个或多个绑定列的数值将导致重要数字的损失。|  
|22007|无效日期时间格式|*操作*参数SQL_ADD或SQL_UPDATE_BY_BOOKMARK，并将日期或时间戳值分配给结果集中的列会导致年份、月份或日字段超过范围。<br /><br /> 参数*操作*SQL_FETCH_BY_BOOKMARK，返回一个或多个绑定列的日期或时间戳值将导致年份、月份或日字段超出范围。|  
|22008|日期/时间字段溢出|*操作*参数SQL_ADD或SQL_UPDATE_BY_BOOKMARK，并且对发送到结果集中的列的数据执行日期时间算术，导致结果超出字段允许的值范围或根据公历的约会时间的自然规则无效的约会时间字段（年份、月份、日、小时、分钟或第二个字段）。<br /><br /> *操作*参数SQL_FETCH_BY_BOOKMARK，并且对从结果集中检索的数据执行日期时间算术，导致结果的日期时间字段（年份、月份、天、小时、分钟或第二个字段）超出字段的允许值范围，或者根据公历的约会时间自然规则无效。|  
|22015|间隔字段溢出|*操作*参数SQL_ADD或SQL_UPDATE_BY_BOOKMARK，将精确数字或间隔 C 类型分配给间隔 SQL 数据类型会导致重要数字丢失。<br /><br /> *操作*参数SQL_ADD或SQL_UPDATE_BY_BOOKMARK;当分配给间隔 SQL 类型时，间隔 SQL 类型中没有 C 类型的值表示形式。<br /><br /> *操作*参数SQL_FETCH_BY_BOOKMARK，并将精确的数字或间隔 SQL 类型分配给间隔 C 类型会导致前导字段中的重要数字丢失。<br /><br /> *行动*论点SQL_FETCH_BY_BOOKMARK;当分配给间隔 C 类型时，间隔 C 类型中没有 SQL 类型的值表示形式。|  
|22018|强制转换规范的无效字符值|*行动*论点SQL_FETCH_BY_BOOKMARK;C 类型是精确或近似的数字、日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;列中的值不是绑定 C 类型的有效文本。<br /><br /> 参数*操作*SQL_ADD或SQL_UPDATE_BY_BOOKMARK;SQL 类型是精确或近似的数字、日期时间或间隔数据类型;C 类型为SQL_C_CHAR;列中的值不是绑定 SQL 类型的有效文本。|  
|23000|完整性约束冲突|*操作*参数SQL_ADD、SQL_DELETE_BY_BOOKMARK或SQL_UPDATE_BY_BOOKMARK，并且违反了完整性约束。<br /><br /> *操作*参数SQL_ADD，未绑定的列定义为非 NULL 且没有默认值。<br /><br /> *操作*参数SQL_ADD，在绑定*StrLen_or_IndPtr*缓冲区中指定的长度SQL_COLUMN_IGNORE，并且列没有默认值。|  
|24000|无效的游标状态|*语句句柄*处于已执行状态，但没有与*语句句柄*关联的结果集。|  
|40001|序列化失败|由于资源与另一个事务死锁，事务被回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|42000|语法错误或访问冲突|驱动程序无法根据需要锁定该行，以执行*操作*参数中请求的操作。|  
|44000|与检查选项冲突|*操作*参数SQL_ADD或SQL_UPDATE_BY_BOOKMARK，插入或更新是在通过指定 **"使用 CHECK 选项**"创建的已查看表（或从已查看表派生的表）上执行的，这样受插入或更新影响的一个或多个行将不再存在于查看的表中。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**调用了*语句句柄*。 然后在*语句处理*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLBulk 操作**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore 结果**被调用语句*句柄*并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecDirect** 在检索所有流参数的数据之前，已调用此函数。<br /><br /> （DM） 指定的*语句句柄*未处于执行状态。 调用该函数时没有首先调用**SQLExecDirect、SQLExecute**或目录函数。 **SQLExecute**<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLSetPos**被调用用于*语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） 驱动程序是 ODBC 2。*x*驱动程序，在调用**SQLFetchScroll**或**SQLFetch**之前，调用**SQLBulk 操作**为*语句句柄*。<br /><br /> （DM） **SQLBulk操作**是在语句*句柄*上调用**SQL 扩展获取**后调用的。|  
|HY011|无法立即设置属性|（DM） 驱动程序是 ODBC 2。*x*驱动程序，并在对**SQLFetch**或**SQLFetchScroll**和**SQLBulk 操作**的调用之间设置了SQL_ATTR_ROW_STATUS_PTR语句属性。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|*操作*参数SQL_ADD或SQL_UPDATE_BY_BOOKMARK;数据值不是空指针;数据值不是空指针。C 数据类型为SQL_C_BINARY或SQL_C_CHAR;并且列长度值小于 0，但不等于SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS或SQL_NULL_DATA，或小于或等于SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 长度/指示器缓冲区中的值SQL_DATA_AT_EXEC;SQL 类型要么是SQL_LONGVARCHAR、SQL_LONGVARBINARY，要么是长数据源特定的数据类型;**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN信息类型为"Y"。<br /><br /> *操作*参数SQL_ADD，SQL_ATTR_USE_BOOKMARK语句属性设置为SQL_UB_VARIABLE，第 0 列绑定到长度不等于此结果集书签的最大长度的缓冲区。 （此长度在 IRD 的SQL_DESC_OCTET_LENGTH字段中可用，可以通过调用**SQLDescribeCol、SQLColattribute**或**SQLGetDescField**获得。 **SQLColAttribute**|  
|HY092|无效属性标识符|（DM） 为*操作*参数指定的值无效。<br /><br /> *操作*参数SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或SQL_DELETE_BY_BOOKMARK，SQL_ATTR_CONCURRENCY语句属性设置为SQL_CONCUR_READ_ONLY。<br /><br /> *操作*参数SQL_DELETE_BY_BOOKMARK、SQL_FETCH_BY_BOOKMARK或SQL_UPDATE_BY_BOOKMARK，书签列未绑定，或者SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_OFF。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持*操作*参数中请求的操作。|  
|HYT00|超时时间已到|查询超时期限在数据源返回结果集之前已过期。 超时期间通过**SQLSetStmtAttr**设置，*属性*参数为SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
  
> [!CAUTION]  
>  有关哪些语句声明**SQLBulk 操作**可以调用，以及它必须做什么才能与 ODBC 2 兼容。*x*应用程序，请参阅附录 G：向后兼容性的驱动程序指南中的[块光标、可滚动光标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)部分。  
  
 应用程序使用**SQLBulk操作**对与当前查询对应的基表或视图执行以下操作：  
  
-   添加新行。  
  
-   更新一组行，其中每行由书签标识。  
  
-   删除一组行，其中每行由书签标识。  
  
-   获取一组行，其中每行由书签标识。  
  
 调用**SQLBulk 操作**后，块游标位置未定义。 应用程序必须调用**SQLFetchScroll**来设置光标位置。 应用程序应仅使用SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_ABSOLUTE或SQL_FETCH_BOOKMARK的 Fetch 方向参数调用**SQLFetchScroll。** *FetchOrientation* 如果应用程序调用**SQLFetch**或**SQLFetchScroll，** 并带有SQL_FETCH_PRIOR、SQL_FETCH_NEXT或SQL_FETCH_RELATIVE*的提取方向*参数，则游标位置未定义。  
  
 通过将调用**SQLBindCol**中指定的列长度/指示器缓冲区设置为SQL_COLUMN_IGNORE，可以在对**SQLBulk 操作**执行的批量操作中忽略列。  
  
 应用程序在调用**SQLBulk 操作**时不必设置SQL_ATTR_ROW_OPERATION_PTR语句属性，因为使用此函数执行批量操作时不能忽略行。  
  
 SQL_ATTR_ROWS_FETCHED_PTR 语句属性指向的缓冲区包含受对**SQLBulk 操作**的调用影响的行数。  
  
 当*操作*参数SQL_ADD或SQL_UPDATE_BY_BOOKMARK，并且与游标关联的查询规范的选择列表包含对同一列的多个引用时，它是驱动程序定义的，无论是生成错误还是驱动程序忽略重复的引用并执行请求的操作。  
  
 有关如何使用**SQLBulk 操作**的详细信息，请参阅使用[SQLBulk 操作更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。  
  
## <a name="performing-bulk-inserts"></a>执行批量插入  
 若要使用**SQLBulk 操作**插入数据，应用程序将执行以下步骤序列：  
  
1.  执行返回结果集的查询。  
  
2.  将SQL_ATTR_ROW_ARRAY_SIZE语句属性设置为要插入的行数。  
  
3.  调用**SQLBindCol**以绑定要插入的数据。 数据绑定到大小等于SQL_ATTR_ROW_ARRAY_SIZE值的数组。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 语句属性指向的数组的大小应等于SQL_ATTR_ROW_ARRAY_SIZE，SQL_ATTR_ROW_STATUS_PTR应为空指针。  
  
4.  调用**SQLBulk 操作**（*语句句柄，SQL_ADD）* 以执行插入。  
  
5.  如果应用程序设置了SQL_ATTR_ROW_STATUS_PTR语句属性，则可以检查此数组以查看操作的结果。  
  
 如果应用程序在调用**SQLBulk 操作**之前绑定列 0，该*参数*为 SQL_ADD，则驱动程序将使用新插入行的书签值更新绑定列 0 缓冲区。 为此，应用程序必须在执行语句之前将SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE。 （这不适用于 ODBC 2。*x*驱动程序。  
  
 通过使用对 SQLParamData 和 SQLPutData 的调用，SQLBulk 操作可以分部分添加长数据。 有关详细信息，请参阅此函数引用后面的"为批量插入和更新提供长数据"。  
  
 应用程序无需在调用**SQLBulk 操作**之前调用**SQLFetch**或**SQLFetchScroll（** 与 ODBC 2 相比除外）。*x*驱动程序;请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 如果**SQLBulk 操作**（*操作参数为*SQL_ADD）在包含重复列的游标上调用，则该行为是驱动程序定义的。 驱动程序可以返回驱动程序定义的 SQLSTATE，将数据添加到结果集中显示的第一列，或执行其他驱动程序定义的行为。  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>使用书签执行批量更新  
 要使用带有**SQLBulk 操作**的书签执行批量更新，应用程序按顺序执行以下步骤：  
  
1.  将SQL_ATTR_USE_BOOKMARKS语句属性设置到SQL_UB_VARIABLE。  
  
2.  执行返回结果集的查询。  
  
3.  将SQL_ATTR_ROW_ARRAY_SIZE语句属性设置为要更新的行数。  
  
4.  调用**SQLBindCol**以绑定要更新的数据。 数据绑定到大小等于SQL_ATTR_ROW_ARRAY_SIZE值的数组。 它还调用**SQLBindCol**来绑定列 0（书签列）。  
  
5.  复制它有兴趣更新到绑定到列 0 的数组中的行的书签。  
  
6.  更新绑定缓冲区中的数据。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 语句属性指向的数组的大小应等于SQL_ATTR_ROW_ARRAY_SIZE，或者SQL_ATTR_ROW_STATUS_PTR应为空指针。  
  
7.  调用**SQLBulk 操作**（*语句句柄，* SQL_UPDATE_BY_BOOKMARK）。  
  
    > [!NOTE]  
    >  如果应用程序设置了SQL_ATTR_ROW_STATUS_PTR语句属性，则可以检查此数组以查看操作的结果。  
  
8.  可选地调用**SQLBulk 操作**（*语句处理*，SQL_FETCH_BY_BOOKMARK），将数据提取到绑定的应用程序缓冲区中，以验证是否发生了更新。  
  
9. 如果数据已更新，驱动程序将相应行的行状态数组中的值更改为SQL_ROW_UPDATED。  
  
 **SQLBulk 操作**执行的批量更新可以通过调用**SQLParamData**和**SQLPutData**来包括长数据。 有关详细信息，请参阅此函数引用后面的"为批量插入和更新提供长数据"。  
  
 如果书签在游标之间保留，则应用程序不需要在按书签更新之前调用**SQLFetch**或**SQLFetchScroll。** 它可以使用从前一个游标存储的书签。 如果书签不保留在游标上，则应用程序必须调用**SQLFetch**或**SQLFetchScroll**来检索书签。  
  
 如果**SQLBulk 操作**（*操作参数为*SQL_UPDATE_BY_BOOKMARK）在包含重复列的游标上调用，则该行为是驱动程序定义的。 驱动程序可以返回驱动程序定义的 SQLSTATE、更新结果集中显示的第一列或执行其他驱动程序定义的行为。  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>使用书签执行批量提取  
 要使用**SQLBulk 操作**中的书签执行批量提取，应用程序按顺序执行以下步骤：  
  
1.  将SQL_ATTR_USE_BOOKMARKS语句属性设置到SQL_UB_VARIABLE。  
  
2.  执行返回结果集的查询。  
  
3.  将SQL_ATTR_ROW_ARRAY_SIZE语句属性设置为要提取的行数。  
  
4.  调用**SQLBindCol**以绑定要获取的数据。 数据绑定到大小等于SQL_ATTR_ROW_ARRAY_SIZE值的数组。 它还调用**SQLBindCol**来绑定列 0（书签列）。  
  
5.  复制它有兴趣提取到绑定到列 0 的数组中的行的书签。 （这假定应用程序已单独获取书签。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 语句属性指向的数组的大小应等于SQL_ATTR_ROW_ARRAY_SIZE，或者SQL_ATTR_ROW_STATUS_PTR应为空指针。  
  
6.  调用**SQLBulk 操作**（*语句句柄，* SQL_FETCH_BY_BOOKMARK）。  
  
7.  如果应用程序设置了SQL_ATTR_ROW_STATUS_PTR语句属性，则可以检查此数组以查看操作的结果。  
  
 如果书签在游标之间保留，则应用程序不需要在通过书签获取之前调用**SQLFetch**或**SQLFetchScroll。** 它可以使用从前一个游标存储的书签。 如果书签不保留在游标上，则应用程序必须调用**SQLFetch**或**SQLFetchScroll**一次才能检索书签。  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>使用书签执行批量删除  
 要使用**SQLBulk 操作**中的书签执行批量删除，应用程序按顺序执行以下步骤：  
  
1.  将SQL_ATTR_USE_BOOKMARKS语句属性设置到SQL_UB_VARIABLE。  
  
2.  执行返回结果集的查询。  
  
3.  将SQL_ATTR_ROW_ARRAY_SIZE语句属性设置为要删除的行数。  
  
4.  调用**SQLBindCol**绑定列 0（书签列）。  
  
5.  复制它有兴趣删除到列 0 列的数组中的行的书签。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 语句属性指向的数组的大小应等于SQL_ATTR_ROW_ARRAY_SIZE，或者SQL_ATTR_ROW_STATUS_PTR应为空指针。  
  
6.  调用**SQLBulk 操作**（*语句句柄，* SQL_DELETE_BY_BOOKMARK）。  
  
7.  如果应用程序设置了SQL_ATTR_ROW_STATUS_PTR语句属性，则可以检查此数组以查看操作的结果。  
  
 如果书签在游标之间保留，则应用程序不必在按书签删除之前调用**SQLFetch**或**SQLFetchScroll。** 它可以使用从前一个游标存储的书签。 如果书签不保留在游标上，则应用程序必须调用**SQLFetch**或**SQLFetchScroll**一次才能检索书签。  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>为批量插入和更新提供长数据  
 可以为通过调用**SQLBulk 操作**执行的批量插入和更新提供长数据。 若要插入或更新长数据，应用程序除了在本主题前面"执行批量插入"和"使用书签执行批量更新"部分中描述的步骤外，还执行以下步骤。  
  
1.  当应用程序使用**SQLBindCol**绑定数据时，应用程序将应用程序定义的值（如列号）放在*\*TargetValuePtr*缓冲区中，用于执行时的数据列。 该值以后可用于标识列。  
  
     应用程序将SQL_LEN_DATA_AT_EXEC（*长度*）宏的结果放在*\*StrLen_or_IndPtr*缓冲区中。 如果列的 SQL 数据类型SQL_LONGVARBINARY、SQL_LONGVARCHAR 或长数据源特定的数据类型，并且驱动程序返回**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN信息类型的"Y"，*则长度*是要为参数发送的数据字节数;否则，它必须是非负值，并且被忽略。  
  
2.  当调用**SQLBulk 操作时**，如果存在执行时的数据列，则函数将返回SQL_NEED_DATA并继续执行步骤 3，如下所示。 （如果没有执行时的数据列，则该过程已完成。  
  
3.  应用程序调用**SQLParamData**检索*\*要*处理的第一个执行数据列的 TargetValuePtr 缓冲区的地址。 **SQLParamData**返回SQL_NEED_DATA。 应用程序从*\*TargetValuePtr*缓冲区检索应用程序定义的值。  
  
    > [!NOTE]  
    >  尽管执行时的数据参数类似于执行时的数据列，但**SQLParamData**返回的值因每个参数而异。  
  
     执行时的数据列是行集中的列，当使用**SQLBulk 操作**更新或插入行时，将随**SQLPutData**一起发送数据。 它们与**SQLBindCol**绑定。 **SQLParamData**返回的值是正在处理的 @*TargetValuePtr*缓冲区中的行的地址。  
  
4.  应用程序调用**SQLPutData**一次或多次以发送列的数据。 如果在**SQLPutData**中指定的*\*TargetValuePtr*缓冲区中无法返回所有数据值，则需要多个调用。仅当将字符 C 数据发送到具有字符、二进制或数据源特定数据类型的列或将二进制 C 数据发送到具有字符、二进制或数据源特定数据类型的列时，才允许对同一列的**SQLPutData**进行多次调用。  
  
5.  应用程序再次调用**SQLParamData**以发出已为该列发送所有数据的信号。  
  
    -   如果有更多的执行数据列 **，SQLParamData**将返回要处理的下一个执行数据列的SQL_NEED_DATA和目标*ValuePtr*缓冲区的地址。 应用程序重复步骤 4 和 5。  
  
    -   如果没有更多的数据执行列，该过程将完成。 如果语句成功执行 **，SQLParamData**将返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO;如果执行失败，它将返回SQL_ERROR。 此时 **，SQLParamData**可以返回**SQLBulk 操作**可以返回的任何 SQLSTATE。  
  
 如果**SQLBulk 操作**返回SQL_NEED_DATA后**SQLParamData**或**SQLPutData**中发生错误，并且在发送所有数据执行列的数据之前，应用程序只能调用 SQLCancel、SQLGetDiagField、SQLGetDiagRec、SQLGet**函数****、SQLParamData**或**SQLPutData**的语句或与语句关联的连接。 **SQLCancel** **SQLGetDiagField** **SQLGetDiagRec** 如果它调用语句或与 语句关联的连接的任何其他函数，则函数将返回SQL_ERROR和 SQLSTATE HY010（函数序列错误）。  
  
 如果应用程序调用**SQLCancel，** 而驱动程序仍然需要执行时的数据列，则驱动程序将取消该操作。 然后，应用程序可以再次调用**SQLBulk 操作**;取消不会影响光标状态或当前游标位置。  
  
## <a name="row-status-array"></a>行状态数组  
 行状态数组包含行集中每行数据在调用**SQLBulk 操作**后的状态值。 调用 SQLFetch、SQLFetchScroll、SQLSetPos**SQLFetch**或**SQLBulk 操作**后**SQLSetPos**，驱动程序将设置此数组中的状态值。 **SQLFetchScroll** 如果**SQLFetch**或**SQLFetchScroll**尚未在**SQLBulk 操作**之前调用，则此数组最初由对**SQLBulk 操作的**调用填充。 此数组由SQL_ATTR_ROW_STATUS_PTR语句属性指向。 行状态数组中的元素数必须等于行集中的行数（由SQL_ATTR_ROW_ARRAY_SIZE语句属性定义）。 有关此行状态数组的信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>代码示例  
 下面的示例一次从"客户"表中获取 10 行数据。 然后，它会提示用户执行操作。 为了减少网络流量，示例缓冲区在绑定数组中本地更新、删除和插入，但在偏移量超过行集数据时。 当用户选择向数据源发送更新、删除和插入时，代码将适当地设置绑定偏移量并调用**SQLBulk 操作**。 为简单起见，用户不能缓冲超过 10 个更新、删除或插入。  
  
```cpp  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|获取描述符的单个字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取描述符的多个字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置描述符的单个字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置描述符的多个字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|定位光标、刷新行集中中的数据或更新或删除行集中中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
