---
title: SQLGetDiagField 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22ccf063486df9a8afc810d4adeffeb96041a8b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826195"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 函数
**符合性**  
 版本引入了： ODBC 3.0 标准符合性： ISO 92  
  
 **摘要**  
 **SQLGetDiagField**返回包含错误、 警告和状态信息的诊断数据结构 （与指定的句柄关联） 的记录的字段的当前值。  
  
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
 [输入]描述诊断为其所需的句柄的类型的句柄类型标识符。 必须是下列选项之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 只能由驱动程序管理器和驱动程序使用 SQL_HANDLE_DBC_INFO_TOKEN 句柄。 应用程序不应使用此句柄类型。 有关 SQL_HANDLE_DBC_INFO_TOKEN 详细信息，请参阅[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [输入]所指示的类型的诊断数据结构的句柄*HandleType*。 如果*HandleType*为 SQL_HANDLE_ENV，*处理*可以是共享或非共享的环境句柄。  
  
 *RecNumber*  
 [输入]指示从其应用程序查找信息的状态记录。 状态记录的编号从 1。 如果*DiagIdentifier*参数指示的诊断标头的任何字段*RecNumber*将被忽略。 如果没有，它应为大于 0。  
  
 *DiagIdentifier*  
 [输入]表示其值是要返回的诊断字段。 有关详细信息，请参阅"*DiagIdentifier*参数"部分中"注释"。  
  
 *DiagInfoPtr*  
 [输出]指向缓冲区中要返回其诊断信息。 数据类型取决于的值*DiagIdentifier*。 如果*DiagInfoPtr*是整数类型、 应用程序应使用的缓冲区 sqlulen 生成和初始化的值为 0 之前调用此函数中，作为某些驱动程序可能仅写入的低 32 位或 16 位的缓冲区和保留顺序更高的位不变。  
  
 如果*DiagInfoPtr*为 NULL， *StringLengthPtr*仍将返回的总字节数 （不包括字符数据的 null 终止字符） 可用于在通过指向的缓冲区中返回*DiagInfoPtr*。  
  
 *BufferLength*  
 [输入]如果*DiagIdentifier*是 ODBC 定义的诊断和*DiagInfoPtr*指向字符字符串或二进制缓冲区中，此参数应为的长度\* *DiagInfoPtr*. 如果*DiagIdentifier*是一个 ODBC 定义的字段和\* *DiagInfoPtr*是一个整数*BufferLength*将被忽略。 如果中的值 *\*DiagInfoPtr*是 Unicode 字符串 (在调用时**SQLGetDiagFieldW**)，则*BufferLength*参数必须为偶数。  
  
 如果*DiagIdentifier*是驱动程序定义的字段，该应用程序通过设置来指示字段到驱动程序管理器的性质*BufferLength*参数。 *BufferLength*可以具有以下值：  
  
-   如果*DiagInfoPtr*是一个字符串，指向*BufferLength*是 sql_nts; 的字符串的长度。  
  
-   如果*DiagInfoPtr* SQL_LEN_BINARY_ATTR 的结果是指向二进制缓冲区中，在应用程序的位置的指针 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果*DiagInfoPtr*指向的字符串或二进制字符串以外的值的指针*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果 *\*DiagInfoPtr*包含一个固定长度的数据类型*BufferLength*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_IS_USMALLINT，根据需要。  
  
 *StringLengthPtr*  
 [输出]指向用于返回的总字节数 （不包括 null 终止字符所需的字节数） 的缓冲区可用于在中返回\* *DiagInfoPtr*，对于字符数据。 可用来返回的字节数是否大于或等于*BufferLength*中的文本\* *DiagInfoPtr*截断为*BufferLength*减null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 sql_no_data 为止。  
  
## <a name="diagnostics"></a>诊断  
 **SQLGetDiagField**不会为其自身发送诊断记录。 它使用了以下返回值来报告其自身执行的结果：  
  
-   SQL_SUCCESS： 该函数成功地返回诊断信息。  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr*太小，无法保存请求的诊断字段。 因此，诊断字段中的数据已被截断。 若要确定发生了截断，应用程序必须进行比较*BufferLength*可用的字节，这写入的实际数目 **StringLengthPtr*。  
  
-   SQL_INVALID_HANDLE： 句柄为由*HandleType*并*处理*不是有效的句柄。  
  
-   以下项之一出现 SQL_ERROR::  
  
    -   *DiagIdentifier*参数不是有效的值之一。  
  
    -   *DiagIdentifier*参数为 SQL_DIAG_CURSOR_ROW_COUNT、 SQL_DIAG_DYNAMIC_FUNCTION、 SQL_DIAG_DYNAMIC_FUNCTION_CODE 或 SQL_DIAG_ROW_COUNT，但*处理*不是语句句柄。 （驱动程序管理器将返回此诊断。）  
  
    -   *RecNumber*参数为负数或 0 时*DiagIdentifier*所指示的诊断记录中的字段。 *RecNumber*对于标头字段将被忽略。  
  
    -   请求的值为字符串和*BufferLength*小于零。  
  
    -   使用异步通知时，句柄上的异步操作是不完整。  
  
-   SQL_NO_DATA: *RecNumber*中指定的句柄已存在的诊断记录数大于*处理。* 函数还将为任何正返回 SQL_NO_DATA *RecNumber*如果有没有可供诊断记录*处理*。  
  
## <a name="comments"></a>注释  
 应用程序通常会调用**SQLGetDiagField**得以实现的三个目标：  
  
1.  若要获取特定错误或警告信息，当函数调用返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO (或为 SQL_NEED_DATA **SQLBrowseConnect**函数)。  
  
2.  若要确定数据源中插入、 删除或更新操作已执行调用时受影响的行数**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos** （从 SQL_DIAG_ROW_COUNT 标头字段），或者如果该驱动程序可以提供此信息确定中当前打开的游标，存在的行数 (从SQL_DIAG_CURSOR_ROW_COUNT 标头字段）。  
  
3.  若要确定哪些函数通过调用执行了**SQLExecDirect**或**SQLExecute** （从 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE 标头字段）。  
  
 任何 ODBC 函数可以发布，以零个或多个诊断记录每次调用它，使应用程序可以调用**SQLGetDiagField**任何 ODBC 函数调用之后。 可以存储在任何一次的诊断记录数没有限制。 **SQLGetDiagField**检索仅在指定的诊断数据结构与最新关联的诊断信息*处理*参数。 如果应用程序调用 ODBC 函数以外**SQLGetDiagField**或**SQLGetDiagRec**，来自具有相同的句柄的上一个调用的任何诊断信息将丢失。  
  
 应用程序可以扫描所有诊断记录通过递增*RecNumber*，只要**SQLGetDiagField**返回 SQL_SUCCESS。 SQL_DIAG_NUMBER 标头字段中指示的状态记录数。 调用**SQLGetDiagField**应是非破坏性的标头和记录字段。 应用程序可以调用**SQLGetDiagField**再次更高版本，只要尚未在此期间，会在相同的句柄发布记录调用的诊断函数之外的函数从一个记录，检索字段。  
  
 应用程序可以调用**SQLGetDiagField**若要在任何时候，除了 SQL_DIAG_CURSOR_ROW_COUNT 或 SQL_DIAG_ROW_COUNT，将返回 SQL_ERROR，如果返回任何诊断字段*处理*不是语句句柄。 如果未定义，则任何其他诊断字段调用**SQLGetDiagField** （前提是不遇到任何其他诊断） 将返回 SQL_SUCCESS 并为该字段的返回未定义的值。  
  
 有关详细信息，请参阅[使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)并[实现 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 调用而不是以异步方式执行的 API 会生成 HY010"函数序列错误"。 但是，在异步操作完成之前，无法检索错误记录。  
  
## <a name="handletype-argument"></a>HandleType 参数  
 每个句柄类型可以有与之关联的诊断信息。 *HandleType*参数指示的句柄类型*处理*。  
  
 某些标头和记录字段不能句柄返回有关环境、 连接、 语句和描述符。 按照在"标头字段"和"记录字段"部分中指示该字段不适用于这些句柄。  
  
 如果*HandleType*为 SQL_HANDLE_ENV，*处理*可以是任一共享或取消共享环境句柄。  
  
 没有特定于驱动程序的标头的诊断字段应与环境句柄相关联。  
  
 仅诊断标头字段为描述符句柄定义为 SQL_DIAG_NUMBER 和 SQL_DIAG_RETURNCODE。  
  
## <a name="diagidentifier-argument"></a>DiagIdentifier 参数  
 此参数指示所需的诊断数据结构中的域的标识符。 如果*RecNumber*大于或等于 1，字段中的数据描述函数返回的诊断信息。 如果*RecNumber*为 0，则该字段是诊断数据结构的标头中，因此包含与函数调用返回的诊断信息，不到的特定信息的相关数据。  
  
 驱动程序可以定义特定于驱动程序的标头和记录字段中的诊断数据结构。  
  
 ODBC 3 *.x*应用程序使用 ODBC 2 *.x*驱动程序将能够调用**SQLGetDiagField**仅与*DiagIdentifier*SQL_DIAG_CLASS_ORIGIN、 SQL_DIAG_CLASS_SUBCLASS_ORIGIN、 SQL_DIAG_CONNECTION_NAME、 SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_NATIVE、 SQL_DIAG_NUMBER、 SQL_DIAG_RETURNCODE、 SQL_DIAG_SERVER_NAME 或 SQL_DIAG_SQLSTATE 的参数。 所有其他诊断字段将返回 SQL_ERROR。  
  
## <a name="header-fields"></a>标头字段  
 下表中列出的标头字段可以包含在*DiagIdentifier*参数。  
  
|DiagIdentifier|返回类型|返回|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|为 SQLLEN|此字段包含游标中的行的计数。 其语义取决**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、 SQL_KEYSET_CURSOR_ATTRIBUTES2 和 SQL_STATIC_CURSOR_ATTRIBUTES2，这表示该信息类型行计数是可用于每种游标类型 （以 SQL_CA2_CRC_EXACT 和 SQL_CA2_CRC_APPROXIMATE 位为单位）。<br /><br /> 此字段的内容定义仅对语句句柄和之后才**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**已调用。 调用**SQLGetDiagField**与*DiagIdentifier*以外语句上 SQL_DIAG_CURSOR_ROW_COUNT 的句柄将返回 SQL_ERROR。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|这是一个字符串，描述基础函数执行的 SQL 语句。 （请参阅"字段的值动态函数，"更高版本在此部分中，特定的值。）仅对语句句柄和调用后，才定义此字段的内容**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**。 调用**SQLGetDiagField**与*DiagIdentifier*以外语句上 SQL_DIAG_DYNAMIC_FUNCTION 的句柄将返回 SQL_ERROR。 此字段的值在调用之前不明确**SQLExecute**或**SQLExecDirect**。|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|这是介绍基础函数已执行的 SQL 语句的数值代码。 （请参阅"值的动态函数字段，"更高版本在此部分中，特定值。）仅对语句句柄和调用后，才定义此字段的内容**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**。 调用**SQLGetDiagField**与*DiagIdentifier*以外语句上 SQL_DIAG_DYNAMIC_FUNCTION_CODE 的句柄将返回 SQL_ERROR。 此字段的值在调用之前不明确**SQLExecute**或**SQLExecDirect**。|  
|SQL_DIAG_NUMBER|SQLINTEGER|可用于指定句柄的状态记录数。|  
|SQL_DIAG_RETURNCODE|SQLRETURN|函数返回的返回代码。 有关返回代码的列表，请参阅[返回代码](../../../odbc/reference/develop-app/return-codes-odbc.md)。 该驱动程序不需要实现 SQL_DIAG_RETURNCODE;它始终被实现由驱动程序管理器。 如果尚未在调用任何函数*处理*，将返回 SQL_SUCCESS SQL_DIAG_RETURNCODE。|  
|SQL_DIAG_ROW_COUNT|为 SQLLEN|受影响的插入、 删除或更新执行的行数**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**. 它是驱动程序定义的后*游标规范*已执行。 此字段的内容仅对语句句柄。 调用**SQLGetDiagField**与*DiagIdentifier*以外语句上 SQL_DIAG_ROW_COUNT 的句柄将返回 SQL_ERROR。 此字段中的数据也会返回以*RowCountPtr*的参数**SQLRowCount**。 此字段中的数据之后重置每个 nondiagnostic 函数调用，而返回的行计数**SQLRowCount**保持不变，直到该语句将重新设置为已准备好或已分配状态。|  
  
## <a name="record-fields"></a>记录字段  
 下表中列出的记录字段可以包含在*DiagIdentifier*参数。  
  
|DiagIdentifier|返回类型|返回|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|一个字符串，指示此记录中定义的 SQLSTATE 值的类部分的文档。 其值为"ISO 9075"为所有 SQLSTATEs 由 Open Group 和 ISO 调用级别接口定义。 对于特定于 ODBC 的 SQLSTATEs （所有这些其 SQLSTATE 类是"IM"），其值是"ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|如果 SQL_DIAG_ROW_NUMBER 字段为行集或一组参数的有效行数字，则此字段将包含表示在结果集中的列号或中的参数集的参数编号的值。 结果集的列在 1; 始终启动数字如果此状态记录与书签列，请在字段可以为零。 参数编号从 1 开始。 如果状态记录不是关联的列号或参数数目，它具有值 SQL_NO_COLUMN_NUMBER。 如果该驱动程序无法确定列数或此记录关联的参数数目，此字段具有 SQL_COLUMN_NUMBER_UNKNOWN 的值。<br /><br /> 此字段的内容仅对语句句柄。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|一个字符串，表示与诊断记录的连接的名称。 此字段是驱动程序定义的。 有关与环境句柄关联的诊断数据结构和不相关的任何连接的诊断，此字段是一个零长度字符串。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|发生错误或警告信息性消息。 该字段的格式中所述[诊断消息](../../../odbc/reference/develop-app/diagnostic-messages.md)。 没有最大长度为诊断消息文本。|  
|SQL_DIAG_NATIVE|SQLINTEGER|驱动程序/数据源特定于本机错误代码。 如果没有任何本机错误代码，该驱动程序将返回 0。|  
|SQL_DIAG_ROW_NUMBER|为 SQLLEN|此字段包含的行集中的行号或状态记录与之关联的参数集中的参数编号。 行号和参数编号从 1 开始。 如果此状态记录不是关联的行号或参数数目，此字段具有 SQL_NO_ROW_NUMBER 的值。 如果该驱动程序无法确定的行号或此记录关联的参数数目，此字段具有 SQL_ROW_NUMBER_UNKNOWN 的值。<br /><br /> 此字段的内容仅对语句句柄。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|一个字符串，表示与诊断记录的服务器名称。 它是对的调用返回的值相同**SQLGetInfo** SQL_DATA_SOURCE_NAME 选项。 与环境句柄关联的诊断数据结构以及与任何服务器不相关的诊断，则此字段是一个零长度字符串。|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|5 个字符的 SQLSTATE 诊断代码。 有关详细信息，请参阅[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|具有相同的格式和有效的值作为 SQL_DIAG_CLASS_ORIGIN，标识 SQLSTATE 代码的子类部分定义部分的字符串。 为其返回"ODBC 3.0"特定于 ODBC 的 SQLSTATES 如下所示：<br /><br /> 01S00，01S01，01S02，01S06，01S07，07S01，08S01 的形式，21S01，21S02，25S01，25S02，25S03，42S01，42S02，42S11，42S12，42S21，42S22，HY095、 HY097、 HY098、 HY099、 HY100、 HY101、 HY105、 HY107、 HY109、 HY110、 HY111、 HYT00、 HYT01、 IM001、 IM002、 IM003、 IM004、 IM005、 IM006，IM007、 IM008、 IM010、 IM011、 IM012。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>动态函数字段的值  
 下表描述了适用于每种类型的调用由执行 SQL 语句的 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE 值**SQLExecute**或**SQLExecDirect**. 该驱动程序可以将驱动程序定义的值添加到列出的内容。  
  
|SQL 语句<br /><br /> 执行|值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*更改域语句*|"更改域"|SQL_DIAG_ALTER_DOMAIN|  
|*alter table 语句*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*断言定义*|"创建断言"|SQL_DIAG_CREATE_ASSERTION|  
|*字符集定义*|"创建字符集"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*排序规则定义*|"创建排序规则"|SQL_DIAG_CREATE_COLLATION|  
|*create index 语句*|"创建索引"|SQL_DIAG_CREATE_INDEX|  
|*create table 语句*|"创建表"|SQL_DIAG_CREATE_TABLE|  
|*创建视图语句*|"创建视图"|SQL_DIAG_CREATE_VIEW|  
|*指定的游标*|"选择光标"|SQL_DIAG_SELECT_CURSOR|  
|*delete 语句定位*|"动态删除游标"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete 语句搜索*|"删除位置"|SQL_DIAG_DELETE_WHERE|  
n-定义 *|"创建域"|SQL_DIAG_CREATE_DOMAIN|  
|*drop 断言语句*|"放置断言"|SQL_DIAG_DROP_ASSERTION|  
|*删除字符组 stmt*|"DROP 字符集"|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop 排序规则语句*|"删除排序规则"|SQL_DIAG_DROP_COLLATION|  
|*drop 域语句*|"删除域"|SQL_DIAG_DROP_DOMAIN|  
|*drop index 语句*|"删除索引"|SQL_DIAG_DROP_INDEX|  
|*drop schema 语句*|"删除架构"|SQL_DIAG_DROP_SCHEMA|  
|*drop table 语句*|"删除表"|SQL_DIAG_DROP_TABLE|  
|*drop 转换语句*|"删除转换"|SQL_DIAG_DROP_TRANSLATION|  
|*drop view 语句*|"删除视图"|SQL_DIAG_DROP_VIEW|  
-语句 *|"授予"|SQL_DIAG_GRANT|  
|*insert 语句*|"插入"|SQL_DIAG_INSERT|  
|*ODBC 过程扩展插件*|"CALL"|SQL_DIAG_ 调用|  
|*revoke 语句*|"撤销"|SQL_DIAG_REVOKE|  
|*架构定义*|"创建架构"|SQL_DIAG_CREATE_SCHEMA|  
|*转换定义*|"创建转换"|SQL_DIAG_CREATE_TRANSLATION|  
|*update 语句定位*|"动态更新游标"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update 语句搜索*|"更新的位置"|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*空字符串*|SQL_DIAG_UNKNOWN_STATEMENT|  
  
## <a name="sequence-of-status-records"></a>状态记录的序列  
 状态记录都将放置在基于行的行号和诊断的类型的序列。 驱动程序管理器确定要返回其生成的状态记录中的最终顺序。 该驱动程序确定要返回其生成的状态记录中的最终顺序。  
  
 如果诊断记录所发送的驱动程序管理器和驱动程序，驱动程序管理器负责对数据进行排序。  
  
 如果有两个或多个状态记录，首先确定记录序列确定按行号。 以下规则适用于按行确定诊断记录的序列：  
  
-   任何行不对应的记录显示在对应于特定行的记录之前，因为 SQL_NO_ROW_NUMBER 被定义为 – 1。  
  
-   对于其中的行号是未知的记录会显示前面所有其他记录，因为 SQL_ROW_NUMBER_UNKNOWN 被定义为 – 2。  
  
-   对于适用于特定行的所有记录，记录按 SQL_DIAG_ROW_NUMBER 字段中的值进行排序。 列出所有错误和警告的第一个受影响的行，然后所有错误和警告的下一个都行受影响，等等。  
  
> [!NOTE]  
>  ODBC 3 *.x*驱动程序管理器不会进行排序状态记录诊断的队列中如果 SQLSTATE 01S01 （行中的错误） 返回的 ODBC 2 *.x*驱动程序或者如果 SQLSTATE 01S01 （行中的错误） 返回的 ODBC3 *.x*驱动程序时**SQLExtendedFetch**称为或**SQLSetPos**称为已定位与对游标**SQLExtendedFetch**.  
  
 在每个行中，或为所有不对应的行或行号为未知的这些记录或行数等于 SQL_NO_ROW_NUMBER 的所有记录，列出的第一个记录取决于通过使用一组的排序规则。 后第一条记录，影响行的其他记录的顺序是未定义。 应用程序不能假定错误后第一条记录之前警告。 应用程序应扫描以获取有关的失败调用的函数的完整信息的完整的诊断数据结构。  
  
 使用以下规则来确定行中的第一个记录。 具有最高排名的记录是第一条记录。 记录 （驱动程序管理器、 驱动程序、 网关，等） 的源不被视为时排名记录。  
  
-   **错误**描述错误的状态记录具有最高排名。 以下规则用于对错误进行排序：  
  
    -   指示事务失败或发生故障的可能的事务的记录 outrank 所有其他记录。  
  
    -   如果两个或多个记录描述相同的错误条件，请打开组 CLI 规范 （通过 HZ 类 03） 所定义的 SQLSTATEs outrank ODBC 和驱动程序定义 SQLSTATEs。  
  
-   **无数据值定义实现**描述驱动程序定义的无数据值 （类 02） 的状态记录具有第二个最高排名。  
  
-   **警告**描述警告 （类 01） 的状态记录具有最低排名。 如果两个或多个记录描述了相同的警告条件，然后警告打开组 CLI 规范所定义的 SQLSTATEs outrank ODBC 定义和驱动程序定义 SQLSTATEs。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取多个字段的诊断数据结构|[SQLGetDiagRec 函数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
