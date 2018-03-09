---
title: "SQLSetPos 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLSetPos
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetPos
helpviewer_keywords: SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 310adbb9cc67ffe6982ca6838285ffe4967ab7c4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetpos-function"></a>SQLSetPos 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLSetPos**设置在行集中的光标位置，并允许应用程序刷新行集中的数据或用于更新或删除在结果集中的数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *RowNumber*  
 [输入]要对其执行该操作使用指定的行集中的行位置*操作*自变量。 如果*RowNumber*为 0，则该操作适用于每个行集中的行。  
  
 有关其他信息，请参阅"注释"。  
  
 *运算*  
 [输入]要执行的操作：  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]  
>  SQL_ADD 值*操作*自变量已被弃用 ODBC 3*.x*。 ODBC 3。*x*驱动程序将需要支持 SQL_ADD 为了向后兼容。 对的调用替换为此功能**SQLBulkOperations**与*操作*SQL_ADD。 当一个 ODBC 3。*x*应用程序处理 ODBC 2。*x*驱动程序，驱动程序管理器映射调用**SQLBulkOperations**与*操作*的到 SQL_ADD **SQLSetPos**与*操作*SQL_ADD。  
  
 有关详细信息，请参阅"注释"。  
  
 *LockType*  
 [输入]指定如何在执行中指定的操作后锁定行*操作*自变量。  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 有关详细信息，请参阅"注释"。  
  
 **返回**  
  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR，或 SQL_INVALID_HANDLE 中。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetPos**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetPos**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
 对于所有这些 SQLSTATEs 可以返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除外 01xxx SQLSTATEs)，将返回 SQL_SUCCESS_WITH_INFO，如果将上一个或多个，但并非所有行的一个多行的操作，发生错误时，如果上发生错误时返回 SQL_ERROR单行更行操作。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01001|游标操作冲突|*操作*参数为 SQL_DELETE 或 SQL_UPDATE，和任何行或多个行已被删除或更新。 (有关更新多个行的详细信息，请参阅 SQL_ATTR_SIMULATE_CURSOR 说明*属性*中**SQLSetStmtAttr**。)（函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> *操作*参数为 SQL_DELETE 或 SQL_UPDATE，并出现开放式并发，操作失败。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据右侧被截断|*操作*自变量为 SQL_REFRESH，和字符串或二进制数据返回为一列或列数据类型为 SQL_C_CHAR 或 SQL_C_BINARY 导致非空白字符或非 NULL 二进制数据截断。|  
