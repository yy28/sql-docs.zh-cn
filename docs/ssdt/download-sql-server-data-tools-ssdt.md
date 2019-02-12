---
title: 下载 SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
keywords:
- 安装 ssdt, 下载 ssdt, 最新 ssdt
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: d296a30e017172e1e753d6dbaaa065b0644792bb
ms.sourcegitcommit: 31c8f9eab00914e056e9219093dbed1b0b4542a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "55513939"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>下载并安装 SQL Server Data Tools (SSDT) for Visual Studio

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

> [!div class="nextstepaction"]
> [请分享你对 SQL Docs 目录的反馈！](https://aka.ms/sqldocsurvey)

SQL Server Data Tools 是一款现代开发工具，用于生成 SQL Server 关系数据库、Azure SQL 数据库、Analysis Services (AS) 数据模型、Integration Services (IS) 包和 Reporting Services (RS) 报表。 使用 SSDT，你可以设计和部署任何 SQL Server 内容类型，就像在 Visual Studio 中开发应用程序一样轻松。

对大多数用户而言，都可以在 Visual Studio 安装期间安装 SQL Server Data Tools (SSDT)。使用 Visual Studio 安装程序安装 SSDT 会添加基本的 SSDT 功能，因此仍需运行 [SSDT 独立安装程序](#ssdt-for-vs-2017-standalone-installer)，获取 AS、IS 和 RS 工具。

## <a name="install-ssdt-with-visual-studio-2017"></a>使用 Visual Studio 2017 安装 SSDT

若要在 [Visual Studio 安装](https://docs.microsoft.com/visualstudio/install/install-visual-studio)过程中安装 SSDT，请选择“数据存储和处理”工作负荷，然后选择“SQL Server Data Tools”。 如果已安装 Visual Studio，则可以[编辑工作负荷列表](https://docs.microsoft.com/visualstudio/install/modify-visual-studio)，使其包括 SSDT：![数据存储和处理工作负荷](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)

## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>安装 Analysis Services、Integration Services 和 Reporting Services 工具

若要安装 AS、IS 和 RS 项目支持，请运行 [SSDT 独立安装程序](#ssdt-for-vs-2017-standalone-installer)。 

该安装程序列出了可将 SSDT 工具添加到其中的可用 Visual Studio 实例。 如果未安装 Visual Studio，则选择“安装新的 SQL Server Data Tools 实例”可通过最低版本的 Visual Studio 安装 SSDT，但为获得最佳体验，建议通过[最新版本的 Visual Studio](https://www.visualstudio.com/downloads) 使用 SSDT。 

![选择 AS、IS、RS](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)



## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT for VS 2017（独立安装程序）

[![下载](../ssdt/media/download.png) 下载 SSDT for Visual Studio 2017 (15.9.0)](https://go.microsoft.com/fwlink/?linkid=2052454) 

> [!IMPORTANT]
> - 安装 SSDT for Visual Studio 2017 (15.9.0) 前，请卸载“Analysis Services 项目”和“Reporting Services 项目”扩展（如已安装），并关闭所有 VS 实例。
> - 自版本 15.8.2 起的 SSDT for Visual Studio 2017 不支持设计包含 Teradata 源/目标的包。 使用 SSDT for Visual Studio 2017 (15.8)。



**版本信息**  
  
版本号：15.9.0  
生成号：14.0.16186.0  
发布日期：2019 年 1 月 28 日  

有关更改的完整列表，请参阅[更改日志](changelog-for-sql-server-data-tools-ssdt.md)。

SSDT for Visual Studio 2017 具有与 Visual Studio 相同的[系统需求](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs)。  

### <a name="available-languages---ssdt-for-vs-2017"></a>支持的语言 - SSDT for VS 2017

此版本的 SSDT for VS 2017 可安装以下语言：

- [简体中文]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x804)
- [繁体中文]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x404)
- [英语（美国）]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x409)
- [法语]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x40c)
- [德语]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x407)
- [意大利语]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x410)
- [日语]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x411)
- [朝鲜语]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x412)
- [葡萄牙语（巴西）]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x416)
- [俄语]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x419)
- [西班牙语]( https://go.microsoft.com/fwlink/?linkid=2052454&clcid=0x40a)

## <a name="offline-install"></a>脱机安装

若要在未连接到 Internet 时安装 SSDT，请按照此部分中的步骤执行操作。 有关详细信息，请参阅 [创建 Visual Studio 2017 的网络安装](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio)。

首先，在联机时完成以下步骤：

1. [下载 SSDT 独立安装程序](#ssdt-for-vs-2017-standalone-installer)。
2. [下载 vs_sql.exe](https://aka.ms/vs/15/release/vs_sql.exe)。
3. 仍联机时，执行以下命令之一以下载脱机安装所需的全部文件。 使用 `--layout` 选项是关键，它将下载脱机安装的实际文件。 将 `<filepath>` 替换为保存文件的实际布局路径。

   
   A.   对于特定语言，请传递区域设置：`vs_sql.exe --layout c:\<filepath> --lang en-us`（一种语言为大约 1 GB）  
   B. 对于所有语言，请省略 `--lang` 参数：`vs_sql.exe --layout c:\<filepath>`（所有语言均为大约 3.9 GB）。

4. 执行 `SSDT-Setup-ENU.exe /layout c:\<filepath>`，将 SSDT 有效负载提取到下载 VS2017 文件的同一 `<filepath>` 位置。 此操作确保这两者中的所有文件均合并到单个布局文件夹中。

完成上一步骤后，可以在脱机时完成以下操作：

1. 运行 `vs_setup.exe --NoWeb` 以安装 VS2017 Shell 和 SQL Server 数据项目。
2. 从布局文件夹运行 `SSDT-Setup-ENU.exe /install` 并选择 SSIS/SSRS/SSAS。

   - 或者若要执行无人参与的安装，请运行 `SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive`  

有关可用选项，请运行 `SSDT-Setup-ENU.exe /help`

> [!NOTE]
> 如果使用完整版本的 Visual Studio 2017，请仅为 SSDT 创建脱机文件夹，并从该新建文件夹运行 `SSDT-Setup-ENU.exe`（请勿将 SSDT 添加到另一个 Visual Studio 2017 脱机布局）。 如果将 SSDT 布局添加到现有 Visual Studio 脱机布局，则无法在其中创建必要的运行时 (.exe) 组件。

## <a name="supported-sql-versions"></a>受支持的 SQL 版本
  
|项目模板|支持的 SQL 平台|  
|-------------------|--------------------|  
|关系数据库|  SQL Server 2005\* - SQL Server 2017<br> （使用适用于 Visual Studio 2017 的 SSDT 17.x 或 SSDT 来连接 [Linux 上的 SQL Server](../linux/sql-server-linux-overview.md)）<br /><br />Azure SQL Database<br /><br />Azure SQL 数据仓库（仅支持查询；尚不支持数据库项目）<br /><br /> \* SQL Server 2005 支持已停止提供，<br /><br /> 请转至官方支持的 SQL 版本|
|Analysis Services 模型<br /><br />Reporting Services 报表 | SQL Server 2008 - SQL Server 2017|
|Integration Services 包| SQL Server 2012 - SQL Server 2019 |
  
## <a name="dacfx"></a>DacFx

SSDT for Visual Studio 2015 和 SSDT for Visual Studio 2017 都使用 DacFx 17.4.1：[下载数据层应用程序框架 (DacFx) 17.4.1](https://www.microsoft.com/download/details.aspx?id=56508)。

## <a name="previous-versions"></a>以前的版本

若要下载并安装 SSDT for Visual Studio 2015 或较旧版本的 SSDT，请参阅[以前版本的 SQL Server Data Tools（SSDT 和 SSDT-BI）](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)。

## <a name="next-steps"></a>后续步骤

安装 SSDT 后，阅读这些教程，了解如何使用 SSDT 创建数据库、包、数据模型和报告：  

- [面向项目的脱机数据库开发](project-oriented-offline-database-development.md)  
- [SSIS 教程：创建简单的 ETL 包](../integration-services/ssis-how-to-create-an-etl-package.md)  
- [Analysis Services 教程](../analysis-services/analysis-services-tutorials-ssas.md)  
- [创建基本表报表（SSRS 教程）](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="see-also"></a>另请参阅

[SSDT MSDN 论坛](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 团队博客](https://blogs.msdn.com/b/ssdt/)  
[DACFx API 参考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下载 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
