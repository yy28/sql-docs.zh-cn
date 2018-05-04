---
title: SQLSetDescRec 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 085543aca838cfe1a8123f891c30f618b86eb15d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLSetDescRec**函数设置会影响的数据类型的多个描述符字段并绑定到的列或参数数据的缓冲区。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 [输入]描述符句柄。 这不能 IRD 句柄。  
  
 *RecNumber*  
 [输入]指示包含要设置的字段的描述符记录。 描述符记录与记录号 0 表示的书签记录编号从 0。 此参数必须等于或大于 0。 如果*RecNumber*大于 SQL_DESC_COUNT，SQL_DESC_COUNTis 更改为的值的值*RecNumber*。  
  
 *类型*  
 [输入]为其设置描述符记录的 SQL_DESC_TYPE 字段值。  
  
 *子类型*  
 [输入]对于其类型为 SQL_DATETIME 或 SQL_INTERVAL 的记录，这是为其设置 SQL_DESC_DATETIME_INTERVAL_CODE 字段的值。  
  
 *长度*  
 [输入]为其设置描述符记录的 SQL_DESC_OCTET_LENGTH 字段值。  
  
 *精度*  
 [输入]为其设置描述符记录的 SQL_DESC_PRECISION 字段值。  
  
 *小数位数*  
 [输入]为其设置描述符记录的 SQL_DESC_SCALE 字段值。  
  
 *DataPtr*  
 [延迟的输入或输出]为其设置描述符记录的 SQL_DESC_DATA_PTR 字段值。 *DataPtr*可以将设置为 null 指针。  
  
 *DataPtr*参数可以设置为 null 指针，以将 SQL_DESC_DATA_PTR 字段设置为 null 指针。 如果句柄以*DescriptorHandle*自变量与 ARD 相关联，这解除绑定列。  
  
 *StringLengthPtr*  
 [延迟的输入或输出]为其设置描述符记录的 SQL_DESC_OCTET_LENGTH_PTR 字段值。 *StringLengthPtr*可以设置为 null 指针以将 SQL_DESC_OCTET_LENGTH_PTR 字段设置为 null 指针。  
  
 *IndicatorPtr*  
 [延迟的输入或输出]为其设置描述符记录的 SQL_DESC_INDICATOR_PTR 字段值。 *IndicatorPtr*可以设置为 null 指针以将 SQL_DESC_INDICATOR_PTR 字段设置为 null 指针。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetDescRec**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_DESC 和*处理*的*DescriptorHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLSetDescRec**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|07009|无效的描述符索引|*RecNumber*参数已设置为 0，和*DescriptorHandle*称为 IPD 句柄。<br /><br /> *RecNumber*自变量为小于 0。<br /><br /> *RecNumber*参数为大于最大列数或数据源可以支持的参数和*DescriptorHandle*参数为 APD、 IPD 或 ARD。<br /><br /> *RecNumber*自变量为等于 0，和*DescriptorHandle*隐式分配 APD 引用自变量。 （此错误不会发生与显式分配应用程序描述符因为并不知道是否是显式分配应用程序描述符是 APD 或直到 ARD 执行时间。）|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY010|函数序列错误|(DM) *DescriptorHandle*与关联*StatementHandle*其中一个以异步方式执行的函数 （而不此是） 调用和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*与其*DescriptorHandle*成功关联并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。<br /><br /> (DM) 为与关联的连接句柄调用以异步方式执行的函数*DescriptorHandle*。 此 aynchronous 函数仍在执行时**SQLSetDescRec**调用函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**与关联的语句句柄之一调用*DescriptorHandle*并返回 SQL_PARAM_DATA_AVAILABLE。 数据已检索到的所有经过流处理参数之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY016|无法修改实现行描述符|*DescriptorHandle*自变量为 IRD 与相关联。|  
