---
title: 确定适当的 Azure SQL 数据库 SKU 的本地数据库 （数据迁移助手） |Microsoft Docs
description: 了解如何使用数据迁移助手来识别你的本地数据库的权限 Azure SQL 数据库 SKU
ms.custom: ''
ms.date: 05/06/2019
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
ms.author: jtoland
manager: jroth
ms.openlocfilehash: 5effd31d37af5fbe119f1ad23781b994fa89c240
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794322"
---
# <a name="identify-the-right-azure-sql-databasemanaged-instance-sku-for-your-on-premises-database"></a>标识你的本地数据库的权限 Azure SQL 数据库/托管实例 SKU

将数据库迁移到云中可能十分复杂，尤其是在尝试为数据库选择最佳的 Azure 数据库目标和 SKU。 我们的目标与数据库迁移助手 (DMA) 是可帮助解决这些问题，使体验更轻松通过提供用户友好输出这些 SKU 建议将数据库迁移。

本文重点介绍 DMA 的 Azure SQL 数据库 SKU 的建议功能。 Azure SQL 数据库具有多个部署选项，包括：

- 单一数据库
- 弹性池
- 托管的实例

功能可用于确定这两个建议的 Azure SQL 数据库单一数据库的最小 SKU 建议或 SKU 基于从托管数据库的计算机收集性能计数器的托管的实例。 该功能提供了与定价层、 计算级别和最大数据大小，以及每月预计的成本相关的建议。 它还提供对大容量预配单一数据库和 Azure 中的所有建议的数据库的托管的实例的功能。

> [!NOTE]
> 此功能目前仅通过命令行接口 (CLI)。

以下是帮助您确定 Azure SQL 数据库 SKU 建议和预配相应的单一数据库或在 Azure 中使用 DMA 的托管的实例的说明。

## <a name="prerequisites"></a>先决条件

