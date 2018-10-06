---
title: 监视群集使用群集管理门户 |Microsoft Docs
description: ''
author: yualan
ms.author: alayu
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 3ae85c9e9078b91589b828d1bee9d3218b5316cc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795924"
---
# <a name="introduction-to-the-cluster-administration-portal"></a>群集管理门户简介
如果你想要监视或进行故障排除 SQL Server 大数据群集，使用群集管理门户。 

群集管理门户，您可以：
- 快速查看运行 pod 和任何问题的数量
- 监视部署状态
- 查看可用的服务终结点
- 视图控制器和 SQL Server 主实例
- 向下钻取 pod 使用，包括访问 Grafana 仪表板和 Kibana 日志的信息

## <a name="access-the-cluster-administration-portal"></a>访问群集管理门户
请按照[快速入门部署大数据群集](quickstart-big-data-cluster-deploy.md)直至到达**群集管理门户**部分。 运行时与 mssqlctl 的大数据群集后，请遵循以下说明：

控制器 pod 运行后，可以使用群集管理门户来监视部署。 您可以访问在门户中使用的外部 IP 地址和端口号`service-proxy-lb`(例如： **https://\<ip 地址\>: 30777**)。 凭据的访问管理门户中的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的环境变量。
> [!NOTE]
> 存在将访问网页，因为我们要使用自动生成的 SSL 证书时一条安全警告。 在将来的版本中，我们将提供的功能来提供自己的签名的证书。

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
