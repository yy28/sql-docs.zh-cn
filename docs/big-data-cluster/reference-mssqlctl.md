---
title: mssqlctl 引用
titleSuffix: SQL Server 2019 big data clusters
description: Mssqlctl 命令的参考文章。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: be1ece46bd171370a91273c832bf89a0bf426cd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018363"
---
# <a name="mssqlctl"></a>mssqlctl

以下文章提供了参考**mssqlctl**工具，用于 SQL Server 2019 大数据群集 （预览版）。

## <a id="commands"></a> 命令

|||
|---|---|
| [app](reference-mssqlctl-app.md) | 创建、 删除、 运行和管理应用程序。 |
| [cluster](reference-mssqlctl-cluster.md) | 选择、 管理和运行群集。 |
| [login](#login) | 登录到群集。 |
| [logout](#logout) | 日志移出群集。 |
| [storage](reference-mssqlctl-storage.md) | 管理群集的存储。 |

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