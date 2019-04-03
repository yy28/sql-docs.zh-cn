---
title: mssqlctl 群集调试参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 群集命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b12b0421cf32a36cfd6d681bc90ad9ca7c3f9209
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860548"
---
# <a name="mssqlctl-cluster-debug"></a>mssqlctl 群集调试

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**群集调试**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [copy-logs](#copy-logs) | 复制日志。 |
| [dump](#dump) | 触发器日志记录转储。 |

## <a id="copy-logs"></a> 群集调试复制日志

复制日志。

```
mssqlctl cluster debug copy-logs
   --namespace
   [--container]
   [--pod]
   [--target-folder]
   [--timeout]
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--namespace -n** | 群集名称，用于 kubernetes 命名空间。 必需的。 |
| **--container -c** | 复制日志的容器的名称类似，可选，默认情况下将复制的所有容器的日志。 无法指定多次。 如果指定了多次，最后一个将使用。 |
| **--pod -p** | 将复制的 pod 名称相似的日志。 可选的所有 pod 的默认副本日志。 无法指定多次。 如果指定了多次，最后一个将使用。 |
| **--target-folder -d** | 要复制到日志的目标文件夹路径。 可选，默认情况下结果中创建的本地文件夹。  无法指定多次。 如果指定了多次，最后一个将使用。 |
| **--timeout -t** | 等待命令完成的秒数。 默认值为 0，这是不受限制。 |

## <a id="dump"></a> 群集调试转储

触发器日志记录转储。

```
mssqlctl cluster debug dump
   [--container]
   [--namespace]
   --target-folder
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--container -c** | 复制日志的容器的名称类似，可选，默认情况下将复制的所有容器的日志。 无法指定多次。 如果指定了多次，最后一个将使用。  允许的值： mssql 控制器。 |
| **--namespace -n** | 群集名称，用于 kubernetes 命名空间。 必需的。 |
| **--target-folder -d** | 要复制到日志的目标文件夹路径。 可选，默认情况下结果中创建的本地文件夹。  无法指定多次。 如果指定了多次，最后一个将使用。  默认值： `./output/dump`。 必需的。 |

## <a name="next-steps"></a>后续步骤

有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。