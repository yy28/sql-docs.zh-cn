---
title: SQLSetPos 函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a8839f1ae540ac9e5f29e144f7f57fb754e50ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287327"
---
# <a name="sqlsetpos-function"></a>SQLSetPos 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLSetPos**设置行集中的游标位置，并允许应用程序刷新行集中的数据或更新或删除结果集中的数据。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *行号*  
 [输入]行在行集中的位置，用于执行使用 *"操作"* 参数指定的操作。 如果*RowNumber*为 0，则该操作将应用于行集中的每一行。  
  
 有关详细信息，请参阅"注释"。  
  
 *操作*  
 [输入]操作以执行：  
  
 SQL_POSITIONSQL_REFRESHSQL_UPDATESQL_DELETE  
  
> [!NOTE]
>  *操作*参数的SQL_ADD值已被弃用为 ODBC *3.x*。 ODBC *3.x*驱动程序需要支持SQL_ADD，以便向后兼容。 此功能已替换为对**SQLBulk 操作**的调用，并带有SQL_ADD*操作*。 当 ODBC *3.x*应用程序与 ODBC *2.x*驱动程序配合使用时，驱动程序管理器将调用映射到*Operation***SQLBulk 操作**，操作操作为*Operation***SQL_ADD，** 操作操作为 SQL_ADD。  
  
 有关详细信息，请参阅"注释"。  
  
 *LockType*  
 [输入]指定在执行*操作*参数中指定的操作后如何锁定行。  
  
 SQL_LOCK_NO_CHANGESQL_LOCK_EXCLUSIVESQL_LOCK_UNLOCK  
  
 有关详细信息，请参阅"注释"。  
  
 **返回**  
  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetPos**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLSetPos**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
 对于可以返回SQL_SUCCESS_WITH_INFO或SQL_ERROR的所有 SQLSTAT（01xxx SQLSTATEs 除外），如果多行操作的一个或多个行发生错误（但不是全部）发生错误，则返回SQL_SUCCESS_WITH_INFO，如果单行操作发生错误，则返回SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01001|光标操作冲突|*操作*参数SQL_DELETE或SQL_UPDATE，并且没有删除或更新任何行或多行。 （有关对多行的更新的详细信息，请参阅**SQLSetStmtAttr**中的SQL_ATTR_SIMULATE_CURSOR*属性*的说明。（函数返回SQL_SUCCESS_WITH_INFO。<br /><br /> *操作*参数SQL_DELETE或SQL_UPDATE，并且操作由于乐观并发而失败。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据右截断|*SQL_REFRESH操作*参数，为数据类型为SQL_C_CHAR或SQL_C_BINARY的列返回字符串或二进制数据，从而导致非空白字符或非 NULL 二进制数据的截断。|  
