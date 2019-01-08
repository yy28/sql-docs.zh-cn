---
title: 群集管理门户
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何使用群集管理门户监视 SQL Server 2019 大数据群集 （预览版）。
author: yualan
ms.author: alayu
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 46d2565ac90bfd007bbe0f3c9e8a2382ca5eeb74
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215533"
---
# <a name="how-to-use-the-cluster-administration-portal-to-monitor-a-sql-server-big-data-cluster"></a>如何使用群集管理门户监视 SQL Server 大数据群集

如果你想要监视或进行故障排除 SQL Server 2019 大数据群集 （预览版），使用群集管理门户。

群集管理门户，您可以：
- 快速查看运行 pod 和任何问题的数量
- 监视部署状态
- 查看可用的服务终结点
- 视图控制器和 SQL Server 主实例
- 向下钻取 pod 使用，包括访问 Grafana 仪表板和 Kibana 日志的信息

## <a name="access-the-cluster-administration-portal"></a>访问群集管理门户

请按照[快速入门部署大数据群集](quickstart-big-data-cluster-deploy.md)直至到达**群集管理门户**部分。 运行时与 mssqlctl 的大数据群集后，请遵循以下说明：

控制器 pod 运行后，可以使用群集管理门户来监视部署。 您可以访问在门户中使用的外部 IP 地址和端口号`service-proxy-lb`(例如： **https://\<ip 地址\>: 30777/门户**)。 凭据的访问管理门户中的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的环境变量。

> [!NOTE]
> 对于 CTP 2.2 没有安全警告时访问 web 页，因为它使用自动生成的 SSL 证书。

## <a name="overview"></a>概述

![概述](./media/cluster-admin-portal/portal-overview.png)

当您首次进入门户时，可以快速查看运行的 pod 数：
- 控制器
- 主实例
- 计算池
- 存储池
- 数据池

如果有任何问题，则可以打开的已知问题的链接。 可以使用左侧的导航窗格以转到特定的池，如果出现问题。

## <a name="deployment"></a>部署

![部署](./media/cluster-admin-portal/portal-deployment.png)

若要监视你的部署，请单击左侧的部署选项卡上。 您可以看到你的部署的树视图以及是否在部署中有任何问题。

## <a name="service-endpoints"></a>服务终结点

![端点](./media/cluster-admin-portal/portal-endpoints.png)

可以通过单击左侧的导航窗格上的终结点选项卡上查看可用的服务终结点。

这包括 Spark 终结点，Grafana 仪表板的链接和 Kibana 日志。

## <a name="controller"></a>控制器

![控制器](./media/cluster-admin-portal/portal-controller.png)

在控制器显示与控制器相关的所有 pod。 了解控制器[此处。](concept-controller.md)

若要了解每个 pod 的更多其他信息，您可以单击**指标**该列以查看 Grafana 仪表板。

若要了解有关的问题的 pod 日志，可以单击**日志**列。

## <a name="master-instance"></a>主实例

![端点](./media/cluster-admin-portal/portal-master.png)

主实例显示了与 SQL Server 主实例相关的所有 pod。 了解 SQL Server 主实例[此处。](concept-master-instance.md)

若要了解每个 pod 的更多其他信息，您可以单击**指标**该列以查看 Grafana 仪表板。

若要了解有关的问题的 pod 日志，可以单击**日志**列。

## <a name="pool-and-pod-pages"></a>池和 Pod 页

![池](./media/cluster-admin-portal/portal-data-pool.png)

在每个池页上 （计算、 存储和数据），您可以深化到每个 pod 页上单击**默认**

![Pod](./media/cluster-admin-portal/portal-data-default-pool.png)

这将显示向下钻取路径顶部痕迹导航。

若要了解每个 pod 的更多其他信息，您可以单击**指标**该列以查看 Grafana 仪表板。

若要了解有关的问题的 pod 日志，可以单击**日志**列。

若要了解有关每个池的详细信息：
- [计算池](concept-compute-pool.md)
- [存储池](concept-storage-pool.md)
- [数据池](concept-data-pool.md)

## <a name="about-page"></a>有关页

![有关](./media/cluster-admin-portal/portal-about.png)

此处你可以查看的文档，例如不同的版本号、 容器和链接群集有关的信息。

## <a name="next-steps"></a>后续步骤

除了群集管理门户中，您还可以运行多个有用的 Kubernetes 命令来浏览状态和群集的运行状况。 有关详细信息，请参阅[Kubectl 命令进行监视和故障排除 SQL Server 大数据群集](cluster-troubleshooting-commands.md)。

若要了解有关 SQL Server 2019 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
