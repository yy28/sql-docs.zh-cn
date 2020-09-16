---
description: 不使用时关闭对象
title: 关闭未用对象 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c8e1242f5090e347dd3dd61d42fedd3698613cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438449"
---
# <a name="closing-objects-when-not-in-use"></a>不使用时关闭对象
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  当处理 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的对象（尤其是 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)，或者某个 Statement 对象，例如 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 或 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)）时，如果不再需要这些对象，应使用其 close 方法来显式关闭它们。 这样可以尽快地释放驱动程序和服务器资源，而不是等待 Java 虚拟机垃圾收集器执行此操作，从而提高性能。  
  
 当您使用滚动锁定时，要在服务器上保持良好的并发性能，则关闭对象尤其重要。 上一次访问的提取缓冲区中的滚动锁定会一直保持，直到关闭结果集。 类似地，语句准备的句柄会一直保留，直到关闭此语句。 如果您对多条语句重复使用一个连接，则在让语句退出作用域之前关闭这些语句会使服务器过早地清除已准备的句柄。  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序提升性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
