---
title: mssqlctl 应用模板参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 应用模板命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0b4cbae0ba35c0cef777b3535b2012ab78f8e6da
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473451"
---
# <a name="mssqlctl-app-template"></a>mssqlctl 应用模板

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**应用模板**中的命令**mssqlctl**工具。 有关其他详细信息**mssqlctl**命令，请参阅[mssqlctl 引用](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl 应用模板列表](#mssqlctl-app-template-list) | 提取支持的模板。
[mssqlctl 应用模板请求](#mssqlctl-app-template-pull) | 下载支持的模板。
## <a name="mssqlctl-app-template-list"></a>mssqlctl 应用模板列表
在指定的 [URL] github 存储库提取支持模板。
```bash
mssqlctl app template list [--url -u] 
                           
```
### <a name="examples"></a>示例
提取默认模板存储库位置下的所有模板。
```bash
mssqlctl app template list
```
提取不同的存储库位置下的所有模板。
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>可选参数
#### `--url -u`
指定不同的模板存储库位置。 默认值： https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-template-pull"></a>mssqlctl 应用模板请求
下载指定的 [URL] github 存储库下支持的模板。
```bash
mssqlctl app template pull [--name -n] 
                           [--url -u]  
                           [--destination -d]
```
### <a name="examples"></a>示例
下载默认模板存储库位置下的所有模板。
```bash
mssqlctl app template pull
```
下载其他存储库位置下的所有模板。
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
下载单个模板，按名称。
```bash
mssqlctl app template pull --name ssis            
```
### <a name="optional-parameters"></a>可选参数
#### `--name -n`
模板名称。 有关支持的模板 namesrun 关闭的完整列表 `mssqlctl app template list`
#### `--url -u`
指定不同的模板存储库位置。 默认值： https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
应用程序框架模板放在何处。
`./templates`
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