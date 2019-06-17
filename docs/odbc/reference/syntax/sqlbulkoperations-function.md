---
title: SQLBulkOperations 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14e51f1d04012e22c198b7ed5f70d9b508933c5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538040"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 函数
**符合性**  
 版本引入了：ODBC 3.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLBulkOperations**执行大容量插入和大容量书签操作，包括更新、 删除和提取按书签。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLBulkOperations**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLBulkOperations** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明. 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
 对于所有这些 SQLSTATEs 可以返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除 01xxx SQLSTATEs)，将返回 SQL_SUCCESS_WITH_INFO，如果上一个或多个，但并非所有行的多行操作，出现错误，并且如果发生错误，则返回 SQL_ERROR单行操作。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据右截断|*操作*参数为 SQL_FETCH_BY_BOOKMARK，并导致截断了非空白字符或二进制数据的非空字符串或二进制数据返回为一列或列数据类型为 SQL_C_CHAR 或 SQL_C_BINARY。|  
|01S01|行中的错误|*操作*参数为 SQL_ADD，并执行操作时，在一个或多个行中时发生错误，但至少有一行已成功添加。 （函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> （仅当应用程序使用 ODBC 2 时，会引发此错误。*x*驱动程序。)|  
|01S07|截断小数部分|*操作*参数为 SQL_FETCH_BY_BOOKMARK、 应用程序缓冲区的数据类型不为 SQL_C_CHAR 或 SQL_C_BINARY，返回到应用程序的一个或多个列缓冲区的数据已被截断。 （对于数值 C 数据类型，已截断数字的小数部分。 对于时间、 时间戳和包含时间部分的时间间隔 C 数据类型，时间的小数部分被截断。）<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|*操作*参数为 SQL_FETCH_BY_BOOKMARK，并且无法为指定的数据类型转换的结果集中的列的数据值*TargetType* 调用中的参数**SQLBindCol**。<br /><br /> *操作*参数为 SQL_UPDATE_BY_BOOKMARK 或 SQL_ADD，并为结果集中的列的数据类型，无法转换的应用程序缓冲区中的数据值。|  
|07009|描述符索引无效|自变量*操作*已 SQL_ADD，并将其列已绑定使用一个大于结果集中的列数的列数。|  
|21S02|派生表等级与列列表不匹配|自变量*操作*SQL_UPDATE_BY_BOOKMARK;，因为所有列都是未绑定或只读的或者绑定的长度 / 指示器缓冲区中的值是 SQL_COLUMN_IGNORE 没有列都已更新。|  
|22001|字符串数据右截断|字符或二进制值与结果集中的列的分配时非空 （适用于字符为单位） 或 （对于二进制文件） 的非 null 字符或字节数的截断。|  
|22003|数值超出范围|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，并为结果集中的列的数值分配导致数字被截断的整个 （而不是小数） 部分。<br /><br /> 自变量*操作*已 SQL_FETCH_BY_BOOKMARK，并返回一个或多个绑定列的数值可能导致重要数字丢失。|  
|22007|日期时间格式无效|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，并分配到结果集中的列的日期或时间戳值导致年、 月或天字段超出范围。<br /><br /> 自变量*操作*已 SQL_FETCH_BY_BOOKMARK，并返回一个或多个绑定列的日期或时间戳值可能会造成年、 月或天字段超出范围。|  
|22008|日期/时间字段溢出|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，和 datetime 算术数据发送到结果集中的列上的性能产生的日期时间字段 （年、 月、 日、 小时、 分钟、 或第二个字段） 的结果值的允许范围之外写入的字段或正在根据公历日历的日期时间的自然规则无效。<br /><br /> *操作*参数为 SQL_FETCH_BY_BOOKMARK，和算术运算的结果集中检索数据的日期时间的性能产生的日期时间字段 （年、 月、 日、 小时、 分钟、 或第二个字段）为字段值的允许范围之外写入或无效的结果基于公历日历的日期时间的自然规则。|  
|22015|间隔字段溢出|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，并分配的精确数字或至间隔为 SQL 数据类型的 C 间隔类型导致重要数字丢失。<br /><br /> *操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK; 分配到 SQL 类型的时间间隔时，没有间隔 SQL 类型中的 C 类型的值没有表示形式。<br /><br /> *操作*参数为 SQL_FETCH_BY_BOOKMARK，并将分配从精确数字或时间间隔 SQL 类型到 C 间隔类型导致重要数字丢失前导字段中。<br /><br /> *操作*参数为 SQL_FETCH_BY_BOOKMARK; 分配到 C 间隔类型时，没有任何表示形式中的 C 间隔类型的 SQL 类型的值。|  
|22018|转换指定的字符值无效|*操作*参数为 SQL_FETCH_BY_BOOKMARK; C 类型为准确或近似数值、 日期时间或间隔数据类型; 该列的 SQL 类型是字符数据类型; 和列中的值不是有效绑定的 C 类型的文本。<br /><br /> 自变量*操作*SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK; 的 SQL 类型是准确或近似数值、 日期时间或间隔数据类型; C 类型为 SQL_C_CHAR; 和列中的值不是有效的文本绑定 SQL 类型。|  
|23000|完整性约束冲突|*操作*参数为 SQL_ADD、 SQL_DELETE_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK，和违反了完整性约束。<br /><br /> *操作*参数为 SQL_ADD，和未绑定的列定义为 NOT NULL 且无默认值。<br /><br /> *操作*参数为 SQL_ADD，绑定中指定的长度*StrLen_or_IndPtr*缓冲区是否 SQL_COLUMN_IGNORE，和的列不具有默认值。|  
|24000|游标状态无效|*StatementHandle*处于执行状态，但无结果集与关联*StatementHandle*。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|42000|语法错误或访问冲突|该驱动程序无法将所需执行请求中的操作将该行锁定*操作*参数。|  
|44000|WITH CHECK OPTION 冲突|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，并且 insert 或查看的表上执行更新 （或派生自查看的表的表） 创建的指定**WITH CHECK OPTION**，一个或多个行受 insert 或 update 将不再存在中查看的表的方式。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLBulkOperations**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 调用函数时没有首先调用**SQLExecDirect**， **SQLExecute**，或目录函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> (DM) 驱动程序是 ODBC 2。*x*驱动程序，并**SQLBulkOperations**曾为*StatementHandle*之前**SQLFetchScroll**或**SQLFetch**调用。<br /><br /> （数据挖掘） **SQLBulkOperations**后调用**SQLExtendedFetch**上调用了*StatementHandle*。|  
|HY011|现在无法设置属性|(DM) 驱动程序是 ODBC 2。*x*驱动程序和 SQL_ATTR_ROW_STATUS_PTR 语句属性设置为调用之间**SQLFetch**或**SQLFetchScroll**和**SQLBulkOperations**.|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK; 数据值不是空指针; C 数据类型为 SQL_C_BINARY 或 SQL_C_CHAR; 和列长度值是小于 0，但不是等于 SQL_DATA_AT_EXECSQL_COLUMN_IGNORE、 sql_nts; 或 SQL_NULL_DATA，或小于或等于 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 长度/指示器缓冲区中的值为 SQL_DATA_AT_EXEC;SQL 类型是 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 数据源特定的数据类型;和中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**是"Y"。<br /><br /> *操作*参数为 SQL_ADD、 SQL_ATTR_USE_BOOKMARK 语句属性设置为 SQL_UB_VARIABLE，并且第 0 列绑定到其的长度不等于此结果集的书签的最大长度的缓冲区。 (此长度可在 IRD 的 SQL_DESC_OCTET_LENGTH 字段中，并且可以通过调用来获取**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY092|无效的属性标识符|(DM) 为指定的值*操作*参数无效。<br /><br /> *操作*参数为 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，和 sql_attr_concurrency 设置语句属性设置为 SQL_CONCUR_READ_ONLY。<br /><br /> *操作*参数为 SQL_DELETE_BY_BOOKMARK、 SQL_FETCH_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK，并且未绑定的书签列或 SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_OFF。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持请求中的操作*操作*参数。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回的结果集。 通过设置超时期限**SQLSetStmtAttr**与*属性*SQL_ATTR_QUERY_TIMEOUT 参数。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
  
> [!CAUTION]  
>  有关哪些语句指出**SQLBulkOperations**可以调用它必须与 ODBC 2 的兼容性所执行的操作。*x*应用程序，请参阅[块游标、 可滚动游标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)附录 g： 中的部分为了向后兼容的驱动程序指南。  
  
 应用程序使用**SQLBulkOperations**执行对基表或视图对应于当前查询执行以下操作：  
  
-   添加新行。  
  
-   更新每个行由一个书签的行的集。  
  
-   删除每个行由一个书签的行的集。  
  
-   提取每个行由一个书签的行的集。  
  
 在调用**SQLBulkOperations**，块游标位置是不确定。 应用程序必须调用**SQLFetchScroll**以设置游标位置。 应用程序应调用**SQLFetchScroll**只用*FetchOrientation* SQL_FETCH_FIRST、 SQL_FETCH_LAST、 SQL_FETCH_ABSOLUTE 或 SQL_FETCH_BOOKMARK 的参数。 光标的位置是未定义在应用程序调用**SQLFetch**或**SQLFetchScroll**与*FetchOrientation*自变量的 SQL_FETCH_PRIOR，SQL_FETCH_NEXT，或SQL_FETCH_RELATIVE。  
  
 可以通过调用执行大容量操作中忽略列**SQLBulkOperations**通过设置对的调用中指定的列长度/指示器缓冲区**SQLBindCol**，到 SQL_COLUMN_IGNORE。  
  
 不需要应用程序时，它调用 SQL_ATTR_ROW_OPERATION_PTR 语句属性设置**SQLBulkOperations**因为执行大容量操作与此函数时，不能忽略行。  
  
 通过将 SQL_ATTR_ROWS_FETCHED_PTR 语句属性指向的缓冲区包含通过调用受影响的行数**SQLBulkOperations**。  
  
 当*操作*参数为 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK 和与游标相关联的查询规范的选择列表包含多个引用同一列，它是驱动程序定义的错误生成或驱动程序忽略重复的引用，并执行所请求的操作。  
  
 有关如何使用详细信息**SQLBulkOperations**，请参阅[使用 SQLBulkOperations 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。  
  
## <a name="performing-bulk-inserts"></a>执行大容量插入  
 若要使用插入数据**SQLBulkOperations**，应用程序执行以下步骤序列：  
  
1.  执行返回一个结果集的查询。  
  
2.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为它想要插入的行数。  
  
3.  调用**SQLBindCol**绑定它想要插入的数据。 将数据与 SQL_ATTR_ROW_ARRAY_SIZE 的值的大小等于绑定到一个数组。  
  
    > [!NOTE]  
    >  通过将 SQL_ATTR_ROW_STATUS_PTR 语句属性指向数组的大小应是等于 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 应为 null 指针。  
  
4.  调用**SQLBulkOperations**(*StatementHandle，* SQL_ADD) 以执行插入。  
  
5.  如果应用程序设置 SQL_ATTR_ROW_STATUS_PTR 语句属性，它可以检查此数组以查看操作的结果。  
  
 如果应用程序将列 0 绑定之前它将调用**SQLBulkOperations**与*操作*SQL_ADD 参数，驱动程序将绑定的列 0 缓冲区的书签值更新为新插入的行。 为此，应用程序必须具有 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE 执行该语句之前。 （这并不适用于 ODBC 2。*x*驱动程序。)  
  
 长时间可以通过添加数据部分 SQLBulkOperations，通过使用 SQLParamData 和 SQLPutData 对的调用。 有关详细信息，请参阅更高版本中此函数引用的"提供长数据为大容量插入和更新"。  
  
 不需要的应用程序以调用**SQLFetch**或**SQLFetchScroll**调用之前**SQLBulkOperations** (针对 ODBC 2 将时除外。*x*驱动程序，请参见[向后兼容性和标准符合性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md))。  
  
 行为是驱动程序定义的如果**SQLBulkOperations**，使用*操作*SQL_ADD，自变量调用包含重复的列的游标。 该驱动程序可以返回驱动程序定义的 SQLSTATE，添加到结果中显示的第一列的数据设置，或执行其他驱动程序定义的行为。  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>使用书签执行大容量更新  
 若要使用书签与执行批量更新**SQLBulkOperations**，应用程序按顺序执行以下步骤：  
  
1.  设置为 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 语句属性。  
  
2.  执行返回一个结果集的查询。  
  
3.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为想要更新的行数。  
  
4.  调用**SQLBindCol**绑定它想要更新的数据。 将数据与 SQL_ATTR_ROW_ARRAY_SIZE 的值的大小等于绑定到一个数组。 它还调用**SQLBindCol**绑定列 0 （书签列）。  
  
5.  副本它希望更新到数组中的行的书签绑定到第 0 列。  
  
6.  更新绑定的缓冲区中的数据。  
  
    > [!NOTE]  
    >  通过将 SQL_ATTR_ROW_STATUS_PTR 语句属性指向数组的大小应等于 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 应为 null 指针。  
  
7.  调用**SQLBulkOperations**(*StatementHandle，* SQL_UPDATE_BY_BOOKMARK)。  
  
    > [!NOTE]  
    >  如果应用程序设置 SQL_ATTR_ROW_STATUS_PTR 语句属性，它可以检查此数组以查看操作的结果。  
  
8.  可以选择调用**SQLBulkOperations**(*StatementHandle*，SQL_FETCH_BY_BOOKMARK) 以将提取到要验证已更新的绑定的应用程序缓冲区的数据。  
  
9. 如果数据已更新，该驱动程序将更改为 SQL_ROW_UPDATED 相应行的行状态数组中的值。  
  
 大容量由执行的更新**SQLBulkOperations**可以通过调用包含长整型数据**SQLParamData**并**SQLPutData**。 有关详细信息，请参阅更高版本中此函数引用的"提供长数据为大容量插入和更新"。  
  
 如果书签在游标中保持原样，应用程序不必调用**SQLFetch**或**SQLFetchScroll**之前更新的书签。 它可以使用它从上一个游标已存储的书签。 如果书签不会保留在游标，则应用程序必须调用**SQLFetch**或**SQLFetchScroll**检索书签。  
  
 行为是驱动程序定义的如果**SQLBulkOperations**，使用*操作*SQL_UPDATE_BY_BOOKMARK，自变量调用包含重复的列的游标。 该驱动程序可以返回驱动程序定义的 SQLSTATE，更新将显示在结果集中的第一列或执行其他驱动程序定义的行为。  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>执行大容量提取使用书签  
 若要执行大容量提取操作使用与书签**SQLBulkOperations**，应用程序按顺序执行以下步骤：  
  
1.  设置为 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 语句属性。  
  
2.  执行返回一个结果集的查询。  
  
3.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为它想要提取的行数。  
  
4.  调用**SQLBindCol**绑定它想要提取的数据。 将数据与 SQL_ATTR_ROW_ARRAY_SIZE 的值的大小等于绑定到一个数组。 它还调用**SQLBindCol**绑定列 0 （书签列）。  
  
5.  副本它关注在数组中提取的行的书签绑定到第 0 列。 （这假设应用程序具有已获得的书签单独。）  
  
    > [!NOTE]  
    >  通过将 SQL_ATTR_ROW_STATUS_PTR 语句属性指向数组的大小应等于 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 应为 null 指针。  
  
6.  调用**SQLBulkOperations**(*StatementHandle，* SQL_FETCH_BY_BOOKMARK)。  
  
7.  如果应用程序设置 SQL_ATTR_ROW_STATUS_PTR 语句属性，它可以检查此数组以查看操作的结果。  
  
 如果书签在游标中保持原样，应用程序不必调用**SQLFetch**或**SQLFetchScroll**之前提取的书签。 它可以使用它从上一个游标已存储的书签。 如果书签不会保留在游标，则应用程序必须调用**SQLFetch**或**SQLFetchScroll**一次，以检索书签。  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>执行大容量删除使用书签  
 若要执行大容量删除操作使用与书签**SQLBulkOperations**，应用程序按顺序执行以下步骤：  
  
1.  设置为 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 语句属性。  
  
2.  执行返回一个结果集的查询。  
  
3.  将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性设置为想要删除的行数。  
  
4.  调用**SQLBindCol**绑定列 0 （书签列）。  
  
5.  副本它关注在数组中删除的行的书签绑定到第 0 列。  
  
    > [!NOTE]  
    >  通过将 SQL_ATTR_ROW_STATUS_PTR 语句属性指向数组的大小应等于 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 应为 null 指针。  
  
6.  调用**SQLBulkOperations**(*StatementHandle，* SQL_DELETE_BY_BOOKMARK)。  
  
7.  如果应用程序设置 SQL_ATTR_ROW_STATUS_PTR 语句属性，它可以检查此数组以查看操作的结果。  
  
 如果书签在游标中保持原样，应用程序不必调用**SQLFetch**或**SQLFetchScroll**之前删除书签。 它可以使用它从上一个游标已存储的书签。 如果书签不会保留在游标，则应用程序必须调用**SQLFetch**或**SQLFetchScroll**一次，以检索书签。  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>对于大容量插入和更新提供的长整型数据  
 长整型数据可提供用于大容量插入和更新执行通过调用**SQLBulkOperations**。 若要插入或更新的长整型数据，应用程序，请执行以下步骤，除了本主题前面的"执行大容量插入"和"执行大容量更新使用书签"部分中所述的步骤。  
  
1.  当将数据绑定通过使用**SQLBindCol**，应用程序中放入应用程序定义的值，例如的列号，  *\*TargetValuePtr*执行时数据的缓冲区列。 可以稍后使用值标识的列。  
  
     SQL_LEN_DATA_AT_EXEC 将结果放置于该应用程序 (*长度*) 中的宏 *\*StrLen_or_IndPtr*缓冲区。 如果 SQL 数据类型的列是 SQL_LONGVARBINARY、 SQL_LONGVARCHAR 或 long 数据源特定的数据类型和驱动程序将返回"Y"SQL_NEED_LONG_DATA_LEN 信息类型中的**SQLGetInfo**，*长度*是数个字节的数据要发送的参数; 否则为它必须为非负的值并将被忽略。  
  
2.  当**SQLBulkOperations**调用时，如果有执行时数据列，函数将返回 SQL_NEED_DATA，继续到步骤 3 中，该过程。 （如果不有任何执行时数据列，该过程已完成。）  
  
3.  应用程序调用**SQLParamData**若要检索的地址 *\*TargetValuePtr*要处理的第一个执行时数据列的缓冲区。 **SQLParamData**返回 SQL_NEED_DATA。 应用程序中检索应用程序定义的值从 *\*TargetValuePtr*缓冲区。  
  
    > [!NOTE]  
    >  返回的值执行时数据参数类似于执行时数据列，尽管**SQLParamData**是为每个不同。  
  
     执行时数据列是包含在行集数据将发送具有**SQLPutData**更新或插入行时**SQLBulkOperations**。 它们被绑定与**SQLBindCol**。 返回的值**SQLParamData**是中的行的地址 **TargetValuePtr*正在处理的缓冲区。  
  
4.  应用程序调用**SQLPutData**一个或多个次多次以发送列数据。 如果不能在中返回所有数据值，则需要多次调用 *\*TargetValuePtr*中指定的缓冲区**SQLPutData**; 多次调用**SQLPutData**只有在将字符 C 数据发送到包含的字符、 二进制或数据源特定的数据类型的列或二进制 C 数据发送到具有二进制文件，一个字符的列时允许同一列或数据源特定的数据类型。  
  
5.  应用程序调用**SQLParamData**再次以指示已将列的所有数据。  
  
    -   如果有多个执行时数据列， **SQLParamData**将返回 SQL_NEED_DATA 和的地址*TargetValuePtr*要处理的下一步执行时数据列的缓冲区。 应用程序重复步骤 4 和 5。  
  
    -   如果没有更多的执行时数据列，该过程已完成。 如果成功，已执行语句**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果执行失败，它将返回 SQL_ERROR。 在此情况下， **SQLParamData**可以返回任何可由返回的 SQLSTATE **SQLBulkOperations**。  
  
 如果将取消该操作，或者在出错**SQLParamData**或**SQLPutData**后**SQLBulkOperations**返回 SQL_NEED_DATA 和之前的所有发送数据执行时数据列，该应用程序可以调用仅**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**语句或用语句相关联的连接。 如果它调用任何其他函数的语句或用语句相关联的连接，则函数返回 SQL_ERROR 并且 SQLSTATE HY010 （函数序列错误）。  
  
 如果应用程序调用**SQLCancel**驱动程序时驱动程序仍需要执行时数据列的数据，取消操作。 然后，应用程序可以调用**SQLBulkOperations**再次取消不会影响游标状态或当前光标位置。  
  
## <a name="row-status-array"></a>行状态数组  
 行状态数组包含在调用后行集中的数据的每一行的状态值**SQLBulkOperations**。 驱动程序后调用此数组中设置状态值**SQLFetch**， **SQLFetchScroll**， **SQLSetPos**，或者**SQLBulkOperations**. 通过调用最初填充此数组**SQLBulkOperations**如果**SQLFetch**或**SQLFetchScroll**尚未调用之前**SQLBulkOperations**. 此数组所指向的 SQL_ATTR_ROW_STATUS_PTR 语句属性。 行状态数组中的元素数必须等于行集 （如 SQL_ATTR_ROW_ARRAY_SIZE 语句属性所定义） 中的行数。 有关此行状态数组的信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>代码示例  
 下面的示例在从客户表中提取一次 10 行数据。 然后会提示用户操作来执行。 若要减少网络流量，示例缓冲区更新、 删除和插入本地在绑定的数组，但在过去的行集数据的偏移量。 当用户选择发送更新、 删除和插入到数据源时，代码设置适当的偏移量的绑定，并调用**SQLBulkOperations**。 为简单起见，用户不能缓冲 10 个以上的更新、 删除或插入。  
  
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
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|获取描述符的单个字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取描述符的多个字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单个字段的描述符|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置多个字段的描述符|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|定位光标，刷新的行集中的数据或更新或删除行集中的数据|[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
