---
title: 下载 SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology: ssdt
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- 安装 ssdt, 下载 ssdt, 最新 ssdt
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 907b8a7d11bbd7889f3796d3f56633caec22a529
ms.sourcegitcommit: c929887686eabd6b754cf644a45656f0a0eb0445
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2018
ms.locfileid: "43743480"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>下载并安装 SQL Server Data Tools (SSDT) for Visual Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
SQL Server Data Tools 是一款现代开发工具，用于生成 SQL Server 关系数据库、Azure SQL 数据库、Analysis Services (AS) 数据模型、Integration Services (IS) 包和 Reporting Services (RS) 报表。 使用 SSDT，你可以设计和部署任何 SQL Server 内容类型，就像在 Visual Studio 中开发应用程序一样轻松。

对大多数用户而言，都可以在 Visual Studio 安装期间安装 SQL Server Data Tools (SSDT)。使用 Visual Studio 安装程序安装 SSDT 会添加基本的 SSDT 功能，因此仍需运行 [SSDT 独立安装程序](#ssdt-for-vs-2017-standalone-installer)，获取 AS、IS 和 RS 工具。

## <a name="install-ssdt-with-visual-studio-2017"></a>使用 Visual Studio 2017 安装 SSDT

若要在 [Visual Studio 安装](https://docs.microsoft.com/visualstudio/install/install-visual-studio)过程中安装 SSDT，请选择“数据存储和处理”工作负荷，然后选择“SQL Server Data Tools”。 如果已安装 Visual Studio，则可以[编辑工作负荷列表](https://docs.microsoft.com/visualstudio/install/modify-visual-studio)，使其包括 SSDT：![数据存储和处理工作负荷](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)



## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>安装 Analysis Services、Integration Services 和 Reporting Services 工具
若要安装 AS、IS 和 RS 项目支持，请运行 [SSDT 独立安装程序](#ssdt-for-vs-2017-standalone-installer)。 

该安装程序列出了可将 SSDT 工具添加到其中的可用 Visual Studio 实例。 如果未安装 Visual Studio，则选择“安装新的 SQL Server Data Tools 实例”可通过最低版本的 Visual Studio 安装 SSDT，但为获得最佳体验，建议通过[最新版本的 Visual Studio](https://www.visualstudio.com/downloads) 使用 SSDT。 

![选择 AS、IS、RS](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)



## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT for VS 2017（独立安装程序）

[![下载](../ssdt/media/download.png) 下载 SSDT for Visual Studio 2017 (15.8)](https://go.microsoft.com/fwlink/?linkid=2014060) 

> [!IMPORTANT]
> - 安装 SSDT for Visual Studio 2017 (15.8) 前，请卸载“Analysis Services 项目”和“Reporting Services 项目”扩展（若已安装），并关闭所有 VS 实例。



**版本信息**  
  
版本号：15.8  
生成号：14.0.16174.0  
发布日期：2018 年 9 月 5 日  

有关更改的完整列表，请参阅[更改日志](changelog-for-sql-server-data-tools-ssdt.md)。

SSDT for Visual Studio 2017 具有与 Visual Studio 相同的[系统需求](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs)。  

### <a name="available-languages---ssdt-for-vs-2017"></a>支持的语言 - SSDT for VS 2017

此版本的 SSDT for VS 2017 可安装以下语言：  

[中文(简体)]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x804) | 
[中文(繁体)]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x404) | 
[英语(美国)]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x409) | 
[法语]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x40c)  
[德语]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x407) | 
[意大利语]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x410) | 
[日语]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x411) | 
[朝鲜语]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x412) | 
[葡萄牙语（巴西）]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x416) | 
[俄语]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x419) | 
[西班牙语]( https://go.microsoft.com/fwlink/?linkid=2014060&clcid=0x40a)  





## <a name="supported-sql-versions"></a>受支持的 SQL 版本
  
|项目模板|支持的 SQL 平台|  
|-------------------|--------------------|  
关系数据库|  SQL Server 2005* - SQL Server 2017<br> （使用适用于 Visual Studio 2017 的 SSDT 17.x 或 SSDT 来连接 [Linux 上的 SQL Server](../linux/sql-server-linux-overview.md)）<br /><br />Azure SQL Database<br /><br />Azure SQL 数据仓库（仅支持查询；尚不支持数据库项目）<br /><br />  * SQL Server 2005 支持已停止提供，<br /><br /> 请转至官方支持的 SQL 版本|
  |Analysis Services 模型<br /><br />Reporting Services 报表 | SQL Server 2008 – SQL Server 2017|
  |Integration Services 包| SQL Server 2012 – SQL Server 2017    |
  
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
[SSDT 团队博客](http://blogs.msdn.com/b/ssdt/)  
[DACFx API 参考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下载 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
