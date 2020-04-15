---
title: SQLGetDescRec 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 87d7b971b379f19f8451e924932a5e699e9b9983
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285482"
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetDescRec**返回描述符记录的多个字段的当前设置或值。 返回的字段描述列或参数数据的名称、数据类型和存储。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>参数  
 *DescriptorHandle*  
 [输入]描述符句柄。  
  
 *RecNumber*  
 [输入]指示应用程序从中查找信息的描述符记录。 描述符记录从 1 编号，记录编号 0 是书签记录。 *RecNumber*参数必须小于或等于SQL_DESC_COUNT的值。 如果*RecNumber*小于或等于SQL_DESC_COUNT但该行不包含列或参数的数据，则对**SQLGetDescRec**的调用将返回字段的默认值。 （有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的"描述字段的初始化"。  
  
 *名称*  
 [输出]指向要返回描述符记录SQL_DESC_NAME字段的缓冲区的指针。  
  
 如果*名称*为 NULL，*则 StringLengthPtr*仍将返回字符总数（不包括字符数据的空终止字符），这些字符可用于*返回名称*指向 的缓冲区中。  
  
 *缓冲区长度*  
 [输入]**名称*缓冲区的长度（以字符表示）。  
  
 *字符串长度 Ptr*  
 [输出]指向缓冲区的指针，用于返回\**名称*缓冲区中可返回的数据字符数，不包括空终止字符。 如果字符数大于或等于*BufferLength，* 则\**名称*中的数据将被截断为*BufferLength*减去空终止字符的长度，并且被驱动程序终止为 null。  
  
 *类型 Ptr*  
 [输出]指向缓冲区的指针，用于在其中返回描述符记录的SQL_DESC_TYPE字段的值。  
  
 *子类型 Ptr*  
 [输出]对于类型为SQL_DATETIME或SQL_INTERVAL的记录，这是指向缓冲区的指针，用于返回SQL_DESC_DATETIME_INTERVAL_CODE字段的值。  
  
 *长度Ptr*  
 [输出]指向缓冲区的指针，用于在其中返回描述符记录的SQL_DESC_OCTET_LENGTH字段的值。  
  
 *精密Ptr*  
 [输出]指向缓冲区的指针，用于在其中返回描述符记录的SQL_DESC_PRECISION字段的值。  
  
 *缩放器*  
 [输出]指向缓冲区的指针，用于在其中返回描述符记录的SQL_DESC_SCALE字段的值。  
  
 *空可点*  
 [输出]指向缓冲区的指针，用于在其中返回描述符记录的SQL_DESC_NULLABLE字段的值。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA或SQL_INVALID_HANDLE。  
  
 如果*RecNumber*大于当前描述符记录数，则返回SQL_NO_DATA。  
  
 如果*描述符句柄*是 IRD 句柄，并且语句处于准备或执行状态，但没有与其关联的打开游标，则返回SQL_NO_DATA。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetDescRec**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有*Handle*SQL_HANDLE_DESC的*句柄类型*和*描述符句柄*。 下表列出了**SQLGetDescRec**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|缓冲区\**名称*不够大，无法返回整个描述符字段。 因此，该字段被截断。 未压缩的描述符字段的长度在 #*StringLengthPtr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|07009|无效描述符索引|*字段标识符*参数是记录字段 *，RecNumber*参数设置为 0，*描述符句柄*参数是 IPD 句柄。<br /><br /> （DM） *RecNumber*参数设置为 0，SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_OFF，*描述符句柄*参数是 IRD 句柄。<br /><br /> *RecNumber*参数小于 0。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY007|未准备关联语句|*描述符句柄*与 IRD 相关联，关联的语句句柄未处于准备或执行状态。|  
|HY010|函数序列错误|（DM）*描述符处理*与*语句句柄*相关联，在调用此函数时，调用了异步执行函数（不是此函数），并且仍在执行。<br /><br /> （DM）*描述符句柄*与*语句句柄*相关联，SQL_NEED_DATA调用并返回 SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLExecute****SQLExecDirect****SQLSetPos。** 在发送所有执行时数据参数或列的数据之前，调用了此功能。<br /><br /> （DM） 对于与*描述符句柄*关联的连接句柄，调用了异步执行函数。 调用**SQLGetDescRec**时，此异步函数仍在执行。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*描述符处理*关联的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLGetDescRec**来检索单个列或参数的以下描述符字段的值：  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE（对于其类型为SQL_DATETIME或SQL_INTERVAL的记录）  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec**不检索标头字段的值。  
  
 应用程序可以通过设置与字段对应的空指针的参数来阻止字段设置的返回。  
  
 当应用程序调用**SQLGetDescRec**检索特定描述符类型未定义的字段的值时，该函数将返回SQL_SUCCESS但返回该字段的值未定义。 例如，为 APD 或 ARD 的SQL_DESC_NAME或SQL_DESC_NULLABLE字段调用**SQLGetDescRec**将返回SQL_SUCCESS但字段的未定义值。  
  
 当应用程序调用**SQLGetDescRec**检索为特定描述符类型定义但尚未设置默认值但尚未设置的字段的值时，该函数将返回SQL_SUCCESS但返回该字段的值未定义。 有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的"描述字段的初始化"。  
  
 还可以通过调用**SQLGetDescField**单独检索字段的值。 有关描述符标题或记录中的字段的说明，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|绑定列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|绑定参数|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|获取描述符字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|设置多个描述符字段|[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
