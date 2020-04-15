---
title: SQLGetStmtAttr 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7c75b412a6358806017102915989a8370dd43
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303301"
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetStmtAttr**返回语句属性的当前设置。  
  
> [!NOTE]  
>  有关驱动程序管理器将此功能映射到 ODBC 3 时的详细信息。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[映射应用程序向后兼容性的替代函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *语句句柄*  
 [输入]语句句柄。  
  
 *特性*  
 [输入]要检索的属性。  
  
 *ValuePtr*  
 [输出]指向要返回*属性*中指定的属性值的缓冲区的指针。  
  
 如果*ValuePtr*为 NULL，*则 StringLengthPtr*仍将返回可用返回*ValuePtr*指向的缓冲区中的字节总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度*  
 [输入]如果*属性*是 ODBC 定义的属性 *，ValuePtr*指向字符串或二进制缓冲区，则此参数应为\**ValuePtr*的长度。 如果*属性*是 ODBC 定义的属性\**，ValuePtr*是整数，则忽略*缓冲区长度*。 如果*\*ValuePtr*中返回的值是 Unicode 字符串（在调用**SQLGetStmtAttrW**时），*缓冲区长度*参数必须是偶数。  
  
 如果*属性*是驱动程序定义的属性，则应用程序通过设置*BufferLength*参数指示该属性对驱动程序管理器的性质。 *缓冲区长度*可以具有以下值：  
  
-   如果*\*ValuePtr*是指向字符串的指针，则*缓冲区长度*是字符串的长度或SQL_NTS。  
  
-   如果*\*ValuePtr*是指向二进制缓冲区的指针，则应用程序将SQL_LEN_BINARY_ATTR（*长度*）宏的结果放在*缓冲区长度*中。 这将在*缓冲区长度*中放置负值。  
  
-   如果*\*ValuePtr*是指向字符串或二进制字符串以外的值的指针，则*BufferLength*应具有该值SQL_IS_POINTER。  
  
-   如果*\*ValuePtr*包含固定长度的数据类型，则*缓冲区长度*SQL_IS_INTEGER或SQL_IS_UINTEGER（视适用而定）。  
  
 *字符串长度 Ptr*  
 [输出]指向缓冲区的指针，用于返回可在*\*ValuePtr*中返回的字节总数（不包括空终止字符）。 如果*ValuePtr*是空指针，则不返回任何长度。 如果属性值是字符串，并且可供返回的字节数大于或等于*BufferLength，* 则*\*ValuePtr*中的数据将被截断为*BufferLength*减去空终止字符的长度，并且被驱动程序终止。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetStmtAttr**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_STMT的*句柄类型*和*语句句柄*的*句柄*。 下表列出了**SQLGetStmtAttr**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|* \*ValuePtr*中返回的数据被截断为*缓冲区长度*减去空终止字符的长度。 未压缩字符串值的长度在 #*StringLengthPtr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|24000|无效的游标状态|参数*属性*处于SQL_ATTR_ROW_NUMBER并且游标未打开，或者游标位于结果集开始之前或结果集结束之后。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在参数*MessageText*中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） 为与*语句句柄*关联的连接句柄调用异步执行函数。 调用**SQLGetStmtAttr**函数时，此异步函数仍在执行。<br /><br /> （DM） 为*语句句柄*调用了异步执行函数，并且在调用此函数时仍在执行。<br /><br /> （DM） SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被调用用于**SQLExecute***语句句柄*并返回SQL_NEED_DATA。 **SQLExecDirect** 在发送所有执行时数据参数或列的数据之前，调用了此功能。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|*（DM） \*ValuePtr*是一个字符串，缓冲区长度小于零，但不等于SQL_NTS。|  
|HY092|无效属性/选项标识符|为参数*属性*指定的值对于驱动程序支持的 ODBC 版本无效。|  
|HY109|光标位置无效|*属性*参数已SQL_ATTR_ROW_NUMBER，并且该行已被删除或无法提取。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|为参数*属性*指定的值是驱动程序支持的 ODBC 版本的有效 ODBC 语句属性，但驱动程序不支持该属性。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*语句句柄*对应的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 有关语句属性的一般信息，请参阅[语句属性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 对**SQLGetStmtAttr 的**调用在*\*ValuePtr*中返回*属性*中指定的语句属性的值。 该值可以是 SQLULEN 值，也可以是 null 端接字符串。 如果值是 SQLULEN 值，则某些驱动程序可能只写入缓冲区的较低 32 位或 16 位，并且保持高阶位不变。 因此，应用程序应在调用此函数之前使用 SQLULEN 的缓冲区并将该值初始化为 0。 此外，不使用*缓冲区长度*和*字符串长度 Ptr*参数。 如果该值是 null 端接字符串，则应用程序在*BufferLength 参数*中指定该字符串的最大长度，并且驱动程序将在*\*StringLengthPtr*缓冲区中返回该字符串的长度。  
  
 允许调用**SQLGetStmtAttr**的应用程序使用 ODBC 2。*x*驱动程序，对**SQLGetStmtAttr**的调用在驱动程序管理器中映射到**SQLGetStmtOption**。  
  
 以下语句属性是只读的，因此可以通过**SQLGetStmtAttr**检索，但不能由**SQLSetStmtAttr**设置：  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 有关可以设置和检索的属性列表，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|设置连接属性|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
