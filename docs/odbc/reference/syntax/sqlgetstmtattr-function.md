---
title: SQLGetStmtAttr 函数 |Microsoft 文档
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
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a45674ecbb65fcedd64551af3b7a2440b2b4621
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetStmtAttr**返回语句属性的当前设置。  
  
> [!NOTE]  
>  有关详细信息有关哪些驱动程序管理器时，将映射此函数可对 ODBC 3。*x*应用程序使用 ODBC 2。*x*驱动程序，请参阅[映射用于向后兼容性的应用程序的替换函数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *StatementHandle*  
 [输入]语句句柄。  
  
 *属性*  
 [输入]要检索的属性。  
  
 *ValuePtr*  
 [输出]指向在其中为返回值中指定的属性的缓冲区*属性*。  
  
 如果*ValuePtr*为 NULL， *StringLengthPtr*仍将返回的 （不包括字符数据的 null 终止字符） 的字节总数可用于返回指向由的缓冲区中*ValuePtr*。  
  
 *BufferLength*  
 [输入]如果*属性*是 ODBC 定义的属性和*ValuePtr*指向字符字符串或二进制缓冲区时，此参数应为的长度\* *ValuePtr*. 如果*属性*是 ODBC 定义的属性和\* *ValuePtr*是一个整数， *BufferLength*将被忽略。 如果在返回的值 *\*ValuePtr*为 Unicode 字符串 (在调用时**SQLGetStmtAttrW**)，则*BufferLength*参数必须为偶数。  
  
 如果*属性*是驱动程序定义的属性，应用程序通过设置指示属性到驱动程序管理器的性质*BufferLength*自变量。 *BufferLength*可以具有下列值：  
  
-   如果 *\*ValuePtr*然后是指向字符串， *BufferLength*是字符串或 sql_nts 以的长度。  
  
-   如果 *\*ValuePtr*为指向二进制缓冲区的指针，则将 SQL_LEN_BINARY_ATTR 结果放置于应用程序 (*长度*) 中的宏*BufferLength*。 这会在负值*BufferLength*。  
  
-   如果 *\*ValuePtr*然后是指向字符字符串或二进制字符串以外的值的*BufferLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果 *\*ValuePtr*是包含固定长度的数据类型，则*BufferLength*为 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，与相应。  
  
 *StringLengthPtr*  
 [输出]指向要返回的 （不包括 null 终止字符） 的字节总数在其中缓冲区的指针可用于返回在 *\*ValuePtr*。 如果*ValuePtr*是 null 指针，返回没有长度。 如果属性值是一个字符串，并且可用于返回的字节数大于或等于*BufferLength*中的数据 *\*ValuePtr*截断为*BufferLength* null 终止字符的长度减和是由驱动程序以 null 结尾。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetStmtAttr**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可能会通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_STMT 和*处理*的*StatementHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetStmtAttr**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|中返回的数据 *\*ValuePtr*被截断为*BufferLength*减 null 终止字符的长度。 在中返回未截断的字符串值的长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|24000|无效的游标状态|自变量*属性*已 SQL_ATTR_ROW_NUMBER 和游标未打开，或早于开始日期的结果集或结果集的末尾之后已定位光标。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**参数中*MessageText*描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY010|函数序列错误|(DM) 为与关联的连接句柄调用以异步方式执行的函数*StatementHandle*。 此异步函数仍在执行时**SQLGetStmtAttr**调用函数。<br /><br /> (DM) 以异步方式执行的函数曾为*StatementHandle*和仍在执行时调用此函数。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**曾为*StatementHandle*并返回 SQL_NEED_DATA。 数据已发送的所有数据在执行参数或列之前调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|*(DM) \*ValuePtr*是一个字符串，BufferLength 小于零，但与 sql_nts 以不相等。|  
|HY092|属性/选项标识符无效|为参数指定的值*属性*对 ODBC 驱动程序支持的版本无效。|  
|HY109|无效的光标位置|*属性*自变量为 SQL_ATTR_ROW_NUMBER 和行已被删除，或者无法获取。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|为参数指定的值*属性*的 ODBC 版本所支持的驱动程序，但不支持驱动程序是有效的 ODBC 语句属性。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 对应的驱动程序*StatementHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 有关语句特性的常规信息，请参阅[语句特性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 调用**SQLGetStmtAttr**中返回 *\*ValuePtr*中指定的语句属性的值*属性*。 该值可以是 SQLULEN 值或以 null 结尾的字符串。 如果值为 SQLULEN 值，某些驱动程序可能仅编写较低的 32 位或 16 位的缓冲区，并保留较高顺序位保持不变。 因此，应用程序应使用 SQLULEN 的缓冲区，并调用此函数之前初始化为 0 的值。 此外， *BufferLength*和*StringLengthPtr*不使用参数。 如果值为以 null 结尾的字符串，应用程序将指定在该字符串的最大长度*BufferLength*自变量和驱动程序返回在该字符串的长度 *\*StringLengthPtr*缓冲区。  
  
 若要允许应用程序调用**SQLGetStmtAttr**用于 ODBC 2。*x*驱动程序，调用**SQLGetStmtAttr**映射在驱动程序管理器到**SQLGetStmtOption**。  
  
 以下语句属性是只读的因此可以通过检索**SQLGetStmtAttr**，但未设置**SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 可以设置和检索的属性的列表，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
