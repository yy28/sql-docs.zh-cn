---
title: Linux 上 SQL Server 的安全限制
description: 本文介绍 Linux 上的 SQL Server 限制。
author: VanMSFT
ms.author: vanto
ms.date: 09/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.openlocfilehash: 8a9094977597fd7c2d76f2c80a1773c176b9c6dc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "70929811"
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Linux 上 SQL Server 的安全限制

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux 上的 SQL Server 当前具有以下限制：

* 提供了标准密码策略。 MUST_CHANGE 是可以配置的唯一选项。 不支持 CHECK_POLICY 选项。
* 不支持可扩展密钥管理。 
* 不支持使用 Azure Key Vault 中存储的密钥。
* SQL Server 生成自己的自签名证书，用于加密连接。 可以将 SQL Server 配置为使用用户提供的用于 TLS 的证书。 

有关 SQL Server 提供的安全功能的详细信息，请参阅[SQL Server 数据库引擎和 Azure SQL 数据库的安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## <a name="next-steps"></a>后续步骤

有关常见安全任务，请参阅 [Linux 上的 SQL Server 的安全功能入门](sql-server-linux-security-get-started.md)。 有关更改 TCP 端口号、SQL Server 目录和配置跟踪标志或排序规则的脚本，请参阅 [使用 mssql conf 配置 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md)。
