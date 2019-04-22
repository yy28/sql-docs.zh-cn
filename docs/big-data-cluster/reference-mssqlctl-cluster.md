---
title: mssqlctl 群集引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl 群集命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e4e54ac3c7206ad8a6592c8cfe0b45d9ea4b8fd8
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860468"
---
# <a name="mssqlctl-cluster"></a>mssqlctl 群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**群集**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [create](#create) | 创建群集。 |
| [delete](#delete) | 删除群集。 |
| [config](reference-mssqlctl-cluster-config.md) | 群集配置命令。 |
| [debug](reference-mssqlctl-cluster-debug.md) | 调试命令。 |

## <a id="create"></a> mssqlctl 群集创建

创建群集。

```
mssqlctl cluster create
   --name
   --accept-eula
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--name -n** | 群集名称，用于 kubernetes 命名空间。 |
| **--accept-eula -e** | 您是否接受许可条款？ \[是/否\]。  允许的值： 不可以，是。 必需的。 |

## <a id="delete"></a> mssqlctl cluster delete

删除群集。

```
mssqlctl cluster delete
   --name
   [--force]
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--name -n** | 群集名称，用于 kubernetes 命名空间。 必需的。 |
| **--force -f** | 强制删除群集。 |

## <a name="next-steps"></a>后续步骤

有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。