---
title: SQLPrepare 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e4c15cfe0d82fc4b68115c029334fa7d3ec7410
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63186221"
---
# <a name="sqlprepare-function"></a>SQLPrepare 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLPrepare**做好执行 SQL 字符串。  
  
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
 当**SQLPrepare**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLPrepare** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|指定的语句属性实现运行情况，由于无效，因此已暂时替换一个相近的值。 (**SQLGetStmtAttr**可以调用以确定暂时被替换的值是什么。)替换值是否为有效*StatementHandle*直到关闭游标。 可以更改的语句属性有：SQL_ATTR_CONCURRENCY 设置 SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|21S01|插入值列表与列列表不匹配|\**StatementText*包含**插入**语句和要插入的值的数目不匹配的派生表的程度。|  
|21S02|派生表等级与列列表不匹配|\**StatementText*包含**CREATE VIEW**语句，并指定名称的数量不是作为查询规范所定义的派生表的相同程度。|  
|22018|转换指定的字符值无效|**StatementText*包含 SQL 语句包含的文字或参数，而与关联的表的列的数据类型不兼容的值。|  
|22019|无效的转义字符|自变量*StatementText*包含**等**谓词以及**转义**中**其中**子句和转义符的长度之后的字符**转义**不是等于 1。|  
|22025|无效的转义序列|自变量*StatementText*包含"**等**_模式值_**转义**_转义符_"中**其中**子句和后面的模式值中的转义字符的字符是"%"既不"_"。|  
|24000|游标状态无效|(DM) 上打开了游标*StatementHandle*，并**SQLFetch**或**SQLFetchScroll**已调用一样。<br /><br /> 在打开游标的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未调用。|  
|34000|无效的游标名称|\**StatementText*包含定位**删除**或定位**更新**，且正在准备的语句所引用的游标未打开。|  
|3D000|目录名称无效|中指定的目录名称*StatementText*无效。|  
|3F000|无效的架构名称|中指定的架构名称*StatementText*无效。|  
|42000|语法错误或访问冲突|\**StatementText*包含 SQL 语句不是可准备对象或包含语法错误。<br /><br /> **StatementText*包含用户没有具有所需的权限的语句。|  
|42S01|基表或视图已存在|\**StatementText*包含**CREATE TABLE**或**CREATE VIEW**语句和表名称或视图指定名称已存在。|  
|42S02|基表或视图找不到|\**StatementText*包含**DROP TABLE**或**DROP VIEW**语句指定的表名或视图名称不存在。<br /><br /> \**StatementText*包含**ALTER TABLE**语句，并指定的表名不存在。<br /><br /> \**StatementText*包含**CREATE VIEW**语句和表名称或视图不存在查询规范所定义的名称。<br /><br /> \**StatementText*包含**CREATE INDEX**语句，并指定的表名不存在。<br /><br /> \**StatementText*包含**授予**或**撤消**语句指定的表名或视图名称不存在。<br /><br /> \**StatementText*包含**选择**语句指定的表名或视图名称不存在。<br /><br /> \**StatementText*包含**删除**，**插入**，或**更新**语句，并指定的表名不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**语句，并指定约束 （引用表而不正在创建） 中的表不存在。|  
|42S11|索引已存在|\**StatementText*包含**CREATE INDEX**语句，并指定的索引名称已存在。|  
|42S12|找不到索引|\**StatementText*包含**DROP INDEX**语句，并指定的索引名称不存在。|  
|42S21|已存在的列|\**StatementText*包含**ALTER TABLE**语句，并在指定的列**添加**子句标识基表中的现有列，或不是唯一的。|  
|42S22|找不到列|\**StatementText*包含**CREATE INDEX**语句，以及一个或多列列表中指定的名称不存在的列。<br /><br /> \**StatementText*包含**授予**或**撤消**语句，并指定的列名称不存在。<br /><br /> \**StatementText*包含**选择**，**删除**，**插入**，或**更新**语句，并指定的列名称不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**语句，并指定约束 （引用表而不正在创建） 中的列不存在。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*，然后调用该函数是在上再次*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY009|使用空指针无效|（数据挖掘） *StatementText*是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLPrepare**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数*TextLength*小于或等于为 0 但不是等于 SQL_NTS。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|并发设置定义游标类型无效。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE，并且 SQL_ATTR_CURSOR_TYPE 语句属性设置为游标类型，该驱动程序不支持书签。|  
|HYT00|超时时间已到|超时期限过期之前的数据源返回的结果集。 通过设置超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 应用程序调用**SQLPrepare**将 SQL 语句发送到准备的数据源。 准备好的执行有关的详细信息，请参阅[准备好执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。 应用程序可以在 SQL 语句中包含一个或多个参数标记。 若要包含的参数标记，该应用程序将嵌入一个问号 （？） 到相应位置处的 SQL 字符串。 有关参数的信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
> [!NOTE]  
>  如果应用程序使用**SQLPrepare**准备并**SQLExecute**提交**提交**或**回滚**语句，它不是DBMS 产品之间互操作。 若要提交或回滚事务，调用**SQLEndTran**。  
  
 该驱动程序可以修改该语句使用的 SQL 数据源使用的窗体，然后将它提交到准备的数据源。 具体而言，该驱动程序将修改用于定义某些功能的 SQL 语法的转义序列。 (有关 SQL 语句语法的说明，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)和[附录 c:SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。)驱动程序语句句柄是类似于语句标识符中的嵌入式 SQL 代码。 如果数据源支持语句标识符，该驱动程序可以向数据源发送语句标识符和参数值。  
  
 语句已准备就绪后，应用程序使用的语句句柄来指代中更高版本的函数调用的语句。 可以通过调用重新执行已准备的语句与语句句柄相关联**SQLExecute**直到应用程序释放通过调用语句**SQLFreeStmt** SQL_DROP 选项或直到调用中使用的语句句柄**SQLPrepare**， **SQLExecDirect**，或一个目录函数 (**SQLColumns**， **SQLTables**，依此类推)。 一旦应用程序准备某个语句，它可以请求结果集的格式的信息。 对于某些实现，调用**SQLDescribeCol**或**SQLDescribeParam**后**SQLPrepare**可能不如之后调用该函数**SQLExecute**或**SQLExecDirect**。  
  
 某些驱动程序不能返回语法错误或访问冲突，当应用程序调用**SQLPrepare**。 驱动程序可以处理语法错误和访问冲突，仅语法错误或语法错误既不访问冲突。 因此，应用程序必须能够处理这些情况，当调用后续相关函数如**SQLNumResultCols**， **SQLDescribeCol**， **SQLColAttribute**，并**SQLExecute**。  
  
 具体取决于驱动程序和数据源的功能，如果 （如果所有参数都已都绑定） 准备的语句，参数信息 （如数据类型） 可能会处于选中状态，或者 （如果尚未都绑定所有参数） 的执行时。 最大互操作性，应用程序应取消绑定应用于旧 SQL 语句前准备新的 SQL 语句在同一个语句上的所有参数。 这可以防止由于旧应用到新的语句的参数信息的错误。  
  
> [!IMPORTANT]  
>  提交事务，通过显式调用**SQLEndTran**或通过在自动提交模式下工作，就可能导致要删除的连接上的所有语句访问计划的数据源。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 信息类型[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)并[对游标和准备的语句影响的事务](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)，并[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配语句句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|绑定到参数的缓冲区|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行提交或回滚操作|[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|执行 SQL 语句|[SQLExecDirect 函数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回语句所影响的行的数|[SQLRowCount 函数](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
