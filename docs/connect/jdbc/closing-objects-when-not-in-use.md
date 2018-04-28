---
title: 关闭在不使用时的对象 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b571b62a52cd25b46cc485cb7a6552bdb51b51a3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="closing-objects-when-not-in-use"></a>不使用时关闭对象
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  当你处理的对象的[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，特别是[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)或语句之一对象如[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)， [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)或[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)，应显式关闭它们在不再需要时通过其关闭的方法。 这样可以尽快地释放驱动程序和服务器资源，而不是等待 Java 虚拟机垃圾收集器执行此操作，从而提高性能。  
  
 当您使用滚动锁定时，要在服务器上保持良好的并发性能，则关闭对象尤其重要。 上一次访问的提取缓冲区中的滚动锁定会一直保持，直到关闭结果集。 类似地，语句准备的句柄会一直保留，直到关闭此语句。 如果您对多条语句重复使用一个连接，则在让语句退出作用域之前关闭这些语句会使服务器过早地清除已准备的句柄。  
  
## <a name="see-also"></a>另请参阅  
 [借助 JDBC 驱动程序提高性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
