---
title: JDBC 4.3 符合性的 JDBC 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f529c88044444f3fb6e428b6c69f5a5cf5917251
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278908"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 驱动程序的 JDBC 4.3 符合性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  早于 Microsoft JDBC Driver 6.4 for SQL Server 的版本兼容 Java Database Connectivity (JDBC) API 4.2 规范。 本部分不适用于 6.4 版本之前的版本。  
  
 自版本 6.4，适用于 SQL Server 的 Microsoft JDBC Driver 为 JAVA 10 兼容，但并不完全符合 JDBC API 4.3 规范。 该驱动程序未实现方法将引发 SQLFeatureNotSupportedException。 
 
 以下 JDBC 4.3 API 方法在 Microsoft JDBC Driver 6.4 for SQL Server 实现。
 
  **SQLServerConnection 类**  
  
|新方法|描述|值得注意的实现|  
|-----------------|-----------------|-------------------------------|  
|void beginrequest （)|对请求的工作，独立的单元开始的此连接的驱动程序的提示。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)。|将保存的值是通过公共 API 方法可修改的连接字段： `databaseAutoCommitMode`， `transactionIsolationLevel`， `networkTimeout`， `holdability`， `sendTimeAsDatetime`， `statementPoolingCacheSize`， `disableStatementPooling`， `serverPreparedStatementDiscardThreshold`， `enablePrepareOnFirstPreparedStatementCall `，`catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert `.|
|void endRequest()|对已完成请求，独立的单元的工作，该驱动程序的提示。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)。|关闭期间的工作单元创建的语句，并回滚任何打开的事务。 该方法还将恢复对上面列出的连接字段的更改。|