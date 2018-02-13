---
title: "在 Linux 上的 SQL Server 的安全限制 |Microsoft 文档"
description: "本文介绍 SQL Server 上 Linux 限制。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/30/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.workload: Inactive
ms.openlocfilehash: 54e7518c24cb75e5f41f8fc6a4c5a159093ca66a
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Linux 上 SQL Server 的安全限制

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux 上的 SQL Server 当前具有以下限制：

* 提供了标准密码策略。 MUST_CHANGE 是可以配置的唯一选项。  
* 不支持可扩展密钥管理。 
* 不支持使用 Azure Key Vault 中存储的密钥。
* SQL Server 生成自己的自签名证书，用于加密连接。 SQL Server 可以配置为使用提供的 TLS 证书的用户。 

有关 SQL Server 中提供的安全功能的详细信息，请参阅[SQL Server 数据库引擎和 Azure SQL 数据库安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## <a name="next-steps"></a>后续步骤

常见的安全任务，请参阅[入门在 Linux 上的 SQL Server 的安全功能](sql-server-linux-security-get-started.md)。 为一个脚本来更改 TCP 端口号，SQL Server 目录中，并配置跟踪标志或排序规则，请参阅[mssql conf 与 Linux 上配置 SQL Server](sql-server-linux-configure-mssql-conf.md)。
