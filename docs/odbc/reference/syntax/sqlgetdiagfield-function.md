---
title: "SQLGetDiagField 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0cd8f64eb18fc6e1fb456b03ef65ef2dc33cc140
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetDiagField**返回的字段包含错误、 警告和状态信息的诊断数据结构 （与指定的句柄关联） 的记录的当前值。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 [输入]描述的类型的诊断为所需的句柄的句柄类型标识符。 必须是下列选项之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 仅由驱动程序管理器和驱动程序使用 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 应用程序不应使用此句柄类型。 有关 SQL_HANDLE_DBC_INFO_TOKEN 的详细信息，请参阅[开发中使用 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [输入]诊断数据结构，指示的类型的句柄*HandleType*。 如果*HandleType*是 SQL_HANDLE_ENV，*处理*可以是共享或非共享的环境句柄。  
  
 *RecNumber*  
 [输入]指示应用程序从中查找信息的状态记录。 状态记录编号从 1。 如果*DiagIdentifier*参数指示诊断标头，任何字段*RecNumber*将被忽略。 否则，它应为大于 0。  
  
 *DiagIdentifier*  
 [输入]指示其值是要返回的诊断的字段。 有关详细信息，请参阅"*DiagIdentifier*自变量"部分中"注释"。  
  
 *DiagInfoPtr*  
 [输出]指向要返回其诊断信息中的缓冲区的指针。 数据类型的值取决于*DiagIdentifier*。 如果*DiagInfoPtr*是整数类型、 应用程序应使用的缓冲区 SQLULEN 和初始化为 0，在作为某些驱动程序调用此函数之前的值可能仅写入的低 32 位或 16 位的缓冲区，并将顺序更高位保持不变。  
  
 如果*DiagInfoPtr*为 NULL， *StringLengthPtr*仍将返回的 （不包括字符数据的 null 终止字符） 的字节总数可用于返回指向由的缓冲区中*DiagInfoPtr*。  
  
 *BufferLength*  
 [输入]如果*DiagIdentifier*是 ODBC 定义的诊断和*DiagInfoPtr*指向字符字符串或二进制缓冲区时，此参数应为的长度\* *DiagInfoPtr*. 如果*DiagIdentifier*是一个 ODBC 定义的字段和\* *DiagInfoPtr*是一个整数， *BufferLength*将被忽略。 如果中的值 *\*DiagInfoPtr*为 Unicode 字符串 (在调用时**SQLGetDiagFieldW**)，则*BufferLength*参数必须为偶数。  
  
 如果*DiagIdentifier*是驱动程序定义的字段，该应用程序通过设置来指明字段到驱动程序管理器的性质*BufferLength*自变量。 *BufferLength*可以具有下列值：  
  
-   如果*DiagInfoPtr*是指向字符串， *BufferLength*是字符串或 sql_nts 以的长度。  
  
-   如果*DiagInfoPtr* SQL_LEN_BINARY_ATTR 的结果是指向二进制缓冲区中，应用程序位置的指针 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果*DiagInfoPtr*是指向字符字符串或二进制字符串以外的值的*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果 *\*DiagInfoPtr*包含固定长度的数据类型， *BufferLength*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_IS_USMALLINT，根据需要。  
  
 *StringLengthPtr*  
 [输出]指向要返回的 （不包括所需的 null 终止字符的字节数） 的字节总数在其中缓冲区的指针可用于返回在\* *DiagInfoPtr*，为字符数据。 可用于返回的字节数是否大于或等于*BufferLength*中的文本\* *DiagInfoPtr*截断为*BufferLength*减null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_NO_DATA。  
  
## <a name="diagnostics"></a>诊断  
 **SQLGetDiagField**不会发送自己的诊断记录。 它使用下列返回值来报告其自己执行的结果：  
  
-   SQL_SUCCESS： 该函数成功地返回诊断信息。  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr*已太小，无法容纳请求的诊断字段。 因此，诊断字段中的数据被截断。 若要确定发生截断，应用程序必须进行比较*BufferLength*可用字节数，这写入的实际数目 **StringLengthPtr*。  
  
-   SQL_INVALID_HANDLE: 句柄由*HandleType*和*处理*不是有效的句柄。  
  
-   以下项之一发生 SQL_ERROR::  
  
    -   *DiagIdentifier*自变量不是有效的值之一。  
  
    -   *DiagIdentifier*自变量为 SQL_DIAG_CURSOR_ROW_COUNT、 SQL_DIAG_DYNAMIC_FUNCTION、 SQL_DIAG_DYNAMIC_FUNCTION_CODE 或 SQL_DIAG_ROW_COUNT，但*处理*未语句句柄。 （驱动程序管理器返回此诊断。）  
  
    -   *RecNumber*自变量为负则为 0 时*DiagIdentifier*指示从诊断记录的字段。 *RecNumber*对于标头字段将被忽略。  
  
    -   请求的值为字符串和*BufferLength*小于零。  
  
    -   使用异步通知时，句柄的异步操作是不完整。  
  
-   SQL_NO_DATA: *RecNumber*存在的句柄中指定的诊断记录的数目大于*处理。* 此函数还为任何正返回 SQL_NO_DATA *RecNumber*是否存在的任何诊断记录*处理*。  
  
## <a name="comments"></a>注释  
 应用程序通常调用**SQLGetDiagField**来完成三个目标之一：  
  
1.  若要获取特定的错误或警告信息的函数调用具有返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 时 (或为 SQL_NEED_DATA **SQLBrowseConnect**函数)。  
  
2.  若要确定数据源中插入、 删除或更新操作已通过调用执行时受影响的行数**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos** （从 SQL_DIAG_ROW_COUNT 标头字段），或者想要确定在当前打开的游标中存在的行数，如果驱动程序可以提供此信息 (从SQL_DIAG_CURSOR_ROW_COUNT 标头字段）。  
  
3.  若要确定哪些函数通过调用执行了**SQLExecDirect**或**SQLExecute** （从 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE 标头字段）。  
  
 任何 ODBC 函数可以将发布零个或多个诊断记录每次调用它时，因此应用程序可以调用**SQLGetDiagField**任何 ODBC 函数调用之后。 对可以在任何时候存储的诊断记录的数量没有限制。 **SQLGetDiagField**只检索诊断信息中指定的诊断数据结构与最近关联*处理*自变量。 如果应用程序调用 ODBC 函数以外**SQLGetDiagField**或**SQLGetDiagRec**，来自具有相同的句柄的先前调用的任何诊断信息将丢失。  
  
 应用程序可以通过将递增扫描所有诊断记录*RecNumber*，只要**SQLGetDiagField**返回 SQL_SUCCESS。 状态记录数是 SQL_DIAG_NUMBER 标头字段中指定的。 调用**SQLGetDiagField**是非到标头和记录字段破坏性的。 应用程序可以调用**SQLGetDiagField**再次稍后，若要从一个记录，检索字段，只要尚未在此期间，将在相同句柄发布记录调用诊断函数以外的函数。  
  
 应用程序可以调用**SQLGetDiagField**随时除外 SQL_DIAG_CURSOR_ROW_COUNT 或 SQL_DIAG_ROW_COUNT，它将返回 SQL_ERROR，如果返回任何诊断字段*处理*不是语句句柄。 如果任何其他诊断字段未定义，调用**SQLGetDiagField** （前提是没有其他诊断，则遇到） 将返回 SQL_SUCCESS 和未定义的值返回为该字段。  
  
 有关详细信息，请参阅[使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)和[实现 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 调用以异步方式执行以外的 API 将生成 HY010"函数序列错误"。 但是，在异步操作完成前，无法检索错误记录。  
  
## <a name="handletype-argument"></a>HandleType 自变量  
 每个句柄类型可以具有与之关联的诊断信息。 *HandleType*参数指示的句柄类型*处理*。  
  
 某些标头和记录字段不能返回环境、 连接、 语句中，和描述符句柄。 后面的"标头字段"和"记录字段"节中指示为其字段并不适用于这些句柄。  
  
 如果*HandleType*是 SQL_HANDLE_ENV，*处理*可以是任意的共享或取消共享环境句柄。  
  
 没有特定于驱动程序的标头诊断字段应为与环境句柄关联。  
  
 为的描述符句柄定义仅诊断标头字段是 SQL_DIAG_NUMBER 和 SQL_DIAG_RETURNCODE。  
  
## <a name="diagidentifier-argument"></a>DiagIdentifier 自变量  
 此参数指示从诊断数据结构所需的域的标识符。 如果*RecNumber*大于或等于 1，字段中的数据描述函数返回的诊断信息。 如果*RecNumber*为 0，则字段中的标头的诊断数据结构，因此包含与返回的诊断信息，不到的特定信息的函数调用相关的数据。  
  
 驱动程序可以定义特定于驱动程序的标头和记录字段中的诊断数据结构。  
  
 ODBC 3*.x*应用程序使用 ODBC 2*.x*驱动程序将能够调用**SQLGetDiagField**只用*DiagIdentifier*SQL_DIAG_CLASS_ORIGIN、 SQL_DIAG_CLASS_SUBCLASS_ORIGIN、 SQL_DIAG_CONNECTION_NAME、 SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_NATIVE、 SQL_DIAG_NUMBER、 SQL_DIAG_RETURNCODE、 SQL_DIAG_SERVER_NAME 或 SQL_DIAG_SQLSTATE 自变量。 诊断的所有其他字段将返回 SQL_ERROR。  
  
## <a name="header-fields"></a>标头字段  
 下表中列出的标头字段可以包含在*DiagIdentifier*自变量。  
  
|DiagIdentifier|返回类型|返回|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|此字段包含的游标中的行的计数。 其语义取决**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2，SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、 SQL_KEYSET_CURSOR_ATTRIBUTES2，并且 SQL_STATIC_CURSOR_ATTRIBUTES2，其指示的信息类型行计数是可用于每种游标类型 （以 SQL_CA2_CRC_EXACT 和 SQL_CA2_CRC_APPROXIMATE 位为单位）。<br /><br /> 此字段的内容定义仅可用于语句句柄而之后才**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**已调用。 调用**SQLGetDiagField**与*DiagIdentifier*以外语句上 SQL_DIAG_CURSOR_ROW_COUNT 的句柄将返回 SQL_ERROR。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|这是一个字符串，描述基础函数执行的 SQL 语句。 （请参阅"的字段的值动态函数，"更高版本在本部分中，特定值）。此字段的内容定义仅进行语句句柄并仅在调用后**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**。 调用**SQLGetDiagField**与*DiagIdentifier*以外语句上 SQL_DIAG_DYNAMIC_FUNCTION 的句柄将返回 SQL_ERROR。 此字段的值未定义在调用之前**SQLExecute**或**SQLExecDirect**。|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|这是介绍执行了基础函数的 SQL 语句的数字代码。 （请参阅"值的动态函数中的字段，"更高版本本部分中，特定值）。此字段的内容定义仅进行语句句柄并仅在调用后**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**。 调用**SQLGetDiagField**与*DiagIdentifier*以外语句上 SQL_DIAG_DYNAMIC_FUNCTION_CODE 的句柄将返回 SQL_ERROR。 此字段的值未定义在调用之前**SQLExecute**或**SQLExecDirect**。|  
|SQL_DIAG_NUMBER|SQLINTEGER|可用于指定句柄的状态记录数。|  
|SQL_DIAG_RETURNCODE|SQLRETURN|返回的函数的返回代码。 有关返回代码的列表，请参阅[返回代码](../../../odbc/reference/develop-app/return-codes-odbc.md)。 该驱动程序不需要实现 SQL_DIAG_RETURNCODE;它始终被实现通过驱动程序管理器。 如果尚未在调用任何函数*处理*，将返回 SQL_SUCCESS SQL_DIAG_RETURNCODE。|  
|SQL_DIAG_ROW_COUNT|SQLLEN|通过插入、 删除或通过执行更新受影响的行数**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**. 它是驱动程序定义后*光标规范*已执行。 此字段的内容仅对语句句柄。 调用**SQLGetDiagField**与*DiagIdentifier*以外语句上 SQL_DIAG_ROW_COUNT 的句柄将返回 SQL_ERROR。 此字段中的数据也会返回以*RowCountPtr*参数**SQLRowCount**。 此字段中的数据之后重置的每个 nondiagnostic 函数调用，而返回的行计数**SQLRowCount**语句重新设置为已准备或已分配状态之前保持不变。|  
  
## <a name="record-fields"></a>记录字段  
 下表中列出的记录字段可以包含在*DiagIdentifier*自变量。  
  
|DiagIdentifier|返回类型|返回|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|一个字符串，指示此记录中定义的 SQLSTATE 值的类部分文档。 对于由 Open Group 和 ISO 调用级接口定义的所有 SQLSTATEs 情况下，其值为"ISO 9075"。 对于 ODBC 特定 SQLSTATEs （所有的那些其 SQLSTATE 类"IM"），其值是"ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|如果 SQL_DIAG_ROW_NUMBER 字段为行集或一组参数中的有效行号，则此字段将包含表示在结果集中的列号或中的参数集的参数号的值。 结果集数字始终在 1; 开始的列如果此状态记录与书签列，请字段可为零。 参数号从 1 开始。 如果状态记录不是关联的列号或参数数，它具有值 SQL_NO_COLUMN_NUMBER。 如果该驱动程序无法确定的列号或此记录关联的参数数量，则此字段具有 SQL_COLUMN_NUMBER_UNKNOWN 的值。<br /><br /> 此字段的内容仅对语句句柄。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|一个字符串，指示与相关的诊断记录的连接的名称。 此字段是驱动程序定义的。 有关与环境句柄关联的诊断数据结构和不与任何连接的诊断，则此字段为零长度字符串。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|错误或警告信息性消息。 该字段的格式中所述[诊断消息](../../../odbc/reference/develop-app/diagnostic-messages.md)。 没有为诊断消息文本无最大长度。|  
|SQL_DIAG_NATIVE|SQLINTEGER|驱动程序中的数据源特定的本机错误代码。 如果没有任何本机错误代码，该驱动程序将返回 0。|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|此字段包含行集中的行号或中的参数，状态记录与之关联集的参数号。 行号和参数号从 1 开始。 如果此状态的记录不是关联的行号或参数数目，则此字段具有 SQL_NO_ROW_NUMBER 的值。 如果该驱动程序无法确定的行号或此记录关联的参数数量，则此字段具有 SQL_ROW_NUMBER_UNKNOWN 的值。<br /><br /> 此字段的内容仅对语句句柄。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|一个字符串，指示与相关的诊断记录的服务器名称。 它是针对调用返回的值相同**SQLGetInfo** SQL_DATA_SOURCE_NAME 选项。 有关与环境句柄关联的诊断数据结构和不与任何服务器的诊断，则此字段为零长度字符串。|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|五个字符的 SQLSTATE 诊断代码。 有关详细信息，请参阅[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|带有相同的格式以及有效的值作为 SQL_DIAG_CLASS_ORIGIN，标识 SQLSTATE 代码的子类部分的定义部分的字符串。 为其返回"ODBC 3.0"ODBC 特定 SQLSTATES 如下所示：<br /><br /> 01S00，01S01，01S02 的警告，01S06，01S07，07S01，08S01，21S01，21S02，25S01，25S02，25S03，42S01，42S02，42S11，42S12，42S21，42S22，HY095、 HY097、 HY098、 HY099、 HY100、 HY101、 HY105、 HY107、 HY109、 HY110、 HY111、 HYT00、 HYT01、 IM001、 IM002、 IM003、 IM004、 IM005、 IM006，IM007、 IM008、 IM010、 IM011、 IM012。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>动态函数字段的值  
 下表描述适用于每种类型的通过调用执行 SQL 语句的 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE 值**SQLExecute**或**SQLExecDirect**. 该驱动程序可以将驱动程序定义的值添加到所列出的那些。  
  
|SQL 语句<br /><br /> 执行|值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter 域语句*|"更改域"|SQL_DIAG_ALTER_DOMAIN|  
|*alter table 语句*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*断言定义*|"创建断言"|SQL_DIAG_CREATE_ASSERTION|  
|*字符集定义*|"创建字符集"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*排序规则定义*|"创建排序规则"|SQL_DIAG_CREATE_COLLATION|  
|*创建索引语句*|"创建索引"|SQL_DIAG_CREATE_INDEX|  
|*创建 table 语句*|"创建表"|SQL_DIAG_CREATE_TABLE|  
|*创建视图语句*|"创建视图"|SQL_DIAG_CREATE_VIEW|  
|*指定的游标*|"选择游标"|SQL_DIAG_SELECT_CURSOR|  
|*delete 语句定位*|"动态删除游标"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete 语句搜索*|"删除 WHERE"|SQL_DIAG_DELETE_WHERE|  
n-定义 *|"创建域"|SQL_DIAG_CREATE_DOMAIN|  
|*drop 断言语句*|"DROP 断言"|SQL_DIAG_DROP_ASSERTION|  
|*拖放字符组 stmt*|"放置字符集"|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop 排序规则语句*|"删除排序规则"|SQL_DIAG_DROP_COLLATION|  
|*drop 域语句*|"删除域"|SQL_DIAG_DROP_DOMAIN|  
|*drop index 语句*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop 架构语句*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*drop table 语句*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*drop 转换语句*|"删除转换"|SQL_DIAG_DROP_TRANSLATION|  
|*drop view 语句*|"删除视图"|SQL_DIAG_DROP_VIEW|  
-语句 *|"授予"|SQL_DIAG_GRANT|  
|*insert 语句*|"插入"|SQL_DIAG_INSERT|  
|*ODBC 过程扩展插件*|"调用"|SQL_DIAG_ 调用|  
|*revoke 语句*|"撤消"|SQL_DIAG_REVOKE|  
|*架构定义*|"创建架构"|SQL_DIAG_CREATE_SCHEMA|  
|*翻译定义*|"创建翻译"|SQL_DIAG_CREATE_TRANSLATION|  
|*更新语句定位*|"动态更新游标"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*更新语句搜索*|"更新位置"|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*空字符串*|SQL_DIAG_UNKNOWN_STATEMENT|  
  
## <a name="sequence-of-status-records"></a>状态记录的序列  
 状态记录都将放置在基于行的行号和诊断的类型的序列。 驱动程序管理器确定最终顺序返回它所生成的状态记录。 该驱动程序确定最终顺序返回它所生成的状态记录。  
  
 如果诊断记录发布的驱动程序管理器和驱动程序，驱动程序管理器负责对数据进行排序。  
  
 如果有两个或多个状态记录，记录的序列，首先确定确定按行号。 以下规则适用于按行确定诊断记录的序列：  
  
-   与任何行并不对应的记录会显示对应的特定行的记录的前面，因为 SQL_NO_ROW_NUMBER 被定义为-1。  
  
-   行号是未知的记录显示于所有其他记录，因为 SQL_ROW_NUMBER_UNKNOWN 被定义为 – 2 之前。  
  
-   对于适用于特定行的所有记录，记录按 SQL_DIAG_ROW_NUMBER 字段中的值进行排序。 列出所有错误和警告的影响的第一个行，，然后所有错误和警告的下一个都行受影响，依次类推。  
  
> [!NOTE]  
>  ODBC 3*.x*如果驱动程序管理器不诊断队列中订购状态记录 SQLSTATE 01S01 （行中的错误） 返回的 ODBC 2*.x*驱动程序或者如果 SQLSTATE 01S01 （行中的错误） 返回的 ODBC3*.x*驱动程序时**SQLExtendedFetch**称为或**SQLSetPos**上的游标已定位与可用于调用**SQLExtendedFetch**.  
  
 在每个行，或为所有不对应的行或行数为未知，这些记录或所有这些记录的行数等于 SQL_NO_ROW_NUMBER，列出的第一个记录取决于使用一组的排序规则。 后第一条记录，影响行的其他记录的顺序是未定义。 应用程序无法假定错误后第一条记录之前警告。 应用程序应扫描完成诊断数据结构，以获取有关对函数的成功调用的完整信息。  
  
 以下规则用于确定行中的第一个记录。 具有最高级别的记录是第一条记录。 记录 （驱动程序管理器、 驱动程序、 网关，等） 的源不会被视为时排名记录。  
  
-   **错误**描述错误的状态记录具有最高的排名。 以下规则用于错误排序：  
  
    -   指明事务失败或发生故障的可能的事务的记录 outrank 所有其他记录。  
  
    -   如果两个或多个记录描述相同的错误条件，请打开组 CLI 规范 （通过 HZ 类 03） 所定义的 SQLSTATEs outrank ODBC 和驱动程序定义 SQLSTATEs。  
  
-   **实现定义无数据值**描述驱动程序定义无数据值 （类 02） 的状态记录具有第二个最高级别。  
  
-   **警告**描述警告 （类 01） 的状态记录具有最低的排名。 如果两个或多个记录描述的相同的警告条件，然后警告打开组 CLI 规范所定义的 SQLSTATEs outrank ODBC 定义和驱动程序定义 SQLSTATEs。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取多个字段的诊断数据结构|[SQLGetDiagRec 函数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

