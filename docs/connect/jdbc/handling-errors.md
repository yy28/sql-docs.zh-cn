---
title: 错误处理 |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: a69bf1d98d666b0b4b76be604abc31e28958adb4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781700"
---
# <a name="handling-errors"></a>处理错误
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 时，所有数据库错误条件都通过使用 [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 类作为异常返回到 Java 应用程序。 SQLServerException 类的以下方法继承自 java.sql.SQLException 和 java.lang.Throwable；并且可用于返回有关出现的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的特定信息：  
  
-   `getSQLState()` 返回异常的标准 X/Open 或 SQL99 状态代码。
  
-   `getErrorCode()` 返回特定的数据库错误号。
  
-   `getMessage()` 返回异常的完整文本。 错误消息文本对问题加以说明，并且经常包括可提供信息的占位符，如对象名称，在显示时，这些占位符会插入到错误消息中。
  
-   `getNextException()` 将返回下一个 `SQLServerException` 对象，如果没有可以返回的异常对象，则返回 null。

-   `getSQLServerError()` 返回`SQLServerError`对象，其中包含有关异常的详细的信息，如从 SQL Server 收到。 此方法返回 null，如果没有服务器错误。

以下方法`SQLServerError`类可用于获取有关从服务器所生成错误的其他详细信息。

-   `SQLServerError.getErrorMessage()` 返回从服务器收到的错误消息。

-   `SQLServerError.getErrorNumber()` 返回一个数字，标识错误的类型。

-   `SQLServerError.getErrorState()` 从表示错误、 警告或"找不到数据"消息的 SQL Server 返回一个数字错误代码。

-   `SQLServerError.getErrorSeverity()` 返回收到的错误的严重性级别。

-   `SQLServerError.getServerName()` 返回正在运行的 SQL Server 实例的计算机的名称生成错误。

-   `SQLServerError.getProcedureName()` 返回生成错误的远程过程调用 (RPC) 的存储的过程的名称。

-   `SQLServerError.getLineNumber()` 返回的 TRANSACT-SQL 批命令或生成错误的存储的过程内的行号。
  
 在下面的示例中，将向函数中传递 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的一个打开连接，并构造一条没有 FROM 子句、格式错误的 SQL 语句。 然后运行该语句并处理 SQL 异常。  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [诊断与 JDBC 驱动程序有关的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
