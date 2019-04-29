---
title: SQLExecDirect 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecDirect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecDirect
helpviewer_keywords:
- SQLExecDirect function [ODBC]
ms.assetid: 985fcee1-f204-425c-bdd1-deb0e7d7bbd9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 794dc83a27d3c4882b5df4edbb4f2a645cd5ca1c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061505"
---
# <a name="sqlexecdirect-function"></a>SQLExecDirect 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLExecDirect**执行可准备对象的语句，使用参数标记变量的当前值，如果在语句中存在任何参数。 **SQLExecDirect**是提交一次性执行的 SQL 语句的最快方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *StatementText*  
 [输入]若要执行的 SQL 语句。  
  
 *TextLength*  
 [输入]长度 **StatementText*以字符为单位。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR、 SQL_NO_DATA、 SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLExecDirect**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*设置为 SQL_HANDLE_STMT，和一个*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLExecDirect** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01001|游标操作冲突|\**StatementText*包含定位的 update 或 delete 语句，并且没有行或多个行未更新或删除。 (有关对多个行的更新的详细信息，请参阅说明 SQL_ATTR_SIMULATE_CURSOR*特性*中**SQLSetStmtAttr**。)<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01003|Set 函数中消除了空值|自变量*StatementText*包含一个集函数 (如**AVG**，**最大**， **MIN**，依次类推)，但不是**计数**设置函数，并且 NULL 参数值在应用函数之前已被消除。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|字符串或二进制数据返回为输入/输出或输出参数导致的非空白字符或非 NULL 二进制数据截断。 如果它是一个字符串值，它是右侧被截断。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01006|未撤消特权|\**StatementText*包含**撤消**语句，并且用户不具有指定的特权。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01007|未授予特权|*\*StatementText*已**授予**语句，并且用户可能不授予指定的特权。|  
