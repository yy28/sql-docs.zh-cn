---
title: SQLSetPos 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e769949c8c57bbec56055c58c9002494fc6d37be
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211986"
---
# <a name="sqlsetpos-function"></a>SQLSetPos 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLSetPos**设置在行集中的游标位置，并允许应用程序刷新行集中的数据或将更新或删除结果集中的数据。  
  
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
 [输入]要对其执行该操作使用指定的行集中的行的位置*操作*参数。 如果*RowNumber*为 0，则该操作适用于每个行集中的行。  
  
 有关其他信息，请参阅"注释"。  
  
 *运算*  
 [输入]要执行的操作：  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  SQL_ADD 值*操作*自变量已被弃用 ODBC 3 *.x*。 ODBC 3。*x*驱动程序将需要向后兼容性支持 SQL_ADD。 此功能已由调用**SQLBulkOperations**与*操作*SQL_ADD。 当 ODBC 3。*x*应用程序适用于 ODBC 2。*x*驱动程序，驱动程序管理器将映射到调用**SQLBulkOperations**与*操作*的到 SQL_ADD **SQLSetPos**与*操作*SQL_ADD。  
  
 有关详细信息，请参阅"注释"。  
  
 *LockType*  
 [输入]指定如何执行中指定的操作后将其锁定该行*操作*参数。  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 有关详细信息，请参阅"注释"。  
  
 **返回**  
  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetPos**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetPos** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
 对于所有这些 SQLSTATEs 可以返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除 01xxx SQLSTATEs)，将返回 SQL_SUCCESS_WITH_INFO，如果上一个或多个，但并非所有行的多行操作，出现错误，并且如果发生错误，则返回 SQL_ERROR单行操作。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01001|游标操作冲突|*操作*参数为 SQL_DELETE 或 SQL_UPDATE，和任何行或多个行已删除或更新。 (有关对多个行的更新的详细信息，请参阅说明 SQL_ATTR_SIMULATE_CURSOR*特性*中**SQLSetStmtAttr**。)（函数返回 SQL_SUCCESS_WITH_INFO。）<br /><br /> *操作*参数为 SQL_DELETE 或 SQL_UPDATE，并且操作失败，因为乐观并发。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据右截断|*操作*参数为 SQL_REFRESH，并导致截断了非空白字符或二进制数据的非空字符串或二进制数据返回为一列或列数据类型为 SQL_C_CHAR 或 SQL_C_BINARY。|  
