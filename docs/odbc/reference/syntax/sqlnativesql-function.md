---
title: "SQLNativeSql 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLNativeSql
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNativeSql
helpviewer_keywords:
- SQLNativeSql function [ODBC]
ms.assetid: b8efc247-27ab-4a00-92b6-1400785783fe
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1672e4c1f21d223ed326c0e0649fc7cbb2376f74
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlnativesql-function"></a>SQLNativeSql 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLNativeSql**返回 SQL 字符串，修改驱动程序。 **SQLNativeSql**不会执行 SQL 语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入]连接句柄。  
  
 *InStatementText*  
 [输入]要转换的 SQL 文本字符串。  
  
 *TextLength1*  
 [输入]以字符为单位的长度 **InStatementText*文本字符串。  
  
 *OutStatementText*  
 [输出]指向在其中以返回已翻译的 SQL 字符串的缓冲区的指针。  
  
 如果*OutStatementText*为 NULL， *TextLength2Ptr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于返回在缓冲区中指向*OutStatementText*。  
  
 *BufferLength*  
 [输入]中的字符数\* *OutStatementText*缓冲区。 如果在返回的值 *\*InStatementText*为 Unicode 字符串 (在调用时**SQLNativeSqlW**)，则*BufferLength*参数必须为偶数。  
  
 *TextLength2Ptr*  
 [输出]指向要返回的字符 （不包括 null 终止） 可用于返回在总数在其中的缓冲区指针\* *OutStatementText*。 可用于返回的字符数是否大于或等于*BufferLength*，则转换中的 SQL 字符串\* *OutStatementText*截断为*BufferLength*减 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLNativeSql**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*SQL_HANDLE_DBC 和*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLNativeSql**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *OutStatementText*不是否足够大以返回整个 SQL 字符串，因此 SQL 字符串被截断。 在中返回未截断的 SQL 字符串的长度 **TextLength2Ptr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|*ConnectionHandle*当时不处于已连接状态。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已连接到数据源之间的通信链接。|  
|22007|无效的日期时间格式|**InStatementText*包含具有无效的日期、 时间戳值 escape 子句。|  
|24000|无效的游标状态|光标在语句中称为所处早于开始日期的结果集或结果集的结尾之后。 具有本机的 DBMS 游标实现的驱动程序不会返回此错误。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或函数完成所需的内存。|  
|HY009|不允许使用 null 指针|(DM) **InStatementText*是空指针。|  
|HY010|函数序列错误|(DM) 以异步方式执行的函数曾为*ConnectionHandle*和仍在执行时调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 自变量*TextLength1*小于 0，但与 sql_nts 以不相等。|  
|||(DM) 自变量*BufferLength*已小于 0 和自变量*OutStatementText*不是空指针。|  
|HY109|无效的光标位置|光标的当前行已被删除，或者不已提取。 具有本机的 DBMS 游标实现的驱动程序不会返回此错误。|  
|HY117|连接是由于未知的事务状态挂起。 仅断开连接，允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与*ConnectionHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 下面是示例的内容的**SQLNativeSql**可能返回包含标量函数转换的以下输入 SQL 字符串。 假定列 empid 为数据源中的整数类型：  
  
```  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 用于 Microsoft SQL Server 的驱动程序可能会返回以下已翻译的 SQL 字符串：  
  
```  
SELECT convert (smallint, empid) FROM employee  
```  
  
 用于 ORACLE 服务器的驱动程序可能会返回以下已翻译的 SQL 字符串：  
  
```  
SELECT to_number (empid) FROM employee  
```  
  
 用于 Ingres 的驱动程序可能会返回以下已翻译的 SQL 字符串：  
  
```  
SELECT int2 (empid) FROM employee  
```  
  
 有关详细信息，请参阅[直接执行](../../../odbc/reference/develop-app/direct-execution-odbc.md)和[已准备的执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
## <a name="related-functions"></a>相关函数  
 无。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

