---
title: 确定适当的 Azure SQL 数据库 SKU 的本地数据库 （数据迁移助手） |Microsoft Docs
description: 了解如何使用数据迁移助手来识别你的本地数据库的权限 Azure SQL 数据库 SKU
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 578e6ac47e84ad764cb050112eae768ff21444f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151899"
---
# <a name="identify-the-right-azure-sql-database-sku-for-your-on-premises-database"></a>确定适当的 Azure SQL 数据库 SKU 的本地数据库

将数据库迁移到云的任务是复杂且耗时，涉及很多的变量。 为数据库选择正确的 Azure 数据库目标和 SKU 颇具挑战性。 我们的目标与数据库迁移助手 (DMA) 是处理这些问题并使数据库迁移体验简单且有效。

本文主要介绍 DMA 的 Azure SQL 数据库 SKU 的建议功能，它允许您标识建议基于从托管数据库的计算机收集性能计数器的 Azure SQL 数据库 SKU 的最小。 此功能提供了与定价层、 计算级别和最大数据大小，以及每月预计的成本相关的建议。 它还提供预配所有数据库到 Azure 中大容量的能力。

> [!NOTE] 
> 此功能目前仅通过命令行接口 (CLI)。 将在即将发布的版本中添加支持此功能通过 DMA 用户界面。

以下说明可帮助您确定 Azure SQL 数据库 SKU 的建议和使用数据迁移助手预配到 Azure，关联的数据库。

## <a name="prerequisites"></a>系统必备

下载数据库迁移助手 v4.0 或更高版本，然后将其安装。 如果已有该工具安装，请关闭并重新打开它，并将提示您升级该工具。

## <a name="collect-performance-counters"></a>收集性能计数器

该过程的第一步是收集有关你数据库的性能计数器。 可以通过在承载您的数据库的计算机上运行 PowerShell 命令收集性能计数器。 DMA 为您提供一份此 PowerShell 文件，但也可以使用您自己的方法来从您的计算机捕获性能计数器。

不需要单独为每个数据库执行此任务。 从计算机收集的性能计数器可以用于建议的计算机上承载的所有数据库的 SKU。

> [!IMPORTANT]
> 运行此命令的计算机需要到宿主数据库的计算机的管理员权限。

1. 验证 DMA 文件夹中安装了收集的性能计数器所需的 PowerShell 文件。

    ![DMA 文件夹中所示的 PowerShell 文件](../dma/media/dma-sku-recommend-data-collection-file.png)

