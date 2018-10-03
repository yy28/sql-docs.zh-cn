---
title: 错误处理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 066aa64a529d2066c0dcce50cd2f2aff12dcf948
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758985"
---
# <a name="handling-errors"></a>处理错误
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 时，所有数据库错误条件都通过使用 [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 类作为异常返回到 Java 应用程序。 SQLServerException 类的以下方法继承自 java.sql.SQLException 和 java.lang.Throwable；并且可用于返回有关出现的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的特定信息：  
  
-   getSQLState 返回异常的标准 X/Open 或 SQL99 状态代码。  
  
-   getErrorCod 返回特定的数据库错误号。  
  
-   getMessage 返回异常的完整文本。 错误消息文本对问题加以说明，并且经常包括可提供信息的占位符，如对象名称，在显示时，这些占位符会插入到错误消息中。  
  
-   getNextException 返回的下一步 SQLServerException 对象或为 null，如果没有更多可以返回的异常对象。  
  
 在下面的示例中，将向函数中传递 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的一个打开连接，并构造一条没有 FROM 子句、格式错误的 SQL 语句。 然后运行该语句并处理 SQL 异常。  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [诊断与 JDBC 驱动程序有关的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