|01S01|行中的错误|*RowNumber*自变量为 0，并且在执行与指定的操作时出现一个或多个行中的错误*操作*自变量。<br /><br /> （如果将上一个或多个，但并非所有行的一个多行的操作，发生错误时，如果对单行更行操作发生错误返回 SQL_ERROR SQL_SUCCESS_WITH_INFO 即被返回。）<br /><br /> (此 SQLSTATE 返回时，才**SQLSetPos**后，会调用**SQLExtendedFetch**，如果驱动程序是 ODBC 2。*x*未使用的是光标库和驱动程序。)|  
|01S07|小数部分组成的截断|*操作*自变量为 SQL_REFRESH，应用程序缓冲区的数据类型不是 SQL_C_CHAR 或 SQL_C_BINARY，并且返回到应用程序的缓冲区的一个或多个列的数据被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳，和包含时间组件的 interval 数据类型，时间的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|无法转换的结果集中的列的数据值，由指定的数据类型为*TargetType*对的调用中**SQLBindCol**。|  
|07009|无效的描述符索引|自变量*操作*SQL_REFRESH 或 SQL_UPDATE，并将其列已绑定与一个大于结果集中的列数的列数。|  
|21S02|派生表的等级与列列表不匹配|自变量*操作*SQL_UPDATE，但没有列已更新，因为所有列是未绑定、 只读的或绑定的长度/指示器缓冲区中的值为 SQL_COLUMN_IGNORE。|  
|22001|字符串数据，右截断|*操作*自变量为 SQL_UPDATE，并分配字符或二进制值的列生成了非空白 （对于字符为单位） 或 （对于二进制） 的非 null 字符或字节数的截断。|  
|22003|数值超出范围|自变量*操作*SQL_UPDATE，并分配到结果集中的列的数字值导致整个 （而不是小数部分组成） 的部分将被截断。<br /><br /> 自变量*操作*SQL_REFRESH，并返回数值的一个或多个绑定的列可能会导致重要数字丢失。|  
|22007|无效的日期时间格式|自变量*操作*SQL_UPDATE，并分配到结果集中的列的日期或时间戳值导致年、 月或天将超出范围的字段。<br /><br /> 自变量*操作*SQL_REFRESH，并返回一个或多个绑定的列的日期或时间戳值将造成年、 月或天将超出范围的字段。|  
|22008|日期/时间字段溢出|*操作*自变量为 SQL_UPDATE，和 datetime 算术上发送到结果集中的列数据的性能产生的结果的日期时间字段 （年、 月、 日、 小时、 分钟、 或第二个字段）外部的字段，或无效的值的允许范围基于公历的自然规则进行日期时间。<br /><br /> *操作*自变量为 SQL_REFRESH，和 datetime 算术对正在检索从结果集中的数据的性能产生的结果的日期时间字段 （年、 月、 日、 小时、 分钟、 或第二个字段）外部的字段，或无效的值的允许范围基于公历的自然规则进行日期时间。|  
|22015|间隔字段溢出|*操作*自变量为 SQL_UPDATE，以及分配的精确数字或为 SQL 数据类型的间隔的间隔 C 类型导致重要数字丢失。<br /><br /> *操作*自变量为 SQL_UPDATE; 当将分配给一个时间间隔 SQL 类型，存在为间隔 SQL 类型的 C 类型的值没有表示形式。<br /><br /> *操作*自变量为 SQL_REFRESH，并将从精确数字或间隔 SQL 类型分配给间隔 C 类型中的前导字段导致重要数字丢失。<br /><br /> *操作*自变量为 SQL_ 刷新; 当将分配给间隔 C 类型，存在为没有间隔 C 类型中的 SQL 类型的值的表示形式。|  
|22018|转换指定的的无效字符值|*操作*自变量为 SQL_REFRESH; C 类型是准确或近似数字、 日期时间或间隔数据类型; 列的 SQL 类型是字符数据类型; 并且在列中的值不是有效的文本的绑定 C 类型。<br /><br /> 自变量*操作*SQL_UPDATE; SQL 类型已准确或近似数字、 日期时间或间隔数据类型; C 类型为 SQL_C_CHAR; 并且列中的值不是有效的文本的绑定的 SQL 类型。|  
|23000|完整性约束冲突|自变量*操作*SQL_DELETE 或 SQL_UPDATE，和违反了完整性约束。|  
|24000|无效的游标状态|*StatementHandle*处于执行状态，但没有结果集与关联*StatementHandle*。<br /><br /> (DM) 上打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**不调用一样。<br /><br /> 在打开游标的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**已调用一样，但光标所处的结果集或之后开始之前结果集的末尾。<br /><br /> 自变量*操作*SQL_DELETE、 SQL_REFRESH 或 SQL_UPDATE，并且光标位于早于开始日期的结果集或结果集的末尾之后。|  
|40001|序列化失败|事务已回滚，因为资源死锁与另一个事务。|  
|40003|未知的语句结束|此函数在执行期间失败关联的连接，无法确定事务的状态。|  
|42000|语法错误或访问冲突|该驱动程序无法锁定行，如执行参数中请求的操作所需*操作*。<br /><br /> 该驱动程序无法按请求自变量中锁定该行*LockType*。|  
|44000|WITH CHECK OPTION 冲突|*操作*自变量为 SQL_UPDATE，和上查看的表执行已更新或通过指定已创建的查看表中派生表**WITH CHECK OPTION**，这样，一个或多个行受此更新将不再存在于查看的表。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数已在上再次*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 调用 SQLSetPos 函数时仍在执行此异步函数。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 第一个调用已调用函数**SQLExecDirect**， **SQLExecute**，或目录函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) 驱动程序是 ODBC 2。*x*驱动程序，和**SQLSetPos**曾为*StatementHandle*后**SQLFetch**调用。|  
|HY011|现在无法设置属性|(DM) 驱动程序是 ODBC 2。*x*驱动程序; SQL_ATTR_ROW_STATUS_PTR 语句属性已设置; 然后**SQLSetPos**之前已调用**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**调用。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|*操作*自变量为 SQL_UPDATE、 数据值是空指针，和的列长度值不是 0、 SQL_DATA_AT_EXEC、 SQL_COLUMN_IGNORE、 SQL_NULL_DATA，或小于或等于 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> *操作*自变量为 SQL_UPDATE; 数据值不是 null 指针; C 数据类型不 SQL_C_BINARY 或 SQL_C_CHAR; 和列长度值已小于 0，但不是等于 SQL_DATA_AT_EXEC，SQL_COLUMN_IGNORESql_nts 以或 SQL_NULL_DATA，或小于或等于 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 长度/指示器缓冲区中的值为 SQL_DATA_AT_EXEC;SQL 类型已 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 数据源 – 特定数据类型;和中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**已"Y"。|  
|HY092|无效的属性标识符|(DM) 为指定的值*操作*自变量无效。<br /><br /> (DM) 为指定的值*LockType*自变量无效。<br /><br /> *操作*参数 SQL_UPDATE 或 SQL_DELETE，且 SQL_ATTR_CONCURRENCY 语句属性为 SQL_ATTR_CONCUR_READ_ONLY。|  
|HY107|行数值超出范围|为参数指定的值*RowNumber*大于在行集中的行数。|  
|HY109|无效的光标位置|与关联的光标*StatementHandle*已定义为只进时，因此未无法在行集内定位光标。 请参阅中的 SQL_ATTR_CURSOR_TYPE 属性的说明**SQLSetStmtAttr**。<br /><br /> *操作*参数为 SQL_UPDATE、 SQL_DELETE 或 SQL_REFRESH，并由行标识*RowNumber*自变量已被删除，或者不已提取。<br /><br /> (DM) *RowNumber*自变量为 0，和*操作*自变量为 SQL_POSITION。<br /><br /> **SQLSetPos**之后调用**SQLBulkOperations**调用和之前**SQLFetchScroll**或**SQLFetch**调用。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持请求中的操作*操作*自变量或*LockType*自变量。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回了结果集。 通过设置的超时期限**SQLSetStmtAttr**与*属性*SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
  
