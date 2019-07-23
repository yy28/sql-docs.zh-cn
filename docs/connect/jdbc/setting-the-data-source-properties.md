---
title: 设置数据源属性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97e285f5f2680e028a9d8fd00901e3e977ffdd80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004429"
---
# <a name="setting-the-data-source-properties"></a>设置数据源属性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

数据源是在 Java Platform, Enterprise Edition (Java EE) 环境中创建 JDBC 连接的首选机制。 数据源可提供连接、池化连接和分布式连接，并且无需将连接属性硬编码到 Java 代码中。 所有 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 数据源都可以分别使用相应的 setter 和 getter 方法来设置或获取任何属性的值。

通过使用 Java EE 产品（例如应用程序服务器和 servlet/JSP 引擎），通常可配置数据库访问的数据源。 配置允许通过“属性=值”对来输入属性时，可以指定[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)主题中列出的任何属性。

有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源的详细信息，请参阅 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 类。 有关如何使用 SQLServerDataSource 类建立与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库的连接的示例, 请参阅[数据源示例](../../connect/jdbc/data-source-sample.md)。

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
