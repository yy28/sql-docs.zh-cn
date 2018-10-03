---
title: SQLSetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetStmtAttr function
ms.assetid: 799c80fd-c561-4912-8562-9229076dfd19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edd96f9927a5fe698dd47489beffc738b5456708
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208510"
---
# <a name="sqlsetstmtattr"></a>SQLSetStmtAttr
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序不支持混合（键集/动态）游标模型。 如果将该值设置为非 0 值，尝试使用 SQL_ATTR_KEYSET_SIZE 设置键集大小将失败。  
  
 应用程序将所有语句，若要声明多个返回的行上设置 SQL_ATTR_ROW_ARRAY_SIZE **SQLFetch**或[SQLFetchScroll](sqlfetchscroll.md)函数调用。 在指示服务器游标的语句中，驱动程序使用 SQL_ATTR_ROW_ARRAY_SIZE 确定服务器为满足游标的提取请求而生成的行块的大小。 在动态游标的块大小内，如果事务隔离级别足以确保对已提交事务的可重复读取，行的成员身份和顺序则是固定的。 游标在该值指示的块之外完全处于动态状态。 服务器游标块大小完全处于动态状态，并且可以在提取过程中的任一点更改。  
  
## <a name="sqlsetstmtattr-and-table-valued-parameters"></a>SQLSetStmtAttr 和表值参数  
 SQLSetStmtAttr 可以用于访问表值参数列的描述符字段之前在应用程序参数描述符 (APD) 中设置 SQL_SOPT_SS_PARAM_FOCUS。  
  
 如果尝试将 SQL_SOPT_SS_PARAM_FOCUS 设置为的第几个参数，它是不是表值参数、 SQLSetStmtAttr 返回 SQL_ERROR 并诊断记录创建具有 SQLSTATE = HY024 和消息"属性值无效"。 返回 SQL_ERROR 时，不更改 SQL_SOPT_SS_PARAM_FOCUS。  
  
 将 SQL_SOPT_SS_PARAM_FOCUS 设置为 0 可以恢复对参数的描述符记录的访问权限。  
  
 SQLSetStmtAttr 还用于设置 SQL_SOPT_SS_NAME_SCOPE。 有关详细信息，请参阅本主题后面的 SQL_SOPT_SS_NAME_SCOPE 部分。  
  
 有关详细信息，请参阅[准备语句的表值参数元数据](../native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetstmtattr-support-for-sparse-columns"></a>SQLSetStmtAttr 对稀疏列的支持  
 SQLSetStmtAttr 可以用于设置 SQL_SOPT_SS_NAME_SCOPE。 详细信息，请参阅后面本主题的 SQL_SOPT_SS_NAME_SCOPE 部分。有关稀疏列的详细信息，请参阅[稀疏列支持&#40;ODBC&#41;](../native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="statement-attributes"></a>语句属性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序还支持以下特定于驱动程序的语句属性。  
  
### <a name="sqlsoptsscursoroptions"></a>SQL_SOPT_SS_CURSOR_OPTIONS  
 SQL_SOPT_SS_CURSOR 属性指定驱动程序是否将在游标上使用特定于驱动程序的性能选项。 [SQLGetData](sqlgetdata.md)设置这些选项时，不允许。 默认设置为 SQL_CO_OFF。 *ValuePtr*的值为类型为 SQLLEN。  
  
|*ValuePtr*值|Description|  
|----------------------|-----------------|  
|SQL_CO_OFF|默认值。 禁用快速只进、 只读游标和自动提取，启用**SQLGetData**对只进、 只读游标。 将 SQL_SOPT_SS_CURSOR_OPTIONS 设置为 SQL_CO_OFF 时，游标类型将不会发生更改。 也就是说，快速只进游标将保持为快速只进游标。 若要更改的游标类型，该应用程序必须现在设置不同的游标类型使用`SQLSetStmtAttr`/SQL_ATTR_CURSOR_TYPE。|  
|SQL_CO_FFO|启用快速只进、 只读游标，禁用**SQLGetData**对只进、 只读游标。|  
|SQL_CO_AF|针对任意游标类型启用自动提取选项。 当此选项设置为语句句柄**SQLExecute**或**SQLExecDirect**将生成隐式**SQLFetchScroll** (SQL_FIRST)。 此时将打开游标，并在与服务器的单个往返中返回第一批行。|  
|SQL_CO_FFO_AF|使用自动提取选项启用快速只进游标。 它与同时指定 SQL_CO_AF 和 SQL_CO_FFO 的效果相同。|  
  
 当设置这些选项时，服务器将在检测到已提取最后一行时自动关闭游标。 应用程序，仍必须调用[SQLFreeStmt](sqlfreestmt.md) (SQL_CLOSE) 或[SQLCloseCursor](sqlclosecursor.md)，但该驱动程序不必向服务器发送关闭通知。  
  
 如果选择列表包含**文本**， **ntext**，或**图像**列中，快速只进游标将转换为动态游标和**SQLGetData**允许。  
  
### <a name="sqlsoptssdeferprepare"></a>SQL_SOPT_SS_DEFER_PREPARE  
 SQL_SOPT_SS_DEFER_PREPARE 属性确定是立即准备还是延迟，直到该语句**SQLExecute**， [SQLDescribeCol](sqldescribecol.md)或[SQLDescribeParam](sqldescribeparam.md)执行。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 和早期版本中，将忽略此属性（没有延迟的准备）。 *ValuePtr*的值为类型为 SQLLEN。  
  
|*ValuePtr*值|Description|  
|----------------------|-----------------|  
|SQL_DP_ON|默认值。 在调用[SQLPrepare 函数](http://go.microsoft.com/fwlink/?LinkId=59360)，将延迟语句准备，直到**SQLExecute**称为或元属性操作 (**SQLDescribeCol**或**SQLDescribeParam**) 执行。|  
|SQL_DP_OFF|准备的语句就立即**SQLPrepare**执行。|  
  
### <a name="sqlsoptssregionalize"></a>SQL_SOPT_SS_REGIONALIZE  
 SQL_SOPT_SS_REGIONALIZE 属性用于确定语句级别的数据转换。 该属性使驱动程序在将日期、时间和货币值转换为字符串时遵循客户端区域设置。 该转换仅针对从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机数据类型到字符串的转换。  
  
 *ValuePtr*的值为类型为 SQLLEN。  
  
|*ValuePtr*值|Description|  
|----------------------|-----------------|  
|SQL_RE_OFF|默认值。 驱动程序不能将日期、时间和货币数据转换为使用客户端区域设置的字符串。|  
|SQL_RE_ON|驱动程序在将日期、时间和货币数据转换为字符串数据时使用客户端区域设置。|  
  
 区域转换设置应用于货币、数字、日期和时间数据类型。 转换设置仅适用于将货币、数字、日期或时间值转换为字符串的输出转换。  
  
> [!NOTE]  
>  当启用语句选项 SQL_SOPT_SS_REGIONALIZE 时，驱动程序使用当前用户的区域设置注册表设置。 该驱动程序不会遵循当前线程的区域设置，如果应用程序将其设置的例如，调用**SetThreadLocale**。  
  
 改变数据源的区域行为可能导致应用程序失败。 对于分析日期字符串并期望日期字符串按 ODBC 定义的方式显示的应用程序，更改该值可能会对它们产生负面影响。  
  
### <a name="sqlsoptsstextptrlogging"></a>SQL_SOPT_SS_TEXTPTR_LOGGING  
 SQL_SOPT_SS_TEXTPTR_LOGGING 属性用于切换的包含的列上的操作的日志记录**文本**或**映像**数据。 *ValuePtr*的值为类型为 SQLLEN。  
  
|*ValuePtr*值|Description|  
|----------------------|-----------------|  
|SQL_TL_OFF|禁用执行的操作的日志记录**文本**并**映像**数据。|  
|SQL_TL_ON|默认值。 启用日志记录执行的操作**文本**并**映像**数据。|  
  
### <a name="sqlsoptsshiddencolumns"></a>SQL_SOPT_SS_HIDDEN_COLUMNS  
 SQL_SOPT_SS_HIDDEN_COLUMNS 属性在结果集中公开隐含在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT FOR BROWSE 语句中的列。 默认情况下，驱动程序不公开这些列。 *ValuePtr*的值为类型为 SQLLEN。  
  
|*ValuePtr*值|Description|  
|----------------------|-----------------|  
|SQL_HC_OFF|默认值。 结果集中不显示 FOR BROWSE 列。|  
|SQL_HC_ON|公开 FOR BROWSE 列。|  
  
### <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 属性返回查询通知请求的消息文本。  
  
### <a name="sqlsoptssquerynotificationoptions"></a>SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
 SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS 属性指定用于查询通知请求的选项。 这些选项是在采用 `name=value` 语法的字符串中指定的，如下所示。 应用程序负责创建服务并从队列中读取通知。  
  
 查询通知选项字符串的语法为：  
  
 `service=<service-name>[;(local database=<database>|broker instance=<broker instance>)]`  
  
 例如：  
  
 `service=mySSBService;local database=mydb`  
  
### <a name="sqlsoptssquerynotificationtimeout"></a>SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
 SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT 属性指定查询通知保持活动状态的秒数。 默认值为 432000 秒（5 天）。 *ValuePtr*的值为类型为 SQLLEN。  
  
### <a name="sqlsoptssparamfocus"></a>SQL_SOPT_SS_PARAM_FOCUS  
 SQL_SOPT_SS_PARAM_FOCUS 属性指定后续 SQLBindParameter、 SQLGetDescField、 SQLSetDescField、 SQLGetDescRec，焦点和 SQLSetDescRec 调用。  
  
 SQL_SOPT_SS_PARAM_FOCUS 的类型为 SQLULEN。  
  
 默认值为 0，表示这些调用将对与 SQL 语句中的参数标记相对应的参数进行寻址。 当设置为表值参数的参数编号时，这些调用将对该表值参数的列进行寻址。 当设置的值不是表值参数的参数编号时，这些调用将返回错误 IM020：“参数焦点未引用表值参数”。  
  
### <a name="sqlsoptssnamescope"></a>SQL_SOPT_SS_NAME_SCOPE  
 SQL_SOPT_SS_NAME_SCOPE 属性指定后续目录函数调用的名称范围。 SQLColumns 返回的结果集取决于 SQL_SOPT_SS_NAME_SCOPE 的设置。  
  
 SQL_SOPT_SS_NAME_SCOPE 的类型为 SQLULEN。  
  
|*ValuePtr*值|Description|  
|----------------------|-----------------|  
|SQL_SS_NAME_SCOPE_TABLE|默认值。<br /><br /> 当使用表值参数时，指示应返回实际表的元数据。<br /><br /> SQLColumns 使用稀疏列功能时，将返回不是成员的稀疏的列`column_set`。|  
|SQL_SS_NAME_SCOPE_TABLE_TYPE|指示应用程序需要表类型的元数据，而不是实际表（目录函数应返回表类型的元数据）。 然后，应用程序将传递作为表值参数的 TYPE_NAME *TableName*参数。|  
|SQL_SS_NAME_SCOPE_EXTENDED|SQLColumns 而不考虑使用稀疏列功能时，返回的所有列，`column_set`成员身份。|  
|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET|SQLColumns 使用稀疏列功能时，返回成员的稀疏的列`column_set`。|  
|SQL_SS_NAME_SCOPE_DEFAULT|等同于 SQL_SS_NAME_SCOPE_TABLE。|  
  
 与使用 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME *CatalogName*和*SchemaName*参数，分别以标识的目录和表值参数的架构。 在应用程序检索完表值参数的元数据之后，该应用程序必须将 SQL_SOPT_SS_NAME_SCOPE 设置回原来的默认值 SQL_SS_NAME_SCOPE_TABLE。  
  
 将 SQL_SOPT_SS_NAME_SCOPE 设置为 SQL_SS_NAME_SCOPE_TABLE 时，对链接服务器的查询将失败。 SQLColumns 或 SQLPrimaryKeys 对包含服务器组件的目录的调用将失败。  
  
 如果尝试将 SQL_SOPT_SS_NAME_SCOPE 设置为无效值，则返回 SQL_ERROR，并生成具有 SQLSTATE HY024 和消息“属性值无效”的诊断记录。  
  
 如果的目录函数则当 SQL_SOPT_SS_NAME_SCOPE 具有值而不调用 SQLTables、 SQLColumns 或 SQLPrimaryKeys SQL_SS_NAME_SCOPE_TABLE，将返回 SQL_ERROR。 生成具有 SQLSTATE HY010 和消息“函数序列错误(SQL_SOPT_SS_NAME_SCOPE 未设置为 SQL_SS_NAME_SCOPE_TABLE)”的诊断记录。  
  
## <a name="see-also"></a>请参阅  
 [SQLGetStmtAttr 函数](http://go.microsoft.com/fwlink/?LinkId=59355)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
