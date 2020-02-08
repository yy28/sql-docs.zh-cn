---
title: 配置复制快照文件夹（非默认端口）
titleSuffix: SQL Server on Linux
description: 了解如何在 Linux 上配置快照文件夹共享（非默认端口），以实现 SQL Server 复制。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikerayW
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cb715e2a0a056c18352361b58ce8ffd67e3da78e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558586"
---
# <a name="configure-replication-with-non-default-ports-sql-server-linux"></a>使用非默认端口配置复制 (SQL Server Linux)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

可以通过 Linux 上的 SQL Server 实例（会侦听使用 network.tcpport mssql-conf 设置配置的任何端口）来配置复制。 如果满足以下条件，则需要在配置过程中将端口追加到服务器名称后：

1. 复制设置涉及 Linux 上的 SQL Server 实例
2. 任何实例（Windows 或 Linux）都在侦听非默认端口。 

可以通过在实例上运行 @@servername 来查找实例的服务器名称。

## <a name="examples"></a>示例

“Server1”侦听 Linux 上的端口 1500。 若要配置“Server1”以进行分发，请搭配 `@distributor` 运行 `sp_adddistributor`。 例如： 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

“Server1”侦听 Linux 上的端口 1500。 若要为分发服务器配置发布服务器，请搭配 `@publisher` 运行 `sp_adddistpublisher`。 例如：

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

“Server2”侦听 Linux 上的端口 6549。 若要将“Server2”配置为订阅服务器，请搭配 `@subscriber` 运行 `sp_addsubscription`。 例如：

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

“Server3”侦听 Windows 上的端口 6549，其中服务器名称为 Server3，实例名称为 MSSQL2017。 若要将“Server3”配置为订阅服务器，请配合 `@subscriber` 运行 `sp_addsubscription`。 例如：

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>后续步骤

[概念：Linux 上的 SQL Server 复制](sql-server-linux-replication.md)

[复制存储过程](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

