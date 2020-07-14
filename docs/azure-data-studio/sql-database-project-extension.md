---
title: SQL 数据库项目扩展
description: 安装和使用 Azure Data Studio 的 SQL 数据库项目扩展（预览版）
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 609af04cec2f6eaaaf1890e19c6d85fbd4bd5b8a
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519146"
---
# <a name="sql-database-projects-extension-preview"></a>SQL 数据库项目扩展（预览版）

SQL 数据库项目扩展（预览版）是在基于项目的开发环境中开发 SQL 数据库的扩展。 此扩展目前处于预览阶段，在 [Azure Data Studio 预览体验内部版本](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main)中提供。


## <a name="install-the-sql-database-projects-extension"></a>安装 SQL 数据库项目扩展

1. 若要打开扩展管理器并访问可用扩展，请选择扩展图标，或在“视图”菜单中选择“扩展” 。
2. 通过在扩展搜索框中键入全部或部分名称来找到“SQL 数据库项目”扩展。 选择某个可用扩展以查看其详细信息。

   ![安装扩展](media/extensions/sql-database-projects-extension/install-database-projects.png)

3. 选择所需的扩展并“安装”它。
4. 选择“重新加载”以启用扩展（仅在第一次安装扩展时是必需的）。
5.  从活动栏中选择文件图标，或从“视图”菜单中选择“资源管理器”。 “项目”的新 viewlet 现已可用。

   > [!NOTE]
   > 建议随 SQL 数据库项目扩展安装[架构比较扩展](schema-compare-extension.md)，以获得完整功能。

## <a name="getting-started-with-database-projects"></a>数据库项目引擎入门

*  在“资源管理器”下转到“项目”viewlet，或在命令面板中搜索“新建数据库项目”，以创建新的数据库项目。
* 可以通过命令面板中的“打开数据库项目”来打开现有数据库项目。
* 通过命令面板“导入新的数据库项目”来使用现有数据库。

   ![新 viewlet](media/extensions/sql-database-projects-extension/projects-viewlet.png)


### <a name="create-an-empty-database-project"></a>创建空数据库项目

   在“资源管理器”下的“项目”viewlet 中，单击“新建项目”按钮，然后在显示的文本输入中输入项目名称。  在出现的“选择文件夹”对话框中，选择项目文件夹的目录、.sqlproj 文件和要包含的其他内容。
空项目在“项目”viewlet 中打开并可见，可以进行编辑。

### <a name="open-an-existing-project"></a>打开现有项目

 在“项目”viewlet 中，单击“打开项目”按钮，然后从显示的文件选取器中打开现有 .sqlproj 文件。 现有项目可以来自 Azure Data Studio 或 [Visual Studio SQL Server Data Tools](../ssdt/sql-server-data-tools.md)。

将打开现有项目，其内容在“项目”viewlet 中可见以供编辑。

### <a name="create-a-database-project-from-an-existing-database"></a>从现有数据库创建数据库项目

 在“项目”viewlet 中，单击“从数据库导入项目”按钮并连接到 SQL Server。  建立连接后，从可用数据库列表选择数据库，然后设置项目的名称。

最后，选择提取的目标结构。  将打开新项目，其中包含所选数据库内容的 SQL 脚本。

## <a name="build-and-publish"></a>生成并发布

通过将项目生成为[数据层应用程序文件](../relational-databases/data-tier-applications/data-tier-applications.md) (DACPAC) 并发布到支持的平台，在 Azure Data Studio 的 SQL 数据库项目扩展中实现数据库项目部署。 有关此过程的详细信息，请参阅[生成并发布项目](sql-database-project-extension-build.md)。

## <a name="schema-compare"></a>架构比较
如果安装了[架构比较扩展](schema-compare-extension.md)，则 SQL 数据库项目扩展与之进行交互，将项目内容与 dacpac 或现有数据库进行比较。  生成的架构比较可用于查看和应用源与目标之间的差异。

## <a name="next-steps"></a>后续步骤

- [使用 Azure Data Studio 的 SQL 数据库项目扩展生成并发布项目](sql-database-project-extension-build.md)
- [数据层应用程序](../relational-databases/data-tier-applications/data-tier-applications.md)