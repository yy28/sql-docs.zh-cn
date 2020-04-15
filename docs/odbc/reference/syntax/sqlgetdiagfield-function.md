---
title: SQLGetDiagfield 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a26319868a4b94b895da73d39b284f612fe35889
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285427"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 函数

**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetDiagField**返回包含错误、警告和状态信息的诊断数据结构记录字段（与指定句柄关联）的当前值。  
  
## <a name="syntax"></a>语法  
  
```cpp

SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *HandleType*  
 [输入]描述需要诊断的句柄类型的句柄类型标识符。 必须是下列选项之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN句柄仅由驱动程序管理器和驱动程序使用。 应用程序不应使用此句柄类型。 有关SQL_HANDLE_DBC_INFO_TOKEN的详细信息，请参阅在[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [输入]诊断数据结构的句柄，由*HandleType*指示的类型。 如果*HandleType*是SQL_HANDLE_ENV，*则句柄*可以是共享环境句柄，也可以是非共享环境句柄。  
  
 *RecNumber*  
 [输入]指示应用程序从中查找信息的状态记录。 状态记录从 1 编号。 如果*DiagIdentifier*参数指示诊断标头的任何字段，则*忽略 RecNumber。* 如果不是，它应该大于 0。  
  
 *诊断器标识符*  
 [输入]指示要返回其值的诊断字段。 有关详细信息，请参阅"注释"中的"*诊断标识符*参数"部分。  
  
 *迪亚格福普*  
 [输出]指向用于返回诊断信息的缓冲区的指针。 数据类型取决于*Diag标识符*的值。 如果*DiagInfoPtr*是整数类型，则应用程序应使用 SQLULEN 的缓冲区，并在调用此函数之前将值初始化为 0，因为某些驱动程序可能只写入缓冲区的较低 32 位或 16 位，并且保持高阶位不变。  
  
 如果*DiagInfoPtr*为 NULL，*则 StringLengthPtr*仍将返回在*DiagInfoPtr*指向的缓冲区中返回的字节总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度*  
 [输入]如果*DiagIdentifier*是 ODBC 定义的诊断，并且*DiagInfoPtr*指向字符字符串或二进制缓冲区，则此参数应\*为*DiagInfoPtr*的长度。 如果*Diag标识符*是 ODBC 定义的字段\*，而*DiagInfoPtr*是整数，则忽略*缓冲区长度*。 如果*\*DiagInfoPtr*中的值是 Unicode 字符串（在调用**SQLGetDiagFieldW**时），*则缓冲区长度*参数必须是偶数。  
  
 如果*DiagIdentifier*是驱动程序定义的字段，则应用程序通过设置*BufferLength*参数向驱动程序管理器指示该字段的性质。 *缓冲区长度*可以具有以下值：  
  
-   如果*DiagInfoPtr*是指向字符串的指针，*则缓冲区长度*是字符串的长度或SQL_NTS。  
  
-   如果*DiagInfoPtr*是指向二进制缓冲区的指针，则应用程序将SQL_LEN_BINARY_ATTR（*长度*）宏的结果放在*缓冲区长度*中。 这将在*缓冲区长度*中放置负值。  
  
-   如果*DiagInfoPtr*是指向字符串或二进制字符串以外的值的指针，则*BufferLength*应具有该值SQL_IS_POINTER。  
  
-   如果*\*DiagInfoPtr*包含固定长度的数据类型，则*缓冲区长度*将根据需要SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT或SQL_IS_USMALLINT。  
  
 *字符串长度 Ptr*  
 [输出]指向一个缓冲区的指针，用于返回字符数据的字节总数（不包括空终止字符所需的字节数）， 可用于在\**DiagInfoPtr*中返回。 如果可用于返回的字节数大于或等于*BufferLength，*\**则 DiagInfoPtr*中的文本将被截断为 *"缓冲区长度*"减去空终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE或SQL_NO_DATA。  
  
## <a name="diagnostics"></a>诊断  
 **SQLGetDiagField**不会自行发布诊断记录。 它使用以下返回值来报告其自身执行的结果：  
  
-   SQL_SUCCESS：该功能已成功返回诊断信息。  
  
-   \* *SQL_SUCCESS_WITH_INFO：DiagInfoPtr*太小，无法容纳请求的诊断字段。 因此，诊断字段中的数据被截断。 要确定发生截断，应用程序必须将*BufferLength*与实际可用字节数进行比较，该字节数写入 **StringLengthPtr*。  
  
-   *SQL_INVALID_HANDLE：HandleType*和*Handle*指示的句柄不是有效的句柄。  
  
-   SQL_ERROR： 发生了以下情况之一：  
  
    -   *Diag标识符参数*不是有效值之一。  
  
    -   *DiagIdentifier 参数*SQL_DIAG_CURSOR_ROW_COUNT、SQL_DIAG_DYNAMIC_FUNCTION、SQL_DIAG_DYNAMIC_FUNCTION_CODE 或SQL_DIAG_ROW_COUNT，但*Handle*不是语句句柄。 （驱动程序管理器返回此诊断。  
  
    -   当*Diag标识符*指示诊断记录中的字段时 *，RecNumber*参数为负数或 0。 对于标头字段，将忽略*RecNumber。*  
  
    -   请求的值是字符串，*缓冲区长度*小于零。  
  
    -   使用异步通知时，句柄上的异步操作未完成。  
  
-   SQL_NO_DATA： *RecNumber*大于*在 Handle*中指定的句柄存在的诊断记录数。 如果*Handle*没有诊断记录，则函数还会返回任何正*RecNumber* SQL_NO_DATA。  
  
## <a name="comments"></a>注释  
 应用程序通常调用**SQLGetDiagField**来实现三个目标之一：  
  
1.  在函数调用返回SQL_ERROR或SQL_SUCCESS_WITH_INFO（或**SQL_NEED_DATA SQLBrowseConnect**函数）时获取特定的错误或警告信息。  
  
2.  确定数据源中使用调用**SQLExecute、SQLExecDirect、SQLBulk****操作**或**SQLSetPos（** 从SQL_DIAG_ROW_COUNT标头字段）执行的**SQLExecDirect**数据源中受影响的行数，或者如果驱动程序可以提供此信息（从SQL_DIAG_CURSOR_ROW_COUNT标头字段）。  
  
3.  确定哪个函数是通过调用**SQLExecDirect**或**SQLExecute（** 从SQL_DIAG_DYNAMIC_FUNCTION和SQL_DIAG_DYNAMIC_FUNCTION_CODE标头字段）执行的。  
  
 任何 ODBC 函数每次调用时都可以发布零个或多个诊断记录，因此应用程序可以在任何 ODBC 函数调用后调用**SQLGetDiagField。** 任何一次可以存储的诊断记录数量没有限制。 **SQLGetDiagField**仅检索最近与*Handle*参数中指定的诊断数据结构关联的诊断信息。 如果应用程序调用的 ODBC 函数不是**SQLGetDiagField**或**SQLGetDiagRec，** 则以前具有相同句柄的调用中的任何诊断信息都丢失。  
  
 只要**SQLGetDiagField**返回SQL_SUCCESS，应用程序就可以通过增加*RecNumber*来扫描所有诊断记录。 状态记录数在SQL_DIAG_NUMBER页标题字段中指示。 对**SQLGetDiagField 的**调用对标头和记录字段没有破坏性。 应用程序可以稍后再次调用**SQLGetDiagField**从记录中检索字段，只要临时未调用诊断函数以外的函数，该函数将在同一句柄上发布记录。  
  
 应用程序可以调用**SQLGetDiagField**随时返回任何诊断字段，但SQL_DIAG_CURSOR_ROW_COUNT或SQL_DIAG_ROW_COUNT除外，如果*Handle*不是语句句柄，则返回SQL_ERROR。 如果未定义任何其他诊断字段，则对**SQLGetDiagField**的调用将返回SQL_SUCCESS（前提是未遇到其他诊断），并为该字段返回未定义的值。  
  
 有关详细信息，请参阅使用[SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) [并实现 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 调用异步执行的 API 以外的 API 将生成 HY010"函数序列错误"。 但是，在异步操作完成之前无法检索错误记录。  
  
## <a name="handletype-argument"></a>句柄类型参数  
 每个句柄类型都可以具有与其关联的诊断信息。 *句柄类型*参数指示*句柄类型的句柄*。  
  
 无法为环境、连接、语句和描述符句柄返回某些标头和记录字段。 以下"标题字段"和"记录字段"部分中指示字段不适用的句柄。  
  
 如果*HandleType*是SQL_HANDLE_ENV，*则句柄*可以是共享环境句柄，也可以是非共享环境句柄。  
  
 不应将特定于驱动程序的标头诊断字段与环境句柄关联。  
  
 为描述符句柄定义的唯一诊断标头字段是SQL_DIAG_NUMBER和SQL_DIAG_RETURNCODE。  
  
## <a name="diagidentifier-argument"></a>诊断参数  
 此参数指示诊断数据结构所需的字段的标识符。 如果*RecNumber*大于或等于 1，则字段中的数据将描述函数返回的诊断信息。 如果*RecNumber*为 0，则该字段位于诊断数据结构的标头中，因此包含与返回诊断信息的函数调用相关的数据，而不是特定信息的数据。  
  
 驱动程序可以在诊断数据结构中定义特定于驱动程序的标头和记录字段。  
  
 使用 ODBC 2 *.x*驱动程序的 ODBC 3 *.x*应用程序只能使用 SQL_DIAG_CLASS_ORIGIN、SQL_DIAG_CLASS_SUBCLASS_ORIGIN、SQL_DIAG_CONNECTION_NAME、SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_NUMBER、SQL_DIAG_RETURNCODE、SQL_DIAG_SERVER_NAME或SQL_DIAG_SQLSTATE的*Diag标识符*参数调用**SQLGetDiagField。** 所有其他诊断字段将返回SQL_ERROR。  
  
## <a name="header-fields"></a>标题字段  
 下表中列出的标头字段可以包含在*DiagIdentifier*参数中。  
  
|诊断器标识符|返回类型|返回|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|此字段包含游标中的行数。 其语义取决于 SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2 和 SQL_STATIC_CURSOR_ATTRIBUTES2的**SQLGetInfo**信息类型，它们指示每种游标类型（在SQL_CA2_CRC_EXACT和SQL_CA2_CRC_APPROXIMATE位）可用的行计数。<br /><br /> 此字段的内容仅为语句句柄定义，并且仅在调用**SQLExecute、SQLExecDirect**或**SQLMore 结果**之后。 **SQLExecute** 调用**SQLGetDiagField**时，在语句句柄之外，使用 SQL_DIAG_CURSOR_ROW_COUNT的*Diag标识符*将返回SQL_ERROR。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR ||这是一个字符串，用于描述基础函数执行的 SQL 语句。 （有关特定值，请参阅本节后面的"动态函数字段的值"。此字段的内容仅为语句句柄定义，并且仅在调用**SQLExecute、SQLExecDirect**或**SQLMore结果**后定义。 **SQLExecute** 调用**SQLGetDiagField**时，在语句句柄之外，使用SQL_DIAG_DYNAMIC_FUNCTION的*Diag标识符*将返回SQL_ERROR。 在调用 SQLExecute 或**SQLExecDirect**之前，此字段**SQLExecDirect**的值未定义。|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|这是描述基础函数执行的 SQL 语句的数字代码。 （有关特定值，请参阅本节后面的"动态函数字段的值"。此字段的内容仅为语句句柄定义，并且仅在调用**SQLExecute、SQLExecDirect**或**SQLMore结果**后定义。 **SQLExecute** 调用**SQLGetDiagField**时，在语句句柄之外，使用 SQL_DIAG_DYNAMIC_FUNCTION_CODE的*Diag标识符*将返回SQL_ERROR。 在调用 SQLExecute 或**SQLExecDirect**之前，此字段**SQLExecDirect**的值未定义。|  
|SQL_DIAG_NUMBER|SQLINTEGER|可用于指定句柄的状态记录数。|  
|SQL_DIAG_RETURNCODE|SQL 返回|返回函数返回的代码。 有关退货代码的列表，请参阅[退货代码](../../../odbc/reference/develop-app/return-codes-odbc.md)。 驱动程序不必实现SQL_DIAG_RETURNCODE;它始终由驱动程序管理器实现。 如果*句柄*上尚未调用任何函数，则SQL_DIAG_RETURNCODE将返回SQL_SUCCESS。|  
|SQL_DIAG_ROW_COUNT|SQLLEN|受**SQLExecute、SQLExecDirect、SQLBulk****操作**或**SQLExecute****SQLSetPos**执行的插入、删除或更新影响的行数。 在执行*游标规范*后，它是驱动程序定义的。 此字段的内容仅为语句句柄定义。 调用**SQLGetDiagField**时，在语句句柄之外，使用 SQL_DIAG_ROW_COUNT的*Diag标识符*将返回SQL_ERROR。 此字段中的数据也会在**SQLRowCount**的*RowCountPtr*参数中返回。 此字段中的数据在每个非诊断函数调用后重置，而**SQLRowCount**返回的行计数保持不变，直到语句返回到已准备或分配的状态。|  
  
## <a name="record-fields"></a>记录字段  
 下表中列出的记录字段可以包含在*DiagIdentifier*参数中。  
  
|诊断器标识符|返回类型|返回|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR ||指示在此记录中定义 SQLSTATE 值的类部分的文档的字符串。 其值为"ISO 9075"，适用于开放组和 ISO 调用级接口定义的所有 SQLSTAT。 对于特定于 ODBC 的 SQLSTATEs（所有其 SQLSTATE 类为"IM"的 SQLSTATEs），其值为"ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|如果SQL_DIAG_ROW_NUMBER字段是行集中的有效行号或一组参数，则此字段包含表示结果集中的列数的值或参数集中的参数编号。 结果集列数始终从 1 开始;结果集列数始终从 1 开始。如果此状态记录与书签列相关，则该字段可以为零。 参数编号从 1 开始。 如果状态记录未与列号或参数编号关联，则具有值SQL_NO_COLUMN_NUMBER。 如果驱动程序无法确定此记录关联的列号或参数编号，则此字段具有值SQL_COLUMN_NUMBER_UNKNOWN。<br /><br /> 此字段的内容仅为语句句柄定义。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR ||指示诊断记录相关的连接名称的字符串。 此字段是驱动程序定义的。 对于与环境句柄关联的诊断数据结构以及与任何连接无关的诊断，此字段为零长度字符串。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR ||有关错误或警告的信息性消息。 此字段的格式为[诊断消息](../../../odbc/reference/develop-app/diagnostic-messages.md)中所述。 诊断消息文本没有最大长度。|  
|SQL_DIAG_NATIVE|SQLINTEGER|驱动程序/数据源特定的本机错误代码。 如果没有本机错误代码，驱动程序返回 0。|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|此字段包含行集中的行号，或参数集中的参数编号，与状态记录关联。 行号和参数编号以 1 开头。 如果此状态记录未与行号或参数编号关联，则此字段具有值SQL_NO_ROW_NUMBER。 如果驱动程序无法确定此记录关联的行号或参数编号，则此字段具有值SQL_ROW_NUMBER_UNKNOWN。<br /><br /> 此字段的内容仅为语句句柄定义。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR ||指示诊断记录与之相关的服务器名称的字符串。 它与使用SQL_DATA_SOURCE_NAME选项调用**SQLGetInfo**返回的值相同。 对于与环境句柄关联的诊断数据结构以及与任何服务器无关的诊断，此字段为零长度字符串。|  
|SQL_DIAG_SQLSTATE|SQLCHAR ||五个字符的 SQLSTATE 诊断代码。 有关详细信息，请参阅[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR ||具有与SQL_DIAG_CLASS_ORIGIN相同的格式和有效值的字符串，用于标识 SQLSTATE 代码子类部分的定义部分。 返回"ODBC 3.0"的特定于 ODBC 的 SQLAA 包括以下内容：<br /><br /> 01S00、 01S01、 01S02、 01S06， 01S07、07S01、08S01、21S01、21S02、25S01、25S02、25S03、42S01、42S02、42S12、42S21、42S22、HY095、HY097、HY098、HY099、 HY100、HY101、HY105、HY107、HY109、HY110、HY111、HYT00、HYT01、IM001、IM002、IM003、IM004、IM005、IM006、IM007、IM008、IM010、IM0111、IM012。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>动态函数字段的值  
 下表描述了适用于调用 SQLExecute 或**SQLExecDirect**执行的每种类型的 SQL 语句的SQL_DIAG_DYNAMIC_FUNCTION和SQL_DIAG_DYNAMIC_FUNCTION_CODE的值**SQLExecDirect**。 驱动程序可以将驱动程序定义的值添加到列出的值。  
  
|SQL 语句<br /><br /> 已执行| 的值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION| 的值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*更改域语句*|"ALTER 域"|SQL_DIAG_ALTER_DOMAIN|  
|*更改表语句*|"更改表"|SQL_DIAG_ALTER_TABLE|  
|*断言定义*|"创建断言"|SQL_DIAG_CREATE_ASSERTION|  
|*字符集定义*|"创建字符集"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*排序规则定义*|"创建排序规则"|SQL_DIAG_CREATE_COLLATION|  
|*域定义*|"创建域"|SQL_DIAG_CREATE_DOMAIN|
|*创建索引语句*|"创建索引"|SQL_DIAG_CREATE_INDEX|  
|*创建表语句*|"创建表"|SQL_DIAG_CREATE_TABLE|  
|*创建-视图语句*|"创建视图"|SQL_DIAG_CREATE_VIEW|  
|*光标规范*|"选择光标"|SQL_DIAG_SELECT_CURSOR|  
|*删除语句定位*|"动态删除光标"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*删除语句搜索*|"删除位置"|SQL_DIAG_DELETE_WHERE|  
|*丢弃断言语句*|"丢弃断言"|SQL_DIAG_DROP_ASSERTION|  
|*放置字符集-stmt*|"丢弃字符集"|SQL_DIAG_DROP_CHARACTER_SET|  
|*丢弃排序规则语句*|"丢弃排序规则"|SQL_DIAG_DROP_COLLATION|  
|*删除域语句*|"DROP 域"|SQL_DIAG_DROP_DOMAIN|  
|*丢弃索引语句*|"下降指数"|SQL_DIAG_DROP_INDEX|  
|*删除架构语句*|"丢弃模式"|SQL_DIAG_DROP_SCHEMA|  
|*下放表语句*|"掉落表"|SQL_DIAG_DROP_TABLE|  
|*删除翻译语句*|"滴翻译"|SQL_DIAG_DROP_TRANSLATION|  
|*放置视图语句*|"下降视图"|SQL_DIAG_DROP_VIEW|  
|*赠款报表*|"格兰特"|SQL_DIAG_GRANT|
|*插入语句*|"插入"|SQL_DIAG_INSERT|  
|*ODBC-程序扩展*|"呼叫"|SQL_DIAG_呼叫|  
|*撤销声明*|"撤销"|SQL_DIAG_REVOKE|  
|*架构定义*|"创建架构"|SQL_DIAG_CREATE_SCHEMA|  
|*翻译定义*|"创建翻译"|SQL_DIAG_CREATE_TRANSLATION|  
|*更新语句定位*|"动态更新光标"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*更新语句搜索*|"更新位置"|SQL_DIAG_UPDATE_WHERE|  
|未知|*空字符串*|SQL_DIAG_UNKNOWN_STATEMENT|  

<!--
These two malformed table rows were fixed by educated GUESS only.
Each pair starts with the original flawed row.
Flawed because treated as only two cells by HTML render,
and because missing info anyway.
Also, these flawed rows lacked '|' as their first nonWhitespace character (although markdown technically allows this omission, unfortunately).
Arguably the following SQL.H file shows the sequence of the flawed rows in the table was suboptimal also.

ftp://www.fpc.org/fpc32/VS6Disk1/VC98/INCLUDE/SQL.H

GeneMi , 2019/01/19
- - - - - - - - - - - - - -

n-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|  

|*domain-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|

-statement*|"GRANT"|SQL_DIAG_GRANT|  

|*grant-statement*|"GRANT"|SQL_DIAG_GRANT|

-->

## <a name="sequence-of-status-records"></a>状态记录的序列

 状态记录根据行号和诊断类型按顺序定位。 驱动程序管理器确定返回它生成的状态记录的最终顺序。 驱动程序确定返回其生成的状态记录的最终顺序。  
  
 如果诊断记录由驾驶员经理和驱动程序过帐，则驾驶员经理负责订购。  
  
 如果有两个或多个状态记录，则记录的顺序首先由行号确定。 以下规则适用于按行确定诊断记录的顺序：  
  
-   不对应于任何行的记录将显示在对应于特定行的记录前面，因为SQL_NO_ROW_NUMBER定义为 -1。  
  
-   行号未知的记录显示在所有其他记录的前面，因为SQL_ROW_NUMBER_UNKNOWN定义为 -2。  
  
-   对于与特定行相关的所有记录，记录按SQL_DIAG_ROW_NUMBER字段中的值排序。 列出受影响的第一行的所有错误和警告，然后列出受影响的下一行的所有错误和警告，等等。  
  
> [!NOTE]
>  如果 SQLSTATE 01S01（行中的错误）由 ODBC 2 *.x*驱动程序返回，或者在调用**SQLExtendedFetch**时由 ODBC 3 .x 驱动程序返回 SQLSTATE 01S01（行中的错误 **），则**ODBC 3 *.x*驱动程序管理器不会在诊断队列中订购状态**记录。***.x*  
  
 在每行中，或对于与行不对应或行号未知的所有记录，或者对于行号等于SQL_NO_ROW_NUMBER的所有记录，使用一组排序规则确定列出的第一个记录。 在第一条记录之后，影响行的其他记录的顺序未定义。 应用程序不能假定错误在第一条记录之后的警告之前。 应用程序应扫描完整的诊断数据结构，以获取有关对函数调用不成功的完整信息。  
  
 以下规则用于确定行中的第一个记录。 排名最高的记录是第一条记录。 在排名记录时，不考虑记录的来源（驱动程序管理器、驱动程序、网关等）。  
  
-   **错误**描述错误的状态记录的排名最高。 以下规则应用于对错误进行排序：  
  
    -   指示事务失败或可能事务失败的记录比所有其他记录都多。  
  
    -   如果两个或多个记录描述相同的错误条件，则由开放组 CLI 规范定义的 SQLSTAT（类 03 到 HZ）比 ODBC 和驱动程序定义的 SQLSTATEs 高。  
  
-   **实现定义的无数据值**描述驱动程序定义的无数据值（类 02）的状态记录具有第二高的排名。  
  
-   **警告**描述警告的状态记录（类 01）的排名最低。 如果两个或多个记录描述相同的警告条件，则警告由开放组 CLI 规范定义的 SQLSTAT 比 ODBC 定义和驱动程序定义的 SQLSTATEs 高。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|获取诊断数据结构的多个字段|[SQLGetDiagRec 函数](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
