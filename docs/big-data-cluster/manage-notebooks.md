---
title: 使用 Azure Data Studio 笔记本管理 SQL Server 大数据群集
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: 使用 Azure Data Studio 中的笔记本管理大数据群集和排除其故障。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cb2fcaf7431b5d79698af009b533ee49254777fe
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846648"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>使用 Azure Data Studio 笔记本管理 SQL Server 的大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 为包含笔记本的 Azure Data Studio 提供扩展。 笔记本包含可在 Azure Data Studio 中用于管理 SQL Server 大数据群集的文档和代码。

[笔记本](notebooks-guidance.md)最初作为开放源代码项目实现，现已应用于 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)。 可以在文本单元格中使用 markdown 作为文本，并使用其中一个可用核心在代码单元格中编写代码。

可以使用笔记本为 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 部署大数据群集。

除笔记本外，用户还可以查看笔记本的集合，这些笔记本称为 Jupyter 书籍。 Jupyter Book 提供用于浏览笔记本集合的目录，这样，无论是对 SQL Server 进行故障排除还是查看群集状态，用户都可以轻松找到所需的笔记本。

## <a name="prerequisites"></a>先决条件

要启动笔记本，需要满足以下必备条件：

* 已安装 [Azure Data Studio 预览体验内部版本](https://aka.ms/azuredatastudio-rc)的最新版本
* 已在 Azure Data Studio 中安装 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 扩展

除上述内容外，部署 SQL Server 2019 大数据群集还需要：

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>访问故障排除笔记本
有三种方法可用于访问对笔记本进行故障排除。

### <a name="command-palette"></a>命令面板
1. 单击 "**查看**"，然后单击**命令面板**
2. 键入 "Jupyter 书籍：SQL Server 2019 指南 "
3. 这会打开 Jupyter 书籍 Viewlet，其中包含与 SQL Server 大数据群集相关的 TSG 的 Jupyter 书籍。

### <a name="sql-master-dashboard"></a>SQL 主仪表板
1. 安装 Azure Data Studio 预览体验内部版本后，连接到 SQL Server 大数据群集实例。
2. 成功连接后，在“连接 viewlet”中右键单击服务器名称，然后单击“管理”。
3. 在仪表板上，单击“SQL Server 大数据群集”。 单击“SQL Server 2019 指南”，打开包含所需笔记本的 Jupyter Book。
    ![按钮](media/manage-notebooks/jupyter-book-button.png)

1. 这将打开已打开 TSG Jupyter 书籍的 Jupyter 书籍 viewlet。
4. 单击需要完成的任务的笔记本。

### <a name="controller-dashboard"></a>控制器仪表板
1. 在 "**连接**" 视图中，展开**SQL Server 大数据群集 "。**
2. 添加控制器终结点详细信息。
3. 成功连接到控制器后，右键单击终结点，然后单击 "**管理"。**
4. 在仪表板加载后，单击 "故障排除" 以启动 Jupyter Book TSG。

## <a name="how-to-use-troubleshooting-notebooks"></a>如何使用笔记本疑难解答
1. 查看现有的 Jupyter 书籍目录，直到找到所需的 TSG。
1. 所有笔记本经过优化，用户只需单击 "**运行单元"。** 这将单独运行笔记本中的每个单元格，直到完成。
1. 如果遇到错误，Jupyter 书籍会推荐一个笔记本，你可以运行该笔记本来修复错误。 按照步骤操作，然后重新运行笔记本。

## <a name="next-steps"></a>后续步骤
有关 Azure Data Studio 中的笔记本的详细信息，请参阅[如何使用 SQL Server 2019 预览版中的笔记本](notebooks-guidance.md)。
