---
title: 将数据从 SQL Server 加载到 Azure SQL 数据仓库中 (SSIS) | Microsoft Docs
description: 介绍如何创建 SQL Server Integration Services (SSIS) 包，以将数据从各种数据源移到 SQL 数据仓库。
services: sql-data-warehouse
documentationcenter: NA
author: douglaslMS
manager: craigg-msft
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.custom: loading
ms.date: 04/04/2018
ms.author: douglasl
ms.openlocfilehash: e5b34e72447d74875e67a0f1a71fb749a8c3d416
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35402529"
---
# <a name="load-data-from-sql-server-to-azure-sql-data-warehouse-with-sql-server-integration-services-ssis"></a>使用 SQL Server Integration Services (SSIS) 将数据从 SQL Server 加载到 Azure SQL 数据仓库

创建 SQL Server Integration Services (SSIS) 包，以将数据从 SQL Server 加载到 [Azure SQL 数据仓库](/azure/sql-data-warehouse/index)中。 可以选择在数据通过 SSIS 数据流时对其进行重构、转换和清理。

在本教程中，你将学习：

* 在 Visual Studio 中创建新的 Integration Services 项目。
* 连接到 SQL Server（作为源）和 SQL 数据仓库（作为目标）等数据源。
* 设计可将数据从源加载到目标中的 SSIS 包。
* 运行 SSIS 包以加载数据。

本教程使用 SQL Server 作为数据源。 SQL Server 可在本地或 Azure 虚拟机中运行。

## <a name="basic-concepts"></a>基本概念
包是 SSIS 中的工作单位。 相关包在项目中进行分组。 可使用 SQL Server Data Tools 在 Visual Studio 中创建项目并设计包。 设计过程是一个可视化过程，通过该过程，可将工具箱中的组件拖放到设计图面、连接这些组件并设置其属性。 完成包后，可以选择将其部署到 SQL Server，以实现全面管理、监视和安全。

## <a name="options-for-loading-data-with-ssis"></a>使用 SSIS 加载数据的选项
SQL Server Integration Services (SSIS) 是一组灵活的工具，提供多种选项，用于执行连接到 SQL 数据仓库和向其中加载数据等操作。

1. 使用 ADO NET 目标连接到 SQL 数据仓库。 本教程使用 ADO NET 目标，因为它的配置选项最少。
2. 使用 OLE DB 目标连接到 SQL 数据仓库。 与 ADO NET 目标相比，此选项提供的性能稍好。
3. 使用 Azure Blob 上载任务可在 Azure Blob 存储中暂存数据。 然后使用 SSIS 执行 SQL 任务，以启动 Polybase 脚本，将数据加载到 SQL 数据仓库中。 在此节列出的三个选项中，此选项提供的性能最佳。 要获取 Azure blob 上载任务，请下载[用于 Azure 的 Microsoft SQL Server 2016 Integration Services 功能包][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]。 要了解有关 PolyBase 的详细信息，请参阅 [PolyBase 指南][PolyBase Guide]。

## <a name="before-you-start"></a>开始之前
要逐步完成本教程，需要以下各项：

1. **SQL Server Integration Services (SSIS)**。 SSIS 是 SQL Server 的一个组件，需要评估版或许可版的 SQL Server。 要获取 SQL Server 2016 预览评估版，请参阅 [SQL Server 评估][SQL Server Evaluations]。
2. **Visual Studio**。 要获取免费的 Visual Studio Community Edition，请参阅 [Visual Studio Community][Visual Studio Community]。
3. **适用于 Visual Studio 的 SQL Server Data Tools (SSDT)**。 要获取适用于 Visual Studio 的 SQL Server Data Tools，请参阅[下载 SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)]。
4. **示例数据**。 本教程使用 AdventureWorks 示例数据库中存储在 SQL Server 中的示例数据，作为要加载到 SQL 数据仓库中的源数据。 要获取 AdventureWorks 示例数据库，请参阅 [AdventureWorks 2014 示例数据库][AdventureWorks 2014 Sample Databases]。
5. **SQL 数据仓库数据库和权限**。 本教程将连接到 SQL 数据仓库实例并向其中加载数据。 必须具有创建表格和加载数据的权限。
6. **防火墙规则**。 必须先使用本地计算机的 IP 地址在 SQL 数据仓库上创建防火墙规则，才可将数据上载到 SQL 数据仓库。

