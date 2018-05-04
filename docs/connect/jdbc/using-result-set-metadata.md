---
title: 使用结果设置元数据 |Microsoft 文档
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
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2b00d44989a4289ed8c6d8bb3d2086732c3aaca
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-result-set-metadata"></a>使用结果集元数据
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要查询的结果集有关它包含的列信息[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]实现[SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)类。 该类包含很多以单个值的形式返回信息的方法。  
  
 若要创建 SQLServerResultSetMetaData 对象，可以使用[getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数，SQLServerResultSet 类的 getMetaData 方法用于返回 SQLServerResultSetMetaData 对象，以及然后各种方法SQLServerResultSetMetaData 对象用于显示包含在结果集中的列的名称和数据类型有关的信息。  
  
 [!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序处理元数据](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
