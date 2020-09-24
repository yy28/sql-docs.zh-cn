---
title: azdata arc dc status 参考
titleSuffix: SQL Server big data clusters
description: azdata arc dc status 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 82408e8a7f1edb37c33a6f1748119f5ff24f563f
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942397"
---
# <a name="azdata-arc-dc-status"></a>azdata arc dc status

适用于 `azdata`

以下文章提供了 azdata 工具中 sql 命令的参考********。 有关其他 azdata 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)****

## <a name="commands"></a>命令

|命令|说明|
| --- | --- |
[azdata arc dc status show](#azdata-arc-dc-status-show) | 显示数据控制器的状态。
## <a name="azdata-arc-dc-status-show"></a>azdata arc dc status show
显示数据控制器的状态。
```bash
azdata arc dc status show [--namespace -ns] 
                          
```
### <a name="examples"></a>示例
显示特定命名空间中数据控制器的状态。
```bash
azdata arc dc status show --namespace <ns>
```
### <a name="optional-parameters"></a>可选参数
#### `--namespace -ns`
数据控制器所在的 Kubernetes 命名空间。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org)，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关其他 azdata 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 

有关如何安装 azdata 工具的详细信息，请参阅[安装 azdata](..\install\deploy-install-azdata.md)。

