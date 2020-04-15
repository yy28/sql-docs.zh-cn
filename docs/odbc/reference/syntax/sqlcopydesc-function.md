---
title: SQLCopyDesc 功能 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef1fa5b319e8d72d5b70e6f2010e493eec6f844a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301224"
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLCopyDesc**将描述符信息从一个描述符句柄复制到另一个描述符句柄。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>参数  
 *来源DescHandle*  
 [输入]源描述符句柄。  
  
 *目标德斯克德尔*  
 [输入]目标描述符句柄。 *TargetDescHandle*参数可以是应用程序描述符或 IPD 的句柄。 *TargetDescHandle*无法设置为 IRD 的句柄，或者**SQLCopyDesc**将返回 SQLSTATE HY016（无法修改实现行描述符）。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLCopyDesc**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_DESC的*句柄类型*和目标*DescHandle的句柄*。 *Handle* 如果在呼叫中传递了无效的*SourceDescHandle，* 将返回SQL_INVALID_HANDLE，但不会返回 SQLSTATE。 下表列出了**SQLCopyDesc**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
 返回错误后，将立即中止对**SQLCopyDesc**的调用，并且未定义*TargetDescHandle*描述符中字段的内容。  
  
 由于**SQLCopyDesc**可以通过调用**SQLGetDescField**和**SQLSetDescField**实现，因此**SQLCopyDesc**可能会返回**SQLGetDescField**或**SQLSetDescField**返回的 SQLStatEs。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY007|未准备关联语句|*SourceDescHandle*与 IRD 相关联，关联的语句句柄未处于准备或执行状态。|  
|HY010|函数序列错误|（DM） *SourceDescHandle*或*TargetDescHandle*中的描述符句柄与*语句句柄相关联，* 其中调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。<br /><br /> （DM） *SourceDescHandle*或*TargetDescHandle*中的描述符句柄与*一个语句句柄*相关联，SQL_NEED_DATA调用 SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos。** **SQLExecute** **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） 对于与*SourceDescHandle*或*TargetDescHandle*关联的连接句柄，调用了异步执行函数。 调用**SQLCopyDesc**函数时，此异步函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore结果**被调用为与*SourceDescHandle 或 TargetDescHandle*关联的语句句柄之一，并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecute** *TargetDescHandle* 在检索所有流参数的数据之前，已调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY016|无法修改实现行描述符|*TargetDescHandle*与 IRD 相关联。|  
|HY021|描述符信息不一致|在一致性检查期间检查的描述符信息不一致。 有关详细信息，请参阅**SQLSetDescField**中的"一致性检查"。|  
|HY092|无效属性/选项标识符|对**SQLCopyDesc 的**调用提示调用**SQLSetDescField，** 但*\*ValuePtr*对*TargetDescHandle*上的*字段标识符*参数无效。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*源DescHandle*或*TargetDescHandle*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 对**SQLCopyDesc 的**调用将源描述符句柄的字段复制到目标描述符句柄。 字段只能复制到应用程序描述符或 IPD，但不能复制到 IRD。 可以从应用程序或实现描述符复制字段。  
  
 仅当语句句柄处于准备或执行状态时，才能从 IRD 复制字段;否则，函数将返回 SQLSTATE HY007（未准备关联语句）。  
  
 无论是否已准备语句，都可以从 IPD 复制字段。 如果已准备具有动态参数的 SQL 语句，并且支持并启用 IPD 的自动填充，则驱动程序将填充 IPD。 当**SQLCopyDesc**调用 IPD 作为*源DescHandle时*，将复制填充的字段。 如果驱动程序未填充 IPD，则复制最初在 IPD 中使用的字段的内容。  
  
 描述符的所有字段（SQL_DESC_ALLOC_TYPE（指定描述符句柄是自动分配还是显式分配）除外，无论是否为目标描述符定义该字段，都将复制该字段。 复制的字段覆盖现有字段。  
  
 如果*SourceDescHandle*和*TargetDescHandle*参数与同一驱动程序关联，即使驱动程序位于两个不同的连接或环境中，驱动程序也会复制所有描述符字段。 如果*SourceDescHandle*和*TargetDescHandle*参数与不同的驱动程序相关联，则驱动程序管理器将复制 ODBC 定义的字段，但不会复制由 ODBC 为描述符类型定义的驱动程序定义的字段。  
  
 如果发生错误，将立即中止对**SQLCopyDesc 的**调用。  
  
 复制SQL_DESC_DATA_PTR字段时，对目标描述符执行一致性检查。 如果一致性检查失败，将返回 SQLSTATE HY021（不一致的描述符信息），并立即中止对**SQLCopyDesc 的**调用。 有关一致性检查的详细信息，请参阅[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)中的"一致性检查"。  
  
 描述符句柄可以跨连接复制，即使连接位于不同的环境中也是如此。 如果驱动程序管理器检测到源和目标描述符句柄不属于同一连接，并且两个连接属于单独的驱动程序，则它通过使用**SQLGetDescField**和**SQLSetDescField**执行逐字段复制来实现**SQLCopyDesc。**  
  
 当**SQLCopyDesc**调用一个驱动程序上的*SourceDescHandle*和另一个驱动程序上的*TargetDescHandle*时，*将清除 SourceDescHandle*的错误队列。 这是因为在这种情况下 **，SQLCopyDesc**是通过对**SQLGetDescField**和**SQLSetDescField**的调用实现的。  
  
