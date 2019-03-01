---
title: mssqlctl 群集配置引用
titleSuffix: SQL Server 2019 big data clusters
description: Mssqlctl 群集命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 26e93151a1150bbbbd1798b38486ca5b01aaab1d
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018433"
---
# <a name="mssqlctl-cluster-config"></a>mssqlctl 群集配置

以下文章提供了参考**群集配置**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [get](#get) | 获取群集。 |

## <a id="get"></a> mssqlctl cluster config get

获取群集。

```
mssqlctl cluster config get
   --name
   --output-file
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--name -n** | 群集名称，用于 kubernetes 命名空间。 必需的。 |
| **--output-file -f** | 若要将结果存储在输出文件。 必需的。 |

## <a name="next-steps"></a>后续步骤

有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。