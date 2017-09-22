---
title: "要开始使用这个简单的示例导入和导出向导的 |Microsoft 文档"
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 1b59268e884d3e797a74ef65d9e75c405d75a0d5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>要开始使用导入和导出向导的此简单示例
了解 SQL Server 导入和导出向导中会逐步运行常见的方案-将数据从 Excel 电子表格导入到 SQL Server 数据库。 即使你计划使用不同的源和不同的目标，本主题说明大多数的你需要了解的有关运行向导。

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>系统必备组件的是在计算机上安装向导？
如果你想要运行向导，但不会获得 [！包括[msCoName](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt)。

## <a name="heres-the-excel-source-data-for-this-example"></a>下面是此示例的 Excel 源数据
下面是你要复制的一个小型的两列表 WizardWalkthrough.xlsx Excel 工作簿中的 WizardWalkthrough 工作表中的源数据。

![Excel 源数据](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>下面是此示例中的 SQL Server 目标数据库
下面 （在 SQL Server Management Studio) 是要复制的源数据的 SQL Server 目标数据库。 目标表不存在-你要让向导为你创建的表。

![SQL Server 目标数据库](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>步骤 1-启动向导
从 Windows 开始菜单上的 Microsoft SQL Server 2016 组启动向导。

![启动向导](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> 对于此示例，你将选取 32 位向导，因为您必须安装 Microsoft Office 的 32 位版本。 因此，你必须使用 32 位数据提供程序连接到 Excel。 对于许多其他数据源，您通常可以选取 64 位向导。
>
> 若要使用 64 位版本的 SQL Server 导入和导出向导，你必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序，仅安装 32 位文件，包括 32 位版本的向导。

有关详细信息，请参阅 [启动 SQL Server 导入和导出向导](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。

## <a name="step-2---view-the-welcome-page"></a>步骤 2-查看欢迎页
该向导的第一页是**欢迎**页。 

你可能不想要看到此页面，同样，因此请继续并单击**不再的显示此起始页**。

![欢迎使用向导](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>步骤 3-选取 Excel 作为数据源
在下一页上，**选择数据源**，作为数据源中选取 Microsoft Excel。 然后，你浏览以选择 Excel 文件。 最后，可以指定用于创建文件的 Excel 版本。

![选择 Excel 数据源](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

有关连接到 Excel 的详细信息，请参阅[连接到 Excel 数据源](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)。 有关向导的此页的详细信息，请参阅[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)。

## <a name="step-4---pick-sql-server-as-your-destination"></a>步骤 4-选取作为目标的 SQL Server
在下一页上，**选择目标**，如通过选取数据提供程序之一在列表中，目标连接到 SQL Server 选取 Microsoft SQL Server。 在此示例中，你选取**.Net Framework Data Provider for SQL Server**。

页面显示提供程序属性的列表。 其中许多为友好名称，不熟悉的设置。 幸运的是，若要连接到任何企业数据库，通常必须提供只包括三部分信息。 你可以忽略其他设置的默认值。

|所需的信息|.Net framework Data Provider for SQL Server 属性|
|---|---|
|服务器名称|**数据源**|
|身份验证 （登录名） 信息|**集成安全性**; 或**用户 ID**和**密码**<br/>如果你想要在服务器上发现的数据库下拉列表，你首先必须提供有效的登录信息。|
|数据库名称|**初始目录**|

![选择 SQL Server 目标](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

有关连接到 SQL Server 的详细信息，请参阅[连接到 SQL Server 数据源](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)。 有关向导的此页的详细信息，请参阅[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>步骤 5-复制一张表，而不是编写查询
在下一页上，**指定表复制或查询**，指定你想要将整个表的源数据复制。 你不想要选择要复制的数据的 SQL 语言中编写查询。

![指定要复制表](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

有关向导的此页的详细信息，请参阅[指定表复制或查询](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。

## <a name="step-6---pick-the-table-to-copy"></a>步骤 6 – 选取要复制的表
在下一页上，**选择源表和源视图**，选取或多个你想要将数据从源分片复制的表。 然后将每个所选的源表映射到新的或现有的目标表。

在此示例中，默认情况下向导已映射**WizardWalkthrough$**中的工作表**源**到具有相同的名称在 SQL Server 目标的新表的列。 （Excel 工作簿只包含一张工作表。）
-   美元符号 （$） 的源表的名称指示 Excel 工作表。 （命名类型的值，范围在 Excel 中表示仅按名称。）
-   目标表图标爆炸形指示，向导将创建新的目标表。

![（在重命名） 之前选择的表](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

你可能想要删除美元符号 （$） 从新的目标表的名称。

![（重命名后） 中选择的表](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

有关向导的此页的详细信息，请参阅[选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-7---review-the-column-mappings"></a>可选步骤 7-检查列映射
你将之前**选择源表和源视图**页上，（可选） 单击**编辑映射**按钮以打开**列映射**对话框。 此处，请在**映射**表，你看到该向导将如何源工作表中的列映射到新的目标表中的列。

![查看列映射](../../integration-services/import-export-data/media/view-column-mappings.jpg)

有关向导的此页的详细信息，请参阅[列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-8---review-the-create-table-statement"></a>可选步骤 8-查看 CREATE TABLE 语句
虽然**列映射**对话框处于打开状态，或者单击**编辑 SQL**按钮以打开**Create Table SQL 语句**对话框。 在这里看到**CREATE TABLE**语句生成的向导以创建新的目标表。 通常，你不必将该语句更改。

![视图 CREATE TABLE 语句](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

有关向导的此页的详细信息，请参阅[Create Table SQL 语句](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-9---preview-the-data-to-copy"></a>可选步骤 9-预览要复制的数据
单击后**确定**关闭**Create Table SQL 语句**对话框框中，然后单击**确定**以关闭**列映射**对话框中，你重新打开**选择源表和源视图**页。 （可选） 单击**预览**按钮以查看数据的示例，该向导即将将复制。 在此示例中，它看起来不错。

![要复制的预览数据](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

有关向导的此页的详细信息，请参阅[预览数据](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>步骤 10-是中，你想要运行导入导出操作
在下一页上，**保存和运行包**，你将**立即运行**启用复制数据，只要你单击**完成**在下一页上。 可以通过单击跳过下一页或者**完成**上**保存和运行包**页。

![运行包](../../integration-services/import-export-data/media/run-the-package.jpg)

有关向导的此页的详细信息，请参阅[保存和运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>步骤 11-完成向导，并运行导入导出操作
如果你单击**下一步**而不是**完成**上**保存和运行包**页上，然后在下一页上，**完成向导**，请参阅向导要做的摘要。 单击**完成**运行导入导出操作。

![完成向导](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

有关向导的此页的详细信息，请参阅[完成向导](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。

## <a name="step-12---review-what-the-wizard-did"></a>步骤 12-查看向导未
在最后一页，观察向导完成后，每个任务，然后查看结果。 突出显示的行指示该向导已成功复制你的数据。 就大功告成了 ！

![向导成功](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

有关向导的此页的详细信息，请参阅[执行操作](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)。

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>下面是数据复制到 SQL Server 的新表
在这里 （SQL Server Management Studio) 中看到该向导在 SQL Server 中创建新的目标表。

![数据复制到 SQL Server](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

在这里 （再次在 SSMS) 中看到向导复制到 SQL Server 的数据。

![数据复制到 SQL Server 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>了解详细信息  
了解有关该向导的工作原理的详细信息。
-   **了解有关该向导的详细信息。** 如果正在寻找有关该向导的概述，请参阅 [使用 SQL Server 导入和导出向导来导入和导出数据](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

-   **了解有关向导中的步骤。** 如果你正在寻找有关向导中的步骤的信息，从此处的列表中选择所需的页[的 SQL Server 导入和导出向导中的步骤](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)。 此外没有单独的页的向导的每一页的文档。

-   **了解如何连接到数据源和目标。** 如果你正在寻找有关如何连接到你的数据的信息，从此处的列表中选择所需的页[连接到数据源的 SQL Server 导入和导出向导](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 没有单独的几个常用的数据源的每个文档的页面。



