---
title: 评估企业和合并评估报表 (SQL Server) |Microsoft Docs
description: 了解如何使用 DMA 评估企业和 SQL Server 在升级或迁移到 Azure SQL 数据库之前合并评估报表。
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 252e162b78f93b156adcea045bc869e618176331
ms.sourcegitcommit: 2663063e29f2868ee6b6d596df4b2af2d22ade6f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305355"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>评估企业和合并使用 DMA 评估报表

以下分步说明可帮助您可以使用数据迁移助手的本地 SQL Server 或 SQL Server Azure Vm 上的运行升级或迁移到 Azure SQL 数据库执行成功缩放的评估。

## <a name="prerequisites"></a>先决条件

- 指定工具的计算机将会启动 DMA 在网络上。 请确保此计算机已连接到 SQL Server 目标。
- 下载并安装：
    - [数据迁移助手](https://www.microsoft.com/download/details.aspx?id=53595)v3.6 或更高版本。
    - [PowerShell](https://aka.ms/wmf5download) 5.0 版或更高版本。
    - [.NET framework](https://www.microsoft.com/download/details.aspx?id=30653) v4.5 或更高版本。
    - [SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.0 或更高版本。
    - [Power Bi desktop](https://docs.microsoft.com/power-bi/desktop-get-the-desktop)。
    - [Azure PowerShell 模块](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.0.0)
- 下载并提取：
    - [DMA 报表 Power BI 模板](https://msdnshared.blob.core.windows.net/media/2019/02/PowerBI-Reports.zip)。
    - [LoadWarehouse 脚本](https://msdnshared.blob.core.windows.net/media/2019/02/LoadWarehouse1.zip)。

## <a name="loading-the-powershell-modules"></a>加载 PowerShell 模块
保存到 PowerShell 模块目录的 PowerShell 模块，可调用而无需使用之前显式加载的模块。

若要加载模块，请执行以下步骤：
1. 导航到 C:\Program Files\WindowsPowerShell\Modules，然后创建名为的文件夹**DataMigrationAssistant**。
2. 打开[PowerShell 模块](https://msdnshared.blob.core.windows.net/media/2019/02/PowerShell-Modules2.zip)，然后将它们保存到你创建的文件夹。

      ![PowerShell 模块](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    每个文件夹包含关联的 psm1 文件中，在下图中所示：

   ![PowerShell 模块 psm1 文件](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > 文件夹和它包含 psm1 文件必须具有相同的名称。

   > [!IMPORTANT]
   > 您可能需要解除锁定 PowerShell 文件后将其保存到 WindowsPowerShell 目录以确保能够正确加载的模块。 若要解除锁定 PowerShell 文件，右键单击文件，选择**属性**，选择**解除阻止**文本框中，并选择**确定**。

   ![psm1 文件属性](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    新的 PowerShell 会话启动时 PowerShell 现在应会自动加载这些模块。

## <a name="create-inventory"></a> 创建 SQL 服务器的清单
然后再运行 PowerShell 脚本，以评估 SQL Server，构建所需的 SQL 服务器，你想要评估的清单。

此清单，可以采用两种形式之一：
- Excel CSV 文件
- SQL Server 表

### <a name="if-using-a-csv-file"></a>如果使用的 CSV 文件
> [!IMPORTANT]
> 确保在清单文件保存为逗号分隔 (CSV) 文件。

如果使用 csv 文件导入数据，请确保有只有两个列的数据-**实例名称**并**数据库名称**，和列不包含标头行。
 
 ![csv 文件内容](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-sql-server-table"></a>如果使用的 SQL Server 表
创建一个数据库，称为**EstateInventory**和名为表**DatabaseInventory**。 包含此清单数据的表可以具有任意数量的列，只要存在以下四列：
- ServerName
- InstanceName
- DatabaseName
- AssessmentFlag

![SQL Server 表的内容](../dma/media//dma-consolidatereports/dma-sql-server-table-contents.png)

如果此数据库不在工具计算机上，确保工具计算机具有到此 SQL Server 实例的网络连接。

通过 CSV 文件中使用 SQL Server 表的好处是，可以使用评估标记列以控制实例 / 数据库，获取选择进行评估，因此可以轻松地单独的较小的区块的评估。  然后可以跨多个评估 （请参阅部分在这篇文章中更高版本运行评估），这是更容易维护多个 CSV 文件。

请记住，具体取决于许多对象和其复杂性，评估可能需要特别长的时间 （小时数 +），因此它是比较明智的做法来分隔成可管理块的评估。

## <a name="running-a-scaled-assessment"></a>运行缩放的评估
加载到模块目录的 PowerShell 模块并创建后清单，您需要通过打开 PowerShell 并运行 dmaDataCollector 函数进行缩放的评估。
 
  ![dmaDataCollector 函数列表](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

介绍了下表与 dmaDataCollector 函数相关联的参数。

|参数  |Description |
|---------|---------|
|**getServerListFrom** | 你的清单。 可能的值为**SqlServer**并**CSV**。<br/>有关详细信息，请参阅[创建的 SQL Server 清单](#create-inventory)。 |
|**serverName** | 清单时使用的 SQL Server 实例名称**SqlServer**中**getServerListFrom**参数。 |
|**databaseName** | 托管库存表的数据库。 |
|**AssessmentName** | DMA 评估的名称。 |
|**TargetPlatform** | 你想要执行评估目标类型。  可能的值为**AzureSQLDatabase**， **SQLServer2012**， **SQLServer2014**， **SQLServer2016**， **SQLServerLinux2017**， **SQLServerWindows2017**，和**ManagedSqlServer**。 |
|**AuthenticationMethod** | 连接到你想要评估的 SQL Server 目标的身份验证方法。 可能的值为**SQLAuth**并**WindowsAuth**。 |
|**OutputLocation** | 评估在其中存储 JSON 输出文件目录。 具体取决于所评估的数据库数目和数据库内的对象数，评估可能需要极长的时间。 所有评估都完成后，将写入文件。 |

如果出现意外的错误，将终止此过程获取启动命令窗口。  查看错误日志以确定失败的原因。
 
  ![错误日志位置](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>使用评估 JSON 文件

现在，你的评估完成后，你准备好将数据导入 SQL Server，以进行分析。 若要使用评估 JSON 文件，打开 PowerShell 并运行 dmaProcessor 函数。
 
  ![dmaProcessor 函数列表](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

介绍了下表与 dmaProcessor 函数相关联的参数。

|参数  |Description |
|---------|---------|
|**processTo** | 将向其处理的 JSON 文件的位置。 可能的值为**SQLServer**并**AzureSQLDatabase**。 |
|**serverName** | SQL Server 实例处理数据。  如果指定**AzureSQLDatabase**有关**processTo**参数，则包括仅 SQL Server 名称 (不包括。 database.windows.net)。 面向 Azure SQL 数据库; 时将提示输入两个登录名第一个是你的 Azure 租户凭据，而第二个是您为 Azure SQL Server 的管理员登录名。 |
|**CreateDMAReporting** | 要创建用于处理 JSON 文件的临时数据库。  如果已指定的数据库存在，此参数设置为其中一个，然后不创建对象。  此参数可用于重新创建已删除的单个对象。 |
|**CreateDataWarehouse** | 创建将由 Power BI 报表数据仓库。 |
|**databaseName** | DMAReporting 数据库的名称。 |
|**warehouseName** | 数据仓库数据库的名称。 |
|**jsonDirectory** | 包含 JSON 评估文件的目录。  如果在目录中，有多个 JSON 文件，则它们正在处理一个一个地。 |

DmaProcessor 函数应该只需要几秒钟来处理单个文件。

## <a name="loading-the-data-warehouse"></a>加载数据仓库
DmaProcessor 已完成处理评估文件后，数据将加载到 DMAReporting 数据库报告表中。 此时，您需要加载数据仓库。

1. 使用 LoadWarehouse 脚本来填充维度中的任何缺失值。

    该脚本将 DMAReporting 数据库中获取报告表中的数据，并将其加载到数据仓库。  如果在此加载过程中不存在任何错误，它们可能导致的维度表中缺失的条目。

2. 加载数据仓库。
 
      ![加载的 LoadWarehouse 内容](../dma/media//dma-consolidatereports/dma-LoadWarehouse-loaded.png)

## <a name="set-your-database-owners"></a>设置数据库所有者
尽管这不是必需的若要从报告，获取最大的价值建议中设置数据库所有者**dimDBOwner**维度，并更新**DBOwnerKey**中**FactAssessment**表。  按此过程将允许进行切片和筛选基于特定的数据库所有者在 Power BI 报表。

LoadWarehouse 脚本还可用于提供基本的 TSQL 语句，你才能设置数据库所有者。

  ![LoadWarehouse 设置所有者](../dma/media//dma-consolidatereports/dma-LoadWarehouse-set-owners.png)

## <a name="dma-reports"></a>DMA 报表

1. 在 Power BI Desktop 中打开 DMA 报表 Power BI 模板。
2. 输入服务器详细信息指向你**DMAWarehouse**数据库，并选择**负载**。
   
      ![加载 DMA 报表 Power BI 模板](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   已刷新报表中的数据后**DMAWarehouse**数据库，您将看到类似于以下的报告。

   ![DMAWarehouse 报表视图](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report1.png)

   > [!TIP]
   > 如果没有看到你所期待的数据，请尝试更改活动书签。  有关详细信息，请参阅以下部分中的详细信息。

## <a name="working-with-dma-reports"></a>使用 DMA 报表
若要处理的 DMA 报表，使用书签和切片器要作为筛选依据：
- 评估类型 （Azure SQL DB、 Azure SQL MI、 SQL 内部） 
- 实例名
- 数据库名称
- 团队名称

若要访问的书签和筛选器边栏选项卡，选择主报表页上的筛选器书签：

![DMA 报表书签和筛选器](../dma/media//dma-consolidatereports/dma-report-bookmarks-filters.png)

这使以下边栏选项卡：

![DMA 报告视图边栏选项卡](../dma/media//dma-consolidatereports/dma-report-views-blade.png)

可以使用书签报表之间切换上下文：
- Azure SQL DB 云评估
- Azure SQL MI 云评估
- 在本地评估

![DMA 报告视图的书签](../dma/media//dma-consolidatereports/dma-report-bookmarks1.png)

若要隐藏筛选器边栏选项卡，ctrl 键并单击后退按钮：

![DMA 报告视图后退按钮](../dma/media//dma-consolidatereports/dma-report-bookmarks-back.png)

要显示在以下任何一项上当前是否应用了筛选器的报表页的左下角还有一个提示：
* FactAssessment-InstanceName
* FactAssessment – DatabaseName
* dimDBOwner-DBOwner

![应用筛选器提示](../dma/media//dma-consolidatereports/dma-filter-applied-prompt.png)

> [!NOTE]
> 如果您仅执行 Azure SQL 数据库评估，然后填充只有云报表。 相反，如果您仅执行内部评估，只有在本地报表进行填充。 但是，如果执行 Azure 和本地评估，然后加载到仓库的这两种评估您可以切换云报表和通过按住 CTRL 单击本地报表关联的图标。

## <a name="reports-visuals"></a>报表视觉对象
以下各节中显示的 Power BI 报表中显示的详细信息。

### <a name="readiness-"></a>准备情况 %

  ![DMA 准备情况百分比](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

根据选定内容上下文更新此视觉对象时 (所有内容，实例，数据库 [序列图的])。

### <a name="readiness-count"></a>准备情况计数

  ![DMA 准备情况计数](../dma/media//dma-consolidatereports/dma-readiness-count.png)

此视觉对象显示的数据库的已准备好迁移不是尚未准备好迁移的数据库的计数的计数。

### <a name="readiness-bucket"></a>准备情况存储桶

  ![DMA 准备情况存储桶](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

此视觉对象显示数据库的以下就绪情况存储桶的细分：
- 100%就绪
- 75 99%就绪
- 50-75%就绪
- 未就绪

### <a name="issues-word-cloud"></a>问题 Word 云
 
  ![DMA 问题 WordCloud](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

此视觉对象中选定内容上下文显示当前内发生的问题 (所有内容，实例，数据库 [序列图的])。 越大单词出现在屏幕上，更高版本的该类别中的问题数。 鼠标指针悬停在某个词显示该类别中出现的问题数。

### <a name="database-readiness"></a>数据库准备情况

  ![DMA 数据库准备情况报告](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

本部分是报表，其中显示了实例数据库的准备情况的主要部分。 此报表具有向下钻取层次的结构：
- InstanceDatabase
- ChangeCategory
- 标题
- ObjectType
- ImpactedObjectName

 ![DMA 数据库准备情况报表向下钻取](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

此报表还可以作为创建修正计划报表的筛选器点。

若要深化到修正计划报表，右键单击数据点在此图中，指向**钻取**，然后选择**修正计划**。

此任务来筛选当前层次结构级别取决于在其中选择钻取选项的点到修正计划报表。

  ![DMA 数据库准备情况报表向下钻取筛选](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![DMA 修正计划报表](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

您还可以使用修正计划报表上其自己构建自定义修正计划通过使用中的筛选器**可视化效果筛选器**边栏选项卡。
 
  ![DMA 修正计划的报表筛选器选项](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>脚本免责声明
*在本文中提供的示例脚本不受任何 Microsoft 标准支持计划或服务。仅按原样提供的所有脚本，而无需任何种类的担保。Microsoft 进一步拒绝所有默示的保证，包括但不限于，任何默示保证的适销性或适用于某种特定用途。与你保持因使用或执行示例脚本和文档的全部风险。在任何 Microsoft、 其作者或创建、 生产或交付的脚本中其他涉及的任何人都应承担任何责任 （包括但不限于，损失业务利润损失、 业务中断、 丢失业务信息或其他 pecuniary 丢失） 因使用或不能使用的示例脚本或文档，即使 Microsoft 已被告知此类损害的可能性。查找之前在其他站点/存储库/博客上重新发布这些脚本的权限。*
