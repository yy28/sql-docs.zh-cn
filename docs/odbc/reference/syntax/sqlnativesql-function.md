---
title: SQLNativeSql 函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9666bc767affb3b6bb624c416614079193d4b921
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304718"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： ODBC  
  
 **摘要**  
 **SQLNativeSql**返回由驱动程序修改的 SQL 字符串。 **SQLNativeSql**不执行 SQL 语句。  
  
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
 *连接句柄*  
 [输入] 连接句柄。  
  
 *声明文本*  
 [输入]要翻译的 SQL 文本字符串。  
  
 *文本长度1*  
 [输入]**语句文本*文本字符串的字符的长度。  
  
 *外文文本*  
 [输出]指向要返回翻译的 SQL 字符串的缓冲区的指针。  
  
 如果*Out语句文本*为*NULL，TextLength2Ptr*仍将返回可用于在*Out语句文本*指向的缓冲区中返回的字符总数（不包括字符数据的空终止字符）。  
  
 *缓冲区长度*  
 [输入]\* *Out声明文本*缓冲区中的字符数。 如果在*\*In语句文本*中返回的值是 Unicode 字符串（在调用**SQLNativeSqlW**时），*缓冲区长度*参数必须是偶数。  
  
 *文本长度2Ptr*  
 [输出]指向缓冲区的指针，其中返回可在\**Out语句文本*中返回的字符总数（不包括空终止）。 如果可返回的字符数大于或等于*BufferLength，* 则\**Out语句文本*中翻译的 SQL 字符串将截断为*BufferLength*减去空终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLNativeSql**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_DBC的*句柄类型*和*连接句柄*的*句柄*。 下表列出了**SQLNativeSql**通常返回的 SQLSTATE 值，并在此函数的上下文中解释了每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01004|字符串数据，右截断|缓冲区\* *Out语句文本*不够大，无法返回整个 SQL 字符串，因此 SQL 字符串被截断。 未压缩的 SQL 字符串的长度在 [*文本长度2Ptr*中返回] （函数返回SQL_SUCCESS_WITH_INFO。|  
|08003|连接未打开|*连接句柄*未处于连接状态。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序连接到的数据源之间的通信链路失败。|  
|22007|无效日期时间格式|**In语句文本*包含具有无效日期、时间或时间戳值的转义子句。|  
|24000|无效的游标状态|语句中引用的游标位于结果集开始之前或结果集结束之后。 具有本机 DBMS 游标实现的驱动程序可能无法返回此错误。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|驱动程序无法分配支持执行或完成函数所需的内存。|  
|HY009|无效使用空指针|（DM） =*声明文本*是一个空指针。|  
|HY010|函数序列错误|（DM） 为*ConnectHandle*调用了异步执行函数，并且在调用此函数时仍在执行。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 参数*TextLength1*小于 0，但不等于SQL_NTS。|  
|||（DM） 参数*BufferLength*小于 0，参数*Out语句文本*不是空指针。|  
|HY109|光标位置无效|游标的当前行已被删除或未提取。 具有本机 DBMS 游标实现的驱动程序可能无法返回此错误。|  
|HY117|由于未知事务状态，连接挂起。 只允许断开连接和只读功能。|（DM） 有关挂起状态的详细信息，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 与*连接句柄*关联的驱动程序不支持该功能。|  
  
## <a name="comments"></a>注释  
 以下是**SQLNativeSql**可能为包含标量函数 CONVERT 的以下输入 SQL 字符串返回的内容的示例。 假设列 empid 在数据源中为 INTEGER 类型：  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server 的驱动程序可能会返回以下翻译的 SQL 字符串：  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE 服务器的驱动程序可能会返回以下翻译的 SQL 字符串：  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres 的驱动程序可能会返回以下翻译的 SQL 字符串：  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 有关详细信息，请参阅[直接执行](../../../odbc/reference/develop-app/direct-execution-odbc.md)和[准备执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
## <a name="related-functions"></a>相关函数  
 无。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
