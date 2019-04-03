---
title: mssqlctl 参考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b050638ee0ca600c5df0ecdbe5616b801f41e7a8
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860349"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

以下文章提供了参考**mssqlctl**适用于工具[SQL Server 2019 大数据群集 （预览版）](big-data-cluster-overview.md)。 有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [app](reference-mssqlctl-app.md) | 创建、 删除、 运行和管理应用程序。 |
| [群集](reference-mssqlctl-cluster.md) | 选择、 管理和运行群集。 |
| [login](#login) | 登录到群集。 |
| [注销](#logout) | 日志移出群集。 |
| [存储](reference-mssqlctl-storage.md) | 管理群集的存储。 |

## <a id="login"></a> mssqlctl login

登录到群集。

```
mssqlctl login
   --endpoint
   --password
   --username
```

### <a name="parameters"></a>Parameters

| 参数 | Description |
|---|---|
|**--endpoint -e**| 群集主机和端口 （例如） `http://host:port"`。 |
|**--password -p**| 密码凭据。 |
|**--username -u**| 帐户的用户。 |

### <a name="examples"></a>示例

以交互方式登录。

```
mssqlctl login
```

用户名和密码登录。

```
mssqlctl login -u johndoe@contoso.com -p VerySecret
```

登录用户名、 密码和群集终结点。

```
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```

## <a id="logout"></a> mssqlctl logout

日志移出群集。

```
mssqlctl logout
   --username
```

### <a name="parameters"></a>Parameters

| Parameters | Description |
|---|---|
| **--username -u** | 帐户用户，如果缺失，注销当前有效的帐户。 |

### <a name="examples"></a>示例

注销此用户。

```
mssqlctl logout --username admin
```

## <a name="next-steps"></a>后续步骤

有关如何安装详细信息**mssqlctl**工具，请参阅[安装 mssqlctl 来管理 SQL Server 2019 大数据群集](deploy-install-mssqlctl.md)。