|01S01|行中的错误|*RowNumber*参数为 0，并执行与指定的操作时一个或多个行中出现错误*操作*参数。<br /><br /> （SQL_SUCCESS_WITH_INFO 返回如果上一个或多个，但并非所有行的多行操作，出现错误，并且如果在单行操作出错，则返回 SQL_ERROR。）<br /><br /> (此 SQLSTATE 返回时，才**SQLSetPos**后，会调用**SQLExtendedFetch**，则该驱动程序是 ODBC 2。*x*不使用驱动程序和游标库。)|  
|01S07|截断小数部分|*操作*参数为 SQL_REFRESH、 应用程序缓冲区的数据类型不为 SQL_C_CHAR 或 SQL_C_BINARY，返回到应用程序的一个或多个列缓冲区的数据已被截断。 对于数值数据类型，数字的小数部分被截断。 对于时间、 时间戳和 interval 数据类型包含时间部分，时间的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07006|受限制的数据类型属性冲突|无法为指定的数据类型转换的结果集中的列的数据值*TargetType*调用中**SQLBindCol**。|  
|07009|描述符索引无效|自变量*操作*SQL_REFRESH 或 SQL_UPDATE，并将其列已绑定使用一个大于结果集中的列数的列数。|  
|21S02|派生表等级与列列表不匹配|自变量*操作*已 SQL_UPDATE，和任何列都可更新，因为所有列都是要么未绑定、 只读的或者绑定的长度/指示器缓冲区中的值是 SQL_COLUMN_IGNORE。|  
|22001|字符串数据，右截断|*操作*参数为 SQL_UPDATE，并赋值的字符或二进制值的列生成了非空 （适用于字符为单位） 或 （对于二进制文件） 的非 null 字符或字节数的截断。|  
|22003|数值超出范围|自变量*操作*已 SQL_UPDATE，并为结果集中的列的数值分配导致数字被截断的整个 （而不是小数） 部分。<br /><br /> 自变量*操作*已 SQL_REFRESH，并返回一个或多个绑定列的数值可能导致重要数字丢失。|  
|22007|日期时间格式无效|自变量*操作*已 SQL_UPDATE，并分配到结果集中的列的日期或时间戳值导致年、 月或天字段超出范围。<br /><br /> 自变量*操作*已 SQL_REFRESH，并返回一个或多个绑定列的日期或时间戳值可能会造成年、 月或天字段超出范围。|  
|22008|日期/时间字段溢出|*操作*参数为 SQL_UPDATE，和 datetime 算术数据发送到结果集中的列上的性能产生的结果的日期时间字段 （年、 月、 日、 小时、 分钟、 或第二个字段）外部字段，或无效的值的允许范围基于公历日历的日期时间的自然规则。<br /><br /> *操作*参数为 SQL_REFRESH，和算术运算的结果集中检索数据的日期时间的性能产生的结果的日期时间字段 （年、 月、 日、 小时、 分钟、 或第二个字段）外部字段，或无效的值的允许范围基于公历日历的日期时间的自然规则。|  
|22015|间隔字段溢出|*操作*参数为 SQL_UPDATE，并分配的精确数字或到 SQL 数据类型的时间间隔的间隔 C 类型导致重要数字丢失。<br /><br /> *操作*参数为 SQL_UPDATE; 分配到 SQL 类型的时间间隔时，没有间隔 SQL 类型中的 C 类型的值没有表示形式。<br /><br /> *操作*参数为 SQL_REFRESH，并将分配从精确数字或时间间隔 SQL 类型到 C 间隔类型导致重要数字丢失前导字段中。<br /><br /> *操作*参数为 SQL_ 刷新; 分配到 C 间隔类型时，没有间隔 C 类型中的 SQL 类型的值的表示形式，则为。|  
|22018|转换指定的字符值无效|*操作*参数为 SQL_REFRESH; C 类型为准确或近似数值、 日期时间或间隔数据类型; 该列的 SQL 类型是字符数据类型; 和列中的值不是有效的文本绑定 C 类型。<br /><br /> 自变量*操作*已 SQL_UPDATE; 的 SQL 类型是准确或近似数值、 日期时间或间隔数据类型; C 类型为 SQL_C_CHAR; 和列中的值不是有效的绑定的 SQL 类型的文本。|  
|23000|完整性约束冲突|自变量*操作*SQL_DELETE 或 SQL_UPDATE，并且违反了完整性约束。|  
|24000|游标状态无效|*StatementHandle*处于执行状态，但无结果集与关联*StatementHandle*。<br /><br /> (DM) 上打开了游标*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未调用。<br /><br /> 在打开游标的*StatementHandle*，并**SQLFetch**或**SQLFetchScroll**已调用一样，但该游标所处的结果集或之后在开始之前结果集的末尾。<br /><br /> 自变量*操作*为 SQL_DELETE、 SQL_REFRESH 或 SQL_UPDATE，和游标早于开始日期的结果集或结果集的末尾之后位置。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|42000|语法错误或访问冲突|该驱动程序不能根据需要来执行请求的参数中的操作将该行锁定*操作*。<br /><br /> 该驱动程序不能在参数中的请求将该行锁定*LockType*。|  
|44000|WITH CHECK OPTION 冲突|*操作*参数为 SQL_UPDATE，和查看的表上执行更新或创建通过指定的查看表中派生表**WITH CHECK OPTION**，这样，一个或多个行受影响的更新将不再存在中查看的表。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数是在上再次*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行调用 SQLSetPos 函数时。<br /><br /> (DM) 指定*StatementHandle*当时不处于执行状态。 调用函数时没有首先调用**SQLExecDirect**， **SQLExecute**，或目录函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> (DM) 驱动程序是 ODBC 2。*x*驱动程序，并**SQLSetPos**曾为*StatementHandle*后**SQLFetch**调用。|  
|HY011 并显示|现在无法设置属性|(DM) 驱动程序是 ODBC 2。*x*驱动程序; SQL_ATTR_ROW_STATUS_PTR 设置语句属性; 然后**SQLSetPos**之前调用**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**调用。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|*操作*参数为 SQL_UPDATE、 数据值为 null 指针，和的列长度值不是 0，SQL_DATA_AT_EXEC，SQL_COLUMN_IGNORE，SQL_NULL_DATA，或小于或等于 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> *操作*参数为 SQL_UPDATE; 数据值不是空指针; C 数据类型为 SQL_C_BINARY 或 SQL_C_CHAR; 和列长度值是小于 0 但不是等于 SQL_DATA_AT_EXEC，SQL_COLUMN_IGNORESQL_NTS 或 SQL_NULL_DATA，或小于或等于 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 长度/指示器缓冲区中的值为 SQL_DATA_AT_EXEC;SQL 类型是 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 数据源特定的数据类型;和中的 SQL_NEED_LONG_DATA_LEN 信息类型**SQLGetInfo**是"Y"。|  
|HY092|无效的属性标识符|(DM) 为指定的值*操作*参数无效。<br /><br /> (DM) 为指定的值*LockType*参数无效。<br /><br /> *操作*参数 SQL_UPDATE 或 SQL_DELETE，而 sql_attr_concurrency 设置语句属性是 SQL_ATTR_CONCUR_READ_ONLY。|  
|HY107|行数值超出范围|为参数指定的值*RowNumber*大于行集中的行数。|  
|HY109|无效的游标位置|与关联的光标*StatementHandle*已定义为只进，因此未无法在行集内定位游标。 请参阅中的 SQL_ATTR_CURSOR_TYPE 属性的说明**SQLSetStmtAttr**。<br /><br /> *操作*自变量是 SQL_UPDATE、 SQL_DELETE，还是 SQL_REFRESH，并由标识该行*RowNumber*参数已删除或尚未提取。<br /><br /> （数据挖掘） *RowNumber*参数为 0，并且*操作*参数为 SQL_POSITION。<br /><br /> **SQLSetPos**后调用**SQLBulkOperations**调用之前**SQLFetchScroll**或**SQLFetch**调用。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持请求中的操作*操作*自变量或*LockType*参数。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回的结果集。 通过设置超时期限**SQLSetStmtAttr**与*属性*的 SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
  
