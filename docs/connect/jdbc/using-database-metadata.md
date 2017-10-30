---
title: "使用数据库元数据 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 421da278e1a4503a73fb4f4f8a8aba0b3cff672f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-database-metadata"></a>使用数据库元数据
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  查询有关它的支持，数据库[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]实现[SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)类。 该类包含很多以单个值或结果集的形式返回信息的方法。  
  
 若要创建 SQLServerDatabaseMetaData 对象，可以使用[getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类，以获取有关连接到数据库的信息。  
  
 在下面的示例中，与的开放连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]示例数据库中传递给函数，SQLServerConnection 类的 getMetaData 方法用于返回 SQLServerDatabaseMetadata 对象，以及然后各种方法SQLServerDatabaseMetaData 对象用于显示有关驱动程序、 驱动程序版本、 数据库名称和数据库版本的信息。  
  
 [!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [处理元数据与 JDBC 驱动程序](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  

