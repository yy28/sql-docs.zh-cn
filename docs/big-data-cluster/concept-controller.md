---
title: 什么是控制器？
titleSuffix: SQL Server big data clusters
description: 本文介绍 SQL Server 2019 大数据群集 (预览版) 的控制器。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e984c3dced4bde713ac98d67c22481e54491cd68
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419535"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>SQL Server 大数据群集上的控制器是什么？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

控制器承载用于部署和管理大数据群集的核心逻辑。 它负责与 Kubernetes 的所有交互, SQL Server 作为群集的一部分的实例以及 HDFS 和 Spark 等其他组件。

控制器服务提供以下核心功能:

- 管理群集生命周期: 群集启动 & 删除、更新配置
- 管理 master SQL Server 实例
- 管理计算、数据和存储池
- 公开监视工具以观察群集状态
- 公开故障排除工具以检测和修复意外问题
- 管理群集安全:
  - 确保安全群集终结点
  - 管理用户和角色
  - 为群集内部通信配置凭据

## <a name="deploying-the-controller-service"></a>部署控制器服务

控制器部署并托管在与客户想要构建大数据群集的同一 Kubernetes 命名空间中。 此服务由 Kubernetes 管理员在群集启动过程中使用**azdata**命令行实用程序进行安装。 有关详细信息, 请参阅[SQL Server 大数据群集入门](deploy-get-started.md)。

Ring 工作流将在 Kubernetes 上布局 SQL Server 大数据群集, 其中包括[概述](big-data-cluster-overview.md)一文中所述的所有组件。 首先, 启动工作流创建控制器服务, 部署此服务后, 控制器服务将协调主机、计算、数据和存储池的其他服务部分的安装和配置。

## <a name="managing-the-cluster-through-the-controller-service"></a>通过控制器服务管理群集

可以使用**azdata**命令通过控制器服务管理群集。 如果将其他 Kubernetes 对象 (如 pod) 部署到同一个命名空间, 则控制器服务不会管理或监视这些对象。 你还可以使用**kubectl**命令来管理 Kubernetes 级别的群集。 有关详细信息, 请参阅[SQL Server 大数据群集的监视和故障排除](cluster-troubleshooting-commands.md)。

为大数据群集创建的控制器和 Kubernetes 对象 (有状态集、箱、机密等) 驻留在专用 Kubernetes 命名空间中。 Kubernetes 群集管理器将授予控制器服务管理该命名空间中的所有资源的权限。  在使用**azdata**进行初始群集部署的过程中, 将自动配置此方案的 RBAC 策略。

### <a name="azdata"></a>azdata

**azdata**是用 Python 编写的命令行实用程序, 群集管理员可以通过控制器服务公开的 REST api 来启动和管理大数据群集。

## <a name="controller-service-security"></a>控制器服务安全

与控制器服务的所有通信都通过 HTTPS 上的 REST API 进行。 在启动时, 将自动为您生成一个自签名证书。 

控制器服务终结点的身份验证基于用户名和密码。 使用环境变量`CONTROLLER_USERNAME`的输入和, `CONTROLLER_PASSWORD`在群集启动时设置这些凭据。

> [!NOTE]
> 必须提供符合[SQL Server 密码复杂性要求](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017)的密码。

## <a name="next-steps"></a>后续步骤

若要详细了解 SQL Server 大数据群集, 请参阅以下资源:

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
- [此次Microsoft SQL Server 大数据群集体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
