---
title: 导入和导出向导的简单示例入门 | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: quickstart
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cc4560b8982bfddfb20f53c70aa4bc98a98e2082
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43018328"
---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>导入和导出向导的简单示例入门
通过浏览常见方案 - 从 Excel 电子表中将数据导入 SQL Server 数据库，了解 SQL Server 导入和导出向导中的内容。 即使计划使用其他源和目标，也可通过本主题最大程度地了解所需的向导相关内容。

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>先决条件 — 计算机上是否安装了向导？
如果想要运行向导，但是尚未在计算机上安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则可以通过安装 SQL Server Data Tools (SSDT) 来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。 有关详细信息，请参阅 [下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

## <a name="heres-the-excel-source-data-for-this-example"></a>下面是用于本示例的 Excel 源数据
以下是要复制的源数据：WizardWalkthrough.xlsx Excel 工作簿 WizardWalkthrough 工作表中一个具有两个列的小型表格。

![Excel 源数据](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>下面是本示例的 SQL Server 目标数据库
下面（在 SQL Server Management Studio 中）是要将源数据复制到的 SQL Server 目标数据库。 目标表格不存在 - 需要通过向导创建。

![SQL Server 目标数据库](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>步骤 1 - 启动向导
通过“Windows 开始”菜单中的 Microsoft SQL Server 2016 组启动向导。

![启动向导](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> 对于本示例，选择 32 位向导，因为安装了 32 位的 Microsoft Office。 因此，必须使用 32 位数据提供程序连接到 Excel。 对于许多其他数据源，通常可以选择 64 位向导。
>
> 若要使用 64 位版本的 SQL Server 导入和导出向导，必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序且仅安装 32 位文件，包括 32 位版本的向导。

有关详细信息，请参阅 [启动 SQL Server 导入和导出向导](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。

## <a name="step-2---view-the-welcome-page"></a>步骤 2 - 查看“欢迎”页
向导第一页是“欢迎”页。 

如果不想再次看到此页面，请继续并单击“不再显示此起始页”。

![欢迎使用向导](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>步骤 3 - 选取 Excel 作为数据源
在下一页“选择数据源”中，选取 Microsoft Excel 作为数据源。 然后浏览选取 Excel 文件。 最后，指定用于创建该文件的 Excel 版本。

> [!IMPORTANT]
> 有关连接到 Excel 文件的详细信息，以及从 Excel 文件加载数据或将数据加载到 Excel 文件的限制和已知问题，请参阅[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../load-data-to-from-excel-with-ssis.md)。

![选择 Excel 数据源](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

有关向导中这一页的详细信息，请参阅[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)。

## <a name="step-4---pick-sql-server-as-your-destination"></a>步骤 4 - 选取 SQL Server 作为目标
在下一页“选择目标”中，选择 Microsoft SQL Server 作为目标，方法是在列表中选择一个用于连接到 SQL Server 的数据提供程序。 在本示例中，选择“用于 SQL Server 的 .NET Framework 数据提供程序”。

该页会显示提供程序属性列表。 其中许多是不友好名称和不熟悉的设置。 所幸，要连接到任何企业数据库，通常只需要提供三条信息。 可以忽略其他设置的默认值。

|必填信息|用于 SQL Server 的 .Net Framework 数据提供程序属性|
|---|---|
|服务器名称|**数据源**|
|身份验证（登录）信息|“集成安全性”或“用户 ID”和“密码”<br/>如果想查看服务器上的数据库的下拉列表，首先必须提供有效的登录信息。|
|数据库名称|**初始目录**|

![选择 SQL Server 目标](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

有关如何连接到 SQL Server 的详细信息，请参阅[连接到 SQL Server 数据源](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)。 有关向导中本页的详细信息，请参阅[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>步骤 5 - 复制表格，而不是编写查询
在下一页“指定表复制或查询”中，指定为要复制源数据的整个表。 不想用 SQL 语言编写查询来选择要复制的数据。

![指定为复制表格](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

有关向导中这一页的详细信息，请参阅[指定表复制或查询](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。

## <a name="step-6---pick-the-table-to-copy"></a>步骤 6 - 选取要复制的表
在下一页“选择源表和视图”中，选择要从数据源复制的一个表或多个表。 然后将每个选定的源表映射到新的或现有的目标表。

在此示例中，向导默认将“源”列中的“WizardWalkthrough$”工作表映射到 SQL Server目标中的同名新表中。 （Excel 工作簿仅包含一张工作表。）
-   源表名称中的美元符号 ($) 指示 Excel 工作表。 （Excel 中的命名范围仅由其名称表示。）
-   目标表图标上的星爆图案指示向导即将新建目标表。

![选择表（重命名前）](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

可能要从新目标表的名称中删除美元符号 ($)。

![选择表（重命名后）](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

有关向导中这一页的详细信息，请参阅[选择源表和视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-7---review-the-column-mappings"></a>（可选）步骤 7 - 查看列映射
离开“选择源表和视图”之前，可选择单击“编辑映射”按钮，打开“列映射”对话框。 此时，在“映射”表中，会看到向导如何将源工作表中的列映射到新的目标表中的列。

![查看列映射](../../integration-services/import-export-data/media/view-column-mappings.jpg)

有关向导中这一页的详细信息，请参阅[列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-8---review-the-create-table-statement"></a>（可选）步骤 8 - 查看 CREATE TABLE 语句
当“列映射”对话框打开时，可选择单击“编辑 SQL”按钮，打开“创建表 SQL 语句”对话框。 此时，将看到向导生成的 CREATE TABLE 语句，用于生成新的目标表。 通常无需更改语句。

![查看 CREATE TABLE 语句](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

有关向导中这一页的详细信息，请参阅[创建表 SQL 语句](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-9---preview-the-data-to-copy"></a>（可选）步骤 9 - 预览要复制的数据
单击“确定”关闭“创建表 SQL 语句”对话框后，再次单击“确定”，关闭“列映射”对话框，即返回“选择源表和视图”页。 可选择单击“预览”按钮，以查看向导要复制的数据的示例。 在本示例中，看起来一切正常。

![预览要复制的数据](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

有关向导中这一页的详细信息，请参阅[预览数据](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>步骤 10 - 是的，要运行导入-导出操作
在下一页“保存并运行包”中，保持启用“立即运行”，以便在单击下一页中的“完成”后，立即复制数据。 或者，可以通过单击“保存并运行包”页中的“完成”，跳过下一页。

![运行包](../../integration-services/import-export-data/media/run-the-package.jpg)

有关向导中这一页的详细信息，请参阅[保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>步骤 11 - 完成向导并运行导入-导出操作
如果在“保存并运行包页中”单击“下一步”，而不是“完成”，则在下一页“完成向导”中，会看到向导将要执行的操作的摘要。 单击“完成”以运行导入-导出操作。

![完成向导](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

有关向导中本页的详细信息，请参阅[完成向导](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。

## <a name="step-12---review-what-the-wizard-did"></a>步骤 12 - 查看向导执行的操作
在最后一页中，观察向导完成每个任务，并查看结果。 突出显示的行指示向导已成功复制数据。 大功告成！

![成功完成向导](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

有关向导中这一页的详细信息，请参阅[执行操作](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)。

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>下面是复制到 SQL Server 的新数据表
此处（SQL Server Management Studio 中），将看到向导在 SQL Server 中创建的新目标表。

![复制到 SQL Server 的数据](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

此处（仍在 SSMS 中），将看到向导复制到 SQL Server 的数据。

![复制到 SQL Server 2 的数据](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>了解更多信息  
了解有关向导工作原理的详细信息。
-   **了解有关向导的详细信息。** 如果正在寻找有关该向导的概述，请参阅 [使用 SQL Server 导入和导出向导来导入和导出数据](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

-   **了解有关向导中的步骤的信息。** 如需有关向导中步骤的信息，请从此处的列表中选择所需页 - [SQL Server 导入和导出向导中的步骤](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)。 还为向导的每一页专门设有一页文档信息页。

-   **了解如何连接到数据源和目标。** 如需有关如何连接到数据的信息，请从此处列表中选择所需的页面：[使用 SQL Server 导入和导出向导连接到数据源](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 其中为几个常用数据源中的每一个数据源专门设有一页文档信息页。

-   **了解有关从 Excel 加载数据和将数据加载到 Excel 中的详细信息。** 如果想要了解连接到 Excel 文件的详细信息，以及从 Excel 文件加载数据或将数据加载到 Excel 文件的限制和已知问题，请参阅[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../load-data-to-from-excel-with-ssis.md)。