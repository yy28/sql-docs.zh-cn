---
title: "在 Linux 上的 SQL Server 的安全限制 |Microsoft 文档"
description: "本主题介绍 SQL Server 上 Linux 限制。"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.workload: Inactive
ms.openlocfilehash: 1c7348433aa9162f64e1ecccb9301276c46ce383
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Linux 上 SQL Server 的安全限制

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Linux 上的 SQL Server 当前具有以下限制：

* 提供了标准密码策略。 MUST_CHANGE 是可以配置的唯一选项。  
* 不支持可扩展密钥管理。 
* 不支持使用 Azure Key Vault 中存储的密钥。
* SQL Server 生成自己的自签名证书，用于加密连接。 目前，无法将 SQL Server 配置为使用用户提供的用于 SSL 或 TLS 的证书。 

有关 SQL Server 中提供的安全功能的详细信息，请参阅[SQL Server 数据库引擎和 Azure SQL 数据库安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## <a name="next-steps"></a>后续步骤

常见的安全任务，请参阅[入门在 Linux 上的 SQL Server 的安全功能](sql-server-linux-security-get-started.md)。   
为一个脚本来更改 TCP 端口号，SQL Server 目录中，并配置跟踪标志或排序规则，请参阅[mssql conf 与 Linux 上配置 SQL Server](sql-server-linux-configure-mssql-conf.md)。
