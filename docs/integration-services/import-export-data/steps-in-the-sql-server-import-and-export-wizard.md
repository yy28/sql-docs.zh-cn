---
title: SQL Server 导入和导出向导中的步骤 | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0a6fb370c80af6221812b88d3694a230dc206f7b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296206"
---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>SQL Server 导入和导出向导中的步骤

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主题介绍使用 SQL Server 导入和导出向导导入和导出数据的一系列步骤。 它还包含一些指向文档各个页面的链接，该文档介绍了向导中显示的每个页面或对话框。

本主题仅介绍向导中的**各个步骤**。 如需其他信息，请参阅[相关任务和内容](#related)。

## <a name="steps-for-importing-and-exporting-data"></a>导入和导出数据的步骤  
 下表列出了导入和导出数据的步骤以及向导的相应页面。 通常不会显示其中所有页面，具体视用户在向导中选择的选项而定。  

若要快速浏览在典型场景中看到的多个屏幕，看看单页上这个端到端的简单示例：[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

|步骤|向导页面|  
|----------|------------------|  
|**欢迎使用**<br />不必在此页上执行任何操作。|[欢迎使用 SQL Server 导入和导出向导](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**选择数据源**。|[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|**选择数据目标**。|[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**配置目标**。 （可选步骤）<br /><br /> -   创建新的目标数据库。<br />-   如果要将数据复制到文本文件，请配置附加设置。|[创建数据库](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[配置平面文件目标](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**指定要复制的内容。**|[指定表复制或查询](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[提供源查询](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**配置复制操作**。 （可选步骤）<br /><br /> -   创建新的目标表。<br />-   确定当向导不知道如何在所选源和目标之间映射数据类型时应执行的操作。<br />-   查看源和目标之间的列映射。<br />-   处理转换源和目标之间的数据类型时发生的问题。<br />-   预览要复制的数据。|[Create Table SQL 语句](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[转换类型时不进行转换检查](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[查看数据类型映射](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[“列转换详细信息”对话框](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[“预览数据”对话框](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**复制数据。**<br /><br /> （可选）将设置另存为 SQL Server Integration Services (SSIS) 包。|[保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[保存 SSIS 包](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[完成向导](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[执行操作](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> 从向导的任何页面或对话框中点击 F1 键，可查看当前页的相关文档。

## <a name="related-tasks-and-content"></a><a name="related"></a>相关任务和内容  
以下是一些其他的基本任务。
-   **查看有关向导工作原理的简短示例。**

    -   **如果想查看屏幕快照。** 查看此仅占用一页的简单端对端示例 — [开始使用这一简单的导入和导出向导示例](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

    -   **如果想观看视频。** 观看这个来自 YouTube 的四分钟视频，该视频演示了此向导，并清晰简明地说明了将数据导出到 Excel 的方法：[使用 SQL Server 导入和导出向导导出到 Excel](https://go.microsoft.com/fwlink/?linkid=829049)。

-   **了解有关向导工作原理的详细信息。**

    -   **了解有关向导的详细信息。** 如果正在寻找有关该向导的概述，请参阅 [使用 SQL Server 导入和导出向导来导入和导出数据](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

    -   **了解如何连接到数据源和目标。** 如需有关如何连接到数据的信息，请从此处列表中选择所需的页面：[使用 SQL Server 导入和导出向导连接到数据源](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 其中为几个常用数据源中的每一个数据源专门设有一页文档信息页。 

-   **启动向导。** 如果已准备好运行向导，并且只想知道如何启动向导，请参阅[启动 SQL Server 导入和导出向导](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。

-     **获取向导。** 如果想要运行向导，但是尚未在计算机上安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则可以通过安装 SQL Server Data Tools (SSDT) 来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导。 有关详细信息，请参阅 [下载 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。