> [!NOTE]  
>  应用程序也许能够将显式分配的描述符句柄与*语句句柄*相关联，而不是调用**SQLCopyDesc**将字段从一个描述符复制到另一个描述符。 通过将SQL_ATTR_APP_ROW_DESC或SQL_ATTR_APP_PARAM_DESC语句属性设置为显式分配的描述符的句柄，可以与同一*连接句柄*上的另一个*语句句柄*关联显式分配的描述符。 完成此操作后，不必调用**SQLCopyDesc**即可将描述符字段值从一个描述符复制到另一个描述符。 但是，描述符句柄不能与另一个*ConnectHandle*上的*语句句柄*关联;要在不同的*连接句柄*上的*语句句柄*上使用相同的描述符字段值，必须调用**SQLCopyDesc。**  
  
 有关描述符标题或记录中的字段的说明，请参阅[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="copying-rows-between-tables"></a>在表之间复制行  
 应用程序可以将数据从一个表复制到另一个表，而无需在应用程序级别复制数据。 为此，应用程序将相同的数据缓冲区和描述符信息绑定到获取数据的语句以及将数据插入到副本中的语句。 这可以通过共享应用程序描述符（将显式分配的描述符绑定为 ARD 到另一个语句中的 APD）或使用**SQLCopyDesc**复制两个语句的 ARD 和 APD 之间的绑定来实现。 如果语句位于不同的连接上，则必须使用**SQLCopyDesc。** 此外，必须调用**SQLCopyDesc**来复制 IRD 和两个语句的 IPD 之间的绑定。 在同一连接上跨语句复制时 SQL_ACTIVE_STATEMENTS，驱动程序返回的调用**SQLGetInfo**的信息类型必须大于 1 才能成功。 （跨连接复制时不是这样。  
  
### <a name="code-example"></a>代码示例  
 在下面的示例中，描述符操作用于将零件源表的字段复制到"零件复制"表中。 零件源表的内容被提取到*hstmt0*中的排集缓冲区中。 这些值用作*hstmt1*上的 INSERT 语句的参数，以填充零件复制表的列。 为此 *，hstmt0*的 IRD 字段被复制到*hstmt1*的 IPD 字段，并将*hstmt0*的 ARD 字段复制到*hstmt1*的 APD 字段。 当您将 IRD 字段从具有输出参数的语句复制到需要输入参数的 IPD 字段时，使用**SQLSetDescField**将 IPD 的SQL_DESC_PARAMETER_TYPE属性设置为SQL_PARAM_INPUT。  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单个描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