|HY021|描述符信息不一致|*类型*字段或描述符中的 SQL_DESC_TYPE 字段关联的任何其他字段未无效或不一致。<br /><br /> 在一致性检查过程中检查的描述符信息未一致。 （请参阅"一致性检查，"本部分中更高版本）。|  
|HY090|字符串或缓冲区长度无效|(DM) 驱动程序是 ODBC 2 *.x*驱动程序，该描述符已 ARD *ColumnNumber*参数已设置为 0，并为参数指定的值*BufferLength*已不等于 4。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*DescriptorHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 应用程序可以调用**SQLSetDescRec**设置为单个列或参数的以下字段：  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE （对于其类型为 SQL_DATETIME 或 SQL_INTERVAL 记录）  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  如果调用**SQLSetDescRec**失败，由标识的描述符记录的内容*RecNumber*自变量是不确定。  
  
 绑定的列或参数时, **SQLSetDescRec**允许您更改影响的情况下调用绑定的多个字段**SQLBindCol**或**SQLBindParameter**或在多个调用**SQLSetDescField**。 **SQLSetDescRec**可将字段设置当前不与语句关联的描述符上。 请注意， **SQLBindParameter**设置字段数多于**SQLSetDescRec**，可将字段设置 APD 和 IPD 一次调用，并且不需要的描述符句柄。  
  
> [!NOTE]  
>  语句属性 SQL_ATTR_USE_BOOKMARKS 应始终设置，然后再调**SQLSetDescRec**与*RecNumber* 0，则设置书签字段的自变量。 虽然这不是必需的强烈建议。  
  
## <a name="consistency-checks"></a>一致性检查  
 一致性检查时，将执行由驱动程序会自动应用程序设置 APD、 ARD，或 IPD SQL_DESC_DATA_PTR 字段。 如果其中任何一个字段是不一致，其他字段， **SQLSetDescRec**将返回 SQLSTATE HY021 （不一致的描述符信息）。  
  
 每当应用程序设置 APD、 ARD，或 IPD SQL_DESC_DATA_PTR 字段，该驱动程序检查 SQL_DESC_TYPE 字段的值和适用于该 SQL_DESC_TYPE 字段值有效且一致。 此检查是始终执行时**SQLBindParameter**或**SQLBindCol**调用时，或者当**SQLSetDescRec** APD、 ARD，或 IPD 调用。 此一致性检查包括以下检查描述符字段：  
  
-   SQL_DESC_TYPE 字段必须是有效的 ODBC C 或 SQL 类型或特定于驱动程序的 SQL 类型之一。 SQL_DESC_CONCISE_TYPE 字段必须是有效的 ODBC C 或 SQL 类型或特定于驱动程序的 C 或 SQL 类型，包括简洁的日期时间和间隔类型之一。  
  
-   如果 SQL_DESC_TYPE 记录字段，SQL_DATETIME 或 SQL_INTERVAL SQL_DESC_DATETIME_INTERVAL_CODE 字段必须是有效的日期时间或间隔代码之一。 (请参阅中的 SQL_DESC_DATETIME_INTERVAL_CODE 字段的说明[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
-   如果 SQL_DESC_TYPE 字段指示数值类型，验证 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段有效。  
  
-   如果 SQL_DESC_CONCISE_TYPE 字段是时间戳数据类型，间隔类型秒组成部分，或从一台 interval 数据类型与时间组件中，验证 SQL_DESC_PRECISION 字段是有效的秒精度。  
  
-   如果 SQL_DESC_CONCISE_TYPE 间隔数据类型，SQL_DESC_DATETIME_INTERVAL_PRECISION 字段被验证为有效的间隔前导精度值。  
  
 通常情况下不设置 IPD SQL_DESC_DATA_PTR 字段;但是，应用程序可以这样做是为了强制 IPD 字段执行一致性检查。 不能在 IRD 上执行一致性检查。 IPD SQL_DESC_DATA_PTR 字段设置为的值不会实际存储，不能通过调用检索**SQLGetDescField**或**SQLGetDescRec**; 进行设置仅用于强制一致性检查。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|绑定列|[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|将参数绑定|[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|获取单个描述符字段|[SQLGetDescField 函数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|获取多个描述符字段|[SQLGetDescRec 函数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|设置单个描述符字段|[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
