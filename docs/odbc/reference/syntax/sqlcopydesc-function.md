---
title: SQLCopyDesc 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e165ca48af3b634f1dcbe80c05c83f2c872d1b01
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642775"
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 函数
**符合性**  
 版本引入了： ODBC 3.0 标准符合性： ISO 92  
  
 **摘要**  
 **SQLCopyDesc**将描述符信息从一个描述符句柄复制到另一个。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>参数  
 *SourceDescHandle*  
 [输入]源描述符句柄。  
  
 *TargetDescHandle*  
 [输入]目标描述符句柄。 *TargetDescHandle*参数可以是应用程序描述符或 IPD 的句柄。 *TargetDescHandle*不能设置为 IRD 的句柄或**SQLCopyDesc**将返回 SQLSTATE HY016 （不能修改实现行描述符）。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLCopyDesc**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_DESC 和一个*处理*的*TargetDescHandle*。 如果无效*SourceDescHandle*传递将在调用中，返回 SQL_INVALID_HANDLE，但会返回任何 SQLSTATE。 下表列出了通常返回的 SQLSTATE 值**SQLCopyDesc** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
 当返回错误，在调用**SQLCopyDesc**立即中止，和中的字段的内容*TargetDescHandle*描述符是不确定。  
  
 因为**SQLCopyDesc**可通过调用来实现**SQLGetDescField**并**SQLSetDescField**， **SQLCopyDesc**可能会返回返回的 SQLSTATEs **SQLGetDescField**或**SQLSetDescField**。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY007|未准备关联的语句|*SourceDescHandle* IRD 的关联和关联的语句句柄当时不处于已准备或执行状态。|  