> [!CAUTION]
>  有关语句的信息表明**SQLSetPos**可中调用，它需要执行与 ODBC 2 的兼容性 *.x*应用程序，请参阅[块游标、 可滚动游标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。  
  
## <a name="rownumber-argument"></a>RowNumber 参数  
 *RowNumber*参数指定要对其执行由指定的操作在行集中的行数*操作*参数。 如果*RowNumber*为 0，则该操作适用于每个行集中的行。 *RowNumber*必须是介于 0 到行集中的行数。  
  
> [!NOTE]  
>  在 C 语言中，数组是从 0 开始， *RowNumber*自变量是从 1 开始。 例如，若要更新的行集的第五个行，应用程序修改的行集缓冲区的数组索引 4 处，但指定*RowNumber*为 5。  
  
 所有操作将游标都定位指定的行上*RowNumber*。 以下操作需要游标位置：  
  
-   定位 update 和 delete 语句。  
  
-   调用**SQLGetData**。  
  
-   调用**SQLSetPos** SQL_DELETE、 SQL_REFRESH 和 SQL_UPDATE 选项。  
  
 例如，如果*RowNumber*为 2 个调用**SQLSetPos**与*操作*的 SQL_DELETE，将光标定位在第二行的行集，该行将被删除。 在实现行状态数组 （由 SQL_ATTR_ROW_STATUS_PTR 语句属性指向） 的第二行条目更改为 SQL_ROW_DELETED。  
  
 调用时，应用程序可以指定游标位置**SQLSetPos**。 通常情况下，它将调用**SQLSetPos**与 SQL_POSITION 或 SQL_REFRESH 操作将游标定位之前执行定位更新或删除语句或者调用**SQLGetData**。  
  
## <a name="operation-argument"></a>操作参数  
 *操作*参数支持以下操作。 若要确定哪些选项支持的数据源，应用程序调用**SQLGetInfo**与 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （具体取决于游标的类型） 的信息类型。  
  
|*运算*<br /><br /> 参数|操作|  
|------------------------------|---------------|  
|SQL_POSITION|该驱动程序将光标置于由指定的行上*RowNumber*。<br /><br /> 指向 SQL_ATTR_ROW_OPERATION_PTR 语句属性的行状态数组的内容会忽略 SQL_POSITION*操作*。|  
|SQL_REFRESH|该驱动程序将光标置于由指定的行上*RowNumber*并刷新数据，为该行的行集缓冲区中。 有关如何驱动程序返回的行集缓冲区中数据的详细信息，请参阅按行和按列绑定中的说明**SQLBindCol**。<br /><br /> **SQLSetPos**与*操作*SQL_REFRESH 的更新的状态和当前提取行集内的行的内容。 这包括刷新书签。 因为缓冲区中的数据刷新，但不是 refetched，被固定的行集中的成员身份。 这是不同于通过调用执行刷新**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_RELATIVE 的和一个*RowNumber*等于 0，refetches如果该驱动程序和游标都支持这些操作，从结果集，以便它可以显示添加的数据和删除的行集删除数据。<br /><br /> 使用成功刷新**SQLSetPos**不会更改的行状态为 SQL_ROW_DELETED。 已删除的行，该行集内仍将被标记为已删除，直到下一次提取。 游标支持装箱会消失在下一次提取行 (在其中的后续**SQLFetch**或**SQLFetchScroll**不会返回已删除的行)。<br /><br /> 添加行时使用刷新不会出现**SQLSetPos**执行。 此行为是不同于**SQLFetchScroll**与*FetchType* SQL_FETCH_RELATIVE 的和一个*RowNumber*等于 0，这还刷新但将当前行集如果游标支持这些操作，则包已删除的记录或显示添加的记录。<br /><br /> 使用成功刷新**SQLSetPos** （如果存在行状态数组） 将变为 SQL_ROW_SUCCESS SQL_ROW_ADDED 行状态。<br /><br /> 使用成功刷新**SQLSetPos**将更改的行状态为 SQL_ROW_UPDATED 为行的新状态 （如果存在行状态数组）。<br /><br /> 如果在出现错误**SQLSetPos**对某行的操作，将行状态设置为 SQL_ROW_ERROR （如果存在行状态数组）。<br /><br /> 游标为打开的 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，使用刷新 sql_attr_concurrency 设置语句属性与**SQLSetPos**可能会更新数据源用于检测的乐观并发值行已更改。 如果发生这种情况，只要行集缓冲区刷新从服务器会更新的行版本或使用，以确保游标并发的值。 刷新每个行发生这种情况。<br /><br /> 指向 SQL_ATTR_ROW_OPERATION_PTR 语句属性的行状态数组的内容会忽略 SQL_REFRESH*操作*。|  
|SQL_UPDATE|该驱动程序将光标置于由指定的行上*RowNumber* ，并使用行集缓冲区中的值更新数据的基础行 ( *TargetValuePtr*中的参数**SQLBindCol**)。 它从长度/指示器缓冲区中检索的数据的长度 ( *StrLen_or_IndPtr*中的参数**SQLBindCol**)。 如果任何列的长度为 SQL_COLUMN_IGNORE，该列不会更新。 在更新后的行，该驱动程序更改行状态数组的对应元素为 SQL_ROW_UPDATED 或 SQL_ROW_SUCCESS_WITH_INFO （如果存在行状态数组）。<br /><br /> 它是驱动程序定义的行为是如果**SQLSetPos**与*操作*SQL_UPDATE 参数调用上包含重复的列的游标。 该驱动程序可以返回驱动程序定义的 SQLSTATE、 可以更新显示在结果集中的第一列或执行其他驱动程序定义的行为。<br /><br /> 行操作数组指向 SQL_ATTR_ROW_OPERATION_PTR 语句属性可以用于指示应在大容量更新期间忽略当前行集中的行。 有关详细信息，请参阅更高版本中此函数引用的"状态和操作数组"。|  
|SQL_DELETE|该驱动程序将光标置于由指定的行上*RowNumber*和删除数据的基础行。 它将更改为 SQL_ROW_DELETED 行状态数组的相应元素。 删除行后，下面不是有效的行： 定位 update 和 delete 语句，对**SQLGetData**，并调用**SQLSetPos**与*操作*设置为 SQL_POSITION 以外。 支持封装的驱动程序，请从数据源中检索新数据时行从游标中删除。<br /><br /> 行是否保持可见取决于游标类型。 例如，已删除的行是静态的和由键集驱动游标可见，但对动态游标不可见。<br /><br /> 行操作数组指向 SQL_ATTR_ROW_OPERATION_PTR 语句属性可以用于指示应在大容量删除期间忽略当前行集中的行。 有关详细信息，请参阅更高版本中此函数引用的"状态和操作数组"。|  
  
## <a name="locktype-argument"></a>LockType 参数  
 *LockType*参数提供的应用程序来控制并发的方法。 在大多数情况下，支持的并发级别和事务的数据源将支持的 SQL_LOCK_NO_CHANGE 值仅*LockType*参数。 *LockType*参数通常仅用于基于文件的支持。  
  
 *LockType*参数指定的行后的锁定状态**SQLSetPos**已执行。 如果驱动程序无法执行请求的操作，或者为了满足将该行锁定*LockType*参数，它将返回 SQL_ERROR 和 SQLSTATE 42000 （语法错误或访问冲突）。  
  
 尽管*LockType*为单个语句指定了参数，该锁 accords 的连接上的所有语句相同的权限。 具体而言，通过在连接上的一条语句获取的锁可以由同一个连接上的不同语句解除锁定。  
  
 通过锁定行**SQLSetPos**应用程序调用之前保持锁定状态**SQLSetPos**的行的*LockType*设置为 SQL_LOCK_UNLOCK，或直到应用程序调用**SQLFreeHandle**语句或**SQLFreeStmt** SQL_CLOSE 选项。 为支持事务的驱动程序，通过将锁定行**SQLSetPos**应用程序调用时，会解锁**SQLEndTran**提交或回滚事务，在连接上 （如果关闭游标当提交或回滚后，由 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 信息类型返回的事务**SQLGetInfo**)。  
  
 *LockType*参数支持以下类型的锁。 若要确定哪些锁支持的数据源，应用程序调用**SQLGetInfo**与 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （具体取决于游标的类型） 的信息类型。  
  