|01S01|行中的错误|*RowNumber*参数为 0，在执行使用 *"操作"* 参数指定的操作时，一个或多个行中发生错误。<br /><br /> （如果多行操作的一个或多个行发生错误（但不是全部），则返回SQL_SUCCESS_WITH_INFO，如果单行操作发生错误，则返回SQL_ERROR。<br /><br /> （仅当**SQLATPos**在**SQLExtendedFetch**之后调用 SQLSetPos 时，如果驱动程序是 ODBC *2.x*驱动程序且未使用游标库，则仅返回此 SQLSTATE。|  
|01S07|分数截断|*SQL_REFRESH操作*参数，应用程序缓冲区的数据类型未SQL_C_CHAR或SQL_C_BINARY，返回到一个或多个列的应用程序缓冲区的数据被截断。 对于数字数据类型，数字的小数部分被截断。 对于包含时间组件的时间、时间戳和间隔数据类型，时间的小数部分被截断。<br /><br /> （函数返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限数据类型属性冲突|无法将结果集中列的数据值转换为*TargetType*在调用**SQLBindCol**时指定的数据类型。|  
|07009|无效描述符索引|参数*操作*SQL_REFRESH或SQL_UPDATE，并且对列绑定的列数大于结果集中的列数。|  
|21S02|派生表的程度与列列表不匹配|参数*操作*是SQL_UPDATE的，没有列是可升的，因为所有列要么是未绑定的、只读的，要么是绑定长度/指示器缓冲区中的值SQL_COLUMN_IGNORE。|  
|22001|字符串数据，右截断|*操作*参数SQL_UPDATE，将字符或二进制值分配给列会导致非空白（字符）或非空字符（二进制字符）或字节的截断。|  
|22003|数值超范围|参数*操作*SQL_UPDATE，并将数值分配给结果集中的列会导致数字的整个部分（而不是小数）被截断。<br /><br /> 参数*操作*SQL_REFRESH，返回一个或多个绑定列的数值将导致重要数字的损失。|  
|22007|无效日期时间格式|参数*操作*SQL_UPDATE，并将日期或时间戳值分配给结果集中的列会导致年份、月份或日字段超过范围。<br /><br /> 参数*操作*SQL_REFRESH，返回一个或多个绑定列的日期或时间戳值将导致年份、月份或日字段超出范围。|  
|22008|日期/时间字段溢出|*操作*参数SQL_UPDATE，并且对发送到结果集中的列的数据执行日期时间算术，导致结果超出字段允许的值范围，或根据公历的约会时间自然规则无效。<br /><br /> *操作*参数SQL_REFRESH，并且对从结果集中检索的数据执行日期时间算术，导致结果超出字段允许的值范围，或根据公历的约会时间自然规则无效。|  
|22015|间隔字段溢出|*操作*参数SQL_UPDATE，将精确数字或间隔 C 类型分配给间隔 SQL 数据类型会导致重要数字丢失。<br /><br /> *行动*论点SQL_UPDATE;当分配给间隔 SQL 类型时，间隔 SQL 类型中没有 C 类型的值表示形式。<br /><br /> *操作*参数SQL_REFRESH，并将从精确数字或间隔 SQL 类型分配给间隔 C 类型会导致前导字段中的重要数字丢失。<br /><br /> *操作*参数SQL_ REFRESH;当分配给间隔 C 类型时，间隔 C 类型中没有 SQL 类型的值表示形式。|  
|22018|强制转换规范的无效字符值|*行动*论点SQL_REFRESH;C 类型是精确或近似的数字、日期时间或间隔数据类型;列的 SQL 类型是字符数据类型;列中的值不是绑定 C 类型的有效文本。<br /><br /> 参数*操作*是SQL_UPDATE;SQL 类型是精确或近似的数字、日期时间或间隔数据类型;C 类型为SQL_C_CHAR;列中的值不是绑定 SQL 类型的有效文本。|  
|23000|完整性约束冲突|参数*操作*SQL_DELETE或SQL_UPDATE，并且违反了完整性约束。|  
|24000|无效的游标状态|*语句句柄*处于已执行状态，但没有与*语句句柄*关联的结果集。<br /><br /> （DM）*语句句柄*上打开了一个游标，但**SQLFetch**或**SQLFetchScroll**尚未调用。<br /><br /> 在*语句句柄*上打开一个游标，并且已调用**SQLFetch**或**SQLFetchScroll，** 但光标位于结果集开始之前或结果集结束之后。<br /><br /> 参数*操作*SQL_DELETE、SQL_REFRESH 或SQL_UPDATE，光标位于结果集开始之前或结果集结束之后。|  
|40001|序列化失败|由于与另一个事务的资源死锁，事务已回滚。|  
|40003|报表完成未知|执行此函数期间，关联的连接失败，无法确定事务的状态。|  
|42000|语法错误或访问冲突|驱动程序无法根据需要锁定该行，以执行参数*操作*中请求的操作。<br /><br /> 驱动程序无法按参数*LockType*中的请求锁定该行。|  
|44000|与检查选项冲突|*操作*参数SQL_UPDATE，更新是在查看的表或从已查看表派生的表上执行的，该表是通过指定 **"使用 CHECK 选项**"创建的，以便受更新影响的一个或多个行不再存在于查看的表中。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|异步处理已启用*语句句柄*。 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**在*语句句柄*上调用 ，然后在*语句句柄*上再次调用该函数。<br /><br /> 调用该函数，在完成执行之前 **，SQLCancel**或**SQLCancelHandle**是从多线程应用程序中的不同线程调用*的语句句柄*。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用 SQLSetPos 函数时，此异步函数仍在执行。<br /><br /> （DM） 指定的*语句句柄*未处于执行状态。 调用该函数时没有首先调用**SQLExecDirect、SQLExecute**或目录函数。 **SQLExecute**<br /><br /> （DM） 为*语句句柄*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） 驱动程序是 ODBC *2.x*驱动程序，在调用**SQLFetch**后调用**SQLSetPos**进行*语句处理*。|  
|HY011|无法立即设置属性|（DM） 驱动程序是 ODBC *2.x*驱动程序;已设置SQL_ATTR_ROW_STATUS_PTR语句属性;然后**SQLSetPos**在调用**SQLFetch、SQLFetchScroll**或 SQL**扩展获取**之前调用。 **SQLFetchScroll**|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|*SQL_UPDATE操作*参数，数据值为空指针，列长度值不是 0、SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NULL_DATA或小于或等于SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> *行动*论点SQL_UPDATE;数据值不是空指针;数据值不是空指针。C 数据类型为SQL_C_BINARY或SQL_C_CHAR;并且列长度值小于 0 但不等于SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS或SQL_NULL_DATA，或小于或等于SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 长度/指示器缓冲区中的值SQL_DATA_AT_EXEC;SQL 类型要么是SQL_LONGVARCHAR、SQL_LONGVARBINARY，要么是长数据源特定的数据类型;**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN信息类型为"Y"。|  
|HY092|无效属性标识符|（DM） 为*操作*参数指定的值无效。<br /><br /> （DM） 为*LockType*参数指定的值无效。<br /><br /> *操作*参数SQL_UPDATE或SQL_DELETE，SQL_ATTR_CONCURRENCY语句属性SQL_ATTR_CONCUR_READ_ONLY。|  
|HY107|行值范围外|为参数*RowNumber*指定的值大于行集中的行数。|  
|HY109|光标位置无效|与*语句句柄*关联的游标定义为仅转发，因此光标无法定位在行集中。 请参阅**SQLSetStmtAttr**中SQL_ATTR_CURSOR_TYPE属性的说明。<br /><br /> *操作*参数SQL_UPDATE、SQL_DELETE或SQL_REFRESH，*并且 RowNumber*参数标识的行已被删除或未提取。<br /><br /> （DM）*行编号*参数为 0，*操作*参数SQL_POSITION。<br /><br /> **SQLSetPos**是在调用**SQLBulk 操作**后以及调用**SQLFetchScroll**或**SQLFetch**之前调用的。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|驱动程序或数据源不支持*操作*参数或*LockType*参数中请求的操作。|  
|HYT00|超时时间已到|查询超时期限在数据源返回结果集之前已过期。 超时期间通过**SQLSetStmtAttr**设置，*属性*为 SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*关联的驱动程序不支持该函数。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
  
