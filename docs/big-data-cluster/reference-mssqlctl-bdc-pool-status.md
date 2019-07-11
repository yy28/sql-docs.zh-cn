---
title: mssqlctl bdc 池状态参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 池状态命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 818773708087927b5c2f3ccea44ba52cd77e7a71
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728568"
---
# <a name="mssqlctl-bdc-pool-status"></a>mssqlctl bdc 池状态

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**bdc 池状态**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl bdc 池状态显示](#mssqlctl-bdc-pool-status-show) | 池的状态。
## <a name="mssqlctl-bdc-pool-status-show"></a>mssqlctl bdc 池状态显示
池的状态。
```bash
mssqlctl bdc pool status show --kind -k 
                              [--name -n]
```
### <a name="examples"></a>示例
获取存储池的状态。
```bash
mssqlctl bdc pool status show --kind storage --name default
```
获取数据池的状态。
```bash
mssqlctl bdc pool status show --kind data --name default
```
获取计算池的状态。
```bash
mssqlctl bdc pool status show --kind compute --name default
```
获取主池的状态。
```bash
mssqlctl bdc pool status show --kind master --name default
```
获取 spark 池的状态。
```bash
mssqlctl bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>必需的参数
#### `--kind -k`
BDC 池类型。
### <a name="optional-parameters"></a>可选参数
#### `--name -n`
BDC 池名称。
`default`
### <a name="global-arguments"></a>全局参数
#### `--debug`
增加日志记录详细程度，以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值： json、 jsonc、 table、 tsv。  默认值： json。
#### `--query -q`
JMESPath 查询字符串。 请参阅[ http://jmespath.org/ ](http://jmespath.org/])有关详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用--debug 可获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。