|*LockType*参数|锁类型|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|驱动程序或数据源可确保之前的一行是相同的锁定或解锁状态**SQLSetPos**调用。 此值的*LockType*允许不支持显式行级锁定要当前的并发性和事务隔离级别使用任何锁定所需的数据源。|  
|SQL_LOCK_EXCLUSIVE|驱动程序或数据源以独占方式锁定行。 在不同连接上或在不同的应用程序中的语句不能用于获取在该行上的任何锁。|  
|SQL_LOCK_UNLOCK|驱动程序或数据源对行进行解锁。|  
  
 如果驱动程序支持 SQL_LOCK_EXCLUSIVE，但不支持 SQL_LOCK_UNLOCK，已锁定的行将保持锁定状态，直到上一个段中所述的函数调用之一发生。  
  
 如果驱动程序支持 SQL_LOCK_EXCLUSIVE，但不支持 SQL_LOCK_UNLOCK，已锁定的行将保持锁定状态直到应用程序调用**SQLFreeHandle**语句或**SQLFreeStmt**与SQL_CLOSE 选项中。 如果该驱动程序支持事务，并且关闭在提交或回滚事务，应用程序调用时游标**SQLEndTran**。  
  
 有关中的 update 和 delete 操作**SQLSetPos**，应用程序使用*LockType*参数，如下所示：  
  
