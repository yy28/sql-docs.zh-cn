---
title: azdata bdc status 参考
titleSuffix: SQL Server big data clusters
description: azdata bdc status 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 01518e62d67c27a72bf1e0d78d249b1a64276883
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "74820999"
---
# <a name="azdata-bdc-status"></a>azdata bdc status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

以下文章提供了 `azdata` 工具中 `bdc status` 命令的参考。 有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc status show](#azdata-bdc-status-show) | 显示 BDC 的状态。
## <a name="azdata-bdc-status-show"></a>azdata bdc status show
显示 BDC 的状态。
```bash
azdata bdc status show [--resource -r] 
                       [--all -a]
```
### <a name="examples"></a>示例
用户登录的 BDC 状态。
```bash
azdata bdc status show
```
包含资源的所有实例的 BDC 状态。
```bash
azdata bdc status show --all
```
包含控制资源的服务的 BDC 状态。
```bash
azdata bdc status show --resource control
```
### <a name="optional-parameters"></a>可选参数
#### `--resource -r`
获取与此资源关联的服务。
#### `--all -a`
显示服务中每个资源的所有实例。
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
