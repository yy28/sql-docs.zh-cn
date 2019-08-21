---
title: azdata bdc control status 参考
titleSuffix: SQL Server big data clusters
description: azdata bdc control status 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c30fa0bdb9e74941387393a7dffeaadcae05b303
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653217"
---
# <a name="azdata-bdc-control-status"></a>azdata bdc control status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了 azdata 工具中的 bdc control status 命令参考。 有关其他 azdata 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc control status show](#azdata-bdc-control-status-show) | 控件状态。
## <a name="azdata-bdc-control-status-show"></a>azdata bdc control status show
控件状态。
```bash
azdata bdc control status show 
```
### <a name="examples"></a>示例
获取控件的状态。
```bash
azdata bdc control status show
```
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关如何安装**azdata**工具的详细信息, 请参阅[install [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]azdata to manage ](deploy-install-azdata.md)。
