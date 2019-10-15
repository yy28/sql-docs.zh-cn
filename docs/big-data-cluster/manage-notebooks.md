---
title: 管理 Azure Data Studio 笔记本 SQL Server 大数据群集
titleSuffix: Manage SQL Server Big Data Clusters with Azure Data Studio notebooks
description: 使用 Azure Data Studio 中的笔记本管理大数据群集和排除其故障。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e22b16cf8658e53e6bdc5db0fcd82692f3730fc7
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313675"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>管理 Azure Data Studio 笔记本 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 为包含笔记本的 Azure Data Studio 提供扩展。 笔记本提供可在 Azure Data Studio 中使用的文档和代码，用于管理 SQL Server 2019 大数据群集。

[笔记本](notebooks-guidance.md)最初实现为开源项目，已合并到[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)中。 可以在文本单元格中使用 markdown 作为文本，并使用其中一个可用核心在代码单元格中编写代码。

可以使用笔记本为 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 部署大数据群集。

除了笔记本，你还可以查看笔记本的集合，这称为 Jupyter 书籍。 Jupyter 书籍提供了一个目录，可帮助你导航笔记本的集合，以便你可以轻松找到所需的笔记本，无论你是要解决 SQL Server 还是查看群集状态。

## <a name="prerequisites"></a>先决条件

若要打开笔记本，需要满足以下先决条件：

* 最新版本的[Azure Data Studio 预览体验内部](https://aka.ms/azuredatastudio-rc)版本
* @No__t-0 扩展，安装在 Azure Data Studio

除了这些先决条件，若要部署 SQL Server 2019 大数据群集，你还需要：

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>访问故障排除笔记本
有三种方法可用于访问对笔记本进行故障排除。

### <a name="command-palette"></a>命令面板
1. 选择 "**查看** > "**命令面板**。
2. 输入 @no__t 0Jupyter 书籍：SQL Server 2019 指南 @ no__t-0。

与 Jupyter 书籍 viewlet 的 Jupyter 书籍将会打开，其中包含与 SQL Server 大数据群集相关的故障排除笔记本。

### <a name="sql-master-dashboard"></a>SQL 主仪表板
1. 安装 Azure Data Studio 内部人员后，连接到 SQL Server 大数据群集实例。
2. 连接到实例后，在 "**连接**" 下右键单击服务器名称，然后选择 "**管理**"。
3. 在仪表板中，选择 " **SQL Server 大数据群集**"。 选择**SQL Server 2019 指南**，打开包含所需笔记本的 Jupyter 书籍。
    仪表板中的0Jupyter 笔记本 @ no__t-1 @no__t

1. 选择需要完成的任务的笔记本。

### <a name="controller-dashboard"></a>控制器仪表板
1. 在 "**连接**" 视图中，展开**SQL Server 大数据群集**"。
2. 添加控制器终结点详细信息。
3. 连接到控制器后，右键单击终结点，然后选择 "**管理**"。
4. 在仪表板加载后，选择 "**故障排除**" 以打开 Jupyter Book 疑难解答指南。

## <a name="use-troubleshooting-notebooks"></a>使用笔记本疑难解答
1. 在 Jupyter 书籍的目录中找到所需的故障排除指南。
1. 笔记本经过优化，因此你只需选择 "**运行单元**"。 此操作会将笔记本中的每个单元单独运行，直到笔记本完成。
1. 如果发现错误，Jupyter 书籍将建议一个可运行的笔记本来修复错误。 遵循建议的步骤，然后再次运行笔记本。

## <a name="next-steps"></a>后续步骤
有关 Azure Data Studio 中的笔记本的详细信息，请参阅[如何使用 SQL Server 2019 预览版中的笔记本](notebooks-guidance.md)。