## <a name="comments"></a>注释  
  
> [!CAUTION]
>  有关该语句的信息，指出**SQLSetPos**可以调用，以及它需要做什么才能与 ODBC *2.x*应用程序兼容，请参阅[块游标、可滚动光标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。  
  
## <a name="rownumber-argument"></a>行编号参数  
 *RowNumber*参数指定行集中要执行*操作*参数指定的操作的行数。 如果*RowNumber*为 0，则该操作将应用于行集中的每一行。 *行编号*必须是从 0 到行集中行数的值。  
  
> [!NOTE]  
>  在 C 语言中，数组基于 0，*行数*参数基于 1。 例如，要更新行集的第五行，应用程序会修改数组索引 4 处的行集缓冲区，但指定*行数*为 5。  
  
 所有操作都将光标放置在*行编号*指定的行上。 以下操作需要光标位置：  
  
-   定位更新和删除语句。  
  
-   调用**SQLGetData**。  
  
-   使用SQL_DELETE、SQL_REFRESH和SQL_UPDATE选项调用**SQLSetPos。**  
  
 例如，如果对**SQLSetPos**的调用的*RowNumber*为*Operation*2，并且操作为 SQL_DELETE，则光标将定位在行集的第二行上，并删除该行。 第二行的实现行状态数组中的条目（由SQL_ATTR_ROW_STATUS_PTR语句属性指向）更改为SQL_ROW_DELETED。  
  
 应用程序可以在调用**SQLSetPos**时指定游标位置。 通常，它调用**SQLSetPos**与SQL_POSITION或SQL_REFRESH操作，以定位游标之前执行定位的更新或删除语句或调用**SQLGetData**。  
  
## <a name="operation-argument"></a>操作参数  
 *操作*参数支持以下操作。 要确定数据源支持哪些选项，应用程序使用SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1信息类型（取决于游标的类型）调用**SQLGetInfo。**  
  
|*操作*<br /><br /> 参数|Operation|  
|------------------------------|---------------|  
|SQL_POSITION|驱动程序将光标定位在*行数指定的行*上。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 语句属性指向的行状态数组的内容将忽略SQL_POSITION*操作*。|  
|SQL_REFRESH|驱动程序将光标定位在*RowNumber*指定的行上，并在该行的行集缓冲区中刷新数据。 有关驱动程序如何返回行集缓冲区中的数据的详细信息，请参阅**SQLBindCol**中按行和按列绑定的说明。<br /><br /> 具有"SQL_REFRESH*操作*的**SQLSetPos**更新当前提取排集中行的状态和内容。 这包括刷新书签。 由于缓冲区中的数据将刷新但不重新提取，因此行集中的成员身份是固定的。 这与调用**SQLFetchScroll**执行的刷新不同，该刷新的*取取方向*为 SQL_FETCH_RELATIVE，*行号*等于 0，后者从结果集中重新提取行集，以便在驱动程序和游标支持这些操作时，可以显示添加的数据并删除已删除的数据。<br /><br /> 使用**SQLSetPos**成功刷新不会更改SQL_ROW_DELETED的行状态。 行集中已删除的行将继续标记为已删除，直到下一次提取。 如果游标支持打包（其中后续**SQLFetch**或**SQLFetchScroll**不会返回已删除的行），则行将在下一个提取时消失。<br /><br /> 使用**SQLSetPos**执行刷新时，不会显示添加的行。 此行为不同于**SQLFetchScroll，** 其*提取类型*为 SQL_FETCH_RELATIVE，*行号*等于 0，后者也会刷新当前行集，但如果游标支持这些操作，则将显示添加的记录或打包已删除的记录。<br /><br /> 使用**SQLSetPos**成功刷新将SQL_ROW_ADDED的行状态更改为SQL_ROW_SUCCESS（如果存在行状态数组）。<br /><br /> 使用**SQLSetPos**成功刷新会将SQL_ROW_UPDATED行状态更改为行的新状态（如果存在行状态数组）。<br /><br /> 如果行上的**SQLSetPos**操作中发生错误，则行状态设置为SQL_ROW_ERROR（如果存在行状态数组）。<br /><br /> 对于使用SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES的SQL_ATTR_CONCURRENCY语句属性打开的游标，使用**SQLSetPos**刷新可能会更新数据源用于检测行已更改的乐观并发值。 如果发生这种情况，每当从服务器刷新行集缓冲区时，用于确保游标并发的行版本或值都会更新。 对于刷新的每行，将发生这种情况。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 语句属性指向的行状态数组的内容将忽略SQL_REFRESH*操作*。|  
|SQL_UPDATE|驱动程序将光标定位在*RowNumber*指定的行上，并使用行集缓冲区中的值 **（SQLBindCol**中的*TargetValuePtr*参数）更新基础数据行。 它从长度/指标缓冲区 **（SQLBindCol**中的*StrLen_or_IndPtr*参数）检索数据的长度。 如果任何列的长度SQL_COLUMN_IGNORE，则不更新该列。 更新行后，驱动程序将行状态数组的相应元素更改为SQL_ROW_UPDATED或SQL_ROW_SUCCESS_WITH_INFO（如果存在行状态数组）。<br /><br /> 如果在包含重复列的游标上调用具有SQL_UPDATE*的"操作"* 参数的**SQLSetPos，** 则该行为是驱动程序定义的。 驱动程序可以返回驱动程序定义的 SQLSTATE，可以更新结果集中显示的第一列，或执行其他驱动程序定义的行为。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 语句属性指向的行操作数组可用于指示在当前行集中的行应在批量更新期间忽略。 有关详细信息，请参阅此函数引用后面的"状态和操作数组"。|  
|SQL_DELETE|驱动程序将光标定位在*行数指定的行*上，并删除基础数据行。 它将行状态数组的相应元素更改为SQL_ROW_DELETED。 删除行后，以下行无效：定位更新和删除语句、对**SQLGetData**的调用以及对**SQLSetPos** *的*调用，操作设置为除SQL_POSITION以外的任何内容。 对于支持打包的驱动程序，当从数据源检索新数据时，该行将从游标中删除。<br /><br /> 行是否保持可见取决于游标类型。 例如，已删除的行对静态和键集驱动的游标可见，但动态游标不可见。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 语句属性指向的行操作数组可用于指示在当前行集中的行应在批量删除期间忽略。 有关详细信息，请参阅此函数引用后面的"状态和操作数组"。|  
  
## <a name="locktype-argument"></a>锁类型参数  
 *LockType*参数为应用程序提供了一种控制并发的方法。 在大多数情况下，支持并发级别和事务的数据源将仅支持*LockType*参数的SQL_LOCK_NO_CHANGE值。 *LockType*参数通常仅用于基于文件的支持。  
  
 *LockType*参数指定执行**SQLSetPos**后行的锁状态。 如果驱动程序无法锁定行以执行请求的操作或满足*LockType*参数，它将返回SQL_ERROR和 SQLSTATE 42000（语法错误或访问冲突）。  
  
 尽管*LockType*参数是为单个语句指定的，但锁对连接上的所有语句都授予相同的权限。 特别是，连接上的一个语句获取的锁可以通过同一连接上的不同语句解锁。  
  
 通过**SQLSetPos**锁定的行将保持锁定状态，直到应用程序为*LockType*设置为SQL_LOCK_UNLOCK的行调用**SQLSetPos，** 或者直到应用程序使用SQL_CLOSE选项调用**SQLFreeHandle**或**SQLFreeStmt。** 对于支持事务的驱动程序，当应用程序调用**SQLEndTran**提交或回滚连接上的事务时（如果游标在提交或回滚事务时关闭，如**SQLGetInfo**返回SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR信息类型所示，通过**SQLSetPos**锁定的行将解锁。  
  
 *LockType*参数支持以下类型的锁。 要确定数据源支持哪些锁，应用程序使用SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1信息类型（取决于游标的类型）调用**SQLGetInfo。**  
  
|*锁类型*参数|锁类型|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|驱动程序或数据源可确保该行处于与调用**SQLSetPos**之前相同的锁定或解锁状态。 *LockType*的此值允许不支持显式行级锁定的数据源使用当前并发和事务隔离级别所需的任何锁定。|  
|SQL_LOCK_EXCLUSIVE|驱动程序或数据源专门锁定行。 不能使用不同连接或不同应用程序中的语句来获取行上的任何锁。|  
|SQL_LOCK_UNLOCK|驱动程序或数据源解锁该行。|  
  
 如果驱动程序支持SQL_LOCK_EXCLUSIVE但不支持SQL_LOCK_UNLOCK，则锁定的行将保持锁定状态，直到发生上一段中描述的函数调用之一。  
  
 如果驱动程序支持SQL_LOCK_EXCLUSIVE但不支持SQL_LOCK_UNLOCK，则锁定的行将保持锁定状态，直到应用程序调用**SQLFreeHandle**进行语句或**SQLFreeStmt** SQL_CLOSE 选项。 如果驱动程序支持事务并在提交或回滚事务时关闭游标，则应用程序将调用**SQLEndTran**。  
  
 对于**SQLSetPos**中的更新和删除操作，应用程序使用*LockType*参数，如下所示：  
  
-   为了保证行在检索后不会更改，应用程序调用**SQLSetPos，***操作*设置为*SQL_REFRESH，LockType*设置为SQL_LOCK_EXCLUSIVE。  
  
-   如果应用程序将*LockType*设置为SQL_LOCK_NO_CHANGE，则驱动程序保证仅当为SQL_ATTR_CONCURRENCY语句属性指定的应用程序SQL_CONCUR_LOCK时，更新或删除操作才会成功。  
  
-   如果应用程序为SQL_ATTR_CONCURRENCY语句属性指定SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES，则驱动程序将比较行版本或值，如果行自应用程序获取行以来已更改，则拒绝该操作。  
  
-   如果应用程序为SQL_ATTR_CONCURRENCY语句属性指定SQL_CONCUR_READ_ONLY，则驱动程序将拒绝任何更新或删除操作。  
  
 有关SQL_ATTR_CONCURRENCY语句属性的详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="status-and-operation-arrays"></a>状态和操作数组  
 调用**SQLSetPos**时使用以下状态和操作数组：  
  
-   行状态数组（如 IRD 中的SQL_DESC_ARRAY_STATUS_PTR字段和SQL_ATTR_ROW_STATUS_ARRAY语句属性）包含行集中每行数据的状态值。 调用**SQLFetch、SQLFetchScroll、SQLBulk****操作**或**SQLSetPos**后，驱动程序将设置此数组中的状态值。 **SQLFetch** 此数组由SQL_ATTR_ROW_STATUS_PTR语句属性指向。  
  
-   行操作数组（如 ARD 中的SQL_DESC_ARRAY_STATUS_PTR字段和SQL_ATTR_ROW_OPERATION_ARRAY语句属性）包含行集中每行的值，指示是忽略还是执行批量操作对**SQLSetPos**的调用。 数组中的每个元素都设置为SQL_ROW_PROCEED（默认值）或SQL_ROW_IGNORE。 此数组由SQL_ATTR_ROW_OPERATION_PTR语句属性指向。  
  
 状态和操作数组中的元素数必须等于行集中的行数（由SQL_ATTR_ROW_ARRAY_SIZE语句属性定义）。  
  
 有关行状态数组的信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。 有关行操作数组的信息，请参阅本节后面的"忽略批量操作中的行"。  
  
## <a name="using-sqlsetpos"></a>使用 SQLSetPos  
 在应用程序调用**SQLSetPos**之前，它必须执行以下步骤序列：  
  
1.  如果应用程序将调用**SQLSetPos，***操作*设置为SQL_UPDATE，请为每个列调用**SQLBindCol（** 或**SQLSetDescRec），** 以指定其数据类型，并绑定列的数据和长度的缓冲区。  
  
2.  如果应用程序将调用**SQLSetPos，***操作*设置为SQL_DELETE或SQL_UPDATE，则调用**SQLColAttribute**以确保要删除或更新的列是可更新的。  
  
3.  调用**SQLExecDirect、SQLExecute**或目录函数以创建结果集。 **SQLExecute**  
  
4.  调用**SQLFetch**或**SQLFetchScroll**来检索数据。  
  
 有关使用**SQLSetPos**的详细信息，请参阅[使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
## <a name="deleting-data-using-sqlsetpos"></a>使用 SQLSetPos 删除数据  
 要使用**SQLSetPos**删除数据，应用程序调用**SQLSetPos，***其中行号*设置为要删除的行数，*操作*设置为SQL_DELETE。  
  
 删除数据后，驱动程序将相应行的实现行状态数组中的值更改为SQL_ROW_DELETED（或SQL_ROW_ERROR）。  
  
## <a name="updating-data-using-sqlsetpos"></a>使用 SQLSetPos 更新数据  
 应用程序可以在绑定的数据缓冲区中传递列的值，也可以通过对**SQLPutData**的一个或多个调用来传递列的值。 其数据随**SQLPutData**传递的列称为*执行时的数据**列*。 它们通常用于发送SQL_LONGVARBINARY和SQL_LONGVARCHAR列的数据，并可以与其他列混合。  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>要使用 SQLSetPos 更新数据，应用程序：  
  
1.  在数据中放置值，长度/指标缓冲区与**SQLBindCol**绑定 ：  
  
    -   对于普通列，应用程序将新列值放在*\*TargetValuePtr*缓冲区中，并将该值的长度放在*\*StrLen_or_IndPtr*缓冲区中。 如果不应更新该行，应用程序将SQL_ROW_IGNORE放在该行操作数组的该行元素中。  
  
    -   对于执行时的数据列，应用程序在*\*TargetValuePtr*缓冲区中放置应用程序定义的值（如列号）。 该值以后可用于标识列。  
  
         应用程序将SQL_LEN_DATA_AT_EXEC（*长度*）宏的结果放在 +*StrLen_or_IndPtr*缓冲区中。 如果列的 SQL 数据类型SQL_LONGVARBINARY、SQL_LONGVARCHAR 或长数据源特定的数据类型，并且驱动程序返回**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN信息类型的"Y"，*则长度*是要为参数发送的数据字节数;否则，它必须是非负值，并且被忽略。  
  
2.  调用**SQLSetPos，***将操作*参数设置为SQL_UPDATE更新数据行。  
  
    -   如果没有执行时的数据列，则该过程已完成。  
  
    -   如果存在任何执行时的数据列，则函数将返回SQL_NEED_DATA并继续执行步骤 3。  
  
3.  调用**SQLParamData**以检索要处理的第一个执行数据列的目标*\*值Ptr*缓冲区的地址。 **SQLParamData**返回SQL_NEED_DATA。 应用程序从*\*TargetValuePtr*缓冲区检索应用程序定义的值。  
  
    > [!NOTE]  
    >  尽管执行时的数据参数与执行时的数据列类似，但**SQLParamData**返回的值因每个列而异。  
  
    > [!NOTE]  
    >  执行时的数据参数是 SQL 语句中的参数，当使用**SQLExecDirect**或**SQLExecute**执行语句时，将随**SQLPutData**一起发送数据。 它们与**SQLBind 参数**绑定，或者通过使用**SQLSetDescRec**设置描述符。 **SQLParamData**返回的值是一个 32 位值，在*参数值Ptr*参数中传递给**SQLBind参数**。  
  
    > [!NOTE]  
    >  执行时的数据列是行集中的列 **，当使用** **SQLSetPos**更新行时，将为此发送数据。 它们与**SQLBindCol**绑定。 **SQLParamData**返回的值是正在处理的 @*TargetValuePtr*缓冲区中的行的地址。  
  
4.  调用**SQLPutData**一次或多次以发送列的数据。 如果在**SQLPutData**中指定的*\*TargetValuePtr*缓冲区中无法返回所有数据值，则需要多个调用。仅当将字符 C 数据发送到具有字符、二进制或数据源特定数据类型的列或将二进制 C 数据发送到具有字符、二进制或数据源特定数据类型的列时，才允许对同一列的**SQLPutData**进行多次调用。  
  
5.  再次调用**SQLParamData**以发出已为该列发送所有数据的信号。  
  
    -   如果有更多的执行数据列 **，SQLParamData**将返回要处理的下一个执行数据列的SQL_NEED_DATA和目标*ValuePtr*缓冲区的地址。 应用程序重复步骤 4 和 5。  
  
    -   如果没有更多的数据执行列，该过程将完成。 如果语句成功执行 **，SQLParamData**将返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO;如果执行失败，它将返回SQL_ERROR。 此时 **，SQLParamData**可以返回**SQLSetPos**可以返回的任何 SQLSTATE。  
  
 如果数据已更新，驱动程序将相应行的实现行状态数组中的值更改为SQL_ROW_UPDATED。  
  
 如果操作被取消或在**SQLParamData**或**SQLPutData**中发生错误，则**在 SQLSetPos**返回SQL_NEED_DATA并在为执行时的所有数据发送数据之前，应用程序只能调用 SQLCancel、SQLGetDiagField、SQLGetDiagrec、SQLGet**函数****、SQLParamData**或**SQLPutData**的语句或与语句关联的连接。 **SQLCancel** **SQLGetDiagField** **SQLGetDiagRec** 如果它调用语句或与 语句关联的连接的任何其他函数，则函数将返回SQL_ERROR和 SQLSTATE HY010（函数序列错误）。  
  
 如果应用程序调用**SQLCancel，** 而驱动程序仍然需要执行时的数据列，则驱动程序将取消该操作。 然后，应用程序可以再次调用**SQLSetPos;** 取消不会影响光标状态或当前游标位置。  
  
 当与游标关联的查询规范的 SELECT 列表包含对同一列的多个引用时，无论生成错误还是驱动程序忽略重复的引用并执行请求的操作都是驱动程序定义的。  
  
## <a name="performing-bulk-operations"></a>执行批量操作  
 如果*RowNumber*参数为 0，则驱动程序将执行行集中的每一行的 *"操作*"参数中指定的操作，这些行在行操作数组中的值为 SQL_ROW_PROCEED，该行位于SQL_ATTR_ROW_OPERATION_PTR语句属性指向的行操作数组中。 这是 *"**操作*"参数（SQL_DELETE、SQL_REFRESH 或SQL_UPDATE）的有效值，但不是SQL_POSITION。 操作SQL_POSITION和*行号*等于 0*的***SQLSetPos**将返回 SQLSTATE HY109（无效游标位置）。  
  
 如果发生与整个行集相关的错误（如 SQLSTATE HYT00（超时已过期），驱动程序将返回SQL_ERROR和相应的 SQLSTATE。 行集缓冲区的内容未定义，光标位置保持不变。  
  
 如果发生与单个行相关的错误，驱动程序：  
  
-   将行状态数组中SQL_ATTR_ROW_STATUS_PTR语句属性指向SQL_ROW_ERROR中行的元素。  
  
-   为错误队列中的错误过帐一个或多个附加 SQLSTATE，并在诊断数据结构中设置SQL_DIAG_ROW_NUMBER字段。  
  
 处理错误或警告后，如果驱动程序完成行集中其余行的操作，它将返回SQL_SUCCESS_WITH_INFO。 因此，对于返回错误的每行，错误队列包含零个或多个其他 SQLSTATE。 如果驱动程序在处理了错误或警告后停止操作，则返回SQL_ERROR。  
  
 如果驱动程序返回任何警告，如 SQLSTATE 01004（数据截断），它将返回应用于整个行集或行集中的未知行的警告，然后再返回适用于特定行的错误信息。 它返回特定行的警告以及有关这些行的任何其他错误信息。  
  
 如果*RowNumber*等于 0，*并且操作*SQL_UPDATE、SQL_REFRESH或SQL_DELETE，**则 SQLSetPos**操作的行数由SQL_ATTR_ROWS_FETCHED_PTR语句属性指出。  
  
 如果*RowNumber*等于 0，*并且操作*SQL_DELETE、SQL_REFRESH 或SQL_UPDATE，则操作后的当前行与操作前的当前行相同。  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>忽略批量操作中的行  
 行操作数组可用于指示在当前行集中的行应在使用**SQLSetPos**进行批量操作期间忽略。 要指示驱动程序在批量操作期间忽略一个或多个行，应用程序应执行以下步骤：  
  
1.  调用**SQLSetStmtAttr**将SQL_ATTR_ROW_OPERATION_PTR语句属性设置为指向 SQLUSMALLINT 数组。 此字段也可以通过调用**SQLSetDescField**来设置 ARD 的SQL_DESC_ARRAY_STATUS_PTR标头字段，该字段要求应用程序获取描述符句柄。  
  
2.  将行操作数组的每个元素设置为两个值之一：  
  
    -   SQL_ROW_IGNORE，以指示为批量操作排除该行。  
  
    -   SQL_ROW_PROCEED，以指示该行包含在批量操作中。 （这是默认值。）  
  
3.  调用**SQLSetPos**以执行批量操作。  
  
 以下规则适用于行操作数组：  
  
-   SQL_ROW_IGNORE和SQL_ROW_PROCEED仅影响使用**SQLSetPos**执行SQL_DELETE或SQL_UPDATE*的批量操作*。 它们不会影响对**SQLSetPos***的调用*，操作SQL_REFRESH或SQL_POSITION。  
  
-   默认情况下，指针设置为 null。  
  
-   如果指针为空，则所有行都将更新，就像所有元素都设置为SQL_ROW_PROCEED一样。  
  
-   将元素设置为SQL_ROW_PROCEED并不保证该操作将发生在该特定行上。 例如，如果行集中的某个行具有SQL_ROW_ERROR状态，则无论应用程序是否指定SQL_ROW_PROCEED，驱动程序可能无法更新该行。 应用程序必须始终检查行状态数组以查看操作是否成功。  
  
-   SQL_ROW_PROCEED在头文件中定义为 0。 应用程序可以将行操作数组初始化为 0，以便处理所有行。  
  
-   如果行操作数组中的元素编号"n"设置为SQL_ROW_IGNORE，并且调用**SQLSetPos**执行批量更新或删除操作，则行集中的第 n 行在调用**SQLSetPos**后保持不变。  
  
-   应用程序应自动将只读列设置为SQL_ROW_IGNORE。  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>忽略批量操作中的列  
 为了避免尝试更新一个或多个只读列而生成不必要的处理诊断，应用程序可以将绑定长度/指示器缓冲区中的值设置为SQL_COLUMN_IGNORE。 有关详细信息，请参阅[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序允许用户浏览 ORDERS 表并更新订单状态。 游标由键集驱动，行集大小为 20，并使用比较行版本的乐观并发控件。 提取每个行集后，应用程序将打印它，并允许用户选择和更新订单的状态。 应用程序使用**SQLSetPos**将光标定位到所选行上，并执行行的位置更新。 （为了清楚起见，省略了错误处理。  
  
```cpp  
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
  
 有关更多示例，请参阅[使用 SQLSetPos 在行集中](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)以及更新行。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|执行与块光标位置无关的批量操作|[SQLBulkOperations 函数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|获取数据块或滚动浏览结果集|[SQLFetchScroll Function（SQLFetchScroll 函数）](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|获取描述符的单个字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取描述符的多个字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置描述符的单个字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置描述符的多个字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