-   若要保证行不会更改在检索之后，应用程序调用**SQLSetPos**与*操作*设置为 SQL_REFRESH 并*LockType*设置为 SQL_LOCK_排他。  
  
-   如果应用程序设置*LockType*到 SQL_LOCK_NO_CHANGE，驱动程序可确保仅当应用程序指定 SQL_CONCUR_LOCK sql_attr_concurrency 设置语句属性的更新或删除操作将会成功。  
  
-   如果应用程序指定的语句属性 SQL_ATTR_CONCURRENCY SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，驱动程序将行版本或值进行比较，如果应用程序提取行更改行，则拒绝该操作。  
  
-   如果应用程序指定 SQL_CONCUR_READ_ONLY sql_attr_concurrency 设置语句属性，该驱动程序将拒绝任何更新或删除操作。  
  
 有关 sql_attr_concurrency 设置语句属性的详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="status-and-operation-arrays"></a>状态和操作数组  
 调用时使用以下的状态和操作数组**SQLSetPos**:  
  
-   行状态数组 （如指向 IRD 和 SQL_ATTR_ROW_STATUS_ARRAY 语句属性中的 SQL_DESC_ARRAY_STATUS_PTR 字段） 包含行集中的数据的每一行的状态值。 驱动程序后调用此数组中设置状态值**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，或者**SQLSetPos**. 此数组所指向的 SQL_ATTR_ROW_STATUS_PTR 语句属性。  
  
