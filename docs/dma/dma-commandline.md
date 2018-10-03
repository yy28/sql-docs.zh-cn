---
title: 从命令行 (SQL Server) 中运行数据迁移助手 |Microsoft Docs
description: 了解如何从命令行来评估要迁移的 SQL Server 数据库运行数据迁移助手
ms.custom: ''
ms.date: 08/29/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 2fa770fad98918ab9e15231822b499787790a900
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745275"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>从命令行运行数据迁移助手
版本 2.1 和更高版本，当你安装数据迁移助手，它还会安装在 dmacmd.exe *%programfiles%\\Microsoft Data Migration Assistant\\*。 Dmacmd.exe 用于评估在无人参与模式下，数据库，并输出到 JSON 或 CSV 文件的结果。 评估多个数据库或大型数据库时，此方法是特别有用。 

> [!NOTE]
> Dmacmd.exe 支持仅运行评估。 目前不支持迁移。


## <a name="assessments-using-the-command-line-interface-cli"></a>使用命令行接口 (CLI) 的评估

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|参数  |Description  | 必需 （是/否）
|---------|---------|---------------|
| `/help or /?`     | 如何使用 dmacmd.exe 帮助文本        | N
|`/AssessmentName`     |   评估项目的名称   | Y
|`/AssessmentDatabases`     | 连接字符串的以空格分隔列表。 数据库名称 （初始目录） 是区分大小写。 | Y
|`/AssessmentTargetPlatform`     | 用于评估，支持的值的目标平台： SqlServer2012、 SqlServer2014、 SqlServer2016 和 AzureSqlDatabaseV12。 默认值是 SqlServer2016   | N
|`/AssessmentEvaluateFeatureParity`  | 运行功能奇偶一致性规则  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 运行兼容性规则  | Y <br> （AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations 是必需的。
|`/AssessmentEvaluateRecommendations`     | 运行功能推荐        | Y <br> （AssessmentEvaluateCompatibilityIssues 或所需的 AssessmentEvaluateRecommendationsis）
|`/AssessmentOverwriteResult`     | 覆盖结果文件    | N
|`/AssessmentResultJson`     | JSON 结果文件的完整路径     | Y <br> （AssessmentResultJson 或 AssessmentResultCsv 是必需的）
|`/AssessmentResultCsv`    | CSV 结果文件的完整路径   | Y <br>（AssessmentResultJson 或 AssessmentResultCsv 是必需的）


## <a name="examples-of-assessments-using-the-cli"></a>评估使用 CLI 的示例

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**使用 Windows 身份验证和运行兼容性规则的单一数据库评估**


```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***Integrated Security=true*"**
***/AssessmentEvaluateCompatibilityIssues*** /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**单一数据库评估，请参阅 SQL Server 身份验证和运行功能建议**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**目标平台 SQL Server 2012 的单个数据库评估将结果保存到.json 和.csv 文件**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
```

**目标平台 SQL Azure 数据库的单一数据库评估将结果保存到.json 和.csv 文件**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="AzureSqlDatabaseV12"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"
```

**多个数据库评估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
***/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"***
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

## <a name="azure-sql-database-sku-recommendations-using-the-cli"></a>使用 CLI 的 azure SQL 数据库 SKU 建议

> [!IMPORTANT]
> SKU 建议为 Azure SQL 数据库是当前可用于迁移 SQL Server 2016 或更高版本。

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

|参数  |Description  | 必需 （是/否）
|---------|---------|---------------|
|`/Action=SkuRecommendation` | 执行 SKU 评估，请参阅 DMA 命令行 | Y
|`/SkuRecommendationInputDataFilePath`  | 从承载数据库的计算机收集的性能计数器文件的完整路径 |    Y
|`/SkuRecommendationTsvOutputResultsFilePath`   | TSV 结果文件的完整路径 |    Y <br>（TSV 或 JSON 或 HTML 文件路径是必需的）
|`/SkuRecommendationJsonOutputResultsFilePath`  | JSON 结果文件的完整路径 |   Y <br>（TSV 或 JSON 或 HTML 文件路径是必需的）
|`/SkuRecommendationHtmlResultsFilePath` |  HTML 结果文件的完整路径 | Y <br>（TSV 或 JSON 或 HTML 文件路径是必需的）
|`/SkuRecommendationPreventPriceRefresh` |  防止发生价格刷新。 如果在脱机模式下运行，请使用此选项。 |    Y <br>（此参数用于静态价格或下面的所有参数都需要选择用于获取最新的价格）
|`/SkuRecommendationCurrencyCode` | 要在其中显示的价格 （例如货币"美元"） | Y <br>（如果你想要获取最新的价格）
|`/SkuRecommendationOfferName` |    产品/服务命名 （例如"MS-条-0003 P")。 有关详细信息，请参阅[Microsoft Azure 产品/服务详细信息](https://azure.microsoft.com/support/legal/offer-details/)页。 |   Y <br>（如果你想要获取最新的价格）
|`/SkuRecommendationRegionName` |   区域名称 （例如"WestUS") |   Y <br>（如果你想要获取最新的价格）
|`/SkuRecommendationSubscriptionId` | 订阅的 ID。 |    Y <br>（如果你想要获取最新的价格）
|`/AzureAuthenticationTenantId` | 身份验证租户中。 |  Y <br>（如果你想要获取最新的价格）
|`/AzureAuthenticationClientId` | 用于身份验证的 AAD 应用客户端 ID。 | Y <br>（如果你想要获取最新的价格）
|`/AzureAuthenticationInteractiveAuthentication`    | 设置为 true 以弹出窗口。 |   Y <br>（如果你想要获取最新的价格） <br>（选择一个 3 个身份验证选项的选项 1）
|`/AzureAuthenticationCertificateStoreLocation` | 设置为证书存储位置 （例如"CurrentUser")。 | Y <br>（如果你想要获取最新的价格） <br>（挑选一位的 3 个身份验证选项-选项 2）
|`/AzureAuthenticationCertificateThumbprint`    | 将设置为证书指纹。 | Y <br>（如果你想要获取最新的价格） <br>（挑选一位的 3 个身份验证选项-选项 2）
|`/AzureAuthenticationToken` |  将设置为证书令牌。 | Y <br>（如果你想要获取最新的价格） <br>（选择一个 3 个身份验证选项-选项 3）

## <a name="examples-of-sku-assessments-using-the-cli"></a>SKU 评估使用 CLI 的示例

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Azure SQL DB SKU，建议使用价格刷新 （获取最新的价格） 的交互式身份验证** 
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
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationInteractiveAuthentication=true 
```

**Azure SQL DB SKU，建议使用价格刷新 （获取最新的价格）-证书身份验证**
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
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationCertificateStoreLocation=<Your Certificate Store Location>
/AzureAuthenticationCertificateThumbprint=<Your Certificate Thumbprint>  
```

**Azure SQL DB SKU 建议价格刷新 （获取最新的价格）-使用令牌身份验证**  
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
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Azure SQL DB SKU 建议，而无需价格刷新 （使用静态价格）** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>另请参阅
- [数据迁移助手](https://aka.ms/get-dma)下载。
- 文章[标识适当 Azure SQL 数据库的 SKU 的本地数据库](https://aka.ms/dma-sku-recommend-sqldb)。
