---
title: 使用结果集元数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86e41f52ed8296c46cfd7b167407b10fc9f0b285
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005940"
---
# <a name="using-result-set-metadata"></a>使用结果集元数据

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

为了查询结果集以获取有关它所包含的列的信息，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 实现了 [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 类。 该类包含很多以单个值的形式返回信息的方法。

若要创建 SQLServerResultSetMetaData 对象, 可以使用[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类的[getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)方法。

在下面的示例中, 将向[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]此函数传递示例数据库的打开连接, 使用 SQLServerResultSet 类的 getMetaData 方法返回 SQLServerResultSetMetaData 对象, 然后使用SQLServerResultSetMetaData 对象用于显示有关结果集中所包含列的名称和数据类型的信息。

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序处理元数据](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