-   行操作数组 （如指向 ARD 和 SQL_ATTR_ROW_OPERATION_ARRAY 语句属性中的 SQL_DESC_ARRAY_STATUS_PTR 字段） 包含每个行集中的一行，该值指示值是否调用**SQLSetPos**忽略或执行大容量操作。 数组中的每个元素设置为 SQL_ROW_PROCEED （默认值） 或 SQL_ROW_IGNORE。 此数组所指向的 SQL_ATTR_ROW_OPERATION_PTR 语句属性。  
  
 状态和操作数组中的元素数必须等于行集 （如 SQL_ATTR_ROW_ARRAY_SIZE 语句属性所定义） 中的行数。  
  
 有关行状态数组的信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。 有关行操作数组的信息，请参阅"忽略行中大容量操作，"更高版本在本部分中。  
  
## <a name="using-sqlsetpos"></a>使用 SQLSetPos  
 应用程序调用之前**SQLSetPos**，它必须执行以下步骤序列：  
  
1.  如果应用程序将调用**SQLSetPos**与*操作*设置为 SQL_UPDATE，调用**SQLBindCol** (或**SQLSetDescRec**) 为每个若要指定其数据类型和绑定的列的数据和长度的缓冲区的列。  
  
2.  如果应用程序将调用**SQLSetPos**与*操作*设置为 SQL_DELETE 或 SQL_UPDATE，调用**SQLColAttribute** ，确保要删除或更新的列是可更新。  
  
3.  调用**SQLExecDirect**， **SQLExecute**，或创建结果集的目录函数。  
  
