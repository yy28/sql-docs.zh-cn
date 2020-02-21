---
title: JDBC 驱动程序的 JDBC 4.3 合规性 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed9b10ad9e9a927789505c7d7327c6cf4d1ff3c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027943"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 驱动程序的 JDBC 4.3 合规性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> 早于 Microsoft SQL Server JDBC 驱动程序 6.4 的版本仅兼容 Java Database Connectivity (JDBC) API 4.2 规范。 本部分不适用于 6.4 版本和之前的版本。

从版本 6.4 开始，Microsoft SQL Server JDBC 驱动程序与 JAVA 9 兼容，并针对具有未实现方法的新 JDBC 4.3 API 引发 `SQLFeatureNotSupportedException`。

发布 Microsoft JDBC Driver 7.0 for SQL Server 后，该驱动程序现在与 JAVA 10 兼容，并支持以下 API。 驱动程序针对 JDBC 4.3 规范中其他未实现的方法引发 `SQLFeatureNotSupportedException`。

|新的 API|说明|值得注意的实现|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|用于提示驱动程序，此连接上正在开始发出某个请求（一个独立工作单元）。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)。|通过以下公共 API 方法保存可修改的连接字段的值：`databaseAutoCommitMode`、`transactionIsolationLevel`、`networkTimeout`、`holdability`、`sendTimeAsDatetime`、`statementPoolingCacheSize`、`disableStatementPooling`、`serverPreparedStatementDiscardThreshold`、`enablePrepareOnFirstPreparedStatementCall`、`catalogName`、`sqlWarnings`、`useBulkCopyForBatchInsert`。|
|void java.sql.connection.endRequest()|用于提示驱动程序，某个请求（一个独立工作单元）已完成。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)。|关闭在工作单元期间创建的语句，并回滚所有未完成的事务。 该方法还会还原对上面列出的连接字段所做的更改。|
