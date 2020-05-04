---
title: azdata bdc 终结点参考
titleSuffix: SQL Server big data clusters
description: Azdata bdc 终结点命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 71f52b8312518cf669751d50dcc857c3d892bd98
ms.sourcegitcommit: db1b6153f0bc2d221ba1ce15543ecc83e1045453
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2020
ms.locfileid: "82588070"
---
# <a name="azdata-bdc-endpoint"></a>azdata bdc 终结点

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

以下文章提供了 `azdata` 工具中 `bdc endpoint` 命令的参考。 有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc endpoint list](#azdata-bdc-endpoint-list) | 列出大数据群集的终结点。
## <a name="azdata-bdc-endpoint-list"></a>azdata bdc endpoint list
列出大数据群集的终结点。

```bash
azdata bdc endpoint list [--endpoint-name -e] 
```

### <a name="optional-parameters"></a>可选参数

#### `--endpoint-name -e`

大数据群集终结点名称。

### <a name="global-arguments"></a>全局参数

#### `--debug`

提高日志记录详细程度以显示所有调试日志。

#### `--help -h`

显示此帮助消息并退出。

#### `--output -o`

输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。

#### `--query -q`

JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/)，获取详细信息和示例。

#### `--verbose`

提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 有关如何安装 `azdata` 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