> [!CAUTION]  
>  为语句的信息指出**SQLSetPos**可以在中调用和它需要执行的与 ODBC 2 的兼容性*.x*应用程序，请参阅[块状游标、 可滚动游标，和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。  
  
## <a name="rownumber-argument"></a>RowNumber 自变量  
 *RowNumber*参数指定要对其执行由指定的操作的行集中的行数*操作*自变量。 如果*RowNumber*为 0，则该操作适用于每个行集中的行。 *RowNumber*必须是一个介于 0 到行集中的行数。  
  
> [!NOTE]  
>  在 C 语言中，数组是基于 0 的和*RowNumber*自变量是基于 1 的。 例如，若要更新的行集的第五个行，应用程序修改的行集缓冲区的数组索引 4 但指定*RowNumber*为 5。  
  
 所有操作将光标都置于指定的行的*RowNumber*。 执行以下操作需要光标位置：  
  
-   定位更新和 delete 语句。  
  
-   调用**SQLGetData**。  
  
-   调用**SQLSetPos**使用 SQL_DELETE、 SQL_REFRESH 和 SQL_UPDATE 选项。  
  
 例如，如果*RowNumber*是 2 个调用**SQLSetPos**与*操作*的 SQL_DELETE，光标位于行集的第二个行，该行将被删除。 在实现行状态数组 （由 SQL_ATTR_ROW_STATUS_PTR 语句属性指向） 的第二行条目更改为 SQL_ROW_DELETED。  
  
 应用程序可以指定光标位置，当它调用**SQLSetPos**。 通常情况下，它调用**SQLSetPos**与 SQL_POSITION 或 SQL_REFRESH 操作，将光标定位在执行定位前更新或删除语句或调用**SQLGetData**。  
  
## <a name="operation-argument"></a>操作参数  
 *操作*参数支持以下操作。 若要确定哪些选项支持的数据源，应用程序调用**SQLGetInfo**与 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （具体取决于游标的类型） 的信息类型。  
  
|*运算*<br /><br /> 参数|运算|  
|------------------------------|---------------|  
|SQL_POSITION|该驱动程序将光标置于由指定的行上*RowNumber*。<br /><br /> 行状态数组的 SQL_ATTR_ROW_OPERATION_PTR 语句属性指向的内容为 SQL_POSITION 忽略*操作*。|  
|SQL_REFRESH|该驱动程序将光标置于由指定的行上*RowNumber*并为该行行集缓冲区中的数据刷新一次。 有关如何驱动程序返回的行集缓冲区中数据的详细信息，请参阅按行和列中的绑定的说明**SQLBindCol**。<br /><br /> **SQLSetPos**与*操作*SQL_REFRESH 的更新的状态和内容的当前读取的行集内的行。 这包括刷新书签。 由于缓冲区中的数据刷新，但不是 refetched，因此被固定的行集中的成员身份。 这是不同于通过调用执行刷新**SQLFetchScroll**与*FetchOrientation*的 SQL_FETCH_RELATIVE 和*RowNumber*等于 0，refetches如果该驱动程序和光标支持这些操作，从结果集中，以便它可以显示添加的数据和删除行集删除数据。<br /><br /> 使用成功刷新**SQLSetPos**将不会更改 SQL_ROW_DELETED 行状态。 已删除的行中的行集仍将被标记为删除到下次提取。 行将在下一步读取消失，如果游标支持装箱 (在其中后续**SQLFetch**或**SQLFetchScroll**不返回已删除的行)。<br /><br /> 添加行时使用刷新不会出现**SQLSetPos**执行。 此行为是不同于**SQLFetchScroll**与*FetchType*的 SQL_FETCH_RELATIVE 和*RowNumber*等于 0，也刷新但将当前行集包已删除的记录，如果游标支持这些操作或显示添加的记录。<br /><br /> 使用成功刷新**SQLSetPos** （如果存在行状态数组） 将变为 SQL_ROW_SUCCESS SQL_ROW_ADDED 行状态。<br /><br /> 使用成功刷新**SQLSetPos**将行状态更改 SQL_ROW_UPDATED 为行的新状态 （如果存在行状态数组）。<br /><br /> 如果错误发生在**SQLSetPos**行上的操作，将行状态设置为 SQL_ROW_ERROR （如果存在行状态数组）。<br /><br /> 对于游标打开与 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，使用刷新的 SQL_ATTR_CONCURRENCY 语句属性**SQLSetPos**可能会更新数据源用于检测开放式并发值行已更改。 如果发生这种情况，则将更新的行版本或用于确保光标并发的值的行集缓冲区刷新从服务器时。 刷新每个行发生这种情况。<br /><br /> 行状态数组的 SQL_ATTR_ROW_OPERATION_PTR 语句属性指向的内容为 SQL_REFRESH 忽略*操作*。|  
|SQL_UPDATE|该驱动程序将光标置于由指定的行上*RowNumber*和行集缓冲区中的值更新基础数据的行 ( *TargetValuePtr*中的参数**SQLBindCol**)。 它从长度/指示器缓冲区中检索数据的长度 ( *StrLen_or_IndPtr*中的参数**SQLBindCol**)。 如果任何列的长度，SQL_COLUMN_IGNORE 列不会更新。 在更新后的行，该驱动程序会变为行状态数组的对应元素 SQL_ROW_UPDATED 或 SQL_ROW_SUCCESS_WITH_INFO （如果存在行状态数组）。<br /><br /> 它是驱动程序定义的行为是如果**SQLSetPos**与*操作*SQL_UPDATE 自变量调用包含重复的列的游标。 该驱动程序可以返回驱动程序定义的 SQLSTATE、 可以更新出现在结果集中的第一列或执行其他驱动程序定义的行为。<br /><br /> 指向由 SQL_ATTR_ROW_OPERATION_PTR 语句属性行操作数组可以用于指示大容量更新期间，应忽略行集中的当前行。 有关详细信息，请参阅此函数引用后面的"状态和操作数组"。|  
|SQL_DELETE|该驱动程序将光标置于由指定的行上*RowNumber*并删除基础行的数据。 它将更改为 SQL_ROW_DELETED 行状态数组的相应元素。 行已被删除后，下面不是有效的行： 定位 update 和 delete 语句，对调用**SQLGetData**，并调用**SQLSetPos**与*操作*设置为 SQL_POSITION 除。 对于支持装箱的驱动程序，行从数据源检索新数据时从光标位置删除。<br /><br /> 行是否保持可见取决于游标类型。 例如，已删除的行是静态的和键集驱动游标对可见，但看不到动态游标。<br /><br /> 指向由 SQL_ATTR_ROW_OPERATION_PTR 语句属性行操作数组可以用于指示行集中的当前行批量删除期间应会被忽略。 有关详细信息，请参阅此函数引用后面的"状态和操作数组"。|  
  
## <a name="locktype-argument"></a>LockType 自变量  
 *LockType*自变量提供了应用程序来控制并发的方法。 在大多数情况下，支持并发级别和事务的数据源将支持只对 SQL_LOCK_NO_CHANGE 数值*LockType*自变量。 *LockType*自变量通常仅用于基于文件的支持。  
  
 *LockType*参数指定后的行的锁定状态**SQLSetPos**已执行。 如果该驱动程序不能锁定的行以执行请求的操作，或者为了满足*LockType*自变量，它将返回 SQL_ERROR 和 SQLSTATE 42000 （语法错误或访问冲突）。  
  
 尽管*LockType*为单个语句指定了参数，该锁 accords 连接上的所有语句相同的权限。 具体而言，可通过在连接上的一个语句来获取的锁可以由同一连接上的不同语句解除锁定。  
  
 通过锁定行**SQLSetPos**保持锁定状态，直到应用程序调用**SQLSetPos**对于有行*LockType*设置为 SQL_LOCK_UNLOCK，或直到应用程序调用**SQLFreeHandle**语句或**SQLFreeStmt** SQL_CLOSE 选项。 驱动程序支持事务，行锁定通过**SQLSetPos**处于解除锁定状态，当应用程序调用**SQLEndTran**无法提交或回滚事务连接上 （如果游标已关闭当事务是提交或回滚，返回的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 信息类型所述**SQLGetInfo**)。  
  
 *LockType*参数支持以下类型的锁。 若要确定哪些锁支持的数据源，应用程序调用**SQLGetInfo**与 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （具体取决于游标的类型） 的信息类型。  
  
