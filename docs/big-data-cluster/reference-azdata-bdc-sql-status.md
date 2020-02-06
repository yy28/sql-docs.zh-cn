---
title: azdata bdc sql status 参考
titleSuffix: SQL Server big data clusters
description: azdata bdc sql status 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d3d640fdeb503a2fe210429f9d2b1ca534b4a0a9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "74821170"
---
# <a name="azdata-bdc-sql-status"></a>azdata bdc sql status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

以下文章提供了 `bdc sql status` 工具中 `azdata` 命令的参考。 有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc sql status show](#azdata-bdc-sql-status-show) | Sql-server 服务状态。
## <a name="azdata-bdc-sql-status-show"></a>azdata bdc sql status show
Sql-server 服务状态。
```bash
azdata bdc sql status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>示例
获取 sql 服务的状态。
```bash
azdata bdc sql status show
```
获取包含所有实例的 sql 服务的状态。
```bash
azdata bdc sql status show --all
```
获取 sql 服务中主资源的状态。
```bash
azdata bdc sql status show --resource master
```
### <a name="optional-parameters"></a>可选参数
#### `--resource -r`
获取此服务中的这个资源。
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