- 下载并安装最新版[DMA](https://aka.ms/get-dma)。 如果已经有该工具的早期版本中，打开它，并将提示您升级 DMA。
- 请确保您的计算机具有[PowerShell 版本 5.1](https://www.microsoft.com/download/details.aspx?id=54616)或更高版本，需要运行所有脚本。 有关 findoug 的您的计算机安装的 PowerShell 版本的信息，请参阅文章[下载并安装 Windows PowerShell 5.1](https://docs.microsoft.com/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1)。
- 请确保您的计算机具有安装 Azure Powershell 模块。 有关详细信息，请参阅文章[安装 Azure PowerShell 模块](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.8.0)。
- 验证 PowerShell 文件**SkuRecommendationDataCollectionScript.ps1**，需要收集的性能计数器，DMA 文件夹中安装。
- 请确保将其执行此过程的计算机具有到托管数据库的计算机的管理员权限。

## <a name="collect-performance-counters"></a>收集性能计数器

该过程的第一步是收集有关你数据库的性能计数器。 可以通过在承载您的数据库的计算机上运行 PowerShell 命令收集性能计数器。 DMA 为您提供一份此 PowerShell 文件，但也可以使用您自己的方法来从您的计算机捕获性能计数器。

不需要单独为每个数据库执行此任务。 从计算机收集的性能计数器可以用于建议的计算机上承载的所有数据库的 SKU。

1. 在 DMA 文件夹中，找到 PowerShell 文件 SkuRecommendationDataCollectionScript.ps1。 需要此文件以收集性能计数器。

    ![DMA 文件夹中所示的 PowerShell 文件](../dma/media/dma-sku-recommend-data-collection-file.png)

2. 使用以下参数运行 PowerShell 脚本：
    - **ComputerName**:计算机承载数据库的名称。
    - **OutputFilePath**:要保存所收集的计数器的输出文件路径。
    - **CollectionTimeInSeconds**:在此期间你想要收集性能计数器数据的时间量。 捕获性能计数器至少 40 分钟，以便获取有意义的建议。 捕获，期越长越准确建议将。 此外请确保工作负荷在运行所需的数据库，以便更准确的建议。
    - **DbConnectionString**:指向要从中收集性能计数器数据的计算机上承载的 master 数据库连接字符串。

    下面是示例调用：

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```

    该命令执行后，该过程将输出文件包括到您指定的位置的性能计数器。 可以使用此文件作为输入的下一步部分的过程中，它将提供 SKU 建议为单一数据库和托管的实例选项。

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>使用 DMA CLI 来获取 SKU 建议

使用性能计数器作为此过程的输入创建输出文件。

对于单一数据库选项，DMA 将提供您的计算机上的定价层、 计算级别和每个数据库的最大数据大小的 Azure SQL 数据库单一数据库的建议。 如果您的计算机上有多个数据库，还可以指定想为其建议的数据库。 DMA 将还为您提供每月估计成本为每个数据库。

对于托管实例，建议支持的提升和转移方案。 因此，DMA 将您提供有关您的计算机上的定价层、 计算级别和组数据库的最大数据大小的 Azure SQL 数据库托管实例的建议。 同样，如果您的计算机上有多个数据库，还可以指定想为其建议的数据库。 DMA 将还为你每月估计成本与托管实例。

若要使用 DMA CLI 获取 SKU 的建议，在命令提示符处，运行 dmacmd.exe 使用以下参数：

- **/ 操作 = SkuRecommendation**:输入此参数，以执行 SKU 评估。
- **/SkuRecommendationInputDataFilePath**:在上一节中收集计数器文件的路径。
- **/ SkuRecommendationTsvOutputResultsFilePath**:要写入的输出结果以 TSV 格式的路径。
- **/ SkuRecommendationJsonOutputResultsFilePath**:要以 JSON 格式写入输出结果的路径。
- **/SkuRecommendationHtmlResultsFilePath**:若要以 HTML 格式写入输出结果的路径。

此外，选择下列参数之一：

- 防止价格刷新
  - **/SkuRecommendationPreventPriceRefresh**:如果设置为 True，防止发生价格刷新并且假定默认价格。 如果在脱机模式下运行，请使用此选项。 如果不使用此参数，则必须指定以下以获得最新价格基于指定的区域参数。
- 获取最新的价格
  - **/ SkuRecommendationCurrencyCode**:要在其中显示的价格 （例如货币"美元"）。
  - **/ SkuRecommendationOfferName**:产品/服务命名 （例如"MS-条-0003 P")。 有关详细信息，请参阅[Microsoft Azure 产品/服务详细信息](https://azure.microsoft.com/support/legal/offer-details/)页。
    - **/ SkuRecommendationRegionName**:区域名称 (例如，"WestUS")。
    - **/ SkuRecommendationSubscriptionId**:订阅的 ID。
    - **/AzureAuthenticationTenantId**:身份验证租户中。
    - **/AzureAuthenticationClientId**:用于身份验证的 AAD 应用客户端 ID。
    - 以下身份验证选项之一：
      - 交互
        - **AzureAuthenticationInteractiveAuthentication**:设置为 true 的身份验证弹出窗口。
      - 基于证书
        - **AzureAuthenticationCertificateStoreLocation**:将设置为证书存储位置 (例如，"CurrentUser")。
        - **AzureAuthenticationCertificateThumbprint**:将设置为证书指纹。
      - 基于令牌
        - **AzureAuthenticationToken**:将设置为证书令牌。

> [!NOTE]
> 若要获取的 ClientId 和 TenantId 进行交互式身份验证，您需要配置一个新的 AAD 应用程序。 有关详细信息身份验证和一文中获取这些凭据[Microsoft Azure 计费 API 代码示例：RateCard API](https://azure.microsoft.com/resources/samples/billing-python-ratecard-api/)，请按照下面的说明**步骤 1:在你的 AAD 租户中配置本机客户端应用程序**。

最后，还有一个可选参数，可用于指定想为其建议的数据库： 

- **/ SkuRecommendationDatabasesToRecommend**:要为其提供建议的数据库的列表。 输入.csv 中找到的数据库名称区分大小写，并且必须 (1)、 （2） 每个将括在双引号、 和 （3） 每个名称之间存在单个空格分隔 (例如 /SkuRecommendationDatabasesToRecommend ="Database1""数据库 2""Database3"). 忽略此参数确保为.csv 输入的文件中标识的所有用户数据库提供的建议。  

以下是一些示例调用：

**示例 1:获取与默认的价格的建议。使用在脱机模式下运行时或您没有所需身份验证凭据。**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

**示例 2:获取指定的区域 （例如，"ukwest") 与最新的价格的建议。**

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

**示例 3:获取为特定数据库的建议 （例如“TPCDS1G,EDW_3G,TPCDS10G”).**

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
/SkuRecommendationDatabasesToRecommend=“TPCDS1G” “EDW_3G” “TPCDS10G” 
/AzureAuthenticationInteractiveAuthentication=true 
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId> 
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

有关单一数据库的建议，TSV 输出文件看起来，如下所示：

![DMA 文件夹中所示的 PowerShell 单数据库文件](../dma/media/dma-sku-recommend-single-db-recommendations.png)

有关托管的实例的建议，TSV 输出文件看起来，如下所示：

![DMA 文件夹中所示的 PowerShell 托管的实例文件](../dma/media/dma-sku-recommend-mi-recommendations.png)

后面的输出文件中每个列说明。

- **DatabaseName** -数据库的名称。
- **MetricType** -建议使用 Azure SQL 数据库单一数据库/托管实例层。
- **MetricValue** -建议使用 Azure SQL 数据库单一数据库/托管实例 SKU。
- **PricePerMonth** – 对于相应的 SKU，每月估计的价格。
- **RegionName** – 相应 SKU 的区域名称。 
- **IsTierRecommended** -我们使每个层的最小 SKU 建议。 我们然后应用试探法来确定您的数据库的适当层。 这反映了数据库，建议的层。 
- **ExclusionReasons** -此值为空白，如果一个层建议。 不建议将每个层，我们提供为什么它不选取的原因。
- **AppliedRules** -已应用的规则的简短表示法。

最终的建议的层 (即**MetricType**) 和值 (即**MetricValue**) 的位置找到**IsTierRecommended**列是 TRUE-反映了最小 SKU所需的查询以在 Azure 中运行使用类似于你的本地数据库的成功率。 对于托管实例，DMA 目前支持为 40vcore Sku 最常使用 8vcore 的建议。 例如，如果建议的最小 SKU 适用于标准层 S4 然后选择 S3 或下面将会导致查询超时或无法执行。

HTML 文件包含此信息以图形格式。 它提供了一种用户友好查看最终的建议和预配过程的下一步的一部分。 下一节中的 HTML 输出的详细信息。

## <a name="provision-recommended-skus-to-azure"></a>预配到 Azure 中建议的 Sku

只需几次单击，可以使用预配目标 Sku 中你可以将数据库迁移到 Azure 中的标识的建议。 可以使用 HTML 文件输入 Azure 订阅;选取定价层、 计算级别和最大数据大小的数据库;并生成一个脚本来预配数据库。 您可以执行此脚本使用 PowerShell。

你可以在单台计算机上执行此过程，或可以确定在规模较大的 SKU 建议多台计算机上执行它。 DMA 目前可以简单且可缩放体验通过支持通过命令行界面的整个过程。

若要输入预配信息并对建议进行更改，请按如下所示更新 HTML 文件。

**有关单一数据库的建议**

![Azure SQL DB SKU 建议屏幕](../dma/media/dma-sku-recommend-single-db-recommendations1.png)

1. 打开 HTML 文件并输入以下信息：
    - **订阅 ID** -你想要预配数据库的 Azure 订阅的订阅 ID。
    - **资源组**-你想要将数据库部署的资源组。 输入存在的资源组。
    - **区域**-在其中设置数据库的区域。 请确保你的订阅支持选择的区域。
    - **服务器名称**-要部署的数据库的 Azure SQL 数据库服务器。 如果输入不存在的服务器名称，将创建它。
    - **管理员用户名**-服务器管理员用户名。
    - **管理员密码**-服务器管理员密码。 密码必须至少为八个字符且长度不能超过 128 个字符。 密码必须含以下类别中的三类 – 英文大写字母、 英文小写字母、 数字 (0-9) 和非字母数字字符 (！、 $、 #、 %等。)。 密码不能包含全部或部分 （3 + 连续字母） 从用户名。

2. 查看每个数据库的建议和修改的定价层、 计算级别，并根据需要的最大数据大小。 请务必取消选中当前不预配到希望的任何数据库。

3. 选择**生成预配脚本**和保存该脚本，然后在 PowerShell 中执行。

    此过程应创建 HTML 页中选择的所有数据库。

**有关托管的实例的建议**

![Azure SQL MI SKU 建议屏幕](../dma/media/dma-sku-recommend-mi-recommendations1.png)

1. 打开 HTML 文件并输入以下信息：
    - **订阅 ID** -你想要预配数据库的 Azure 订阅的订阅 ID。
    - **资源组**-你想要将数据库部署的资源组。 输入存在的资源组。
    - **区域**-在其中设置数据库的区域。 请确保你的订阅支持选择的区域。
    - **实例名称**– Azure SQL 托管实例你想要迁移的数据库的实例。 实例名称可以包含仅小写字母、 数字和-，但它不能开始或结尾-或具有超过 63 个字符。
    - **实例管理员用户名**– 实例管理员用户名。 请确保您的登录名满足以下要求-它是 SQL 标识符和不典型系统名称 （如管理员、 管理员、 sa、 根、 dbmanager、 loginmanager 等），或内置数据库用户或角色 （如 dbo、 guest、 public 等）。 请确保你的名称不包含空格、 Unicode 字符或非字母字符，并且它不以数字或符号开头。 
    - **实例管理员密码**-实例管理员密码。 你的密码必须至少 16 个字符且长度不能超过 128 个字符。 密码必须含以下类别中的三类 – 英文大写字母、 英文小写字母、 数字 (0-9) 和非字母数字字符 (！、 $、 #、 %等。)。 密码不能包含全部或部分 （3 + 连续字母） 从用户名。
    - **Vnet 名称**– 应在其下预配的托管的实例 VNet 名称。 输入现有的 VNet 名称。
    - **子网名称**– 应在其下预配的托管的实例的子网名称。 输入现有的子网名称。

2. 查看建议对于每个实例，并修改的定价层、 计算级别和最大数据大小根据需要。 目前仅限于为 40vcore Sku 8vcore 建议时，就仍有设置 64vcore 和 80vcore Sku，如果所需的选项。 请务必取消选中当前不预配到希望的任何实例。

    此过程应创建 HTML 页中选择的所有数据库。

    > [!NOTE]
    > （尤其是为第一次） 在子网上创建托管的实例可能需要几个小时才能完成。 通过 PowerShell 运行预配脚本后，可以检查在 Azure 门户中部署的状态。

## <a name="next-step"></a>下一步

- 用于从 CLI 运行 DMA 命令的完整列表，请参阅文章[运行数据迁移助手从命令行](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017)。
