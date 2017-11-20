---
title: "SQLBulkOperations 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ea439a41a6a3d42c9266bbccfe53aace1c0f37f4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLBulkOperations**执行大容量插入和大容量书签操作，包括更新、 删除和提取由书签。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *运算*  
 [输入]要执行的操作：  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 有关详细信息，请参阅"注释"。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR，或 SQL_INVALID_HANDLE 中。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBulkOperations**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLBulkOperations**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明. 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
 对于所有这些 SQLSTATEs 可以返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除外 01xxx SQLSTATEs)，将返回 SQL_SUCCESS_WITH_INFO，如果将上一个或多个，但并非所有行的一个多行的操作，发生错误时，如果上发生错误时返回 SQL_ERROR单行更行操作。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据右侧被截断|*操作*自变量为 SQL_FETCH_BY_BOOKMARK，和字符串或二进制数据返回为一列或列数据类型为 SQL_C_CHAR 或 SQL_C_BINARY 导致非空白字符或非 NULL 二进制数据截断。|  
|01S01|行中的错误|*操作*自变量为 SQL_ADD，和执行操作时，一个或多个行中发生错误但至少有一行已成功添加。 （函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> （仅当应用程序使用 ODBC 2 时，会引发此错误。*x*驱动程序。)|  
|01S07|小数部分组成的截断|*操作*自变量为 SQL_FETCH_BY_BOOKMARK，应用程序缓冲区的数据类型不是 SQL_C_CHAR 或 SQL_C_BINARY，并且返回到应用程序的缓冲区的一个或多个列的数据被截断。 （对于数值 C 数据类型，已截断的数字的小数部分。 对于时间、 时间戳，和包含时间组件的 interval C 数据类型，时间的小数部分被截断。）<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|*操作*自变量为 SQL_FETCH_BY_BOOKMARK，并且无法转换的结果集中的列的数据值，由指定的数据类型为*TargetType*对调用中的参数**SQLBindCol**。<br /><br /> *操作*参数为 SQL_UPDATE_BY_BOOKMARK 或 SQL_ADD，并为结果集中的列的数据类型，无法转换的应用程序缓冲区中的数据值。|  
|07009|无效的描述符索引|自变量*操作*已 SQL_ADD，并将其列已绑定与一个大于结果集中的列数的列数。|  
|21S02|派生表的等级与列列表不匹配|自变量*操作*SQL_UPDATE_BY_BOOKMARK; 但没有列已更新，因为所有列是未绑定或只读的或绑定的长度/指示器缓冲区中的值为 SQL_COLUMN_IGNORE。|  
|22001|字符串数据右侧被截断|字符或二进制值到结果集中的列分配导致非空白 （对于字符为单位） 或 （对于二进制） 的非 null 字符或字节数的截断。|  
|22003|数值超出范围|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，和的数值与结果集中的列分配导致整个 （而不是小数部分组成） 的部分将被截断。<br /><br /> 自变量*操作*SQL_FETCH_BY_BOOKMARK，并返回数值的一个或多个绑定的列可能会导致重要数字丢失。|  
|22007|无效的日期时间格式|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，并分配到结果集中的列的日期或时间戳值导致年、 月或天将超出范围的字段。<br /><br /> 自变量*操作*SQL_FETCH_BY_BOOKMARK，并返回一个或多个绑定的列的日期或时间戳值将造成年、 月或天将超出范围的字段。|  
|22008|日期/时间字段溢出|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，和 datetime 算术上发送到结果集中的列数据的性能产生的 datetime 字段 （年、 月、 日、 小时、 分钟或秒字段） 的结果为该字段值的允许范围升降或正在基于公历的自然规则进行 datetime 无效。<br /><br /> *操作*自变量为 SQL_FETCH_BY_BOOKMARK，和 datetime 算术对正在检索从结果集中的数据的性能产生的日期时间字段 （年、 月、 日、 小时、 分钟、 或第二个字段）为该字段的允许范围内的值落或无效的结果基于公历的自然规则进行日期时间。|  
|22015|间隔字段溢出|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，以及分配的精确数字或为 SQL 数据类型的间隔的间隔 C 类型导致重要数字丢失。<br /><br /> *操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK; 将分配给 SQL 类型的时间间隔，没有任何值的表示形式的 C 类型在时间间隔内 SQL 类型。<br /><br /> *操作*自变量为 SQL_FETCH_BY_BOOKMARK，并将从精确数字或间隔 SQL 类型分配给间隔 C 类型中的前导字段导致重要数字丢失。<br /><br /> *操作*自变量为 SQL_FETCH_BY_BOOKMARK; 当将分配给间隔 C 类型，存在为没有间隔 C 类型中的 SQL 类型的值的表示形式。|  
|22018|转换指定的的无效字符值|*操作*自变量为 SQL_FETCH_BY_BOOKMARK; C 类型是准确或近似数字、 日期时间或间隔数据类型; 的 SQL 类型的列是字符数据类型; 并且列中的值不是有效绑定的 C 类型的文本。<br /><br /> 自变量*操作*SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK; SQL 类型是准确或近似数字、 日期时间或间隔数据类型; C 类型为 SQL_C_CHAR; 并且在列中的值不是有效的文本的绑定 SQL 类型。|  
|23000|完整性约束冲突|*操作*参数为 SQL_ADD、 SQL_DELETE_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK，和违反了完整性约束。<br /><br /> *操作*自变量为 SQL_ADD，和未绑定的列被定义为不为 NULL 且没有默认值。<br /><br /> *操作*自变量为 SQL_ADD，在绑定中指定的长度*StrLen_or_IndPtr*缓冲区是否 SQL_COLUMN_IGNORE，和列没有默认值。|  
|24000|无效的游标状态|*StatementHandle*处于执行状态，但没有结果集与关联*StatementHandle*。|  
|40001|序列化失败|事务已回滚，由于资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|42000|语法错误或访问冲突|该驱动程序无法锁定行所需执行请求中的操作*操作*自变量。|  
|44000|WITH CHECK OPTION 冲突|*操作*自变量为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK 和插入或查看的表上执行更新 （或派生自查看表的表） 创建通过指定**WITH CHECK OPTION**，一个或多个行受插入或更新不再将在查看的表中显示的方式。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLBulkOperations**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 第一个调用已调用函数**SQLExecDirect**， **SQLExecute**，或目录函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) 驱动程序是 ODBC 2。*x*驱动程序，和**SQLBulkOperations**曾为*StatementHandle*之前**SQLFetchScroll**或**SQLFetch**调用。<br /><br /> (DM) **SQLBulkOperations**之后调用**SQLExtendedFetch**上调用了*StatementHandle*。|  
|HY011|现在无法设置属性|(DM) 驱动程序是 ODBC 2。*x*驱动程序，以及 SQL_ATTR_ROW_STATUS_PTR 语句属性已设置到的调用之间**SQLFetch**或**SQLFetchScroll**和**SQLBulkOperations**.|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK; 数据值不是 null 指针; C 数据类型不 SQL_C_BINARY 或 SQL_C_CHAR; 和列长度值已小于 0，但不是等于 SQL_DATA_AT_EXECSQL_COLUMN_IGNORE、 sql_nts 以或 SQL_NULL_DATA，或小于或等于 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 长度/指示器缓冲区中的值为 SQL_DATA_AT_EXEC;SQL 类型已 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 数据源 – 特定数据类型;和中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**已"Y"。<br /><br /> *操作*自变量为 SQL_ADD，SQL_ATTR_USE_BOOKMARK 语句属性已设置为 SQL_UB_VARIABLE，以及第 0 列已绑定到其的长度不等于该结果集的书签的最大长度的缓冲区。 (此长度的 IRD SQL_DESC_OCTET_LENGTH 字段中是否可用，并可以通过调用获取**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY092|无效的属性标识符|(DM) 为指定的值*操作*自变量无效。<br /><br /> *操作*参数为 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，且 SQL_ATTR_CONCURRENCY 语句属性被设置为 SQL_CONCUR_READ_ONLY。<br /><br /> *操作*参数为 SQL_DELETE_BY_BOOKMARK、 SQL_FETCH_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK，和未绑定的书签列或者 SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_OFF。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持请求中的操作*操作*自变量。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回了结果集。 通过设置的超时期限**SQLSetStmtAttr**与*属性*SQL_ATTR_QUERY_TIMEOUT 自变量。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
  
> [!CAUTION]  
>  有关哪些语句状态信息**SQLBulkOperations**可以在中调用和它必须对与 ODBC 2 的兼容性所执行的操作。*x*应用程序，请参阅[块状游标可滚动游标，向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)为了向后兼容的附录 g： 驱动程序指南中的部分。  
  
 应用程序使用**SQLBulkOperations**执行对基表或视图对应于当前的查询执行以下操作：  
  
-   添加新行。  
  
-   更新每个行由书签的行的集。  
  
-   删除每个行由书签的行的集。  
  
-   提取一组的每个行由书签的行。  
  
 调用了**SQLBulkOperations**，块光标的位置是未定义。 应用程序调用**SQLFetchScroll**设置光标位置。 应用程序应调用**SQLFetchScroll**只用*FetchOrientation* SQL_FETCH_FIRST、 SQL_FETCH_LAST、 SQL_FETCH_ABSOLUTE 或 SQL_FETCH_BOOKMARK 自变量。 光标的位置是未定义的如果应用程序调用**SQLFetch**或**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_PRIOR，SQL_FETCH_NEXT，自变量或SQL_FETCH_RELATIVE。  
  
 列可以在通过调用执行的大容量操作中忽略**SQLBulkOperations**通过设置对的调用中指定的列长度/指示器缓冲区**SQLBindCol**，到 SQL_COLUMN_IGNORE。  
  
 它不是必需的应用程序时，它调用设置 SQL_ATTR_ROW_OPERATION_PTR 语句属性**SQLBulkOperations**因为执行大容量操作与此函数时，不能忽略行。  
  
 由 SQL_ATTR_ROWS_FETCHED_PTR 语句属性指向的缓冲区包含通过调用受影响的行号**SQLBulkOperations**。  
  
 当*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK 和与游标关联的查询规范的选择列表包含对同一列的多个引用，它是驱动程序定义是否出错生成或驱动程序会忽略重复的引用，并执行请求的操作。  
  
 有关如何使用**SQLBulkOperations**，请参阅[更新数据与 SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。  
  
## <a name="performing-bulk-inserts"></a>执行大容量插入  
 若要使用插入数据**SQLBulkOperations**，应用程序执行以下步骤序列：  
  
1.  执行返回的结果集的查询。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为它想要插入的行数。  
  
3.  调用**SQLBindCol**将它想要插入的数据绑定。 其大小等于 SQL_ATTR_ROW_ARRAY_SIZE 的值将数据绑定到一个数组。  
  
    > [!NOTE]  
    >  由 SQL_ATTR_ROW_STATUS_PTR 语句属性指向数组的大小应为等于 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 应为 null 指针。  
  
4.  调用**SQLBulkOperations**(*StatementHandle，* SQL_ADD) 以执行插入。  
  
5.  如果应用程序已设置 SQL_ATTR_ROW_STATUS_PTR 语句属性，它可以检查此数组以查看操作的结果。  
  
 如果应用程序绑定列 0，然后才能调用**SQLBulkOperations**与*操作*SQL_ADD 参数，驱动程序将绑定的列 0 缓冲区使用书签值更新为新插入的行。 为此，应用程序必须具有 SQL_ATTR_USE_BOOKMARKS 语句将属性设置为 SQL_UB_VARIABLE 在执行该语句之前。 （这不适用于 ODBC 2。*x*驱动程序。)  
  
 Long 数据可以在中添加部件 SQLBulkOperations，通过使用 SQLParamData 和 SQLPutData 调用。 有关详细信息，请参阅此函数引用后面的"提供长数据为大容量插入和更新"。  
  
 不需要应用程序可以调用**SQLFetch**或**SQLFetchScroll**调用之前**SQLBulkOperations** (时针对 ODBC 2 转除外。*x*驱动程序，请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md))。  
  
 行为是驱动程序定义的如果**SQLBulkOperations**，与*操作*SQL_ADD，自变量调用包含重复的列的游标。 该驱动程序可以返回驱动程序定义的 SQLSTATE，添加到显示在结果的第一列的数据设置，或执行其他驱动程序定义的行为。  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>使用书签中执行批量更新  
 若要使用的书签中执行批量更新**SQLBulkOperations**，应用程序在序列中执行以下步骤：  
  
