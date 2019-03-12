---
title: JDBC 4.3 符合性的 JDBC 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc2fbb2b217880b255d522149dabd38701a8c0e4
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579057"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 驱动程序的 JDBC 4.3 符合性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> 早于 Microsoft SQL Server JDBC 驱动程序 6.4 的版本仅兼容 Java Database Connectivity (JDBC) API 4.2 规范。 本部分不适用于 6.4 版本和之前的版本。

自版本 6.4，SQL Server 的 Microsoft JDBC 驱动程序将 JAVA 9 兼容，并且`SQLFeatureNotSupportedException`具有未实现方法的新 JDBC 4.3 api。

使用 SQL Server 版本的 Microsoft JDBC 驱动程序 7.0，该驱动程序现在是 JAVA 10 兼容，并且支持下面所述的 Api。 驱动程序将引发`SQLFeatureNotSupportedException`有关从 JDBC 4.3 规范的其他未实现方法。

|新的 API|描述|值得注意的实现|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|对请求的工作，独立的单元开始的此连接的驱动程序的提示。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)。|将保存的值是通过公共 API 方法可修改的连接字段： `databaseAutoCommitMode`， `transactionIsolationLevel`， `networkTimeout`， `holdability`， `sendTimeAsDatetime`， `statementPoolingCacheSize`， `disableStatementPooling`， `serverPreparedStatementDiscardThreshold`， `enablePrepareOnFirstPreparedStatementCall`，`catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|对已完成请求，独立的单元的工作，该驱动程序的提示。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)。|关闭期间的工作单元创建的语句，并回滚任何打开的事务。 该方法还将恢复对上面列出的连接字段的更改。|
