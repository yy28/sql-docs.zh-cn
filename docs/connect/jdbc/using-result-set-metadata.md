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
manager: jroth
ms.openlocfilehash: 60b854cc260f0488f56e77fb10a34025c80d7620
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798635"
---
# <a name="using-result-set-metadata"></a>使用结果集元数据

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

为了查询结果集以获取有关它所包含的列的信息，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 实现了 [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 类。 该类包含很多以单个值的形式返回信息的方法。

若要创建 SQLServerResultSetMetaData 对象，可以使用[getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类。

在下面的示例中，到打开的连接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]向函数传递示例数据库、 SQLServerResultSet 类的 getMetaData 方法用于返回一个 SQLServerResultSetMetaData 对象，然后的各种方法SQLServerResultSetMetaData 对象用于显示有关结果集内包含的列的名称和数据类型的信息。

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序处理元数据](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