## <a name="step-1-create-a-new-integration-services-project"></a>步骤 1：创建新的 Integration Services 项目
1. 启动 Visual Studio。
2. 在“文件”菜单中，依次选择“新建”、“项目”。
3. 依次导航到“已安装”、“模板”、“商业智能”、“Integration Services”项目类型。
4. 选择“Integration Services 项目”。 提供“名称”和“位置”的值，然后选择“确定”。

Visual Studio 随即打开，并创建新的 Integration Services (SSIS) 项目。 然后，Visual Studio 在项目中打开单个新 SSIS 包 (Package.dtsx) 的设计器。 可看到以下屏幕区域：

* 左侧是 SSIS 组件的“工具箱”。
* 中间是包含多个选项卡的设计图面。 通常情况下，至少会使用“控制流”和“数据流”选项卡。
* 右侧是“解决方案资源管理器”和“属性”窗格。
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a>步骤 2：创建基本数据流
1. 将“数据流任务”从“工具箱”拖动到“控制流”选项卡上的设计图面。
   
    ![][02]
2. 双击“数据流任务”以便切换到“数据流”选项卡。
3. 从工具箱中的其他源列表中，将 ADO.NET 源拖到设计图面。 如果源适配器仍处于选中状态，请在“属性”窗格中将其名称更改为“SQL Server 源”。
4. 从“工具箱”的“其他目标”列表中，将 ADO.NET 目标拖动到 ADO.NET 源下的设计图面。 如果目标适配器仍处于选中状态，请在“属性”窗格中将其名称更改为“SQL DW 目标”。
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a>步骤 3：配置源适配器
1. 双击源适配器，打开“ADO.NET 源编辑器”。
   
    ![][03]
2. 在“ADO.NET 源编辑器”的“连接管理器”选项卡上，单击“ADO.NET 连接管理器”列表旁边的“新建”按钮，打开“配置 ADO.NET 连接管理器”对话框，并创建适用于 SQL Server 数据库的连接设置，本教程将从该数据库加载数据。
   
    ![][04]
3. 在“配置 ADO.NET 连接管理器”对话框中，单击“新建”按钮，打开“连接管理器”对话框并创建新的数据连接。
   
    ![][05]
4. 在“连接管理器”对话框中，执行以下操作。
   
   1. 对于“提供程序”，请选择 SqlClient 数据提供程序。
   2. 对于“服务器名称”，请输入 SQL Server 名称。
   3. 在“登录服务器”部分中，选择或输入身份验证信息。
   4. 在“连接到数据库”部分中，选择 AdventureWorks 示例数据库。
   5. 单击 **“测试连接”**。
      
       ![][06]
   6. 在报告连接测试结果的对话框中，单击“确定”返回“连接管理器”对话框。
   7. 在“连接管理器”对话框中，单击“确定”返回“配置 ADO.NET 连接管理器”对话框。
5. 在“配置 ADO.NET 连接管理器”对话框中，单击“确定”返回“ADO.NET 源编辑器”。
6. 在“ADO.NET 源编辑器”的“表格或视图名称”列表中，选择 Sales.SalesOrderDetail 表。
   
    ![][07]
7. 单击“预览”在“预览查询结果”对话框中查看源表中的前 200 行数据。
   
    ![][08]
8. 在“预览查询结果”对话框中，单击“关闭”返回“ADO.NET 源编辑器”。
9. 在“ADO.NET 源编辑器”中，单击“确定”完成配置数据源。

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a>步骤 4：将源适配器连接到目标适配器
1. 在设计图面上选择源适配器。
2. 选择从源适配器延伸出来的蓝色箭头，并将其拖动到目标编辑器，直到完好入位。
   
    ![][10]
   
    在典型的 SSIS 包中，可在源和目标之间使用 SSIS 工具箱中的许多其他组件，以在数据通过 SSIS 数据流时对其重构、转换和清理。 为了使此示例尽可能简单，我们将源直接连接到目标。

