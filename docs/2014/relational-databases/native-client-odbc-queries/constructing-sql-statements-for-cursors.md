---
title: 为游标构造 SQL 语句 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], statement construction
- ODBC applications, cursors
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
- statements [ODBC], cursors
ms.assetid: 134003fd-9c93-4f5c-a988-045990933b80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dc86f27ab9e111c5d93c91de65c51da9008ba33
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68207079"
---
# <a name="constructing-sql-statements-for-cursors"></a>为游标构造 SQL 语句
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序使用服务器游标来实现 ODBC 规范中定义的游标功能。 ODBC 应用程序通过使用[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)设置不同的语句特性来控制游标行为。 以下为属性及其默认值。  
  
|Attribute|默认|  
|---------------|-------------|  
|SQL_ATTR_CONCURRENCY|SQL_CONCUR_READ_ONLY|  
|SQL_ATTR_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE|SQL_NONSCROLLABLE|  
|SQL_ATTR_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_ATTR_ROW_ARRAY_SIZE|1|  
  
 当执行 SQL 语句时，将这些选项设置为默认值时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序不使用服务器游标来实现结果集;而是使用默认结果集。 如果在执行 SQL 语句时，这些选项中的任何一种都已更改为默认值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则 NATIVE Client ODBC 驱动程序会尝试使用服务器游标来实现结果集。  
  
 默认结果集支持所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 对使用默认结果集时可以执行的 SQL 语句类型没有限制。  
  
 服务器游标不支持所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 服务器游标不支持生成多个结果集的任何 SQL 语句。  
  
 服务器游标不支持以下语句类型：  
  
-   批处理  
  
     SQL 语句从两个或多个单独的 SQL SELECT 语句中生成，例如：  
  
    ```  
    SELECT * FROM Authors; SELECT * FROM Titles  
    ```  
  
-   带有多个 SELECT 语句的存储过程  
  
     执行包含多个 SELECT 语句的存储过程的 SQL 语句。 这包括填充参数或变量的 SELECT 语句。  
  
-   Keywords  
  
     包含关键字 FOR BROWSE 或 INTO 的 SQL 语句。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果使用服务器游标执行符合这些条件中任意一条的 SQL 语句，则服务器游标将隐式转换为默认结果集。 **SQLExecDirect**或**SQLExecute**返回 SQL_SUCCESS_WITH_INFO 后，游标属性将设置回其默认设置。  
  
 不适合以上类别的 SQL 语句可以通过任何语句属性设置执行，它们通过默认结果集或服务器游标均可正常执行。  
  
## <a name="errors"></a>错误  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 和更高版本中，尝试执行生成多个结果集的语句将生成 SQL_SUCCESS_WITH INFO 和下列消息：  
  
```  
SqlState: 01S02"  
pfNative: 0  
szErrorMsgString: "[Microsoft][SQL Server Native Client][SQL Server]  
               Cursor type changed."  
```  
  
 接收此消息的 ODBC 应用程序可以调用[SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md)来确定当前游标设置。  
  
 使用服务器游标时尝试执行带有多个 SELECT 语句的过程将产生下列错误：  
  
```  
SqlState: 42000  
pfNative: 16937  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               A server cursor is not allowed on a stored procedure  
               with more than one SELECT statement in it. Use a  
               default result set or client cursor.  
```  
  
 使用服务器游标时尝试执行带有多个 SELECT 语句的批处理将产生下列错误：  
  
```  
SqlState: 42000  
pfNative: 16938  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               sp_cursoropen. The statement parameter can only  
               be a single SELECT statement or a single stored   
               procedure.  
```  
  
 ODBC 应用程序收到这些错误后，在尝试执行该语句前必须将所有游标语句属性重置为其默认值。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;执行查询](executing-queries-odbc.md)  
  
  
