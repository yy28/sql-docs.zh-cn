---
title: SQLGetEnvAttr 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0940a5a2c70a7b670ca6a81521759fd08e60461e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345625"
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 函数
**度**  
 引入的版本:ODBC 3.0 标准符合性:ISO 92  
  
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
 *EnvironmentHandle*  
 送环境句柄。  
  
 *Attribute*  
 送要检索的属性。  
  
 *ValuePtr*  
 输出指向缓冲区的指针, 该缓冲区用于返回*特性*指定的特性的当前值。  
  
 如果*将 valueptr*为 NULL, 则*StringLengthPtr*将仍返回在*将 valueptr*指向的缓冲区中可返回的总字节数 (不包括字符数据的 NULL 终止字符)。  
  
 *BufferLength*  
 送如果*将 valueptr*指向一个字符串, 则此参数应为\**将 valueptr*的长度。 如果\**将 valueptr*是一个整数, 则将忽略*BufferLength* 。 *如果\*将 valueptr*是 Unicode 字符串 (在调用**SQLGetEnvAttrW**时), 则*BufferLength*参数必须是偶数。 如果属性值不是字符串, 则不使用*BufferLength* 。  
  
 *StringLengthPtr*  
 输出指向缓冲区的指针, 该缓冲区用于返回可在 *\*将 valueptr*中返回的总字节数 (不包括 null 终止字符)。 如果*将 valueptr*为 null 指针, 则不返回长度。 如果属性值为字符串, 并且可返回的字节数大于或等于*BufferLength*, 则\**将 valueptr*中的数据将被截断为*BufferLength*减去 null 终止的长度字符, 由驱动程序以 null 结尾。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetEnvAttr**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 时, 可以通过使用*SQLGetDiagRec 的 HandleType*和*SQL_HANDLE_ENV*的*句柄*调用**EnvironmentHandle**来获取关联的 SQLSTATE 值。 下表列出了通常由**SQLGetEnvAttr**返回的 SQLSTATE 值, 并对该函数的上下文中的每个值进行了说明:"(DM)" 表示法位于驱动程序管理器返回的 SQLSTATEs 的说明之前。 除非另有说明, 否则与每个 SQLSTATE 值相关联的返回代码为 SQL_ERROR。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驱动程序特定的信息性消息。 (函数返回 SQL_SUCCESS_WITH_INFO。)|  
|01004|字符串数据, 右截断|\**将 valueptr*中返回的数据被截断为*BufferLength*减去 null 终止字符。 在 **StringLengthPtr*中返回未截断字符串值的长度。 (函数返回 SQL_SUCCESS_WITH_INFO。)|  
|HY000|一般错误|发生了一个错误, 该错误没有特定的 SQLSTATE, 没有为其定义实现特定的 SQLSTATE。 MessageText 缓冲区中**的 SQLGetDiagRec**返回的错误消息描述了错误及其原因。  *\**|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成此函数所需的内存。|  
|HY010|函数序列错误|(DM) **SQL_ATTR_ODBC_VERSION**尚未通过**SQLSetEnvAttr**设置。 如果使用的是**SQLAllocHandleStd**, 则无需显式设置**SQL_ATTR_ODBC_VERSION** 。|  
|HY013|内存管理错误|未能处理函数调用, 原因可能是由于内存不足而无法访问基础内存对象。|  
|HY092|无效的属性/选项标识符|为该驱动程序支持的 ODBC 版本指定*的参数值*无效。|  
|HY117|由于未知的事务状态, 连接被挂起。 仅允许断开连接和只读函数。|(DM) 有关挂起状态的详细信息, 请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未实现的可选功能|为 argument*特性*指定的值为驱动程序支持的 odbc 版本的有效 odbc 环境特性, 但驱动程序不支持该特性。|  
|IM001|驱动程序不支持此功能|(DM) 与*EnvironmentHandle*相对应的驱动程序不支持该函数。|  
  
## <a name="comments"></a>注释  
 有关属性列表, 请参阅[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 没有特定于驱动程序的环境属性。 如果*特性*指定了一个返回字符串的属性, 则*将 valueptr*必须是指向要在其中返回字符串的缓冲区的指针。 字符串的最大长度 (包括 null 终止字节) 将为*BufferLength*字节。  
  
 可以在分配和释放环境句柄之间随时调用**SQLGetEnvAttr** 。 环境的应用程序成功设置的所有环境属性都将保留, 直到在*HandleType*为 SQL_HANDLE_ENV 的*EnvironmentHandle*上调用**SQLFreeHandle** 。 可以在 ODBC 2.x 中同时分配多个环境句柄 *。* 如果已分配其他环境, 则一个环境上的环境属性不会受到影响。  
  
> [!NOTE]
>  符合标准的应用程序支持 SQL_ATTR_OUTPUT_NTS 环境属性。 调用**SQLGetEnvAttr**时, ODBC*3.X 驱动程序*管理器始终为此属性返回 SQL_TRUE。 仅可通过调用**SQLSetEnvAttr**将 SQL_ATTR_OUTPUT_NTS 设置为 SQL_TRUE。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|返回语句特性的设置|[SQLGetStmtAttr 函数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|设置连接属性|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|设置环境属性|[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|设置语句特性|[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