## <a name="step-5-configure-the-destination-adapter"></a>步骤 5：配置目标适配器
1. 双击目标适配器，打开“ADO.NET 目标编辑器”。
   
    ![][11]
2. 在“ADO.NET 目标编辑器”的“连接管理器”选项卡上，单击“连接管理器”列表旁边的“新建”按钮，打开“配置 ADO.NET 连接管理器”对话框，并创建适用于 Azure SQL 数据仓库数据库的连接设置，本教程将向该数据库加载数据。
3. 在“配置 ADO.NET 连接管理器”对话框中，单击“新建”按钮，打开“连接管理器”对话框并创建新的数据连接。
4. 在“连接管理器”对话框中，执行以下操作。
   1. 对于“提供程序”，请选择 SqlClient 数据提供程序。
   2. 针对“服务器名称”，请输入 SQL 数据仓库名称。
   3. 在“登录服务器”部分中，选择“使用 SQL Server 身份验证”或输入身份验证信息。
   4. 在“连接到数据库”部分中，选择现有 SQL 数据仓库数据库。
   5. 单击 **“测试连接”**。
   6. 在报告连接测试结果的对话框中，单击“确定”返回“连接管理器”对话框。
   7. 在“连接管理器”对话框中，单击“确定”返回“配置 ADO.NET 连接管理器”对话框。
5. 在“配置 ADO.NET 连接管理器”对话框中，单击“确定”返回“ADO.NET 目标编辑器”。
6. 在“ADO.NET 目标编辑器”中，单击“使用表格或视图”列表旁边的“新建”，打开“创建表格”对话框，创建包含与源表匹配的列列表的新目标表。
   
    ![][12a]
7. 在“创建表格”对话框中，执行以下操作。
   
   1. 将目标表的名称更改为 SalesOrderDetail。
   2. 删除 rowguid 列。 SQL 数据仓库不支持 uniqueidentifier 数据类型。
   3. 将 LineTotal 列的数据类型更改为 money。 SQL 数据仓库不支持 decimal 数据类型。 有关受支持数据类型的信息，请参阅 [CREATE TABLE（Azure SQL 数据仓库、并行数据仓库）][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]。
      
       ![][12b]
   4. 单击“确定”创建表格并返回“ADO.NET 目标编辑器”。
8. 在“ADO.NET 目标编辑器”中，选择“映射”选项卡以查看源中的列如何映射到目标中的列。
   
    ![][13]
9. 单击“确定”完成配置数据源。

## <a name="step-6-run-the-package-to-load-the-data"></a>步骤 6：运行包以加载数据
单击工具栏上的“开始”按钮，或在“调试”菜单上选择其中一个“运行”选项，以运行包。

当包开始运行时，可看到黄色的旋转齿轮，指示活动以及目前为止处理的行数。

![][14]

包运行完毕后，可看到绿色的对勾标记，指示操作成功以及从源加载到目标的数据总行数。

![][15]

恭喜！ 已成功使用 SQL Server Integration Services 将数据加载到 Azure SQL 数据仓库。

## <a name="next-steps"></a>后续步骤
* 了解 SSIS 数据流。 从此处开始：[数据流][Data Flow]。
* 了解如何在设计环境中调试包和排查包问题。 从此处开始：[包开发的故障排除工具][Troubleshooting Tools for Package Development]。
* 了解如何将 SSIS 项目和包部署到 Integration Services 服务器或其他存储位置。 从此处开始：[项目和包的部署][Deployment of Projects and Packages]。

<!-- Image references -->
[01]:  ./media/load-data-to-sql-data-warehouse/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-data-warehouse/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-data-warehouse/test-connection-06.png
[07]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-data-warehouse/preview-data-08.png
[09]:  ./media/load-data-to-sql-data-warehouse/source-destination-09.png
[10]:  ./media/load-data-to-sql-data-warehouse/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-data-warehouse/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-data-warehouse/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-data-warehouse/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-data-warehouse/column-mapping-13.png
[14]:  ./media/load-data-to-sql-data-warehouse/package-running-14.png
[15]:  ./media/load-data-to-sql-data-warehouse/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: ../relational-databases/polybase/polybase-guide.md
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: ../t-sql/statements/create-table-azure-sql-data-warehouse.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