|*LockType*自变量|锁类型|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|驱动程序或数据源可确保之前行处于相同的锁定或解锁状态**SQLSetPos**调用。 此值的*LockType*允许不支持显式行级锁定，以通过当前的并发性和事务隔离级别使用任何锁定所需的数据源。|  
|SQL_LOCK_EXCLUSIVE|驱动程序或数据源以独占方式锁定行。 在不同的连接上或在不同的应用程序中的语句不能用于获取在该行上的任何锁。|  
|SQL_LOCK_UNLOCK|驱动程序或数据源解除锁定行。|  
  
 如果驱动程序支持 SQL_LOCK_EXCLUSIVE，但不支持 SQL_LOCK_UNLOCK，已锁定的行会保持锁定状态，直到上一个段中所述的函数调用之一发生。  
  
 如果驱动程序支持 SQL_LOCK_EXCLUSIVE，但不支持 SQL_LOCK_UNLOCK，已锁定的行将继续处于锁定状态之前应用程序调用**SQLFreeHandle**语句或**SQLFreeStmt**与SQL_CLOSE 选项中。 如果驱动程序支持事务，并关闭在提交或回滚事务，应用程序调用后的光标**SQLEndTran**。  
  
 为中的更新和删除操作**SQLSetPos**，应用程序使用*LockType*自变量，如下所示：  
  
