---
title: azdata bdc 参考
titleSuffix: SQL Server big data clusters
description: azdata bdc 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 408b3c2d55d5e2515a2df979cd54b380a0d54704
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155143"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本文是**azdata**的参考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | 创建大数据群集。
[azdata bdc delete](#azdata-bdc-delete) | 删除大数据群集。
[azdata bdc config](reference-azdata-bdc-config.md) | 配置命令。
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | 终结点命令。
[azdata bdc debug](reference-azdata-bdc-debug.md) | 调试命令。
[azdata bdc status](reference-azdata-bdc-status.md) | BDC 状态命令。
[azdata bdc control](reference-azdata-bdc-control.md) | 控制服务命令。
[azdata bdc sql](reference-azdata-bdc-sql.md) | Sql 服务命令。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Hdfs 服务命令。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 服务命令。
[azdata bdc 网关](reference-azdata-bdc-gateway.md) | 网关服务命令。
[azdata bdc 应用](reference-azdata-bdc-app.md) | 应用服务命令。
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS 模块提供用于访问 HDFS 文件系统的命令。
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 命令允许用户通过创建和管理会话、语句及批处理来与 Spark 系统交互。
## <a name="azdata-bdc-create"></a>azdata bdc create
创建 SQL Server 大数据群集-在系统上需要 Kubernetes 配置, 同时提供以下环境变量 [' CONTROLLER_USERNAME '、' CONTROLLER_PASSWORD '、' MSSQL_SA_PASSWORD '、' KNOX_PASSWORD ']。
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>示例
引导式 BDC 部署体验 - 你将收到所需值的提示。
```bash
azdata bdc create
```
使用参数的 BDC 部署。
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
使用指定名称（而不使用配置文件中的默认名称）的 BDC 部署。
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```
使用参数的 BDC 部署 - 由于使用了 --force 标志，不会给出任何提示。
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>可选参数
#### `--name -n`
大数据群集名称，用于 kubernetes 命名空间。
#### `--config-profile -c`
大数据群集配置配置文件, 用于部署群集: [' aks '、' kubeadm '、' minikube '、' kubeadm-开发-测试 ']
#### `--accept-eula -a`
是否接受许可条款？ [是/否]。 如果不想使用此参数，则可将环境变量 ACCEPT_EULA 设置为“是”。 可以在 https://aka.ms/azdata-eula 和 https://go.microsoft.com/fwlink/?LinkId=2002534 查看此产品的许可条款。
#### `--node-label -l`
大数据群集节点标签，用于指定要部署到的节点。
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
## <a name="azdata-bdc-delete"></a>azdata bdc delete
删除 SQL Server 大数据群集-系统上需要 Kubernetes 配置。
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>示例
BDC 删除。
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>必需的参数
#### `--name -n`
大数据群集名称，用于 kubernetes 命名空间。
### <a name="optional-parameters"></a>可选参数
#### `--force -f`
强制删除大数据群集。
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