4.  调用**SQLFetch**或**SQLFetchScroll**来检索数据。  
  
 有关使用详细信息**SQLSetPos**，请参阅[使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
## <a name="deleting-data-using-sqlsetpos"></a>使用 SQLSetPos 删除数据  
 若要删除数据**SQLSetPos**，应用程序调用**SQLSetPos**与*RowNumber*设置为的行数，以删除和*操作*设置为 SQL_DELETE。  
  
 删除数据后，驱动程序将更改为 SQL_ROW_DELETED （或 SQL_ROW_ERROR） 中的相应行实现行状态数组的值。  
  
## <a name="updating-data-using-sqlsetpos"></a>使用 SQLSetPos 更新数据  
 应用程序可以绑定的数据缓冲区中或通过一个或多个调用将传递列的值**SQLPutData**。 其数据传递使用的列**SQLPutData**称为*执行时数据**列*。 这些通常用于发送 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 列的数据，可以与其他列组合。  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>使用 SQLSetPos，应用程序中更新数据：  
  
1.  通过绑定数据和长度/指示器缓冲区中的位置值**SQLBindCol**:  
  
    -   对于正常的列，应用程序将放置中的新列值 *\*TargetValuePtr*缓冲区和中该值的长度 *\*StrLen_or_IndPtr*缓冲区。 如果不应更新行，应用程序会将 SQL_ROW_IGNORE 置于该行的行操作数组的元素。  
  
    -   对于执行时数据列，应用程序中放入应用程序定义值，如列数 *\*TargetValuePtr*缓冲区。 可以稍后使用值标识的列。  
  
         SQL_LEN_DATA_AT_EXEC 将结果放置于该应用程序 (*长度*) 中的宏 **StrLen_or_IndPtr*缓冲区。 如果 SQL 数据类型的列是 SQL_LONGVARBINARY、 SQL_LONGVARCHAR 或 long 数据源特定的数据类型和驱动程序将返回"Y"SQL_NEED_LONG_DATA_LEN 信息类型中的**SQLGetInfo**，*长度*是数个字节的数据要发送的参数; 否则为必须为非负值，并且将被忽略。  
  
2.  调用**SQLSetPos**与*操作*参数设置为 SQL_UPDATE 来更新数据的行。  
  
    -   如果不有任何执行时数据列，该过程已完成。  
  
    -   如果有任何执行时数据列，该函数将返回 SQL_NEED_DATA，并转到步骤 3。  
  
3.  调用**SQLParamData**若要检索的地址 *\*TargetValuePtr*要处理的第一个执行时数据列的缓冲区。 **SQLParamData**返回 SQL_NEED_DATA。 应用程序中检索应用程序定义的值从 *\*TargetValuePtr*缓冲区。  
  
    > [!NOTE]  
    >  尽管执行时数据参数类似于执行时数据列，但返回的值**SQLParamData**是为每个不同。  
  
    > [!NOTE]  
    >  执行时数据参数是数据将发送与 SQL 语句中的参数**SQLPutData**时执行语句**SQLExecDirect**或**SQLExecute**. 它们被绑定与**SQLBindParameter**或通过设置与描述符**SQLSetDescRec**。 返回的值**SQLParamData**是一个 32 位值传递给**SQLBindParameter**中*ParameterValuePtr*参数。  
  
    > [!NOTE]  
    >  执行时数据列是包含在行集数据将发送具有**SQLPutData**更新某一行时**SQLSetPos**。 它们被绑定与**SQLBindCol**。 返回的值**SQLParamData**是中的行的地址 **TargetValuePtr*正在处理的缓冲区。  
  
4.  调用**SQLPutData**一个或多个次多次以发送列数据。 如果所有这些数据值不能返回的则需要多次调用 *\*TargetValuePtr*中指定的缓冲区**SQLPutData**; 多次调用**SQLPutData**只有在将字符 C 数据发送到包含的字符、 二进制或数据源特定的数据类型的列或二进制 C 数据发送到具有二进制文件，一个字符的列时允许同一列或数据源特定的数据类型。  
  
5.  调用**SQLParamData**再次以指示已将列的所有数据。  
  
    -   如果有多个执行时数据列， **SQLParamData**将返回 SQL_NEED_DATA 和的地址*TargetValuePtr*要处理的下一步执行时数据列的缓冲区。 应用程序重复步骤 4 和 5。  
  
    -   如果没有更多的执行时数据列，该过程已完成。 如果成功，已执行语句**SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果执行失败，它将返回 SQL_ERROR。 在此情况下， **SQLParamData**可以返回任何可由返回的 SQLSTATE **SQLSetPos**。  
  
 如果数据已更新，该驱动程序将更改为 SQL_ROW_UPDATED 在实现行状态数组的相应行的值。  
  
 如果将取消该操作，或者在出错**SQLParamData**或**SQLPutData**后**SQLSetPos**返回 SQL_NEED_DATA 和之前的所有发送数据执行时数据列，该应用程序可以调用仅**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**语句或用语句相关联的连接。 如果它调用任何其他函数的语句或用语句相关联的连接，则函数返回 SQL_ERROR 并且 SQLSTATE HY010 （函数序列错误）。  
  
 如果应用程序调用**SQLCancel**驱动程序时驱动程序仍需要执行时数据列的数据，取消操作。 然后，应用程序可以调用**SQLSetPos**再次取消不会影响游标状态或当前光标位置。  
  
 当查询规范与游标相关联的选择列表包含多个引用同一列，是否会生成错误或驱动程序忽略重复的引用，并执行所请求的操作是驱动程序定义的。  
  
## <a name="performing-bulk-operations"></a>执行大容量操作  
 如果*RowNumber*参数为 0，则该驱动程序执行中指定的操作*操作*参数中的值为 SQL_ROW_PROCEED 行操作中与其字段中的行集的每一行指向数组由 SQL_ATTR_ROW_OPERATION_PTR 语句属性。 这是一个有效的值*RowNumber*参数*操作*SQL_DELETE，SQL_REFRESH，或 SQL_UPDATE，但不是 SQL_POSITION 的参数。 **SQLSetPos**与*操作*SQL_POSITION 的和一个*RowNumber*等于 0 将返回 SQLSTATE HY109 （无效的游标位置）。  
  
 如果发生错误适用于整个行集，如 SQLSTATE HYT00 （超时过期），驱动程序将返回 SQL_ERROR 并且相应的 SQLSTATE。 行集缓冲区的内容是不确定，并且光标位置保持不变。  
  
 如果发生错误适用于单个行，该驱动程序：  
  
-   行状态数组指向 SQL_ROW_ERROR 将 SQL_ATTR_ROW_STATUS_PTR 语句属性中设置行的元素。  
  
-   发布错误队列中的错误的一个或多个其他 SQLSTATEs 和设置 SQL_DIAG_ROW_NUMBER 字段中的诊断数据结构。  
  
 它已处理的错误或警告，如果该驱动程序完成的剩余行集中的行的操作后，它将返回 SQL_SUCCESS_WITH_INFO。 因此，对于每个返回了错误的行，错误队列中包含零个或多个其他 SQLSTATEs。 如果它已处理的错误或警告后，该驱动程序将停止操作，则返回 SQL_ERROR。  
  
 如果该驱动程序返回任何警告，如 SQLSTATE 01004 （数据被截断），它返回应用于整个行集或未知行集中的行才会返回应用到特定行的错误信息的警告。 它将返回特定的行，以及有关这些行的任何其他错误信息的警告。  
  
 如果*RowNumber*等于 0 并且*操作*SQL_UPDATE、 SQL_REFRESH，或 SQL_DELETE，行的数目**SQLSetPos**运行 SQL_ATTR_ROWS 上指向_FETCHED_PTR 语句属性。  
  
 如果*RowNumber*等于 0 并且*操作*是 SQL_DELETE、 SQL_REFRESH，还是 SQL_UPDATE，该操作后执行操作前的当前行相同的当前行。  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>忽略大容量操作中的行  
 行操作数组可用于指示应在过程中大容量操作使用忽略当前行集中的行**SQLSetPos**。 若要指示要在大容量操作过程中忽略一个或多个行的驱动程序，应用程序应执行以下步骤：  
  
1.  调用**SQLSetStmtAttr**设置为指向数组 SQLUSMALLINTs SQL_ATTR_ROW_OPERATION_PTR 语句属性。 此外可以通过调用设置此字段**SQLSetDescField**设置 ARD，这要求应用程序获取描述符句柄的 SQL_DESC_ARRAY_STATUS_PTR 标头字段。  
  
2.  将行操作数组的每个元素设置为两个值之一：  
  
    -   SQL_ROW_IGNORE，以指示该行大容量操作中排除。  
  
    -   SQL_ROW_PROCEED，以指示在大容量操作中包括的行。 （这是默认值。）  
  
3.  调用**SQLSetPos**执行大容量操作。  
  
 以下规则适用于行操作数组：  
  
-   SQL_ROW_IGNORE 和 SQL_ROW_PROCEED 影响仅使用大容量操作**SQLSetPos**与*操作*SQL_DELETE 或 SQL_UPDATE。 它们不会影响对调用**SQLSetPos**与*操作*SQL_REFRESH 或 SQL_POSITION。  
  
-   将指针设置为默认情况下为 null。  
  
-   如果指针为 null，如同所有元素都设置为 SQL_ROW_PROCEED 更新所有行。  
  
-   将元素设置为 SQL_ROW_PROCEED 不保证该操作会在该特定行上发生。 例如，如果某一行的行集中有状态 SQL_ROW_ERROR，驱动程序可能无法更新无论是否在应用程序指定 SQL_ROW_PROCEED 该行。 应用程序必须始终检查行状态数组，以查看操作是否成功。  
  
-   SQL_ROW_PROCEED 被定义为标头文件中为 0。 应用程序可以初始化为 0 的行操作数组以便处理所有行。  
  
-   如果行操作数组中的元素数量"n"设置为 SQL_ROW_IGNORE 并**SQLSetPos**调用以执行大容量更新或删除操作，在调用后保持不变的行集保留了中的第 n 行**SQLSetPos**.  
  
-   应用程序应自动设置为 SQL_ROW_IGNORE 的只读列。  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>忽略在大容量操作中的列  
 若要避免不必要的处理由一个或多个只读列的尝试更新生成的诊断，应用程序可以设置到 SQL_COLUMN_IGNORE 绑定的长度/指示器缓冲区中的值。 有关详细信息，请参阅[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="code-example"></a>代码示例  
 在以下示例中，应用程序允许用户浏览订单表和更新订单状态。 游标是由键集驱动的行集大小为 20，并使用比较行版本的乐观并发控制。 提取每个行集后，应用程序进行打印，允许用户选择和更新订单的状态。 应用程序使用**SQLSetPos**将游标定位在所选行上，并执行定位的更新的行。 （省略了错误处理为清楚起见。）  
  
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
  
 有关更多示例，请参阅[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)并[更新行集中的行使用 SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行块的光标位置不相关的大容量操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|获取描述符的单个字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取描述符的多个字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单个字段的描述符|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置多个字段的描述符|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
