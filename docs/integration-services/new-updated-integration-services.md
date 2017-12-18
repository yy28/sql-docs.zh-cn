---
title: "已更新 - 适用于 SQL Server 的 Integration Services 文档 | Microsoft Docs"
description: "显示 Microsoft SQL Server Integration Services 文档中最近更新内容的片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: integration-services
ms.openlocfilehash: 9660fa7239c14c3adc963cc75ceb98de8316734c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>新增内容和最近更新内容：适用于 SQL Server 的 Integration Services



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017-09-28 到 2017-12-02&nbsp;&nbsp;&nbsp;
- 主题区域：SQL Server Integration Services&nbsp;。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [借助 SSIS 存储和检索本地和 Azure 中文件共享上的文件](lift-shift/ssis-azure-files-file-shares.md)
2. [验证部署到 Azure 的 SSIS 包](lift-shift/ssis-azure-validate-packages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [Hadoop 连接管理器](#TitleNum_1)
2. [使用 Windows 身份验证连接到本地数据源和 Azure 文件共享](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-hadoop-connection-managerconnection-managerhadoop-connection-managermd"></a>1.&nbsp; [Hadoop 连接管理器](connection-manager/hadoop-connection-manager.md)

更新日期：2017-11-28 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  （[下一篇](#TitleNum_2)）

<!-- Source markdown line 65.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2d68f4e884304f1a28045b42b680c15cc6a41ec5 fb2429466ea4d545682975d8dbea47451ce98ec7  (PR=4113  ,  Filename=hadoop-connection-manager.md  ,  Dirpath=docs\integration-services\connection-manager\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



**连接 Kerberos 身份验证**

有两个选项可用来设置本地环境，以便可以配合使用 Kerberos 身份验证和 Hadoop 连接管理器。 可选择更符合你情况的选项。
-   选项 1：[将 SSIS 计算机联接到 Kerberos 领域--#kerberos-join-realm）
-   选项 2：[启用 Windows 域和 Kerberos 领域之间的相互信任--#kerberos-mutual-trust）

**<a name="kerberos-join-realm"></a>选项 1：将 SSIS 计算机联接到 Kerberos 领域**


**要求：**


-   网关计算机需要联接 Kerberos 领域，且不能联接任何 Windows 域。

**配置方式：**


**在 SSIS 计算机上：**

1.  运行 Ksetup 实用工具来配置 Kerberos KDC 服务器和领域。

    计算机必须配置为工作组的成员，因为 Kerberos 领域与 Windows 域不同。 设置 Kerberos 领域并添加 KDC 服务器，如以下示例所示。 根据需要，将 REALM.COM 替换为各自的领域。

```
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
```

    Restart the computer after executing these two commands.

2.  使用 Ksetup 命令验证配置。 输出应该如下例所示：

```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
```

**<a name="kerberos-mutual-trust"></a>选项 2：启用 Windows 域和 Kerberos 领域之间的相互信任**


**要求：**

-   网关计算机必须联接 Windows 域。
-   需要用于更新域控制器设置的权限。

**配置方式：**


> [!NOTE]
> 根据需要，将下面教程中的 REALM.COM 和 AD.COM 替换为各自的领域和域控制器。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authenticationlift-shiftssis-azure-connect-with-windows-authmd"></a>2.&nbsp; [使用 Windows 身份验证连接到本地数据源和 Azure 文件共享](lift-shift/ssis-azure-connect-with-windows-auth.md)

更新日期：2017-11-27 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  （[上一篇](#TitleNum_1)）

<!-- Source markdown line 66.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 673386fca53cb60b983e0cb3cd4b9e2ee1dee0de 65458b4dceb92d01184c5e9c6f68ec0e8f16ba08  (PR=4104  ,  Filename=ssis-azure-connect-with-windows-auth.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=19e1c4067142d33e8485cb903a7a9beb7d894015) -->



**连接到本地 SQL Server**

若要检查能否连接到本地 SQL Server，请执行以下操作：

1.  若要运行此测试，请找一台未加入域的计算机。

2.  在未加入域的计算机上，运行以下命令，以通过要使用的域凭据启动 SQL Server Management Studio (SSMS)：

```
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
```

3.  从 SSMS 中，检查能否连接到要使用的本地 SQL Server。

**连接到本地文件共享**

若要检查能否连接到本地文件共享，请执行以下操作：

1.  若要运行此测试，请找一台未加入域的计算机。

2.  在未加入域的计算机上运行以下命令。 此命令会打开一个命令提示符窗口，其中包含要使用的域凭据，然后通过获取目录列表测试与文件共享的连接性。

```
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
```

3.  检查该目录列表是不是为要使用的本地文件共享返回的。

**连接到 Azure VM 上的文件共享**

若要连接到 Azure 虚拟机上的文件共享，请执行以下操作：

1.  使用 SQL Server Management Studio (SSMS) 或其他工具连接到托管 SSIS 目录数据库 (SSISDB) 的 SQL 数据库。

2.  将 SSISDB 设置为当前数据库后，打开一个查询窗口。

3.  按以下选项中所述运行 `catalog.set_execution_credential` 存储过程：

```
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
```

**连接到 Azure 文件中的文件共享**

有关 Azure 文件的详细信息，请参阅 [Azure 文件](https://azure.microsoft.com/services/storage/files/)。







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