1.  将 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE。  
  
2.  执行返回的结果集的查询。  
  
3.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为它想要更新的行数。  
  
4.  调用**SQLBindCol**将它想要更新的数据绑定。 其大小等于 SQL_ATTR_ROW_ARRAY_SIZE 的值将数据绑定到一个数组。 它还会调用**SQLBindCol**可将列 0 （书签列） 绑定。  
  
5.  副本书签的行更新到数组中要绑定到列 0。  
  
6.  更新绑定的缓冲区中的数据。  
  
    > [!NOTE]  
    >  由 SQL_ATTR_ROW_STATUS_PTR 语句属性指向数组的大小应为等于 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 应为 null 指针。  
  
7.  调用**SQLBulkOperations**(*StatementHandle，* SQL_UPDATE_BY_BOOKMARK)。  
  
    > [!NOTE]  
    >  如果应用程序已设置 SQL_ATTR_ROW_STATUS_PTR 语句属性，它可以检查此数组以查看操作的结果。  
  
8.  （可选） 调用**SQLBulkOperations**(*StatementHandle*，SQL_FETCH_BY_BOOKMARK) 提取到绑定的应用程序缓冲区，若要验证已更新的数据。  
  
9. 如果数据已更新，该驱动程序将更改为 SQL_ROW_UPDATED 相应行的行状态数组中的值。  
  
 批量更新由**SQLBulkOperations**可以通过调用包含长整型数据**SQLParamData**和**SQLPutData**。 有关详细信息，请参阅此函数引用后面的"提供长数据为大容量插入和更新"。  
  
 如果书签在游标中保持原样，应用程序不必调用**SQLFetch**或**SQLFetchScroll**之前更新的书签。 它可以使用它已存储从上一个游标的书签。 如果书签不会保留在游标，则应用程序必须调用**SQLFetch**或**SQLFetchScroll**检索书签。  
  
 行为是驱动程序定义的如果**SQLBulkOperations**，与*操作*SQL_UPDATE_BY_BOOKMARK，自变量调用包含重复的列的游标。 该驱动程序可以返回驱动程序定义的 SQLSTATE、 更新出现在结果集中的第一列或执行其他驱动程序定义的行为。  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>执行大容量提取使用书签  
 若要执行使用的书签的大容量提取**SQLBulkOperations**，应用程序在序列中执行以下步骤：  
  
