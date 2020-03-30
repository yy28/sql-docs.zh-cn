---
title: 使用 SQL 语句修改数据 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a9de31bad8ef2980e7322b529a6a2b68a12355c2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026753"
---
# <a name="using-an-sql-statement-to-modify-data"></a>使用 SQL 语句修改数据

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

若要使用 SQL 语句修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中包含的数据，可以使用 [SQLServerStatement](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 类的 [executeUpdate](../../connect/jdbc/reference/sqlserverstatement-class.md) 方法。 executeUpdate 方法会将 SQL 语句传递到数据库进行处理，然后返回一个表示受影响的行数的值。

若要执行此操作，必须首先使用 [SQLServerConnection](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 类的 [createStatement](../../connect/jdbc/reference/sqlserverconnection-class.md) 方法创建一个 SQLServerStatement 对象。

在下面的实例中，将向此函数传递 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 示例数据库的打开连接，并构造一条向表中添加新数据的 SQL 语句，然后运行该语句并显示返回值。

[!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]

> [!NOTE]  
> 如果需要使用包含参数的 SQL 语句来修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据，则应使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) 类的 [executeUpdate](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 方法。
>
> 如果试图向其中插入数据的列包含特殊字符（例如空格），则必须提供要插入的值，即使它们是默认值也必须提供。 如果不执行此操作，插入操作就会失败。
>
> 如果要让 JDBC 驱动程序返回所有更新计数，包括任何可能已不再使用的触发器所返回的更新计数，请将 lastUpdateCount 连接字符串属性设置为“false”。 有关 lastUpdateCount 属性的详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。

## <a name="see-also"></a>另请参阅

[使用 SQL 语句](../../connect/jdbc/using-statements-with-sql.md)
