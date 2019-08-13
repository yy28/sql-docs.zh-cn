---
title: 分析结果 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 163055a630f8e37678f99359a244bf211b035e7e
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894069"
---
# <a name="parsing-the-results"></a>分析结果

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文介绍 SQL Server 期望用户完全处理从任何查询返回的结果。

## <a name="update-counts-and-result-sets"></a>更新计数和结果集

本节将讨论 SQL Server: 更新计数和结果集返回的两个最常见的结果。 通常, 用户执行的任何查询都将导致返回其中的一个结果;处理结果时, 用户应同时处理这两种情况。

下面的代码是一个示例, 说明用户如何循环访问服务器中的所有结果:
```java
try (Connection connection = DriverManager.getConnection(URL); Statement statement = connection.createStatement()) {
    boolean resultsAvailable = statement.execute(USER_SQL);
    int updateCount = -2;
    while (true) {
        updateCount = statement.getUpdateCount();
        if (!resultsAvailable && updateCount == -1)
            break;
        if (resultsAvailable) {
            // handle ResultSet
        } else {
            // handle Update Count
        }
        resultsAvailable = statement.getMoreResults();
    }
}
```

## <a name="exceptions"></a>异常
当您执行导致错误或信息性消息的语句时, SQL Server 的响应方式将有所不同, 具体取决于它是否可以生成执行计划。 可以在语句执行后立即引发错误消息, 也可以需要单独的结果集。 在后一种情况下, 应用程序需要分析结果集以检索异常。

当 SQL Server 无法生成执行计划时, 将立即引发异常。

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

如果 SQL Server 在结果集中返回错误消息, 则需要对结果集进行处理以检索该异常。

```java
String SQL = "SELECT 1/0;";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    if (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            // Exception is thrown on next().
            while (rs.next()) {}
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

如果语句执行生成了多个结果集, 则需要处理每个结果集, 直到达到具有异常的结果集。

```java
String SQL = "SELECT 1; SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    // Does not throw an exception on execute().
    boolean hasResult = statement.execute(SQL);
    while (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            while (rs.next()) {
                System.out.println(rs.getString(1));
            }
        }
        // Moves the next result set that generates the exception.
        hasResult = statement.getMoreResults();
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

在这种情况`String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";`下, 将`execute()`立即引发异常, `SELECT 1`并且根本不执行。

如果 SQL Server 的错误的严重性`0`为`9`, 则将其视为信息性消息, 并返回为`SQLWarning`。

```java
String SQL = "RAISERROR ('WarningLevel5', 5, 2);";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    SQLWarning warning = statement.getWarnings();
    System.out.println(warning);
}
```

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)