1.  将 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE。  
  
2.  执行返回的结果集的查询。  
  
3.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为它想要提取的行数。  
  
4.  调用**SQLBindCol**将它想要提取的数据绑定。 其大小等于 SQL_ATTR_ROW_ARRAY_SIZE 的值将数据绑定到一个数组。 它还会调用**SQLBindCol**可将列 0 （书签列） 绑定。  
  
5.  副本书签的行在提取到数组中要绑定到列 0。 （假设，应用程序已经获得书签单独。）  
  
    > [!NOTE]  
    >  由 SQL_ATTR_ROW_STATUS_PTR 语句属性指向数组的大小应为等于 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 应为 null 指针。  
  
6.  调用**SQLBulkOperations**(*StatementHandle，* SQL_FETCH_BY_BOOKMARK)。  
  
7.  如果应用程序已设置 SQL_ATTR_ROW_STATUS_PTR 语句属性，它可以检查此数组以查看操作的结果。  
  
 如果书签在游标中保持原样，应用程序不必调用**SQLFetch**或**SQLFetchScroll**之前按书签提取。 它可以使用它已存储从上一个游标的书签。 如果书签不会保留在游标，则应用程序必须调用**SQLFetch**或**SQLFetchScroll**一次，以检索书签。  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>执行大容量删除使用书签  
 若要执行使用的书签的大容量删除操作**SQLBulkOperations**，应用程序在序列中执行以下步骤：  
  
