---
title: "已更新 - SQL Server Reporting Services 文档 | Microsoft Docs"
description: "显示 Microsoft SQL Server Reporting Services 文档中最近更新内容的片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: reporting-services
ms.suite: pro-bi
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.author: genemi
ms.workload: reporting-services
ms.openlocfilehash: a4bb2b714a4a20d299c22e6952f135cd9786748c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="new-and-recently-updated-reporting-services-for-sql-server"></a>新增内容和最近更新内容：SQL Server Reporting Services



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017-09-28 到 2017-12-02&nbsp;&nbsp;&nbsp;
- 主题区域：&nbsp; SQL Server Reporting Services。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [SQL Server Reporting Services 的更改日志](change-log-sql-server-reporting-services.md)
2. [使用 Reporting Services 的 REST API 进行开发](developer/rest-api.md)
3. [SharePoint 站点上的报表查看器 Web 部件](report-server-sharepoint/report-viewer-web-part-sharepoint-site.md)
4. [用于报表查看器 Web 部件的 SharePoint 网站设置](report-server-sharepoint/report-viewer-web-part-sharepoint-site-settings.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [安装 SQL Server Reporting Services](#TitleNum_1)
2. [在 SharePoint 网站上部署 SQL Server Reporting Services 报表查看器 Web 部件](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-install-sql-server-reporting-servicesinstall-windowsinstall-reporting-servicesmd"></a>1.&nbsp; [安装 SQL Server Reporting Services](install-windows/install-reporting-services.md)

更新日期：2017-11-30 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[下一篇](#TitleNum_2)）

<!-- Source markdown line 66.  ms.author= "asaxton".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c959622d4d10a71ed598256e8e284130eb49af5b 77dc1b4f6696e911ed036fc27724ff8a96b79f57  (PR=4150  ,  Filename=install-reporting-services.md  ,  Dirpath=docs\reporting-services\install-windows\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    > The default path is C:\Program Files\Microsoft SQL Server Reporting Services.

7. 安装成功后，选择“配置报表服务器”，启动 Reporting Services 配置管理器。

    ![Configure the report server--media/install-reporting-services/report-server-install-configure.png)

**配置报表服务器**


在安装程序中选择“配置报表服务器”后，可看到“报表服务器配置管理器”。 有关详细信息，请参阅 [Report Server Configuration Manager--reporting-services-configuration-manager-native-mode.md)。

需要 [create a report server database--ssrs-report-server-create-a-report-server-database.md)，以便完成 Reporting Services 的初始配置。 完成此步骤需要 SQL Server 数据库服务器。

**在不同服务器上创建数据库**


如果要在其他计算机上的数据库服务器中创建报表服务器数据库，需要将报表服务器的服务帐户更改为数据库服务器上已识别的凭据。

默认情况下，报表服务器使用虚拟服务帐户。 如果尝试在不同服务器上创建数据库，则可能会在“应用连接权限”步骤中收到以下错误消息。

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

要解决此错误，可将服务帐户更改为网络服务或域帐户。 将服务帐户更改为网络服务会在报表服务器计算机帐户的上下文中应用权限。

有关详细信息，请参阅 [Configure the report server service account--configure-the-report-server-service-account-ssrs-configuration-manager.md)。

**Windows 服务**


Windows 服务是在安装过程中创建的。 它显示为 SQL Server Reporting Services。 服务名称为 SQLServerReportingServices。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-sitereport-server-sharepointdeploy-report-viewer-web-partmd"></a>2.&nbsp;[在 SharePoint 网站上部署 SQL Server Reporting Services 报表查看器 Web 部件](report-server-sharepoint/deploy-report-viewer-web-part.md)

更新日期：2017-11-30 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_1)）

<!-- Source markdown line 129.  ms.author= "asaxton".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 99275aa597f491bb09688060b3f713406e2f0624 a282486da6df55154212c98fa06c7e62e66c8350  (PR=4150  ,  Filename=deploy-report-viewer-web-part.md  ,  Dirpath=docs\reporting-services\report-server-sharepoint\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



可以使用 PowerShell 尝试删除 Web 部件，但没有直接的命令用于此操作。 有关脚本示例，请参阅 [How to delete web parts from the web part Gallery](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f)（如何从 Web 部件库中删除 Web 部件）。

**支持的语言**


Web 部件支持以下语言：

* 英语 (en)
* 德语 (de)
* 西班牙语 (sp)
* 法语 (fr)
* 意大利语 (it)
* 日语 (ja)
* 朝鲜语 (ko)
* 葡萄牙语 (pt)
* 俄语 (ru)
* 中文（简体 - zh-HANS 和 zh-CHS）







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (3+14)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新的和更新的文章 (1+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)
- [新文章和更新的文章 (87+0)：SQL 分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章和更新的文章 (5+4)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (0+1)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (2+2)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章 (10+9)：Linux 版 SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (2+4)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章 (4+2)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章 (0+1)：SQL 示例文档](../sample/new-updated-sample.md)
- [新文章和更新的文章 (21+0)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章和更新的文章 (5+1)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新的和更新的文章 (0+1)：SQL Server Data Tool (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新文章和更新的文章 (1+0)：SQL Server 迁移助手 (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+1)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章 (0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新文章和更新的文章 (0+0)：SQL 数据迁移助手 (DMA) 文档](../dma/new-updated-dma.md)
- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)


