---
title: mssqlctl bdc 终结点引用
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 终结点命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ae9a5ad79f388f260494c18448dd80e815b3ac02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958080"
---
# <a name="mssqlctl-bdc-endpoint"></a>mssqlctl bdc 终结点

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**bdc 终结点**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl bdc 终结点列表](#mssqlctl-bdc-endpoint-list) | 列出了大数据群集终结点。
## <a name="mssqlctl-bdc-endpoint-list"></a>mssqlctl bdc 终结点列表
列出了大数据群集终结点。
```bash
mssqlctl bdc endpoint list [--endpoint-name -e] 
                           
```
### <a name="optional-parameters"></a>可选参数
#### `--endpoint-name -e`
BDC 终结点名称。
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

有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。