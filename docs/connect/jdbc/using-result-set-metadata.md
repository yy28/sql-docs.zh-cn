---
title: 使用结果集元数据 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed0b1eedcafa1fab59d17f756523fc0fc189200
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026124"
---
# <a name="using-result-set-metadata"></a>使用结果集元数据

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

为了查询结果集以获取有关它所包含的列的信息，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 实现了 [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 类。 该类包含很多以单个值的形式返回信息的方法。

若要创建 SQLServerResultSetMetaData 对象，可以使用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 类的 [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) 方法。

在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，使用 SQLServerResultSet 类的 getMetaData 方法返回 SQLServerResultSetMetaData 对象，然后使用 SQLServerResultSetMetaData 对象的各种方法显示有关结果集中所包含列的名称和数据类型的信息。

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序处理元数据](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
