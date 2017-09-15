---
title: "SQLGetEnvAttr 函数 |Microsoft 文档"
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
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a7e353d41c1065f8d65a70c6633901ef22547a61
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 函数
**一致性**  
 版本引入了： ODBC 3.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLGetEnvAttr**返回环境属性的当前设置。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>参数  
 *EnvironmentHandle*  
 [输入]环境句柄。  
  
 *Attribute*  
 [输入]要检索的属性。  
  
 *ValuePtr*  
 [输出]指向在其返回由指定的属性的当前值的缓冲区的指针*属性*。  
  
 如果*ValuePtr*为 NULL， *StringLengthPtr*仍将返回的 （不包括字符数据的 null 终止字符） 的字节总数可用于返回指向由的缓冲区中*ValuePtr*。  
  
 *BufferLength*  
 [输入]如果*ValuePtr*指向字符字符串，该参数应为的长度\* *ValuePtr*。 如果\* *ValuePtr*是一个整数， *BufferLength*将被忽略。 如果* \*ValuePtr*为 Unicode 字符串 (在调用时**SQLGetEnvAttrW**)，则*BufferLength*参数必须为偶数。 如果属性值不是字符串， *BufferLength*未使用。  
  
 *StringLengthPtr*  
 [输出]指向要返回的 （不包括 null 终止字符） 的字节总数在其中缓冲区的指针可用于返回在* \*ValuePtr*。 如果*ValuePtr*是 null 指针，返回没有长度。 如果属性值为字符串，可用于返回的字节数为大于或等于*BufferLength*中的数据\* *ValuePtr*截断为*BufferLength* null 终止字符的长度减和是由驱动程序以 null 结尾。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetEnvAttr**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_ENV 和*处理*的*EnvironmentHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLGetEnvAttr**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|中返回的数据\* *ValuePtr*被截断为*BufferLength*减去的 null 终止字符。 在中返回未截断的字符串值的长度 **StringLengthPtr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY010|函数序列错误|(DM) **SQL_ATTR_ODBC_VERSION**尚未设置通过**SQLSetEnvAttr**。 不需要设置**SQL_ATTR_ODBC_VERSION**显式如果你使用**SQLAllocHandleStd**。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY092|属性/选项标识符无效|为参数指定的值*属性*对 ODBC 驱动程序支持的版本无效。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|为参数指定的值*属性*是有效的 ODBC 环境属性的 ODBC 版本所支持的驱动程序，但该驱动程序不支持。|  
|IM001|驱动程序不支持此函数|(DM) 对应的驱动程序*EnvironmentHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 属性的列表，请参阅[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 没有特定于驱动程序的环境属性。 如果*属性*指定属性返回一个字符串， *ValuePtr*必须是指向在其中返回的字符串的缓冲区的指针。 将包括 null 终止的字节的字符串的最大长度*BufferLength*字节。  
  
 **SQLGetEnvAttr**可以随时之间分配和释放的环境句柄调用。 已成功设置环境的应用程序的所有环境属性都保留直到**SQLFreeHandle**上调用*EnvironmentHandle*与*HandleType*SQL_HANDLE_ENV。 ODBC 3 中可以同时分配多个环境句柄*.x*。 已分配另一个环境时，不会影响在一个环境的环境属性。  
  
> [!NOTE]  
>  符合标准的应用程序都支持 SQL_ATTR_OUTPUT_NTS 环境属性。 当**SQLGetEnvAttr**调用时，ODBC 3*.x*驱动程序管理器始终返回 SQL_TRUE 此特性。 SQL_ATTR_OUTPUT_NTS 可以将设置为 SQL_TRUE 仅通过调用**SQLSetEnvAttr**。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|返回语句特性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置环境属性|[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|设置语句属性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
