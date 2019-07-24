---
title: azdata 笔记本参考
titleSuffix: SQL Server big data clusters
description: Azdata 笔记本命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b96c5e06ec51f53964a28cac86f385d6b42c1dc4
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426007"
---
# <a name="azdata-notebook"></a>azdata 笔记本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了**azdata**工具中**笔记本**命令的参考。 有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata 笔记本视图](#azdata-notebook-view) | 查看笔记本。  在第一次出现单元执行错误时停止的选项。
[azdata 笔记本运行](#azdata-notebook-run) | 运行笔记本。  第一次出现错误时, 执行停止。
## <a name="azdata-notebook-view"></a>azdata 笔记本视图
此命令可获取笔记本文件, 并将 markdown、code 和 output 转换为彩色终端格式。
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>示例
查看笔记本。  这会显示所有单元格。
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
查看笔记本。  这会显示所有单元格, 除非遇到输出中包含错误的单元格。  在这种情况下, 输出将停止。
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要查看的笔记本的路径。
### <a name="optional-parameters"></a>可选参数
#### `--continue-on-error -c`
继续显示其他单元, 忽略在笔记本输出中找到的任何单元格错误。  默认行为是在出现错误时停止。  停止会使第一个出现错误的单元格变得更容易。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值: json、jsonc、table、tsv。  默认值: json。
#### `--query -q`
JMESPath 查询字符串。 有关[http://jmespath.org/](http://jmespath.org/])详细信息和示例, 请参阅。
#### `--verbose`
提高日志记录详细程度。 使用--debug 获取完整的调试日志。
## <a name="azdata-notebook-run"></a>azdata 笔记本运行
此命令创建一个临时目录, 并在其中执行给定的笔记本作为工作目录。
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]
```
### <a name="examples"></a>示例
运行笔记本。
```bash
azdata notebook run --path '/home/me/notebooks/demo_notebook.ipynb'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要运行的笔记本的文件路径。
### <a name="optional-parameters"></a>可选参数
#### `--output-path`
用于笔记本输出的目录路径。  带有输出数据的笔记本和任何笔记本生成的文件都是相对于此目录生成的。
#### `--output-html`
可选标志 indicatingg 是否另外将输出笔记本转换为 HTML 格式。  创建第二个输出文件。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值: json、jsonc、table、tsv。  默认值: json。
#### `--query -q`
JMESPath 查询字符串。 有关[http://jmespath.org/](http://jmespath.org/])详细信息和示例, 请参阅。
#### `--verbose`
提高日志记录详细程度。 使用--debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

有关如何安装**azdata**工具的详细信息, 请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