|HY010|函数序列错误|中 (DM) 描述符句柄*SourceDescHandle*或*TargetDescHandle*与关联*StatementHandle*为其正在以异步方式执行的函数 （非此一个） 调用时，仍在执行时调用此函数。<br /><br /> 中 (DM) 描述符句柄*SourceDescHandle*或*TargetDescHandle*与关联*StatementHandle*为其**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**调用和返回 SQL_NEED_DATA。 数据已发送的所有执行时数据参数或列之前调用此函数。<br /><br /> (DM) 为与之关联的连接句柄调用以异步方式执行的函数*SourceDescHandle*或*TargetDescHandle*。 此异步函数仍在执行时**SQLCopyDesc**调用函数。<br /><br /> （数据挖掘） **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**一个与相关联的语句句柄调用*SourceDescHandle*或*TargetDescHandle*和返回 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY016|无法修改实现行描述符|*TargetDescHandle* IRD 与相关联。|  
|HY021|描述符信息不一致|一致性检查期间检查的描述符信息不是一致的。 详细信息，请参阅"一致性检查"中**SQLSetDescField**。|  
|HY092|属性/选项标识符无效|在调用**SQLCopyDesc**提示调用**SQLSetDescField**，但 *\*ValuePtr*不是有效的*FieldIdentifier*上的参数*TargetDescHandle*。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*SourceDescHandle*或*TargetDescHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 调用**SQLCopyDesc**副本的源描述符字段的句柄目标描述符句柄。 可以复制字段，仅对应用程序描述符或 IPD，而不是属于 IRD。 可以从应用程序或实现描述符复制字段。  
  
 仅当语句句柄处于已准备或执行状态，则可以从 IRD 复制字段否则，该函数将返回 SQLSTATE HY007 （未准备关联语句）。  
  
 可以从 IPD 复制字段，指示已准备语句。 如果使用动态参数的 SQL 语句已准备好支持且启用了自动填充 IPD，由驱动程序填充 IPD。 当**SQLCopyDesc**被调用，作为 IPD *SourceDescHandle*，填充的字段被复制。 如果驱动程序未填充 IPD，最初在 IPD 字段的内容复制。  
  
 复制描述符 SQL_DESC_ALLOC_TYPE （它指定是否描述符句柄已自动或显式分配），除的所有字段，指示为目标描述符定义字段。 复制的字段会覆盖现有字段。  
  
 该驱动程序将复制所有描述符字段，如果*SourceDescHandle*并*TargetDescHandle*参数是与相同的驱动程序相关联，即使驱动程序位于两个不同的连接或环境。 如果*SourceDescHandle*并*TargetDescHandle*参数都与不同的驱动程序、 驱动程序管理器将复制 ODBC 定义的字段，但不会复制驱动程序定义的字段或字段ODBC 类型描述符的未定义的。  
  
 在调用**SQLCopyDesc**出错时，将立即中止。  
  
 复制 SQL_DESC_DATA_PTR 字段时，目标描述符上执行一致性检查。 如果一致性检查失败，SQLSTATE HY021 返回 （描述符信息不一致） 以及对调用**SQLCopyDesc**立即中止。 一致性检查的详细信息，请参阅"一致性检查"中[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 即使连接是不同的环境下，可以跨连接复制描述符句柄。 如果驱动程序管理器检测到源和目标描述符句柄不属于同一个连接，并将两个连接属于单独的驱动程序时，它实现**SQLCopyDesc**通过执行由字段使用复制**SQLGetDescField**并**SQLSetDescField**。  
  
 当**SQLCopyDesc**使用调用*SourceDescHandle*上一个驱动程序和一个*TargetDescHandle*上另一个驱动程序，错误队列中的*SourceDescHandle*清除。 这是因为**SQLCopyDesc**在这种情况下实现通过调用**SQLGetDescField**并**SQLSetDescField**。  
  
> [!NOTE]  
>  应用程序可能能够将使用一个显式分配的描述符句柄相关联*StatementHandle*，而不是调用**SQLCopyDesc**将字段从一个描述符复制到另一个。 显式分配的描述符可以与另一个相关联*StatementHandle*同一*ConnectionHandle*通过设置 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 语句属性的显式分配的描述符句柄。 完成此操作后， **SQLCopyDesc**无需调用将描述符字段值从一个描述符复制到另一个。 不能与之关联的描述符句柄*StatementHandle*在另一台*ConnectionHandle*，但是; 上使用相同的描述符字段值*StatementHandles*上不同*ConnectionHandles*， **SQLCopyDesc**必须调用。  
  
 描述符标头或记录中字段的说明，请参阅[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="copying-rows-between-tables"></a>复制表之间的行  
 应用程序可能会数据从一个表复制到另一个而不复制应用程序级别的数据。 若要执行此操作，该应用程序的同一个数据缓冲区和绑定描述符信息到提取数据的语句和语句将数据插入到副本。 这可以通过共享应用程序描述符 （作为一条语句到 ARD 和 APD 中另一个绑定是显式分配的描述符） 或通过使用实现**SQLCopyDesc**复制 ARD 之间的绑定和两个语句的 APD。 如果该语句在连接的不同**SQLCopyDesc**必须使用。 此外， **SQLCopyDesc**必须调用复制 IRD 和 IPD 的两个语句之间的绑定。 在复制跨同一个连接上的语句时，调用的驱动程序返回 SQL_ACTIVE_STATEMENTS 信息类型**SQLGetInfo**必须是大于 1 的此操作才能成功。 （这不是这种情况时在连接之间复制。）  
  
### <a name="code-example"></a>代码示例  
 在以下示例中，描述符操作用于将 PartsSource 表的字段复制到 PartsCopy 表。 PartsSource 表的内容提取到行集缓冲区*hstmt0*。 在使用这些值作为参数的 INSERT 语句*hstmt1*来填充 PartsCopy 表的列。 若要执行此操作的 IRD 字段*hstmt0*复制到的 IPD 的字段*hstmt1*，和字段的 ARD *hstmt0*复制到的字段的APD*hstmt1*。 使用**SQLSetDescField**以 IRD 字段中具有输出参数的语句复制到 IPD 字段所需的输入的参数时 IPD 的 SQL_DESC_PARAMETER_TYPE 属性设置为 SQL_PARAM_INPUT。  
  
```  
#define ROWS 100  
#define DESC_LEN 50  
#define SQL_SUCCEEDED(rc) (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO)  
  
// Template for a row  
typedef struct {  
   SQLINTEGER   sPartID;  
   SQLINTEGER   cbPartID;  
   SQLUCHAR     szDescription[DESC_LENGTH];  
   SQLINTEGER   cbDescription;  
   REAL         sPrice;  
   SQLINTEGER   cbPrice;  
} PartsSource;  
  
PartsSource    rget[ROWS];          // rowset buffer  
SQLUSMALLINT   sts_ptr[ROWS];       // status pointer  
SQLHSTMT       hstmt0, hstmt1;  
SQLHDESC       hArd0, hIrd0, hApd1, hIpd1;  
  
// ARD and IRD of hstmt0  
SQLGetStmtAttr(hstmt0, SQL_ATTR_APP_ROW_DESC, &hArd0, 0, NULL);  
SQLGetStmtAttr(hstmt0, SQL_ATTR_IMP_ROW_DESC, &hIrd0, 0, NULL);  
  
// APD and IPD of hstmt1  
SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_PARAM_DESC, &hApd1, 0, NULL);  
SQLGetStmtAttr(hstmt1, SQL_ATTR_IMP_PARAM_DESC, &hIpd1, 0, NULL);  
  
// Use row-wise binding on hstmt0 to fetch rows  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER) sizeof(PartsSource), 0);  
  
// Set rowset size for hstmt0  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
  
// Execute a select statement  
SQLExecDirect(hstmt0, "SELECT PARTID, DESCRIPTION, PRICE FROM PARTS ORDER BY 3, 1, 2"",  
               SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt0, 1, SQL_C_SLONG, rget[0].sPartID, 0,   
   &rget[0].cbPartID);  
SQLBindCol(hstmt0, 2, SQL_C_CHAR, &rget[0].szDescription, DESC_LEN,   
   &rget[0].cbDescription);  
SQLBindCol(hstmt0, 3, SQL_C_FLOAT, rget[0].sPrice,   
   0, &rget[0].cbPrice);  
  
// Perform parameter bindings on hstmt1.   
SQLCopyDesc(hArd0, hApd1);  
SQLCopyDesc(hIrd0, hIpd1);  
  
// Set the array status pointer of IRD  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_STATUS_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the ARRAY_STATUS_PTR field of APD to be the same  
// as that in IRD.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_PARAM_OPERATION_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the hIpd1 records as input parameters  
rc = SQLSetDescField(hIpd1, 1, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 2, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 3, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
  
// Prepare an insert statement on hstmt1. PartsCopy is a copy of  
// PartsSource  
SQLPrepare(hstmt1, "INSERT INTO PARTS_COPY VALUES (?, ?, ?)", SQL_NTS);  
  
// In a loop, fetch a rowset, and copy the fetched rowset to PARTS_COPY  
  
rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
while (SQL_SUCCEEDED(rc)) {  
  
   // After the call to SQLFetchScroll, the status array has row   
   // statuses. This array is used as input status in the APD  
   // and hence determines which elements of the rowset buffer  
   // are inserted.  
   SQLExecute(hstmt1);  
  
   rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
} // while  
```  
  
### <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单一的描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
