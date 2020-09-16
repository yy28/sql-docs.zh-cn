---
title: azdata extension 参考
titleSuffix: SQL Server big data clusters
description: azdata extension 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: de222d502cb7caf6faa3118ae39b679e47f3577e
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733495"
---
# <a name="azdata-extension"></a>azdata extension

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

以下文章提供了 `azdata` 工具中 `sql` 命令的参考。 有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。

## <a name="commands"></a>命令
| 命令 | 描述 |
| --- | --- |
[azdata extension add](#azdata-extension-add) | 添加扩展。
[azdata extension remove](#azdata-extension-remove) | 删除扩展。
[azdata extension list](#azdata-extension-list) | 列出所有已安装的扩展。
## <a name="azdata-extension-add"></a>azdata extension add
添加扩展。
```bash
azdata extension add --source -s 
                     [--index]  
                     
[--pip-proxy]  
                     
[--pip-extra-index-urls]  
                     
[--yes -y]
```
### <a name="examples"></a>示例
从 URL 添加扩展。
```bash
azdata extension add --source https://contoso.com/some_ext-0.0.1-py2.py3-none-any.whl
```
从本地磁盘添加扩展。
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl
```
从本地磁盘添加扩展，并将 pip 代理用于依赖项。
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl --pip-proxy https://user:pass@proxy.server:8080
```
### <a name="required-parameters"></a>必需的参数
#### `--source -s`
磁盘上扩展 wheel 或扩展 URL 的路径
### <a name="optional-parameters"></a>可选参数
#### `--index`
Python 包索引的基 URL（默认值为 https://pypi.org/simple) 。 这应该指向符合 PEP 503（简单存储库 API）的存储库或以相同格式展开的本地目录。
#### `--pip-proxy`
用于扩展依赖项的 pip 的代理，格式为 [user:passwd@]proxy.server:port
#### `--pip-extra-index-urls`
要使用的包索引的附加 URL 的空格分隔列表。 这应该指向符合 PEP 503（简单存储库 API）的存储库或以相同格式展开的本地目录。
#### `--yes -y`
不提示确认。
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
## <a name="azdata-extension-remove"></a>azdata extension remove
删除扩展。
```bash
azdata extension remove --name -n 
                        [--yes -y]
```
### <a name="examples"></a>示例
删除扩展。
```bash
azdata extension remove --name some-ext
```
### <a name="required-parameters"></a>必需的参数
#### `--name -n`
扩展名
### <a name="optional-parameters"></a>可选参数
#### `--yes -y`
不提示确认。
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
## <a name="azdata-extension-list"></a>azdata extension list
列出所有已安装的扩展。
```bash
azdata extension list 
```
### <a name="examples"></a>示例
列出扩展。
```bash
azdata extension list
```
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

有关其他 `azdata` 命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 有关如何安装 `azdata` 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](../install/deploy-install-azdata.md)。
