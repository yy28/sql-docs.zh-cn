---
title: SQLPrepare 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f4f752416fd704d3976728eabbe6a8b9d00bd37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlprepare-function"></a>SQLPrepare 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLPrepare**做好执行准备一个 SQL 字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *StatementText*  
 [输入]SQL 文本字符串。  
  
 *TextLength*  
 [输入]长度 **StatementText*以字符为单位。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLPrepare**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLPrepare**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02 的警告|选项值已更改|指定的语句属性由于实现工作条件无效，因此暂时替换类似的值。 (**SQLGetStmtAttr**可以调用以确定暂时被替换的值是什么。)替换值可用于*StatementHandle*直到关闭游标。 可以更改这些语句属性包括： SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|21S01|插入值列表与列列表不匹配|\**StatementText*包含**插入**语句，并要插入的值的数目与派生表的等级不匹配。|  
|21S02|派生表的等级与列列表不匹配|\**StatementText*包含**CREATE VIEW**语句和的名称指定的数量并不与查询规范定义的派生表的相同程度。|  
|22018|转换指定的的无效字符值|**StatementText*包含 SQL 语句包含的文本或参数，而与关联的表列的数据类型不兼容的值。|  
|22019|无效的转义字符|自变量*StatementText*包含**如**谓词和**转义**中**其中**子句和转义的长度之后的字符**转义**未等于 1。|  
|22025|无效的转义序列|自变量*StatementText*包含"**如***模式值***转义***转义符*"中**其中**子句，而后面模式值中的转义字符的字符为"%"和"_"都不。|  
|24000|无效的游标状态|(DM) 上打开游标的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**已调用一样。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**不调用一样。|  
|34000|无效的临时表名称|\**StatementText*包含定位**删除**或定位**更新**，并正准备的语句所引用的游标未打开。|  
|3D000|无效的目录名称|中指定的目录名称*StatementText*无效。|  
|3F000|无效的架构名称|中指定的架构名称*StatementText*无效。|  
|42000|语法错误或访问冲突|\**StatementText*包含 SQL 语句未 preparable 或包含的语法错误。<br /><br /> **StatementText*包含为其用户没有所需的权限的语句。|  
|42S01|基表或视图已存在|\**StatementText*包含**CREATE TABLE**或**CREATE VIEW**语句和表名或视图指定名称已经存在。|  
|42S02|基表或视图找不到|\**StatementText*包含**DROP TABLE**或**DROP VIEW**语句指定的表名或视图名称不存在。<br /><br /> \**StatementText*包含**ALTER TABLE**语句，并指定的表名不存在。<br /><br /> \**StatementText*包含**CREATE VIEW**语句和表名或视图不存在查询规范所定义的名称。<br /><br /> \**StatementText*包含**CREATE INDEX**语句，并指定的表名不存在。<br /><br /> \**StatementText*包含**授予**或**撤消**语句指定的表名或视图名称不存在。<br /><br /> \**StatementText*包含**选择**语句和指定的表名或视图名称不存在。<br /><br /> \**StatementText*包含**删除**，**插入**，或**更新**语句，并指定的表名不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**语句，并指定约束 （引用的表而不正在创建） 中的表不存在。|  
|42S11|已存在的索引|\**StatementText*包含**CREATE INDEX**语句，并指定的索引名称已存在。|  
|42S12|找不到索引|\**StatementText*包含**DROP INDEX**语句，并指定的索引名称不存在。|  
|42S21|已存在的列|\**StatementText*包含**ALTER TABLE**语句，并在指定的列**添加**子句不是唯一的或标识基表中的现有列。|  
|42S22|找不到列|\**StatementText*包含**CREATE INDEX**语句，和一个或多个指定列列表中的名称不存在的列。<br /><br /> \**StatementText*包含**授予**或**撤消**语句，并指定的列名称不存在。<br /><br /> \**StatementText*包含**选择**，**删除**，**插入**，或**更新**语句，并指定的列名称不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**语句，并指定约束 （引用的表而不正在创建） 中的列不存在。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*StatementHandle*。 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数已在上再次*StatementHandle*。<br /><br /> 已调用函数，和它之前完成执行， **SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自中的不同线程多线程应用程序。|  
|HY009|不允许使用 null 指针|(DM) *StatementText*是空指针。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLPrepare**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*并返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 以异步方式执行的函数 （而不是此的一个） 曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 自变量*TextLength*小于或等于为 0，但与 sql_nts 以不相等。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|并发设置的定义的游标类型无效。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性已设置为 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 语句属性被设置为该驱动程序不支持书签游标类型。|  
|HYT00|超时时间已到|超时期限过期之前的数据源返回了结果集。 通过设置的超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*StatementHandle*不支持该函数。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 应用程序调用**SQLPrepare**将 SQL 语句发送到准备的数据源。 准备好的执行有关的详细信息，请参阅[已准备的执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。 应用程序可以包含一个或多个参数标记中的 SQL 语句。 若要包括参数标记，应用程序将嵌入问号 （？） 到 SQL 字符串中相应的位置。 有关参数的信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
> [!NOTE]  
>  如果应用程序使用**SQLPrepare**准备和**SQLExecute**提交**提交**或**回滚**语句，它不是DBMS 产品之间互操作。 若要提交或回滚事务，调用**SQLEndTran**。  
  
 该驱动程序可以修改语句以使用 SQL 数据源使用的表单，然后将它提交到准备的数据源。 具体而言，该驱动程序修改用于定义某些功能的 SQL 语法的转义序列。 (有关 SQL 语句语法的说明，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)和[附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。)对于该驱动程序，语句句柄是类似于语句标识符中的嵌入式 SQL 代码。 如果数据源支持语句标识符，该驱动程序可以向数据源发送语句标识符和参数值。  
  
 准备语句后，应用程序将使用语句句柄来引用到更高版本的函数调用中的语句。 可以通过调用重新执行已准备的语句与语句句柄关联**SQLExecute**直到应用程序释放通过调用语句**SQLFreeStmt** SQL_DROP 选项或到在调用中使用的语句句柄**SQLPrepare**， **SQLExecDirect**，或一个目录函数 (**SQLColumns**， **SQLTables**，依次类推)。 一旦应用程序准备语句，它可以请求有关格式的结果集的信息。 对于某些实现，调用**SQLDescribeCol**或**SQLDescribeParam**后**SQLPrepare**可能不是与后调用函数一样有效**SQLExecute**或**SQLExecDirect**。  
  
 某些驱动程序不能返回语法错误或访问冲突，当应用程序调用**SQLPrepare**。 驱动程序可以处理语法错误，以及访问冲突，仅语法错误或既不语法错误也不访问冲突。 因此，应用程序必须能够处理这些情况，当调用后续相关函数如**SQLNumResultCols**， **SQLDescribeCol**， **SQLColAttribute**，和**SQLExecute**。  
  
 具体取决于驱动程序和数据源的功能，如果 （如果所有参数都具有已都绑定） 准备该语句，参数信息 （如数据类型） 可能会处于选中状态，或者 （如果尚未都绑定所有参数） 的执行时。 最大互操作性，应用程序应取消绑定应用于旧的 SQL 语句，在准备新的 SQL 语句在一条语句之前的所有参数。 这可以防止由于旧正在应用于新的语句的参数信息的错误。  
  
> [!IMPORTANT]  
>  提交事务，通过显式调用**SQLEndTran**或通过在自动模式下工作，就可能导致要删除的所有语句，在连接上的访问计划的数据源。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 信息类型[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)和[游标和准备的语句上的事务影响](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)，和[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配的语句句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|绑定到结果集中的列的缓冲区|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|绑定到参数的缓冲区|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行提交或回滚操作|[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回由语句影响的行数|[SQLRowCount 函数](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
