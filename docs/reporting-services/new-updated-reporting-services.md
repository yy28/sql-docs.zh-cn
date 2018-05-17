---
title: 已更新 - SQL Server Reporting Services 文档 | Microsoft Docs
description: 显示 Microsoft SQL Server Reporting Services 文档中最近更新内容的片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssrs
ms.date: 04/28/2018
ms.openlocfilehash: 5fc0153c45e12f8cef47ef2b9eef10f73343b87e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-reporting-services-for-sql-server"></a>新增内容和最近更新内容：SQL Server Reporting Services



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：2018-02-03 到 2018-04-28&nbsp;&nbsp;&nbsp;
- 主题区域：&nbsp; SQL Server Reporting Services。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


暂时无新文章列出。



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [SQL Server Reporting Services 的更改日志](#TitleNum_1)
2. [在 SharePoint 网站上部署 SQL Server Reporting Services 报表查看器 Web 部件](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-change-log-for-sql-server-reporting-serviceschange-log-sql-server-reporting-servicesmd"></a>1.&nbsp; [SQL Server Reporting Services 的更改日志](change-log-sql-server-reporting-services.md)

更新日期：2018-04-27 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一篇](#TitleNum_2))

<!-- Source markdown line 28.  ms.author= "edugonz".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 025d58c01310215df423e7c3848e929b935bcfff 89310524b904dfba41e301cf1323b9a2a5e05064  (PR=575  ,  Filename=change-log-sql-server-reporting-services.md  ,  Dirpath=docs\reporting-services\  ,  MergeCommitSha40=98b04e2388872d1c7b8d819438c150c4ff2df94c) -->




- 版本 14.0.600.744，发布日期：2018 年 4 月 25 日
    - Bug 修复：
        - 创建后，数据驱动订阅页不会显示传递选项
        - 将 SSRS 2012 升级到 SSRS 2017 会导致 RSManagement 每几秒钟就引发异常
        - 无法更改 IE11 中多值参数的默认值
        - 只要执行共享计划，计划就为空

- 版本 14.0.600.689（发布日期：2018 年 2 月 28 日）
    - Bug 修复：
        - 链接报表中的报表参数可见性在用户编辑它的属性后还原
        - URL 参数 rc:Toolbar = false 在 Express edition 中不起作用
        - 如果在将 CanGrow 属性设为 false 的文本框中使用表达式，生成的值无法显示
        - 为安装程序中的产品密钥添加了“了解更多”链接
        - 使用自定义表单身份验证的 Web 门户忽略弹性到期 Cookie
        - “导出到 Word”导致行高度不等（如果行内容为空的话）



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-sitereport-server-sharepointdeploy-report-viewer-web-partmd"></a>2.&nbsp;[在 SharePoint 网站上部署 SQL Server Reporting Services 报表查看器 Web 部件](report-server-sharepoint/deploy-report-viewer-web-part.md)

更新日期：2018-04-10 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_1))

<!-- Source markdown line 154.  ms.author= "maghan".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 42b763a610d378a7cedc9b5778bc5048d65fa730 ce7e2619689fd50be51a2689b07e3137470d9adf  (PR=5481  ,  Filename=deploy-report-viewer-web-part.md  ,  Dirpath=docs\reporting-services\report-server-sharepoint\  ,  MergeCommitSha40=31e0b2ebfc08c0b57870ac412fbd49bf3a1dffb8) -->



**故障排除**


* 如果已配置 SharePoint 集成模式，则卸载 SSRS 时出错：

    Install-SPRSService：[A] Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService 无法强制转换为 [B]Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService。 A 类型来自“C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll”位置处上下文“Default”中的“Microsoft.ReportingServices.SharePoint.SharedService,Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91”。 B 类型来自“C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll”位置处上下文“Default”中的“Microsoft.ReportingServices.SharePoint.SharedService,Version=12.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91”。

    解决方案：
    1. 删除报表查看器 Web 部件
    2. 卸载 SSRS
    3. 重新安装报表查看器 Web 部件

* 如果已配置 SharePoint 集成模式，则尝试升级 SharePoint 时出错：

    无法加载文件或程序集“Microsoft.ReportingServices.Alerting.ServiceContract, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91”或其依赖项之一。 系统找不到指定的文件。 00000000-0000-0000-0000-000000000000

    解决方案：
    1. 删除报表查看器 Web 部件
    2. 卸载 SSRS
    3. 重新安装报表查看器 Web 部件







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

