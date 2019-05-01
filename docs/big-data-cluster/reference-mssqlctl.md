---
title: mssqlctl 参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ebd3b63d641c77dae1afbff21264ec4fe34df4d0
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473467"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**mssqlctl**适用于工具[SQL Server 2019 大数据群集 （预览版）](big-data-cluster-overview.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
|[mssqlctl 应用](reference-mssqlctl-app.md) | 创建、 删除、 运行和管理应用程序。 |
|[mssqlctl cluster](reference-mssqlctl-cluster.md) | 选择、 管理和运行群集。 |
[mssqlctl login](#mssqlctl-login) | 登录到群集。
[mssqlctl logout](#mssqlctl-logout) | 日志移出群集。
|[mssqlctl storage](reference-mssqlctl-storage.md) | 管理群集的存储。 |
## <a name="mssqlctl-login"></a>mssqlctl 登录名
登录到群集。
```bash
mssqlctl login [--username -u] 
               [--password -p]  
               [--endpoint -e]
```
### <a name="examples"></a>示例
以交互方式登录。
```bash
mssqlctl login
```
用户名和密码登录。
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret
```
登录用户名、 密码和群集终结点。
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```
### <a name="optional-parameters"></a>可选参数
#### `--username -u`
帐户的用户。
#### `--password -p`
密码凭据。
#### `--endpoint -e`
群集主机和端口 （例如）"http://host:port"。
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
## <a name="mssqlctl-logout"></a>mssqlctl 注销
日志移出群集。
```bash
mssqlctl logout 
```
### <a name="examples"></a>示例
注销此用户。
```bash
mssqlctl logout
```
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