---
title: 什么是 SQL Server 大数据群集控制器？ | Microsoft Docs
description: ''
author: mihaelablendea
ms.author: mihaelab
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 6b3a8f01170fecf21fd85dbb2d85d228430fc100
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795901"
---
# <a name="what-is-the-sql-server-big-data-clusters-controller"></a>什么是 SQL Server 大数据群集控制器？

控制器托管用于部署和管理大数据群集的核心逻辑。 它负责与 Kubernetes，是在群集和 HDFS 和 Spark 等其他组件的一部分的 SQL Server 实例的所有交互。 

控制器服务提供了以下的核心功能：

- 管理群集生命周期： 群集启动和删除、 更新配置
- 管理主 SQL Server 实例
- 管理计算、 数据和存储池
- 公开监视工具来观察群集的状态
- 公开来检测和修复意外的问题的故障排除工具
- 管理群集安全性： 确保安全的群集终结点、 管理用户和角色，配置为群集内通信的凭据
- 管理升级的工作流，以便安全地实现 （在 CTP 2.0 中不可用）
- 管理 （在 CTP 2.0 中不可用） 群集中的有状态服务的高可用性和灾难恢复

## <a name="deploying-the-controller-service"></a>部署控制器服务

控制器是部署并托管在客户要构建大数据群集相同的 Kubernetes 命名空间中。 在群集启动，使用 mssqlctl 命令行实用工具，Kubernetes 管理员安装此服务：

```bash
mssqlctl create cluster <name of your cluster>
```

建设工作流将基于 Kubernetes 的布局包括中所述的所有组件的完全正常运行的 SQL Server 大数据群集[概述](big-data-cluster-overview.md)一文。 启动工作流首先创建控制器服务，这部署后，控制器服务会协调安装和配置 master、 计算、 数据和存储池的服务部分的其余部分。

## <a name="managing-the-cluster-through-the-controller-service"></a>控制器服务通过群集进行管理
你可以管理仅通过使用控制器服务在群集`mssqlctl`Api 或群集中承载的群集管理门户。 如果 pod 等其他 Kubernetes 对象部署到相同的命名空间时，它们是未托管或由控制器服务监视。

在控制器和大数据群集创建的 Kubernetes 对象 （有状态集，pod、 机密等） 驻留在专用的 Kubernetes 命名空间。 控制器服务将由 Kubernetes 群集管理器来管理该命名空间中的所有资源授予的权限。  初始群集部署使用的过程中自动配置此方案中的 RBAC 策略`mssqlctl`。 

### <a name="mssqlctl"></a>mssqlctl

`mssqlctl` 可让群集管理员若要启动和管理大数据群集控制器服务公开的 REST Api 通过 Python 编写命令行实用程序。

### <a name="cluster-administration-portal"></a>群集管理门户

控制器服务启动并运行后，群集管理员可以使用群集管理门户来监视部署进度、 检测和解决群集内服务的问题。 

## <a name="monitoring-and-troubleshooting-the-controller-service"></a>监视和故障排除控制器服务

即将推出。。。

## <a name="controller-service-security"></a>控制器服务安全性
与控制器服务的所有通信通过 HTTPS 都执行通过 REST API。 生成自签名的证书将会自动为你在启动时。 

向控制器服务终结点进行身份验证基于用户名和密码。 这些凭据都在群集启动时使用环境变量的输入预配`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`。
```

> [!NOTE]
> You must provide a password that is in compliance with [SQL Server password complexity requirements](https://docs.microsoft.com/en-us/sql/relational-databases/security/password-policy?view=sql-server-2017).

## Next steps

To learn more about the SQL Server big data clusters, see the following overview:

- [What is SQL Server 2019 big data clusters?](big-data-cluster-overview.md)