1.  将 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE。  
  
2.  执行返回的结果集的查询。  
  
3.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为它想要删除的行数。  
  
4.  调用**SQLBindCol**可将列 0 （书签列） 绑定。  
  
5.  副本它关注删除到数组中的行的书签绑定到列 0。  
  
    > [!NOTE]  
    >  由 SQL_ATTR_ROW_STATUS_PTR 语句属性指向数组的大小应为等于 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 应为 null 指针。  
  
6.  调用**SQLBulkOperations**(*StatementHandle，* SQL_DELETE_BY_BOOKMARK)。  
  
7.  如果应用程序已设置 SQL_ATTR_ROW_STATUS_PTR 语句属性，它可以检查此数组以查看操作的结果。  
  
 如果书签在游标中保持原样，应用程序不必调用**SQLFetch**或**SQLFetchScroll**之前删除书签。 它可以使用它已存储从上一个游标的书签。 如果书签不会保留在游标，则应用程序必须调用**SQLFetch**或**SQLFetchScroll**一次，以检索书签。  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>对于大容量插入和更新提供的长整型数据  
 Long 数据可提供用于大容量插入和更新通过调用执行**SQLBulkOperations**。 若要插入或更新的长整型数据，应用程序，请执行以下步骤，除了本主题前面的"执行大容量插入"和"执行大容量更新使用书签"部分中所述的步骤。  
  
