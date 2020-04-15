---
title: SQLSetDescRec 功能 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b29879ff7635d6eb7d5a0f7489ff3994758d4a35
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299527"
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetDescRec**函数设置多个描述符字段，这些描述符字段会影响绑定到列或参数数据的数据类型和缓冲区。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLSetDescRec(  
      SQLHDESC      DescriptorHandle,  
      SQLSMALLINT   RecNumber,  
      SQLSMALLINT   Type,  
      SQLSMALLINT   SubType,  
      SQLLEN        Length,  
      SQLSMALLINT   Precision,  
      SQLSMALLINT   Scale,  
      SQLPOINTER    DataPtr,  
      SQLLEN *      StringLengthPtr,  
      SQLLEN *      IndicatorPtr);  
```  
  
## <a name="arguments"></a>参数  
 *DescriptorHandle*  
 [输入]描述符句柄。 这不能是 IRD 句柄。  
  
 *RecNumber*  
 [输入]指示包含要设置的字段的描述符记录。 描述符记录从 0 编号，记录编号 0 是书签记录。 此参数必须等于或大于 0。 如果*RecNumber*大于SQL_DESC_COUNT的值，SQL_DESC_COUNTis更改为*RecNumber*的值 。  
  
 *Type*  
 [输入]要为描述符记录设置SQL_DESC_TYPE字段的值。  
  
 *亚*  
 [输入]对于类型为SQL_DATETIME或SQL_INTERVAL的记录，这是要设置SQL_DESC_DATETIME_INTERVAL_CODE字段的值。  
  
 *长度*  
 [输入]要为描述符记录设置SQL_DESC_OCTET_LENGTH字段的值。  
  
 *精度*  
 [输入]要为描述符记录设置SQL_DESC_PRECISION字段的值。  
  
 *缩放*  
 [输入]要为描述符记录设置SQL_DESC_SCALE字段的值。  
  
 *数据Ptr*  
 [延迟输入或输出]要为描述符记录设置SQL_DESC_DATA_PTR字段的值。 *DataPtr*可以设置为空指针。  
  
 *DataPtr*参数可以设置为空指针，以将SQL_DESC_DATA_PTR字段设置为空指针。 如果*描述符处理*参数中的句柄与 ARD 关联，则取消绑定列。  
  
 *字符串长度 Ptr*  
 [延迟输入或输出]要为描述符记录设置SQL_DESC_OCTET_LENGTH_PTR字段的值。 *可以将 StringLengthPtr*设置为空指针，以将SQL_DESC_OCTET_LENGTH_PTR字段设置为空指针。  
  
 *指标Ptr*  
 [延迟输入或输出]要为描述符记录设置SQL_DESC_INDICATOR_PTR字段的值。 *指标Ptr*可以设置为空指针，以将SQL_DESC_INDICATOR_PTR字段设置为空指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetDescRec**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有*Handle*SQL_HANDLE_DESC的*句柄类型*和*描述符句柄*。 下表列出了**SQLSetDescRec**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07009|无效描述符索引|*RecNumber*参数设置为 0，*描述符句柄*引用 IPD 句柄。<br /><br /> *RecNumber*参数小于 0。<br /><br /> *RecNumber*参数大于数据源可以支持的最大列或参数数，并且*描述符句柄*参数是 APD、IPD 或 ARD。<br /><br /> *RecNumber*参数等于 0，*描述符句柄*参数引用隐式分配的 APD。 （显式分配的应用程序描述符不会发生此错误，因为在执行时间之前，不知道显式分配的应用程序描述符是 APD 还是 ARD。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM）*描述符处理*与*语句句柄*相关联，在调用此函数时，调用了异步执行函数（不是此函数），并且仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*，其中*描述符句柄*SQL_NEED_DATA关联并返回。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） 对于与*描述符句柄*关联的连接句柄，调用了异步执行函数。 调用**SQLSetDescRec**函数时，此 aynchronous 函数仍在执行。<br /><br /> （DM） **SQLExecute、SQLExecDirect**或**SQLMore结果**被调用为与*描述符句柄*关联的语句句柄之一，并返回SQL_PARAM_DATA_AVAILABLE。 **SQLExecute** 在检索所有流参数的数据之前，已调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY016|无法修改实现行描述符|*描述符处理*参数与 IRD 相关联。|  
|HY021|描述符信息不一致|*"类型"* 字段或与描述符中SQL_DESC_TYPE字段关联的任何其他字段无效或一致。<br /><br /> 在一致性检查期间检查的描述符信息不一致。 （请参阅本节后面的"一致性检查"。|  
|HY090|无效的字符串或缓冲区长度|（DM） 驱动程序是 ODBC *2.x*驱动程序，描述符是 ARD，*列号*参数设置为 0，为参数*BufferLength*指定的值不等于 4。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*描述符处理*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLSetDescRec**为单个列或参数设置以下字段：  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE（对于其类型为SQL_DATETIME或SQL_INTERVAL的记录）  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  如果对**SQLSetDescRec**的调用失败，则*RecNumber*参数标识的描述符记录的内容将未定义。  
  
 绑定列或参数时 **，SQLSetDescCRec**允许您更改影响绑定的多个字段，而无需调用**SQLBindCol**或**SQLBind参数**或对**SQLSetDescField**进行多次调用。 **SQLSetDescRec**可以在描述符上设置当前未与语句关联的字段。 请注意 **，SQLBind参数**设置的字段比**SQLSetDescRec**多，可以在一个调用中同时设置 APD 和 IPD 上的字段，并且不需要描述符句柄。  
  
> [!NOTE]  
>  在调用使用*RecNumber*参数为 0 的**SQLSetDescRec**来设置书签字段之前，应始终设置语句属性SQL_ATTR_USE_BOOKMARKS。 虽然这不是强制性的，但强烈建议这样做。  
  
## <a name="consistency-checks"></a>一致性检查  
 每当应用程序设置 APD、ARD 或 IPD 的SQL_DESC_DATA_PTR字段时，驱动程序会自动执行一致性检查。 如果任何字段与其他字段不一致 **，SQLSetDescRec**将返回 SQLSTATE HY021（描述符信息不一致）。  
  
 每当应用程序设置 APD、ARD 或 IPD SQL_DESC_DATA_PTR字段时，驱动程序都会检查SQL_DESC_TYPE字段的值以及适用于该SQL_DESC_TYPE字段的值是否有效且一致。 当调用**SQLBind 参数**或**SQLBindCol**或调用**SQLSetDescRec**进行 APD、ARD 或 IPD 时，始终执行此检查。 此一致性检查包括以下对描述符字段的检查：  
  
-   SQL_DESC_TYPE字段必须是有效的 ODBC C 或 SQL 类型之一，或者特定于驱动程序的 SQL 类型。 SQL_DESC_CONCISE_TYPE字段必须是有效的 ODBC C 或 SQL 类型之一，或特定于驱动程序的 C 或 SQL 类型，包括简洁的日期时间和间隔类型。  
  
-   如果SQL_DESC_TYPE记录字段是SQL_DATETIME或SQL_INTERVAL，则SQL_DESC_DATETIME_INTERVAL_CODE字段必须是有效的日期时间或间隔代码之一。 （请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中SQL_DESC_DATETIME_INTERVAL_CODE字段的说明。  
  
-   如果SQL_DESC_TYPE字段指示数值类型，则SQL_DESC_PRECISION和SQL_DESC_SCALE字段将验证为有效。  
  
-   如果SQL_DESC_CONCISE_TYPE字段是时间戳数据类型、具有秒分量的间隔类型或具有时间分量的间隔数据类型之一，则SQL_DESC_PRECISION字段将验证为有效的秒精度。  
  
-   如果SQL_DESC_CONCISE_TYPE是间隔数据类型，则SQL_DESC_DATETIME_INTERVAL_PRECISION字段将验证为有效的间隔前导精度值。  
  
 通常不设置 IPD 的SQL_DESC_DATA_PTR字段;但是，应用程序可以这样做来强制对 IPD 字段进行一致性检查。 无法对 IRD 执行一致性检查。 IPD 的SQL_DESC_DATA_PTR字段的值实际上未存储，并且无法通过调用**SQLGetDescField**或**SQLGetDescRec**检索该值。设置仅用于强制一致性检查。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|绑定列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|绑定参数|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|获取单个描述符字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单个描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
