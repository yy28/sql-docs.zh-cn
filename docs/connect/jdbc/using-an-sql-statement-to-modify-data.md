---
title: 使用 SQL 语句修改数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 750e91c909e859d5d1e3d2bf15b5e0bf4cc11db1
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662429"
---
# <a name="using-an-sql-statement-to-modify-data"></a>使用 SQL 语句修改数据

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

若要使用 SQL 语句修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中包含的数据，可以使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 方法。 executeUpdate 方法会将 SQL 语句传递到数据库进行处理，然后返回一个表示受影响的行数的值。

若要执行此操作，必须首先使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法创建一个 SQLServerStatement 对象。

在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，并构造一条向表中添加新数据的 SQL 语句，然后运行该语句并显示返回值。

[!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]

> [!NOTE]  
> 如果需要使用包含参数的 SQL 语句来修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中的数据，则应使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 类的 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) 方法。
>
> 如果试图向其中插入数据的列包含特殊字符（例如空格），则必须提供要插入的值，即使它们是默认值也必须提供。 如果不执行此操作，插入操作就会失败。
>
> 如果要让 JDBC 驱动程序返回所有更新计数，包括任何可能已不再使用的触发器所返回的更新计数，请将 lastUpdateCount 连接字符串属性设置为“false”。 有关 lastUpdateCount 属性的详细信息，请参阅[连接属性设置](../../connect/jdbc/setting-the-connection-properties.md)。

## <a name="see-also"></a>另请参阅

[使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)