1.  当将数据绑定通过**SQLBindCol**，应用程序将应用程序定义的值，如列数，放在 *\*TargetValuePtr*执行中的数据的缓冲区列。 值可以在稍后用于标识的列。  
  
     将 SQL_LEN_DATA_AT_EXEC 结果放置于应用程序 (*长度*) 中的宏 *\*StrLen_or_IndPtr*缓冲区。 如果 SQL 数据类型的列是 SQL_LONGVARBINARY、 SQL_LONGVARCHAR、 或的长整型数据源 – 特定数据类型和驱动程序返回"Y"SQL_NEED_LONG_DATA_LEN 信息类型中的**SQLGetInfo**，*长度*是参数; 发送数据的字节数否则为它必须是一个非负的值，且将被忽略。  
  
2.  当**SQLBulkOperations**调用时，如果没有执行中的数据列，函数将返回 SQL_NEED_DATA 并转到步骤 3，该过程。 （如果没有执行中的数据列，该过程已完成。）  
  
3.  应用程序调用**SQLParamData**来检索的地址 *\*TargetValuePtr*要处理的第一个执行中的数据列的缓冲区。 **SQLParamData**返回 SQL_NEED_DATA。 应用程序检索应用程序定义的值从 *\*TargetValuePtr*缓冲区。  
  
    > [!NOTE]  
    >  尽管执行中的数据参数类似于执行中的数据列，返回的值**SQLParamData**每个不同。  
  
     执行中的数据列是包含在行集数据将发送与**SQLPutData**更新或插入与某行时**SQLBulkOperations**。 它们被绑定与**SQLBindCol**。 返回的值**SQLParamData**是中的行的地址 **TargetValuePtr*正在处理的缓冲区。  
  
4.  应用程序调用**SQLPutData**一个或多个时间来发送数据的列。 如果不能在中返回所有数据值，则需要多个调用 *\*TargetValuePtr*中指定的缓冲区**SQLPutData**; 多次调用**SQLPutData**仅当将字符 C 数据发送到具有字符、 binary 或数据源 – 特定数据类型的列或将二进制 C 数据发送到列，但字符，二进制文件，允许相同的列或数据源 – 特定的数据类型。  
  
5.  应用程序调用**SQLParamData**以指示所有数据均已都发送的列。  
  
    -   如果没有更多的执行中的数据列， **SQLParamData**返回 SQL_NEED_DATA 和的地址*TargetValuePtr*要处理的下一步执行中的数据列的缓冲区。 应用程序重复步骤 4 和 5。  
  
    -   如果没有更多的执行中的数据列，则过程已完成。 如果已成功时，请执行语句**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果执行失败，它将返回 SQL_ERROR。 此时， **SQLParamData**可以返回可以由任何 SQLSTATE **SQLBulkOperations**。  
  
 如果该操作被取消，或者在发生错误**SQLParamData**或**SQLPutData**后**SQLBulkOperations**返回 SQL_NEED_DATA 和所有发送数据前执行中的数据列，则应用程序可以调用仅**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**语句或语句与关联的连接。 如果语句或语句与关联的连接，它调用任何其他函数，该函数将返回 SQL_ERROR 和 SQLSTATE HY010 （函数序列错误）。  
  
 如果应用程序调用**SQLCancel**驱动程序时驱动程序仍需要执行中的数据列数据，取消操作。 然后，应用程序可以调用**SQLBulkOperations**再次取消不会影响光标状态或当前光标位置。  
  
## <a name="row-status-array"></a>行状态数组  
 行状态数组到调用后包含行集中的数据的每一行的状态值**SQLBulkOperations**。 该驱动程序后调用此数组中设置的状态值范围**SQLFetch**， **SQLFetchScroll**， **SQLSetPos**，或**SQLBulkOperations**. 通过调用最初填充此数组**SQLBulkOperations**如果**SQLFetch**或**SQLFetchScroll**不之前调用**SQLBulkOperations**. 此数组被指向 SQL_ATTR_ROW_STATUS_PTR 语句属性。 行状态数组中的元素数必须等于的行集 （如由 SQL_ATTR_ROW_ARRAY_SIZE 语句属性定义） 中的行数。 有关此行状态数组的信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>代码示例  
 下面的示例在从客户表中读取一次的数据的 10 行。 然后，它提示操作的用户来执行。 为了减少网络流量，示例缓冲区更新、 删除和插入本地在绑定的数组，但在以前的行集数据的偏移量处。 当用户选择发送更新、 删除和插入到数据源时，代码会设置正确偏移量的绑定并调用**SQLBulkOperations**。 为简单起见，用户无法缓冲 10 个以上的更新、 删除或插入。  
  
```  
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
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|获取单个字段的描述符|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取多个字段的描述符|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单个字段的描述符|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置多个字段的描述符|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|将光标置于、 刷新数据集中的行，或更新或删除行集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

