---
title: azdata 应用程序模板参考
titleSuffix: SQL Server big data clusters
description: Azdata 应用模板命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3b257a2bacc56a7907ab0d25f492ed0ebd605543
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426327"
---
# <a name="azdata-app-template"></a>azdata 应用模板

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了**azdata**工具中的**应用模板**命令参考。 有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata 应用模板列表](#azdata-app-template-list) | 提取支持的模板。
[azdata 应用模板拉取](#azdata-app-template-pull) | 下载支持的模板。
## <a name="azdata-app-template-list"></a>azdata 应用模板列表
提取指定的 [URL] github 存储库下支持的模板。
```bash
azdata app template list [--url -u] 
                         
```
### <a name="examples"></a>示例
提取默认模板存储库位置下的所有模板。
```bash
azdata app template list
```
获取不同存储库位置下的所有模板。
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>可选参数
#### `--url -u`
指定不同的模板存储库位置。 缺省值 https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="azdata-app-template-pull"></a>azdata 应用模板拉取
下载指定的 [URL] github 存储库下支持的模板。
```bash
azdata app template pull [--name -n] 
                         [--url -u]  
                         [--destination -d]
```
### <a name="examples"></a>示例
下载默认模板存储库位置下的所有模板。
```bash
azdata app template pull
```
下载其他存储库位置下的所有模板。
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
按名称下载单个模板。
```bash
azdata app template pull --name ssis            
```
### <a name="optional-parameters"></a>可选参数
#### `--name -n`
模板名称。 有关支持的模板的完整列表 namesrun`azdata app template list`
#### `--url -u`
指定不同的模板存储库位置。 缺省值 https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
应用程序主干模板的放置位置。
`./templates`
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

有关其他**azdata**命令的详细信息, 请参阅[azdata reference](reference-azdata.md)。 有关如何安装**azdata**工具的详细信息, 请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
