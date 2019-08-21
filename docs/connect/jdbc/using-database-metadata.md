---
title: 使用数据库元数据 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fce2bf9d72136b303ee3bc974f3aede313233a82
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026422"
---
# <a name="using-database-metadata"></a>使用数据库元数据

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

为了查询数据库以获得其支持内容的有关信息，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 实现了 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 类。 该类包含很多以单个值或结果集的形式返回信息的方法。

若要创建一个 SQLServerDatabaseMetaData 对象，可以使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) 方法获得有关已连接到的数据库的信息。

在下面的示例中, 将向[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]此函数传递示例数据库的打开连接, 使用 SQLServerConnection 类的 getMetaData 方法返回 SQLServerDatabaseMetadata 对象, 然后使用SQLServerDatabaseMetaData 对象用于显示有关驱动程序、驱动程序版本、数据库名和数据库版本的信息。

[!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序处理元数据](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