-   若要确保行不会更改它检索后，应用程序调用**SQLSetPos**与*操作*设置为 SQL_REFRESH 和*LockType*设置为 SQL_LOCK_排他。  
  
-   如果应用程序将设置*LockType*到 SQL_LOCK_NO_CHANGE，驱动程序可保证仅当应用程序为 SQL_ATTR_CONCURRENCY 语句属性指定 SQL_CONCUR_LOCK update 或 delete 操作将会成功。  
  
-   如果应用程序指定 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY 语句属性，该驱动程序比较行版本或值，并拒绝该操作，如果行已更改，因为应用程序提取行。  
  
-   如果应用程序指定 SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY 语句属性，该驱动程序将拒绝任何更新或删除操作。  
  
 有关 SQL_ATTR_CONCURRENCY 语句属性的详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="status-and-operation-arrays"></a>状态和操作数组  
 在调用时使用以下的状态和操作数组**SQLSetPos**:  
  
-   行状态数组 （如指向 IRD 和 SQL_ATTR_ROW_STATUS_ARRAY 语句属性中的 SQL_DESC_ARRAY_STATUS_PTR 字段） 包含行集中的数据的每一行的状态值。 该驱动程序后调用此数组中设置的状态值范围**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，或**SQLSetPos**. 此数组被指向 SQL_ATTR_ROW_STATUS_PTR 语句属性。  
  
-   行操作的数组 （如指向 ARD 和 SQL_ATTR_ROW_OPERATION_ARRAY 语句属性中的 SQL_DESC_ARRAY_STATUS_PTR 字段） 包含的值，每个行集中的行，该值指示是否对的调用**SQLSetPos**忽略或执行大容量操作。 数组中的每个元素设置为 SQL_ROW_PROCEED （默认值） 或 SQL_ROW_IGNORE。 此数组被指向 SQL_ATTR_ROW_OPERATION_PTR 语句属性。  
  
 状态和操作数组中元素的数目必须等于的行集 （如由 SQL_ATTR_ROW_ARRAY_SIZE 语句属性定义） 中的行数。  
  
 有关行状态数组的信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。 有关行操作数组的信息，请参阅"忽略行中大容量操作，"本部分中更高版本。  
  
## <a name="using-sqlsetpos"></a>使用 SQLSetPos  
 应用程序调用之前**SQLSetPos**，它必须执行以下步骤序列：  
  
1.  如果应用程序将调用**SQLSetPos**与*操作*设置为 SQL_UPDATE，调用**SQLBindCol** (或**SQLSetDescRec**) 为每个指定其数据类型，并将绑定的列的数据和长度的缓冲区的列。  
  
2.  如果应用程序将调用**SQLSetPos**与*操作*设置为 SQL_DELETE 或 SQL_UPDATE，调用**SQLColAttribute**若要确保要删除或更新的列是可更新的。  
  
