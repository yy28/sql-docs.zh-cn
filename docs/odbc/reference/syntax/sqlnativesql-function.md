---
title: SQLNativeSql 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f58d262f133fc242592e62e0bb5a4152877adf6
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536535"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ODBC  
  
 **摘要**  
 **SQLNativeSql**为已修改驱动程序返回的 SQL 字符串。 **SQLNativeSql**不会执行 SQL 语句。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 [输出]指向用于返回已翻译的 SQL 字符串缓冲区的指针。  
  
 如果*OutStatementText*为 NULL， *TextLength2Ptr*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于在缓冲区中返回指向*OutStatementText*。  
  
 *BufferLength*  
 [输入]中的字符数\* *OutStatementText*缓冲区。 如果在返回的值 *\*InStatementText*是 Unicode 字符串 (在调用时**SQLNativeSqlW**)，则*BufferLength*参数必须为偶数。  
  
 *TextLength2Ptr*  
 [输出]指向的缓冲区中要返回的字符 （不包括 null 终止） 可用于在返回总数\* *OutStatementText*。 可用于返回的字符数是否大于或等于*BufferLength*，则转换中的 SQL 字符串\* *OutStatementText*截断为*BufferLength*减去 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLNativeSql**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以通过调用获取关联的 SQLSTATE 值**SQLGetDiagRec**与*HandleType*设为 SQL_HANDLE_DBC 和一个*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLNativeSql** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01004|字符串数据，右截断|缓冲区\* *OutStatementText*是否不足够大以返回整个 SQL 字符串，因此 SQL 字符串已被截断。 在返回未截断的 SQL 字符串的长度 **TextLength2Ptr*。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08003|连接未打开|*ConnectionHandle*当时不处于连接状态。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已连接到数据源之间的通信链接失败之前函数已完成处理。|  
|22007|日期时间格式无效|**InStatementText*包含具有无效的日期、 时间戳值转义子句。|  
|24000|游标状态无效|在声明游标的结果集或结果集的末尾之后在开始之前所处。 具有本机的 DBMS 游标实现的驱动程序可能不返回此错误。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|该驱动程序无法分配支持执行或完成该函数所需的内存。|  
|HY009|使用空指针无效|(DM) **InStatementText*是空指针。|  
|HY010|函数序列错误|(DM) 的调用以异步方式执行的函数*ConnectionHandle*和仍在执行时调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数*TextLength1*小于 0，但不是等于 SQL_NTS。|  
|||(DM) 参数*BufferLength*是小于 0，将参数*OutStatementText*不是空指针。|  
|HY109|无效的游标位置|光标的当前行已删除或尚未提取。 具有本机的 DBMS 游标实现的驱动程序可能不返回此错误。|  
|HY117|由于未知的事务状态而挂起连接。 仅断开连接，并允许使用只读的函数。|(DM) 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 驱动程序与相关联*ConnectionHandle*不支持该函数。|  
  
## <a name="comments"></a>注释  
 下面的示例的内容**SQLNativeSql**可能会返回包含标量函数转换以下输入 SQL 字符串。 假设列 empid 是数据源中的整数类型的：  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server 的驱动程序可能会返回以下已翻译的 SQL 字符串：  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE 服务器的驱动程序可能会返回以下已翻译的 SQL 字符串：  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres 的驱动程序可能会返回以下已翻译的 SQL 字符串：  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 有关详细信息，请参阅[直接执行](../../../odbc/reference/develop-app/direct-execution-odbc.md)并[已准备的执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
## <a name="related-functions"></a>相关函数  
 无。  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