2. 使用以下参数运行 PowerShell 脚本：
    - **ComputerName**:计算机承载数据库的名称。
    - **OutputFilePath**:要保存所收集的计数器的输出文件路径。
    - **CollectionTimeInSeconds**:在此期间你想要收集性能计数器数据的时间量。
      捕获性能计数器至少 40 分钟，以便获取有意义的建议。 捕获，期越长越准确建议将。
    - **DbConnectionString**:指向要从中收集性能计数器数据的计算机上承载的 master 数据库连接字符串。
     
    下面是示例调用：

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```
    
    该命令执行后，该过程将输出具有您指定的位置中的性能计数器的文件。 此文件可以用作下一节中的 SKU 建议命令输入。

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>使用 DMA CLI 来获取 SKU 建议

使用性能计数器作为此步骤的输入来自上一步的输出文件。 DMA 将为您提供有关 Azure SQL 数据库的建议在计算机上的定价层、 计算级别和每个数据库的最大数据大小。 DMA 将还为您提供每月估计成本为每个数据库。

使用以下参数运行 dmacmd.exe:

- **/ 操作 = SkuRecommendation**:输入此参数，以执行 SKU 评估。
- **/SkuRecommendationInputDataFilePath**:在上一节中收集计数器文件的路径。
- **/ SkuRecommendationTsvOutputResultsFilePath**:要写入的输出结果以 TSV 格式的路径。
- **/ SkuRecommendationJsonOutputResultsFilePath**:要以 JSON 格式写入输出结果的路径。
- **/SkuRecommendationHtmlResultsFilePath**:若要以 HTML 格式写入输出结果的路径。

此外，您需要选择以下参数之一：
- 防止价格刷新
    - **/SkuRecommendationPreventPriceRefresh**:防止发生价格刷新。 如果在脱机模式下运行，请使用此选项。
- 获取最新的价格 
    - **/ SkuRecommendationCurrencyCode**:要在其中显示的价格 （例如货币"美元"）。
    - **/ SkuRecommendationOfferName**:产品/服务命名 （例如"MS-条-0003 P")。 有关详细信息，请参阅[Microsoft Azure 产品/服务详细信息](https://azure.microsoft.com/support/legal/offer-details/)页。
    - **/ SkuRecommendationRegionName**:区域名称 （例如"WestUS")。
    - **/ SkuRecommendationSubscriptionId**:订阅的 ID。
    - **/AzureAuthenticationTenantId**:身份验证租户中。
    - **/AzureAuthenticationClientId**:用于身份验证的 AAD 应用客户端 ID。
    - 以下身份验证选项之一：
        - 交互
            - **AzureAuthenticationInteractiveAuthentication**:设置为 true 的身份验证弹出窗口。
        - 基于证书
            - **AzureAuthenticationCertificateStoreLocation**:设置为证书存储位置 （例如"CurrentUser")。
            - **AzureAuthenticationCertificateThumbprint**:将设置为证书指纹。
        - 基于令牌
            - **AzureAuthenticationToken**:将设置为证书令牌。

下面是一些示例调用：

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationInteractiveAuthentication=true
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

TSV 输出文件将包含下图中显示的列：

   ![DMA 文件夹中所示的 PowerShell 文件](../dma/media/dma-tsv-file-column.png)

后面的每个列说明。

- **DatabaseName** -数据库的名称。
- **MetricName** -是否执行某个度量值。
- **MetricType** -建议使用 Azure SQL 数据库层。
- **MetricValue** -建议使用 Azure SQL 数据库 SKU。
- **SQLMiEquivalentCores** -如果你选择只用于 Azure SQL 数据库托管实例，您可以使用此值为核心计数。
- **IsTierRecommended** -我们使每个层的最小 SKU 建议。 我们然后应用试探法来确定您的数据库的适当层。 
- **ExclusionReasons** -此值为空白，如果一个层建议。 不建议将每个层，我们提供为什么它不选取的原因。
- **AppliedRules** -已应用的规则的简短表示法。

建议的值为所需的查询使用成功率类似于你的本地数据库运行在 Azure 中的最小 SKU。 例如，如果建议的最小 SKU 适用于标准层 S4 然后选择 S3 或下面将会导致查询超时或无法执行。

HTML 文件包含此信息以图形格式。 HTML 文件可用于输入 Azure 订阅信息、 选取定价层、 数据库、 计算级别和最大数据大小和生成一个脚本来预配数据库。 可以使用 PowerShell 执行此脚本。

## <a name="provision-your-databases-to-azure"></a>预配到 Azure 数据库
只需几次单击，可以在你可以将数据库迁移到 Azure 中使用前一步骤中预配目标数据库的建议。 您还可以通过按如下所示更新 HTML 文件的建议进行更改。

1. 打开 HTML 文件并输入以下信息：
    - **订阅 ID** -你想要预配数据库的 Azure 订阅的订阅 ID。
    - **区域**-在其中设置数据库的区域。 请确保你的订阅支持选择的区域。
    - **资源组**-你想要将数据库部署的资源组。 输入存在的资源组。
    - **服务器名称**-要部署的数据库的 Azure SQL 数据库服务器。 如果输入不存在的服务器名称，将创建它。
    - **管理员用户名 \ 密码**-服务器管理员用户名和密码。

2. 查看每个数据库的建议和修改的定价层、 计算级别，并根据需要的最大数据大小。 请务必取消选中当前不预配到希望的任何数据库。

3. 选择**生成预配脚本**和保存该脚本，然后在 PowerShell 中执行。

    此过程应创建 HTML 页中选择的所有数据库。

您可以在此过程中在单台计算机上执行所有步骤，或可以都对多个计算机，以确定 SKU 在规模较大的建议。 DMA 可以通过支持所有这些步骤通过命令行界面简单且可缩放的体验。 同样，支持此功能通过 DMA 用户界面可今年晚些时候。

## <a name="next-steps"></a>后续步骤
- 下载最新版[数据迁移助手](https://aka.ms/get-dma)。
- 请参阅文章[运行数据迁移助手从命令行](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017)有关用于从 CLI 运行 DMA 的命令的完整列表。