3.  调用**SQLExecDirect**， **SQLExecute**，或创建结果集的目录函数。  
  
4.  调用**SQLFetch**或**SQLFetchScroll**检索的数据。  
  
 有关使用**SQLSetPos**，请参阅[更新数据与 SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
## <a name="deleting-data-using-sqlsetpos"></a>删除使用 SQLSetPos 数据  
 若要删除数据与**SQLSetPos**，应用程序调用**SQLSetPos**与*RowNumber*设置为的行数，以删除和*操作*设置为 SQL_DELETE。  
  
 已经删除了数据后，该驱动程序将更改为 SQL_ROW_DELETED （或 SQL_ROW_ERROR） 中的相应行的实现行状态数组的值。  
  
## <a name="updating-data-using-sqlsetpos"></a>使用 SQLSetPos 更新数据  
 应用程序可以传递列的值，绑定的数据缓冲区中或通过一个或多个调用**SQLPutData**。 其数据传递与列**SQLPutData**称为*数据在执行**列*。 这些通常用于发送 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 列的数据，并可与其他列组合。  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>若要使用 SQLSetPos，应用程序中更新数据：  
  
1.  通过绑定数据和长度/指示器缓冲区中的位置值**SQLBindCol**:  
  
    -   对于正常列，应用程序将放在新的列值 *\*TargetValuePtr*缓冲区和中的该值的长度 *\*StrLen_or_IndPtr*缓冲区。 如果行不会更新，应用程序会将 SQL_ROW_IGNORE 放置在该行的行操作数组元素中。  
  
    -   对于执行中的数据列，应用程序将应用程序定义的值，如列数，放在 *\*TargetValuePtr*缓冲区。 值可以在稍后用于标识的列。  
  
         将 SQL_LEN_DATA_AT_EXEC 结果放置于应用程序 (*长度*) 中的宏 **StrLen_or_IndPtr*缓冲区。 如果 SQL 数据类型的列是 SQL_LONGVARBINARY、 SQL_LONGVARCHAR、 或的长整型数据源 – 特定数据类型和驱动程序返回"Y"SQL_NEED_LONG_DATA_LEN 信息类型中的**SQLGetInfo**，*长度*是参数; 发送数据的字节数否则为必须为非负值，将被忽略。  
  
2.  调用**SQLSetPos**与*操作*参数设置为 SQL_UPDATE 若要更新的数据行。  
  
    -   如果没有执行中的数据列，则过程已完成。  
  
    -   如果没有任何执行中的数据列，该函数将返回 SQL_NEED_DATA，并将继续到步骤 3。  
  
3.  调用**SQLParamData**来检索的地址 *\*TargetValuePtr*要处理的第一个执行中的数据列的缓冲区。 **SQLParamData**返回 SQL_NEED_DATA。 应用程序检索应用程序定义的值从 *\*TargetValuePtr*缓冲区。  
  
    > [!NOTE]  
    >  虽然执行中的数据参数类似于执行中的数据列，但返回的值**SQLParamData**每个不同。  
  
    > [!NOTE]  
    >  数据在执行参数是数据将发送与 SQL 语句中的参数**SQLPutData**与执行该语句时**SQLExecDirect**或**SQLExecute**. 它们被绑定与**SQLBindParameter**或通过设置与描述符**SQLSetDescRec**。 返回的值**SQLParamData**是传递给 32 位值**SQLBindParameter**中*ParameterValuePtr*自变量。  
  
    > [!NOTE]  
    >  执行中的数据列是包含在行集数据将发送与**SQLPutData**行使用的更新时**SQLSetPos**。 它们被绑定与**SQLBindCol**。 返回的值**SQLParamData**是中的行的地址 **TargetValuePtr*正在处理的缓冲区。  
  
4.  调用**SQLPutData**一个或多个时间来发送数据的列。 如果不能在中返回所有数据值，则需要多个调用 *\*TargetValuePtr*中指定的缓冲区**SQLPutData**; 多次调用**SQLPutData**仅当将字符 C 数据发送到具有字符、 binary 或数据源 – 特定数据类型的列或将二进制 C 数据发送到列，但字符，二进制文件，允许相同的列或数据源 – 特定的数据类型。  
  
5.  调用**SQLParamData**以指示所有数据均已都发送的列。  
  
    -   如果没有更多的执行中的数据列， **SQLParamData**返回 SQL_NEED_DATA 和的地址*TargetValuePtr*要处理的下一步执行中的数据列的缓冲区。 应用程序重复步骤 4 和 5。  
  
    -   如果没有更多的执行中的数据列，则过程已完成。 如果已成功时，请执行语句**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果执行失败，它将返回 SQL_ERROR。 此时， **SQLParamData**可以返回可以由任何 SQLSTATE **SQLSetPos**。  
  
 如果数据已更新，该驱动程序将更改为 SQL_ROW_UPDATED 的相应行实现行状态数组中的值。  
  
 如果该操作被取消，或者在发生错误**SQLParamData**或**SQLPutData**后面**SQLSetPos**返回 SQL_NEED_DATA 和所有发送数据前执行中的数据列，则应用程序可以调用仅**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**语句或语句与关联的连接。 如果语句或语句与关联的连接，它调用任何其他函数，该函数将返回 SQL_ERROR 和 SQLSTATE HY010 （函数序列错误）。  
  
 如果应用程序调用**SQLCancel**驱动程序时驱动程序仍需要执行中的数据列数据，取消操作。 然后，应用程序可以调用**SQLSetPos**再次取消不会影响光标状态或当前光标位置。  
  
 当与游标关联的查询规范的选择列表包含多个引用相同的列，是否会生成错误或驱动程序会忽略重复的引用，并执行请求的操作是驱动程序定义的。  
  
## <a name="performing-bulk-operations"></a>执行大容量操作  
 如果*RowNumber*自变量为 0 时，该驱动程序执行中指定的操作*操作*中在行操作中与其字段中具有的 SQL_ROW_PROCEED 值的行集的每一行的自变量数组指向 SQL_ATTR_ROW_OPERATION_PTR 语句属性。 这是一个有效的值*RowNumber*参数*操作*SQL_DELETE、 SQL_REFRESH，或 SQL_UPDATE，但不是 SQL_POSITION 自变量。 **SQLSetPos**与*操作*的 SQL_POSITION 和*RowNumber*等于 0 将返回 SQLSTATE HY109 （无效的光标位置）。  
  
 如果发生错误适用于整个行集，如 SQLSTATE HYT00 （超时过期），该驱动程序返回 SQL_ERROR 和相应的 SQLSTATE。 行集缓冲区的内容是不确定，并且光标位置不变。  
  
 如果发生错误适用于单个行，该驱动程序：  
  
-   行状态数组指向 SQL_ROW_ERROR SQL_ATTR_ROW_STATUS_PTR 语句属性中设置行的元素。  
  
-   错误队列中发送的错误的一个或多个其他 SQLSTATEs 并设置 SQL_DIAG_ROW_NUMBER 字段中的诊断数据结构。  
  
 它已处理错误或警告，如果驱动程序完成在行集中的其余行的操作后，它将返回 SQL_SUCCESS_WITH_INFO。 因此，对于每个返回了错误的行，错误队列中包含零个或多个其他 SQLSTATEs。 如果它已处理错误或警告后，该驱动程序将停止操作，则返回 SQL_ERROR。  
  
 如果该驱动程序返回任何警告，如 SQLSTATE 01004 （截断的数据），它返回应用于整个行集或在行集中的未知行之前它将返回适用于特定行的错误信息的警告。 它将返回以及有关这些行的任何其他错误信息的特定行的警告。  
  
 如果*RowNumber*等同于 0 和*操作*是 SQL_UPDATE、 SQL_REFRESH，还是 SQL_DELETE，行的数目**SQLSetPos**操作在通过 SQL_ATTR_ROWS 指向_FETCHED_PTR 语句属性。  
  
 如果*RowNumber*等同于 0 和*操作*是 SQL_DELETE、 SQL_REFRESH，还是 SQL_UPDATE，该操作后当前行操作之前相同的当前行。  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>忽略大容量操作中的行  
 行操作数组可以用于指示大容量操作使用期间，应忽略行集中的当前行**SQLSetPos**。 若要指示要大容量操作期间忽略一个或多个行的驱动程序，请应用程序应执行以下步骤：  
  
1.  调用**SQLSetStmtAttr**设置为指向数组 SQLUSMALLINTs 该 SQL_ATTR_ROW_OPERATION_PTR 语句属性。 此字段也可以通过调用设置**SQLSetDescField**设置 ARD，这要求应用程序获取的描述符句柄的 SQL_DESC_ARRAY_STATUS_PTR 标头字段。  
  
2.  将行操作数组的每个元素设置为两个值之一：  
  
    -   SQL_ROW_IGNORE，以指示大容量操作，排除的行。  
  
    -   SQL_ROW_PROCEED，若要指示该行包括在大容量操作中。 （这是默认值。）  
  
3.  调用**SQLSetPos**执行大容量操作。  
  
 以下规则适用于行操作数组：  
  
-   SQL_ROW_IGNORE 和 SQL_ROW_PROCEED 影响仅使用大容量操作**SQLSetPos**与*操作*SQL_DELETE 或 SQL_UPDATE。 它们不会影响对调用**SQLSetPos**与*操作*SQL_REFRESH 或 SQL_POSITION。  
  
-   将指针设置为默认情况下 null。  
  
-   如果指针为 null，就像所有元素都设置为 SQL_ROW_PROCEED 将更新所有行。  
  
-   将元素设置为 SQL_ROW_PROCEED 不保证在该特定行上将发生，该操作。 例如，如果某些行集中的行具有状态 SQL_ROW_ERROR 时，该驱动程序可能无法更新无论是否应用程序指定 SQL_ROW_PROCEED 该行。 应用程序必须始终检查行状态数组，以查看该操作是否成功。  
  
-   SQL_ROW_PROCEED 定义为标头文件中的 0。 应用程序可以初始化为 0 的行操作数组，以便处理所有行。  
  
-   如果行操作数组中的元素数"n"设置为 SQL_ROW_IGNORE 和**SQLSetPos**调用以执行大容量更新或删除操作，在调用之后保持不变的行集保留了中的第 n 个行**SQLSetPos**.  
  
-   应用程序应自动设置为 SQL_ROW_IGNORE 的只读的列。  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>忽略大容量操作中的列  
 若要避免不必要的处理由尝试更新一个或多个只读列生成的诊断，应用程序可以设置到 SQL_COLUMN_IGNORE 绑定的长度/指示器缓冲区中的值。 有关详细信息，请参阅[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序允许用户浏览 ORDERS 表和更新订单状态。 光标键集驱动的行集大小为 20，并使用乐观并发控制比较行版本。 提取每个行集后，应用程序将它打印，允许用户选择和更新订单的状态。 应用程序使用**SQLSetPos**将光标定位在所选该行上并执行的定位的更新的行。 （错误处理省略为清楚起见中）。  
  
```  
#define ROWS 20  
#define STATUS_LEN 6  
  
SQLCHAR        szStatus[ROWS][STATUS_LEN], szReply[3];  
SQLINTEGER     cbStatus[ROWS], cbOrderID;  
SQLUSMALLINT   rgfRowStatus[ROWS];  
SQLUINTEGER    sOrderID, crow = ROWS, irow;  
SQLHSTMT       hstmtS, hstmtU;  
  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CONCURRENCY, (SQLPOINTER) SQL_CONCUR_ROWVER, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER) SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_STATUS_PTR, (SQLPOINTER) rgfRowStatus, 0);  
SQLSetCursorName(hstmtS, "C1", SQL_NTS);  
SQLExecDirect(hstmtS, "SELECT ORDERID, STATUS FROM ORDERS ", SQL_NTS);  
  
SQLBindCol(hstmtS, 1, SQL_C_ULONG, &sOrderID, 0, &cbOrderID);  
SQLBindCol(hstmtS, 2, SQL_C_CHAR, szStatus, STATUS_LEN, &cbStatus);  
  
while ((retcode == SQLFetchScroll(hstmtS, SQL_FETCH_NEXT, 0)) != SQL_ERROR) {  
   if (retcode == SQL_NO_DATA_FOUND)  
      break;  
   for (irow = 0; irow < crow; irow++) {  
      if (rgfRowStatus[irow] != SQL_ROW_DELETED)  
         printf("%2d %5d %*s\n", irow+1, sOrderID, NAME_LEN-1, szStatus[irow]);  
   }  
   while (TRUE) {  
      printf("\nRow number to update?");  
      gets_s(szReply, 3);  
      irow = atoi(szReply);  
      if (irow > 0 && irow <= crow) {  
         printf("\nNew status?");  
         gets_s(szStatus[irow-1], (ROWS * STATUS_LEN));  
         SQLSetPos(hstmtS, irow, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
         SQLPrepare(hstmtU,  
          "UPDATE ORDERS SET STATUS=? WHERE CURRENT OF C1", SQL_NTS);  
         SQLBindParameter(hstmtU, 1, SQL_PARAM_INPUT,  
            SQL_C_CHAR, SQL_CHAR,  
            STATUS_LEN, 0, szStatus[irow], 0, NULL);  
         SQLExecute(hstmtU);  
      } else if (irow == 0) {  
         break;  
      }  
   }  
}  
```  
  
 有关更多示例，请参阅[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)和[更新中行 SQLSetPos 行集](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行不与块光标位置的大容量操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取的数据块，或通过结果滚动设置|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|获取单个字段的描述符|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取多个字段的描述符|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单个字段的描述符|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置多个字段的描述符|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
