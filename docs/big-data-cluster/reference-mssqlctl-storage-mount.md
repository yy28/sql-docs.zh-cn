---
title: mssqlctl 存储装载参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 存储命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3ad8a97bac1f708dcf01612368c76d584fa39f5c
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860288"
---
# <a name="mssqlctl-storage-mount"></a>mssqlctl 存储装载

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**存储装载**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [create](#create) | 在 HDFS 中创建的远程存储的装载。 |
| [delete](#delete) | 删除远程存储在 HDFS 中的装载。 |
| [status](#status) | Mount(s) 的状态。 |

## <a id="create"></a> mssqlctl storage mount create

在 HDFS 中创建的远程存储的装载。

```
mssqlctl storage mount create
   --local-path
   --remote-uri
   [--credential-file]
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--local-path** | 装入必须是其中的 HDFS 路径创建 （装入的目标）。 必需的。 |
| **--remote-uri** | 要装载 （装入的源） 的远程存储的 URI。 必需的。 |
| **--credential-file** | 包含用于访问远程存储的凭据文件。 凭据必须指定为键 = 值对通过一个键 = 每行的值。 任何等于在键或值需要进行转义。 默认情况下需要没有凭据。 所需的密钥取决于所装入的远程存储的类型和授权使用的类型。 |

### <a name="examples"></a>示例

若要在 HDFS 路径上装载第 2 代 ADLS 帐户"adlsv2example"中的容器"数据"`/mounts/adlsv2/data`使用共享的密钥：

```
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/ --local-path /mounts/adlsv2/data --credentials credential_file
```

若要装载远程 HDFS 群集 (`hdfs://namenode1:8080/`) 上本地 HDFS 路径`/mounts/hdfs/`:

```
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --local-path /mounts/hdfs/
```

## <a id="delete"></a> mssqlctl storage mount delete

删除远程存储在 HDFS 中的装载。

```
mssqlctl storage mount delete
   --local-path
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--local-path** | 对应于具有要删除此安装的 HDFS 路径。 必需的。 |

### <a name="examples"></a>示例

删除装载在 /mounts/adlsv2/data 第 2 代 ADLS 存储帐户的创建。

```
mssqlctl storage mount delete --local-path /mounts/adlsv2/data
```

## <a id="status"></a> mssqlctl storage mount status

Mount(s) 的状态。

```
mssqlctl storage mount status
   --local-path
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--mount-path** | 装载路径。 必需的。 |

### <a name="examples"></a>示例

按路径获取装入状态

```
mssqlctl storage mount status --mount-path /mounts/hdfs
```

获取所有装载的状态。

```
mssqlctl storage mount status
```

## <a name="next-steps"></a>后续步骤

有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。