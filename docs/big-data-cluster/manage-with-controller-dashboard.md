---
title: 通过控制器仪表板管理 SQL Server 大数据群集
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: 使用 Azure Data Studio 中的笔记本管理大数据群集和排除其故障。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 08/29/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5fadb9b069e6f70cb780e6dc69295f63330a683a
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160717"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>管理 SQL Server 控制器仪表板的大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

除了**azdata**和群集状态笔记本以外, 还有另一种方法可以查看 SQL Server 大数据群集的状态。 现在可以通过**连接**viewlet 添加 SQL Server 大数据群集控制器。 这使你可以使用仪表板查看群集运行状况。

![面板](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>先决条件

若要启动笔记本, 需要满足以下先决条件:

* 已安装 [Azure Data Studio 预览体验内部版本](https://docs.microsoft.com/sql/big-data-cluster/deploy-big-data-tools?view=sqlallproducts-download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc)的最新版本
* 已在 Azure Data Studio 中安装 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 扩展

除此之外, SQL Server 2019 大数据群集也需要:

* **azdata**
    - [Linux 包管理器](deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)


## <a name="add-sql-server-big-data-cluster-controller"></a>添加 SQL Server 大数据群集控制器

1. 单击左侧窗格中的 "连接" 视图。
2. 在 "连接" 视图底部, 单击 " **SQL Server 大数据群集**" 将其展开。
3. 单击 "**添加 SQL Server 大数据群集控制器**", 这将启动一个新对话框。

## <a name="add-new-controller"></a>添加新控制器

1. 添加群集名称。
2. 添加群集管理服务 URL。 这可以在 BDC 仪表板的 "服务终结点" 表中找到, 也可以询问群集管理员。
3. 添加用户名和密码。

## <a name="launch-controller-dashboard"></a>启动控制器仪表板

1. 成功添加控制器后, 可以在 SQL Server 大数据群集 "下查看它。
2. 若要启动该仪表板, 请右键单击该控制器, 然后单击 "**管理**"。

## <a name="controller-dashboard"></a>控制器仪表板

1. 控制器仪表板上有3个主要组件:

    - 顶层**工具栏**, 其中包含仪表板的操作。
    - 左侧的**导航窗格**, 可更改仪表板上的不同视图。
    - 涵盖大部分页面的**视图**。

2. 在**大数据群集概述**页上, 可以看到:

    - 用于查看有关群集的信息的**群集属性**。
    - **群集概述**若要查看所有群集组件的高级概述以及哪些组件不正常
    - 用于复制或访问 SQL Server 大数据群集内的不同服务的**服务终结点**。

3. 在**导航窗格中,** 可以看到服务列表, 单击其中一个可查看其他群集详细信息。 单击**群集概述**中的服务时, 这是相同的视图。

4. **群集详细信息**下的每个视图都包含相同的 UI 组件:

    - 共享组件的状态和运行状况状态的**运行状况详细信息**。
    - 通过 Grafana 和 Kibana 查看其他指标和日志的**指标和日志**。

1. 如果查看不正常的组件, 请单击工具栏上的 "**故障排除**", 启动包含可帮助诊断问题的笔记本的 Jupyter 书籍。

## <a name="next-steps"></a>后续步骤

有关控制器的详细信息, 请参阅[控制器文档](concept-controller.md)。