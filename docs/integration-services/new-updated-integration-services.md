---
title: 已更新 - 适用于 SQL Server 的 Integration Services 文档 | Microsoft Docs
description: 显示 Microsoft SQL Server Integration Services 文档中最近更新内容的片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssis
ms.date: 04/28/2018
ms.openlocfilehash: f1d0c96c7ee0a835c1fc1cf6db6e3cf1e03ca9d6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>新增内容和最近更新内容：适用于 SQL Server 的 Integration Services



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：2018-02-03 到 2018-04-28&nbsp;&nbsp;&nbsp;
- 主题区域：SQL Server Integration Services&nbsp;。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](load-data-to-from-excel-with-ssis.md)
2. [使用 SQL Server Integration Services (SSIS) 将数据从 SQL Server 加载到 Azure SQL 数据仓库](load-data-to-sql-data-warehouse.md)
3. [Scale Out 通过 SQL Server 故障转移群集实例对高可用性的支持](scale-out/scale-out-failover-cluster-instance.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [安装集成服务](#TitleNum_1)
2. [在 Azure 上部署、运行和监视 SSIS 包](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-install-integration-servicesinstall-windowsinstall-integration-servicesmd"></a>1.&nbsp; [安装集成服务](install-windows/install-integration-services.md)

更新日期：2018-04-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一篇](#TitleNum_2))

<!-- Source markdown line 75.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 49551f3b1138f805e6d5e0f6099a100e2f3b3e7a 97caaafc1587b2326f4c357dd5eb21f2de7d358f  (PR=5676  ,  Filename=install-integration-services.md  ,  Dirpath=docs\integration-services\install-windows\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**完整安装 Integration Services**


要完整安装 {Included-Content-Goes-Here}，请从以下列表中选择所需组件：

-   **Integration Services (SSIS)**。 使用 SQL Server 安装向导安装 SSIS。 选择 SSIS 会安装以下各项：
    -   对 SQL Server 数据库引擎上 SSIS 目录的支持。
    -   （可选）SSIS Scale Out 功能，包括 Master 和 Worker。
    -   32 位和 64 位 SSIS 组件。
    -   安装 SSIS 时不会安装设计和开发 SSIS 包所需的工具。
-   **SQL Server 数据库引擎**。 使用 SQL Server 安装向导安装数据库引擎。 通过选择“数据库引擎”，可创建并托管 SSIS 目录数据库 `SSISDB`，并存储、管理、运行和监视 SSIS 包。
-   **SQL Server Data Tools (SSDT)**。 要下载并安装 SSDT，请参阅[下载 SQL Server Data Tools (SSDT)]。 安装 SSDT 后，可设计和部署 SSIS 包。 SSDT 安装以下各项：
    -   SSIS 包设计和开发工具，包括 SSIS 设计器。
    -   仅 32 位 SSIS 组件。
    -   Visual Studio 的受限制版本（如果尚未安装 Visual Studio 版本）。
    -   SSIS 脚本任务和脚本组件所使用的脚本编辑器 Tools for Applications (VSTA)。
    -   SSIS 向导，包括部署向导和包升级向导。
    -   SQL Server 导入和导出向导。
-   **用于 Azure 的 Integration Services 功能包**。 要下载并安装功能包，请参阅[用于 Azure 的 Microsoft SQL Server 2017 Integration Services 功能包](https://www.microsoft.com/download/details.aspx?id=54798)。 通过安装功能包，可将包连接到 Azure 云中的存储和分析服务，包括以下服务：



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-run-and-monitor-an-ssis-package-on-azurelift-shiftssis-azure-deploy-run-monitor-tutorialmd"></a>2.&nbsp; [在 Azure 上部署、运行和监视 SSIS 包](lift-shift/ssis-azure-deploy-run-monitor-tutorial.md)

更新日期：2018-04-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_1))

<!-- Source markdown line 99.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07f2b752818f2e786c4380fb822099190c59f302 54de9497353bac2d6a8a87e546fc6ab9e444a734  (PR=5676  ,  Filename=ssis-azure-deploy-run-monitor-tutorial.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**使用 PowerShell 部署项目**


若要使用 PowerShell 将项目部署到 Azure SQL 数据库上的 SSISDB，请根据具体要求修改以下脚本。 此脚本枚举了 `$ProjectFilePath` 下的子文件夹以及每个子文件夹中的项目，然后在 SSISDB 中创建相同的文件夹，并将项目部署到这些文件夹。

此脚本要求在运行脚本的计算机上安装 SQL Server Data Tools 版本 17.x 或 SQL Server Management Studio。

```
**Variables**

$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

**Load the IntegrationServices Assembly**

[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

**Store the IntegrationServices Assembly namespace to avoid typing it every time**

$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

**Create a connection to the server**

$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

**Create the Integration Services object**

$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

**Get the catalog**

$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
```







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (11+6)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)&nbsp; &nbsp;
- [新文章和更新的文章 (18+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (218+14)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (14+0)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)&nbsp; &nbsp;
- [新文章和更新的文章 (3+2)： SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (3+3)： Linux for SQL 文档](../linux/new-updated-linux.md)&nbsp; &nbsp;
- [新文章和更新的文章 (7+10)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)&nbsp; &nbsp;
- [新文章和更新的文章 (0+2)：Reporting Services for SQL 文档](../reporting-services/new-updated-reporting-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+3)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)&nbsp; &nbsp;
- [新文章和更新的文章 (2+3)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+1)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)&nbsp; &nbsp;
- [新文章和更新的文章 (5+2)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)&nbsp; &nbsp;
- [新文章和更新的文章 (0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+1)：SQL 工具文档](../tools/new-updated-tools.md)&nbsp; &nbsp;



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主题区域没有新的或最近更新的文章

- [新文章和更新的文章 (0+0)：SQL 分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../samples/new-updated-samples.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)

