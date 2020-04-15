---
title: SQLGetEnvAttr 函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77cd24386a8eea6769aee59f3674b681c516d9ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285307"
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 函数
**一致性**  
 推出版本： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetEnvAttr**返回环境属性的当前设置。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *环境处理*  
 [输入]环境句柄。  
  
 *特性*  
 [输入]要检索的属性。  
  
 *ValuePtr*  
 [输出]指向要返回*属性*指定的属性的当前值的缓冲区的指针。  
  
 如果*ValuePtr*为 NULL，*则 StringLengthPtr*仍将返回可用返回*ValuePtr*指向的缓冲区中的字节总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度*  
 [输入]如果*ValuePtr*指向字符串，则此参数应为\**ValuePtr*的长度。 如果\* *ValuePtr*是整数，则忽略*缓冲区长度*。 如果*\*ValuePtr*是 Unicode 字符串（在调用**SQLGetEnvAttrW**时），*缓冲区长度*参数必须是偶数。 如果属性值不是字符串，则*缓冲区长度*未使用。  
  
 *字符串长度 Ptr*  
 [输出]指向缓冲区的指针，用于返回可在*\*ValuePtr*中返回的字节总数（不包括空终止字符）。 如果*ValuePtr*是空指针，则不返回任何长度。 如果属性值是字符串，并且可供返回的字节数大于或等于*BufferLength，* 则\**ValuePtr*中的数据将被截断为*BufferLength*减去空终止字符的长度，并且由驱动程序终止。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetEnvAttr**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_ENV的*句柄类型*和环境*句柄**句柄。* 下表列出了**SQLGetEnvAttr**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|\* *ValuePtr*中返回的数据被截断为*缓冲区长度*减去 null 终止字符。 未压缩字符串值的长度在 #*StringLengthPtr*中返回。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY010|函数序列错误|（DM） **SQL_ATTR_ODBC_VERSION**尚未通过**SQLSetEnvAttr**设置。 如果使用**SQLAllocHandleStd，** 则无需显式设置**SQL_ATTR_ODBC_VERSION。**|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY092|无效属性/选项标识符|为参数*属性*指定的值对于驱动程序支持的 ODBC 版本无效。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现可选功能|为参数*属性*指定的值是驱动程序支持的 ODBC 版本的有效 ODBC 环境属性，但驱动程序不支持该属性。|  
|IM001|驱动程序不支持此功能|（DM） 与*环境处理*对应的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 有关属性列表，请参阅[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 没有特定于驱动程序的环境属性。 如果*属性*指定返回字符串的属性 *，ValuePtr*必须是指向要返回字符串的缓冲区的指针。 字符串的最大长度（包括 null 端接字节）将为*BufferLength*字节。  
  
 **SQLGetEnvAttr**可以在环境句柄的分配和自由之间随时调用。 应用程序为环境成功设置的所有环境属性将一直持续到在具有 SQL_HANDLE_ENV*的处理类型的**环境处理*上调用**SQLFreeHandle**为止。 可以在 ODBC 3 *.x*中同时分配多个环境句柄。 分配另一个环境后，一个环境中的环境属性不受影响。  
  
> [!NOTE]
>  SQL_ATTR_OUTPUT_NTS环境属性由符合标准的应用程序支持。 调用**SQLGetEnvAttr**时，ODBC 3 *.x*驱动程序管理器始终返回此属性的SQL_TRUE。 SQL_ATTR_OUTPUT_NTS只能通过调用**SQLSetEnvAttr**设置为SQL_TRUE。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|返回语句属性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|设置连接属性|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置环境属性|[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
