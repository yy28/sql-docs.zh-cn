---
title: azdata 控件引用
titleSuffix: SQL Server big data clusters
description: Azdata 控件命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6fceea54c6ea7d5c904cc27c87033c4a40cff59f
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158212"
---
# <a name="azdata-control"></a>azdata 控件

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本文是**azdata**的参考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata 控件创建](#azdata-control-create) | 创建控制平面。
[azdata 控件删除](#azdata-control-delete) | 删除控制平面。
## <a name="azdata-control-create"></a>azdata 控件创建
Create control 飞机-需要在系统上安装 kube config 以及以下环境变量 [' CONTROLLER_USERNAME '、' CONTROLLER_PASSWORD '、' MSSQL_SA_PASSWORD '、' KNOX_PASSWORD ']。
```bash
azdata control create [--name -n] 
                      [--config-profile -c]  
                      [--accept-eula -a]  
                      [--node-label -l]  
                      [--force -f]
```
### <a name="examples"></a>示例
控件部署。
```bash
azdata control create
```
### <a name="optional-parameters"></a>可选参数
#### `--name -n`
控制平面名称, 用于 kubernetes 命名空间。
#### `--config-profile -c`
用于部署群集的群集配置配置文件: [' aks '、' kubeadm '、' minikube '、' kubeadm-开发-测试 ']
#### `--accept-eula -a`
是否接受许可条款？ [是/否]。 如果不想使用此参数，可以将环境变量 ACCEPT_EULA 设置为“yes”。 可以在 https://aka.ms/azdata-eula 查看此产品的许可条款。
#### `--node-label -l`
节点标签, 用于指定要部署到的节点。
#### `--force -f`
强制创建，系统不会提示用户输入任何值且所有问题都将作为 stderr 的一部分输出。
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
## <a name="azdata-control-delete"></a>azdata 控件删除
删除控制平面-系统上需要 kube 配置。
```bash
azdata control delete --name -n 
                      [--force -f]
```
### <a name="examples"></a>示例
控件部署。
```bash
azdata control delete
```
### <a name="required-parameters"></a>必需的参数
#### `--name -n`
控制平面名称, 用于 kubernetes 命名空间。
### <a name="optional-parameters"></a>可选参数
#### `--force -f`
强制删除控制平面。
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

- 有关其他“azdata”命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 

- 有关如何安装 **azdata** 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。
