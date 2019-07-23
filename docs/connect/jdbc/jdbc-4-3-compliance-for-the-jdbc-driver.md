---
title: JDBC 驱动程序的 JDBC 4.3 符合性 |Microsoft Docs
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
ms.openlocfilehash: 20cefb029a126b0a262d86a2dc0a0791959085bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956369"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 驱动程序的 JDBC 4.3 符合性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> 早于 Microsoft SQL Server JDBC 驱动程序 6.4 的版本仅兼容 Java Database Connectivity (JDBC) API 4.2 规范。 本部分不适用于 6.4 版本和之前的版本。

从6.4 版, 适用于 SQL Server 的 Microsoft JDBC Driver 是 JAVA 9 兼容的`SQLFeatureNotSupportedException` , 并为具有未实现方法的新 JDBC 4.3 api 引发。

对于 SQL Server 版本的 Microsoft JDBC Driver 7.0, 该驱动程序现在兼容 JAVA 10, 并支持下面所述的 Api。 驱动程序对`SQLFeatureNotSupportedException` JDBC 4.3 规范中其他未实现的方法引发。

|新 API|描述|值得注意的实现|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|此连接上开始了请求 (独立工作单元) 的提示。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)。|保存可通过`databaseAutoCommitMode`公共 API 方法修改的连接字段的值:、 `serverPreparedStatementDiscardThreshold` `disableStatementPooling` `transactionIsolationLevel`、 `networkTimeout`、 `holdability`、 `sendTimeAsDatetime`、 `statementPoolingCacheSize` `enablePrepareOnFirstPreparedStatementCall`、、、、`catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|有关请求 (独立工作单元) 已完成的驱动程序提示。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)。|关闭在工作单元期间创建的语句, 并回滚任何打开的事务。 方法还会还原对上面列出的连接字段所做的更改。|
