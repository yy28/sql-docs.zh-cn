---
title: "处理错误 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cfcb29aa70f9bfb56c793f6fa5d1d8b31d45f8bf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="handling-errors"></a>处理错误
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用时[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，所有数据库错误条件将都返回到 Java 应用程序作为使用异常[SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md)类。 以下 SQLServerException 类的方法继承自 java.sql.SQLException 和 java.lang.Throwable;它们可以用于返回有关的特定信息和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]已发生错误：  
  
-   getSQLState 返回的标准 X / Open 或异常 SQL99 状态代码。  
  
-   getErrorCode 返回特定数据库错误号。  
  
-   getMessage 返回异常的完整文本。 错误消息文本对问题加以说明，并且经常包括可提供信息的占位符，如对象名称，在显示时，这些占位符会插入到错误消息中。  
  
-   如果没有更多异常对象以返回，getNextException 返回的下一步 SQLServerException 对象或为 null。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数和格式不正确的 SQL 语句构造没有 FROM 子句。 然后运行该语句并处理 SQL 异常。  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [诊断 JDBC 驱动程序的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
