---
title: 使用数据库元数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2f3e0a4e19b30eeb494f89281a01195cf98b7d9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982109"
---
# <a name="using-database-metadata"></a>使用数据库元数据
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  为了查询数据库以获得其支持内容的有关信息，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 实现了 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 类。 该类包含很多以单个值或结果集的形式返回信息的方法。  
  
 若要创建一个 SQLServerDatabaseMetaData 对象，可以使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) 方法获得有关已连接到的数据库的信息。  
  
 在下面的示例中，到打开的连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]向函数传递示例数据库、 SQLServerConnection 类的 getMetaData 方法用于返回一个 SQLServerDatabaseMetadata 对象，然后的各种方法SQLServerDatabaseMetaData 对象，用于显示有关驱动程序、 驱动程序版本、 数据库名称和数据库版本的信息。  
  
 [!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序处理元数据](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
