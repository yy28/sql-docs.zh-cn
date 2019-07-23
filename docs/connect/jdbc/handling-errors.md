---
title: 处理错误 |Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bc0e483c70033c8a8132a27879c5616e550ec26
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956536"
---
# <a name="handling-errors"></a>处理错误
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 时，所有数据库错误条件都通过使用 [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 类作为异常返回到 Java 应用程序。 SQLServerException 类的以下方法继承自 java.sql.SQLException 和 java.lang.Throwable；并且可用于返回有关出现的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的特定信息：  
  
-   `getSQLState()` 返回异常的标准 X/Open 或 SQL99 状态代码。
  
-   `getErrorCode()` 返回特定的数据库错误号。
  
-   `getMessage()` 返回异常的完整文本。 错误消息文本对问题加以说明，并且经常包括可提供信息的占位符，如对象名称，在显示时，这些占位符会插入到错误消息中。
  
-   `getNextException()` 将返回下一个 `SQLServerException` 对象，如果没有可以返回的异常对象，则返回 null。

-   `getSQLServerError()`返回对象`SQLServerError` , 该对象包含与 SQL Server 收到的异常有关的详细信息。 如果未发生服务器错误, 则此方法返回 null。

`SQLServerError`类的以下方法可用于获取有关服务器生成的错误的更多详细信息。

-   `SQLServerError.getErrorMessage()`返回从服务器接收的错误消息。

-   `SQLServerError.getErrorNumber()`返回标识错误类型的数字。

-   `SQLServerError.getErrorState()`从 SQL Server 返回表示错误、警告或 "找不到数据" 消息的数字错误代码。

-   `SQLServerError.getErrorSeverity()`返回收到的错误的严重级别。

-   `SQLServerError.getServerName()`返回运行生成错误的 SQL Server 实例的计算机的名称。

-   `SQLServerError.getProcedureName()`返回生成错误的存储过程或远程过程调用 (RPC) 的名称。

-   `SQLServerError.getLineNumber()`返回生成错误的 Transact-sql 命令批处理或存储过程中的行号。
  
 在下面的示例中，将向函数中传递 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的一个打开连接，并构造一条没有 FROM 子句、格式错误的 SQL 语句。 然后运行该语句并处理 SQL 异常。  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [诊断与 JDBC 驱动程序有关的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