|01S02|选项值已更改|指定的语句属性实现运行情况，由于无效，因此已暂时替换一个相近的值。 (**SQLGetStmtAttr**可以调用以确定暂时被替换的值是什么。)替换值是否为有效*StatementHandle*直到关闭游标，此时语句属性将恢复为以前的值。 可以更改的语句属性有：<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S07|截断小数部分|用于输入/输出返回的数据或输出参数已被截断数值数据类型的小数部分被截断或时间部分的时间、 时间戳或时间间隔的数据类型的小数部分被截断。<br /><br /> （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07002|COUNT 字段不正确|在指定的参数数目**SQLBindParameter**中包含的 SQL 语句中的参数数量小于\* *StatementText*。<br /><br /> **SQLBindParameter**调用时使用*ParameterValuePtr*设置为 null 指针*StrLen_or_IndPtr*未设置为 SQL_NULL_DATA 或 SQL_DATA_AT_EXEC，和*InputOutputType*不将设置为 SQL_PARAM_OUTPUT，以便在指定的参数数目**SQLBindParameter**大于中包含的 SQL 语句中的参数数目 **StatementText*.|  
|07006|受限制的数据类型属性冲突|标识的数据值*ValueType*中的参数**SQLBindParameter**无法为数据类型由标识转换绑定的参数为*ParameterType*中的参数**SQLBindParameter**。<br /><br /> 参数绑定为 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT 不无法转换为标识的数据类型返回的数据值*ValueType*中的参数**SQLBindParameter**。<br /><br /> （如果无法转换为一个或多个行的数据值，但没有成功返回一个或多个行，此函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07007|受限制的参数值冲突|参数类型 SQL_PARAM_INPUT_OUTPUT_STREAM 仅用于发送和接收数据部分中的参数。 输入此参数类型不允许绑定的缓冲区。<br /><br /> 参数类型是 SQL_PARAM_INPUT_OUTPUT，以及时，将发生此错误\* *StrLen_or_IndPtr*中指定**SQLBindParameter**不等于 SQL_NULL_DATA，SQL_DEFAULT_PARAM、 SQL_LEN_DATA_AT_EXEC(len) 或 SQL_DATA_AT_EXEC。|  
|07S01|默认参数的使用无效|参数值，设置**SQLBindParameter**、 是 SQL_DEFAULT_PARAM，并且相应参数没有默认值。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|21S01|插入值列表与列列表不匹配|\**StatementText*包含**插入**语句和要插入的值的数目不匹配的派生表的程度。|  
|21S02|派生表等级与列列表不匹配|\**StatementText*包含**CREATE VIEW**语句和非限定的列列表 (图中指定的列数*列标识符*参数的 sql语句） 包含定义的派生表中的列数与多个名称，*查询规范*SQL 语句的参数。|  
|22001|字符串数据，右截断|字符或二进制值的列的分配时截断了非空白字符数据或非 null 的二进制数据。|  
|22002|需要指示器变量，但未提供|NULL 数据被绑定到一个输出参数，其*StrLen_or_IndPtr*设置**SQLBindParameter**是空指针。|  
|22003|数值超出范围|**StatementText*包含包含绑定的数值参数、 文字、 一个 SQL 语句，并且值被截断时分配给关联的表列数字的整个 （而不是小数） 部分。<br /><br /> 返回一个数字值 （数值或字符串） 的一个或多个输入/输出参数或输出参数将导致要截断的数字的整个 （而不是小数） 部分。|  
|22007|日期时间格式无效|**StatementText*包含了包含日期、 时间戳结构作为绑定参数，一个 SQL 语句，该参数，分别，无效的日期、 时间戳。<br /><br /> 输入/输出或输出参数绑定到日期、 时间或时间戳 C 结构，返回的参数中的值时，分别，无效的日期、 时间戳。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|22008|日期时间字段溢出|**StatementText*包含包含日期时间表达式，计算，产生的日期时间戳结构的 SQL 语句无效。<br /><br /> 日期时间表达式计算的输入/输出或输出参数导致了日期、 时间或时间戳 C 结构无效。|  
|22012|被零除|**StatementText*包含了一个包含导致被零除的算术表达式的 SQL 语句。<br /><br /> 算术表达式计算的输入/输出或输出参数导致除零。|  
|22015|间隔字段溢出|*\*StatementText*包含一个确切的数值或时间间隔参数，当转换到 SQL 数据类型的时间间隔，导致重要数字丢失。<br /><br /> *\*StatementText*包含多个字段是间隔参数，当转换为数值数据类型列中，没有表示形式具有数值数据类型。<br /><br /> *\*StatementText*包含已分配到的时间间隔 SQL 类型的参数数据，并且在时间间隔内 SQL 类型的 C 类型的值没有表示形式。<br /><br /> 分配为精确数字或间隔时导致重要数字丢失 C 间隔类型到 SQL 类型的输入/输出或输出参数。<br /><br /> 输入/输出或输出参数分配给一个 C 间隔结构，间隔数据结构中的数据没有表示形式。|  
|22018|转换指定的字符值无效|*\*StatementText*包含 C 类型的为准确或近似数值、 日期时间或间隔数据类型; 该列的 SQL 类型是字符数据类型; 和列中的值不是有效的绑定 C 类型的文本。<br /><br /> SQL 类型时返回的输入/输出或输出参数，已准确或近似数值、 日期时间或间隔数据类型;C 类型为 SQL_C_CHAR;和列中的值不是有效的绑定的 SQL 类型的文本。|  
|22019|无效的转义字符|\**StatementText*包含了包含一个 SQL 语句**等**谓词以及**转义**中**其中**子句和转义符的长度之后的字符**转义**不是等于 1。|  
|22025|无效的转义序列|\**StatementText*包含了包含一个 SQL 语句"**等**_模式值_**转义**_转义符_"中**其中**子句和后面的模式值中的转义字符的字符不是之一"%"或"_"。|  
|23000|完整性约束冲突|**StatementText*包含了一个包含参数的 SQL 语句。 参数值为空的定义为 NOT NULL 列关联的表中的列、 列约束为仅包含唯一值，却提供了重复的值或违反了某个其他的完整性约束。|  
|24000|游标状态无效|在光标*StatementHandle*通过**SQLFetch**或**SQLFetchScroll**。 如果此错误返回由驱动程序管理器**SQLFetch**或**SQLFetchScroll**未返回 SQL_NO_DATA，和如果驱动程序返回**SQLFetch**或**SQLFetchScroll**已返回 sql_no_data 为止。<br /><br /> 游标已打开但未在定位*StatementHandle*。<br /><br /> **StatementText*包含和定位的 update 或 delete 语句，游标早于开始日期的结果集或结果集的末尾之后位置。|  
|34000|无效的游标名称|**StatementText*包含和定位的 update 或 delete 语句，正在执行的语句所引用的游标未打开。|  
|3D000|目录名称无效|中指定的目录名称*StatementText*无效。|  
|3F000|无效的架构名称|中指定的架构名称*StatementText*无效。|  
|40001|序列化失败|事务已回滚，由于其他事务与资源死锁。|  
|40003|语句完成情况未知|此函数中，在执行期间失败关联的连接，无法确定事务的状态。|  
|42000|语法错误或访问冲突|\**StatementText*包含 SQL 语句不是可准备对象或包含语法错误。<br /><br /> 用户没有权限执行 SQL 语句中包含 **StatementText*。|  
|42S01|基表或视图已存在|\**StatementText*包含**CREATE TABLE**或**CREATE VIEW**语句和表名称或视图指定名称已存在。|  
|42S02|基表或视图找不到|\**StatementText*包含**DROP TABLE**或**DROP VIEW**语句指定的表名或视图名称不存在。<br /><br /> \**StatementText*包含**ALTER TABLE**语句，并指定的表名不存在。<br /><br /> \**StatementText*包含**CREATE VIEW**语句和表名称或视图不存在查询规范所定义的名称。<br /><br /> \**StatementText*包含**CREATE INDEX**语句，并指定的表名不存在。<br /><br /> \**StatementText*包含**授予**或**撤消**语句指定的表名或视图名称不存在。<br /><br /> \**StatementText*包含**选择**语句指定的表名或视图名称不存在。<br /><br /> \**StatementText*包含**删除**，**插入**，或**更新**语句，并指定的表名不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**语句，并指定约束 （引用表而不正在创建） 中的表不存在。<br /><br /> \**StatementText*包含**CREATE SCHEMA**语句指定的表名或视图名称不存在。|  
|42S11|索引已存在|\**StatementText*包含**CREATE INDEX**语句，并指定的索引名称已存在。<br /><br /> \**StatementText*包含**CREATE SCHEMA**语句，并指定的索引名称已存在。|  
|42S12|找不到索引|\**StatementText*包含**DROP INDEX**语句，并指定的索引名称不存在。|  
|42S21|已存在的列|\**StatementText*包含**ALTER TABLE**语句，并在指定的列**添加**子句标识基表中的现有列，或不是唯一的。|  
|42S22|找不到列|\**StatementText*包含**CREATE INDEX**语句，以及一个或多列列表中指定的名称不存在的列。<br /><br /> \**StatementText*包含**授予**或**撤消**语句，并指定的列名称不存在。<br /><br /> \**StatementText*包含**选择**，**删除**，**插入**，或**更新**语句，并指定的列名称不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**语句，并指定约束 （引用表而不正在创建） 中的列不存在。<br /><br /> \**StatementText*包含**CREATE SCHEMA**语句，并指定的列名称不存在。|  
|44000|WITH CHECK OPTION 冲突|自变量*StatementText*包含**插入**上查看的表执行的语句或派生自查看已通过指定的表的表**WITH CHECK OPTION**，这样，受影响的一个或多个行**插入**语句无法再查看表中存在。<br /><br /> 自变量*StatementText*包含**更新**上查看的表执行的语句或派生自查看已通过指定的表的表**WITH CHECK OPTION**，这样，受影响的一个或多个行**更新**语句无法再查看表中存在。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*StatementHandle*。 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*。 然后在再次调用该函数*StatementHandle*。<br /><br /> 调用该函数，和之前执行完毕**SQLCancel**或**SQLCancelHandle**上调用了*StatementHandle*来自不同线程中多线程应用程序。|  
|HY009|使用空指针无效|(DM) **StatementText*是空指针。|  
|HY010|函数序列错误|(DM) 为与之关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLExecDirect**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**曾为*StatementHandle*和返回 SQL_PARAM_DATA_可用。 数据已检索到的所有经过流处理参数之前调用此函数。<br /><br /> (DM) 的调用以异步方式执行的函数 （不是此类似） *StatementHandle*和仍在执行时调用此函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或者**SQLSetPos**曾为*StatementHandle*和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数*TextLength*小于或等于为 0 但不是等于 SQL_NTS。<br /><br /> 参数值，设置**SQLBindParameter**、 是空指针和参数长度值不是 0，SQL_NULL_DATA，SQL_DATA_AT_EXEC，SQL_DEFAULT_PARAM，或小于或等于 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 参数值，设置**SQLBindParameter**、 不是空指针; C 数据类型为 SQL_C_BINARY 或 SQL_C_CHAR; 和参数长度值是小于 0，但不是 SQL_NTS、 SQL_NULL_DATA、 SQL_DATA_AT_EXEC、 SQL_DEFAULT_参数，或小于或等于 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 参数长度值受**SQLBindParameter**为设置为 SQL_DATA_AT_EXEC; 的 SQL 类型为 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 数据源特定的数据类型; 和 SQL_NEED_LONG_DATA_LEN 信息在键入**SQLGetInfo**是"Y"。|  
|HY105|无效的参数类型|为参数指定的值*InputOutputType*中**SQLBindParameter** SQL_PARAM_OUTPUT，而该参数是输入的参数。|  
|HY109|无效的游标位置|\**StatementText*包含和定位的 update 或 delete 语句，光标被定位 (通过**SQLSetPos**或**SQLFetchScroll**) 上的行已删除或无法提取。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|驱动程序或数据源不支持 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 语句属性的当前设置的组合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE，并且 SQL_ATTR_CURSOR_TYPE 语句属性设置为游标类型，该驱动程序不支持书签。|  
|HYT00|超时时间已到|查询超时期限过期之前的数据源返回的结果集。 通过设置超时期限**SQLSetStmtAttr**，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*StatementHandle*不支持该函数。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
  
## <a name="comments"></a>注释  
 应用程序调用**SQLExecDirect**将 SQL 语句发送到数据源。 有关直接执行的详细信息，请参阅[直接执行](../../../odbc/reference/develop-app/direct-execution-odbc.md)。 驱动程序修改该语句以使用 SQL 数据源使用的窗体，然后将其提交到数据源。 具体而言，该驱动程序将修改用于定义某些功能在 SQL 中的转义序列。 转义序列的语法，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。  
  
 应用程序可以在 SQL 语句中包含一个或多个参数标记。 若要包含的参数标记，应用程序，请嵌入到 SQL 语句中的相应位置的问号 （？）。 有关参数的信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 如果 SQL 语句是**选择**语句，如果应用程序中调用**SQLSetCursorName**以将游标与语句相关联，然后驱动程序将使用指定的游标。 否则，该驱动程序生成的游标名称。  
  
 如果数据源在手动提交模式下 （需要显式事务启动），并且尚未启动事务，驱动程序将启动一个事务发送的 SQL 语句之前。 有关详细信息，请参阅[手动提交模式](../../../odbc/reference/develop-app/manual-commit-mode.md)。  
  
 如果应用程序使用**SQLExecDirect**提交**提交**或**回滚**语句，它不会 DBMS 产品之间的互操作性。 若要提交或回滚事务，应用程序调用**SQLEndTran**。  
  
 如果**SQLExecDirect**遇到执行时数据参数，它将返回 SQL_NEED_DATA。 应用程序发送的数据使用**SQLParamData**并**SQLPutData**。 请参阅[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)， [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)，以及[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
 如果**SQLExecDirect**执行搜索的 update、 insert 或 delete 语句，但不影响任何行在数据源，调用**SQLExecDirect**返回 sql_no_data 为止。  
  
 如果将 SQL_ATTR_PARAMSET_SIZE 语句属性的值大于 1，并且 SQL 语句中包含至少一个参数标记， **SQLExecDirect**将执行的每组参数值从一次的 SQL 语句指向数组*ParameterValuePointer*调用中的参数**SQLBindParameter**。 有关详细信息，请参阅[参数值数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 如果书签被打开，并且执行的查询不能支持书签，则驱动程序应尝试强制为通过更改属性值并返回 SQLSTATE 01S02 支持书签环境 （选项值已更改）。 如果不能更改的属性，则驱动程序应返回 SQLSTATE 为 HY024 （无效的属性值）。  
  
> [!NOTE]  
>  当使用连接池时，应用程序必须执行 SQL 语句，如更改数据库或数据库的上下文**使用**_数据库_语句在 SQL Server 中，这会更改使用数据源的目录。  
  
## <a name="code-example"></a>代码示例  
 请参阅[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)， [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)，并[示例 ODBC 程序](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将缓冲区绑定到结果集中的列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消语句处理|[SQLCancel 函数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|执行提交或回滚操作|[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|执行已准备的 SQL 语句|[SQLExecute 函数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|正在提取多行数据|[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取的数据块或滚动浏览结果集|[SQLFetchScroll 函数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回游标名称|[SQLGetCursorName 函数](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|正在提取部分或全部的数据列|[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|返回下一个参数将数据发送用于|[SQLParamData 函数](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|准备执行的语句|[SQLPrepare 函数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|在执行时发送参数数据|[SQLPutData 函数](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|设置游标名称|[SQLSetCursorName 函数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
