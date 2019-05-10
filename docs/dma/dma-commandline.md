---
title: 从命令行 (SQL Server) 中运行数据迁移助手 |Microsoft Docs
description: 了解如何从命令行来评估要迁移的 SQL Server 数据库运行数据迁移助手
ms.custom: ''
ms.date: 05/06/2019
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
ms.openlocfilehash: ccb2b0b6a60bfc2df94f2cc09b087a22b22ce7ab
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105837"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>从命令行运行数据迁移助手

版本 2.1 和更高版本，当你安装数据迁移助手，它还会安装在 dmacmd.exe *%programfiles%\\Microsoft Data Migration Assistant\\*。 Dmacmd.exe 用于评估在无人参与模式下，数据库，并输出到 JSON 或 CSV 文件的结果。 评估多个数据库或大型数据库时，此方法是特别有用。 

> [!NOTE]
> Dmacmd.exe 支持仅运行评估。 目前不支持迁移。

## <a name="assessments-using-the-command-line-interface-cli"></a>使用命令行接口 (CLI) 的评估

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
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
|`/AssessmentSourcePlatform`     | 评估源平台： <br>支持的值进行评估：SqlOnPrem，RdsSqlServer （默认值） <br>对于目标准备情况评估支持的值：SqlOnPrem，RdsSqlServer （默认值），Cassandra （预览版）   | N
|`/AssessmentTargetPlatform`     | 用于评估的目标平台：  <br> 支持的值进行评估：AzureSqlDatabase、 ManagedSqlServer、 SqlServer2012、 SqlServer2014、 SqlServer2016、 SqlServerLinux2017 和 SqlServerWindows2017 （默认值）  <br> 对于目标准备情况评估支持的值：ManagedSqlServer （默认）、 CosmosDB （预览版）   | N
|`/AssessmentEvaluateFeatureParity`  | 运行功能奇偶一致性规则。 如果源平台是 RdsSqlServer，不支持将功能奇偶校验计算为目标平台 AzureSqlDatabase  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 运行兼容性规则  | Y <br> （AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations 是必需的。
|`/AssessmentEvaluateRecommendations`     | 运行功能推荐        | Y <br> （AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations 是必需的）
|`/AssessmentOverwriteResult`     | 覆盖结果文件    | N
|`/AssessmentResultJson`     | JSON 结果文件的完整路径     | Y <br> （AssessmentResultJson 或 AssessmentResultCsv 是必需的）
|`/AssessmentResultCsv`    | CSV 结果文件的完整路径   | Y <br> （AssessmentResultJson 或 AssessmentResultCsv 是必需的）
|`/Action`    | 使用 SkuRecommendation 若要获取 SKU 建议，请使用 AssessTargetReadiness 执行目标准备情况评估。   | N
|`/SourceConnections`    | 以空格分隔的连接字符串的列表。 数据库名称 （初始目录） 是可选的。 如果未不提供任何数据库名称，将评估源上的所有数据库。   | Y <br> （必需操作是否 AssessTargetReadiness）
|`/TargetReadinessConfiguration`    | 描述值的名称、 源连接和结果文件的 XML 文件的完整路径。   | Y <br> （TargetReadinessConfiguration 或 SourceConnections 是必需的）
|`/FeatureDiscoveryReportJson`    | 功能发现 JSON 报表的路径。 如果生成此文件，然后它可再次运行目标准备情况评估，无需连接到源。 | N
|`/ImportFeatureDiscoveryReportJson`    | 前面创建的功能发现 JSON 报表路径。 而不是源连接，将使用此文件。   | N

## <a name="examples-of-assessments-using-the-cli"></a>评估使用 CLI 的示例

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**使用 Windows 身份验证和运行兼容性规则的单一数据库评估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**单一数据库评估，请参阅 SQL Server 身份验证和运行功能建议**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**目标平台 SQL Server 2012 的单个数据库评估将结果保存到.json 和.csv 文件**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
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
/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

**使用 Windows 身份验证的单一数据库目标准备情况评估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**单一数据库目标准备情况评估，请参阅 SQL Server 身份验证**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**目标平台 SQL Azure 数据库的单一数据库评估将结果保存到.json 和.csv 文件**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentSourcePlatform="SqlOnPrem"
/AssessmentTargetPlatform="AzureSqlDatabase"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"

```

**多个数据库目标准备情况评估**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/AssessmentSourcePlatform=SourcePlatform
/AssessmentTargetPlatform=TargetPlatform
/SourceConnections="Server=SQLServerInstanceName1;Initial Catalog=DatabaseName1;Integrated Security=true" "Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated Security=true" "Server=SQLServerInstanceName2;Initial Catalog=DatabaseName3;Integrated Security=true"
/AssessmentOverwriteResult  
/AssessmentResultJson="C:\Results\test2016.json"

(/AssessmentSourcePlatform and /AssessmentTargetPlatform are optional.)
```

**使用 Windows 身份验证的服务器上的所有数据库的目标准备情况评估**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**通过导入先前创建的功能发现报告目标准备情况评估**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**通过提供配置文件的目标准备情况评估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

使用源连接时的配置文件内容：

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <SourcePlatform>Source Platform</SourcePlatform> <!-- Optional. The default is SqlOnPrem -->
  <TargetPlatform>TargetPlatform</TargetPlatform> <!-- Optional. The default is ManagedSqlServer -->
  <SourceConnections>
    <SourceConnection>connection string 1</SourceConnection>
    <SourceConnection>connection string 2</SourceConnection>
    <!-- ... -->
    <SourceConnection>connection string n</SourceConnection>
  </SourceConnections>
  <AssessmentResultJson>path\to\file.json</AssessmentResultJson>
  <FeatureDiscoveryReportJson>path\to\featurediscoveryreport.json</FeatureDiscoveryReportJson>
  <OverwriteResult>true</OverwriteResult> <!-- or false -->
</TargetReadinessConfiguration>
```

配置文件中的内容时导入功能发现报告：

```
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-databasemanaged-instance-sku-recommendations-using-the-cli"></a>Azure SQL 数据库/托管实例 SKU 建议使用 CLI

这些命令支持为 Azure SQL 数据库单一数据库和托管的实例的部署选项的建议。

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
|`/SkuRecommendationInputDataFilePath` | 从承载数据库的计算机收集的性能计数器文件的完整路径 | Y
|`/SkuRecommendationTsvOutputResultsFilePath` | TSV 结果文件的完整路径 | Y <br> （需要 TSV 或 JSON 或 HTML 文件路径）
|`/SkuRecommendationJsonOutputResultsFilePath` | JSON 结果文件的完整路径 | Y <br> （需要 TSV 或 JSON 或 HTML 文件路径）
|`/SkuRecommendationHtmlResultsFilePath` | HTML 结果文件的完整路径 | Y <br> （需要 TSV 或 JSON 或 HTML 文件路径）
|`/SkuRecommendationPreventPriceRefresh` | 防止发生价格刷新。 如果 （例如，true），在脱机模式下运行，请使用此选项。 | Y <br> （选择任一此参数的静态价格或下面的所有参数都需要选择以获得最新价格）
|`/SkuRecommendationCurrencyCode` | 要在其中显示的价格 （例如货币"美元"） | Y <br> （适用于最新的价格）
|`/SkuRecommendationOfferName` | 产品/服务命名 （例如"MS-条-0003 P")。 有关详细信息，请参阅[Microsoft Azure 产品/服务详细信息](https://azure.microsoft.com/support/legal/offer-details/)页。 | Y <br> （适用于最新的价格）
|`/SkuRecommendationRegionName` | 区域名称 （例如"WestUS") | Y <br> （适用于最新的价格）
|`/SkuRecommendationSubscriptionId` | 订阅的 ID。 | Y <br> （适用于最新的价格）
|`/SkuRecommendationDatabasesToRecommend` | 数据库要 （例如建议的以空格分隔列表"Database1""数据库 2""Database3")。 名称区分大小写，并且必须用双引号引起来。 如果省略，建议提供的所有数据库。 | N
|`/AzureAuthenticationTenantId` | 身份验证租户中。 | Y <br> （适用于最新的价格）
|`/AzureAuthenticationClientId` | 用于身份验证的 AAD 应用客户端 ID。 | Y <br> （适用于最新的价格）
|`/AzureAuthenticationInteractiveAuthentication` | 设置为 true 以弹出窗口。 | Y <br> （适用于最新的价格） <br>（选择一个 3 个身份验证选项的选项 1）
|`/AzureAuthenticationCertificateStoreLocation` | 设置为证书存储位置 （例如"CurrentUser")。 | Y <br>（适用于最新的价格） <br> （挑选一位的 3 个身份验证选项-选项 2）
|`/AzureAuthenticationCertificateThumbprint` | 将设置为证书指纹。 | Y <br> （适用于最新的价格） <br>（挑选一位的 3 个身份验证选项-选项 2）
|`/AzureAuthenticationToken` | 将设置为证书令牌。 | Y <br> （适用于最新的价格） <br>（选择一个 3 个身份验证选项-选项 3）

## <a name="examples-of-sku-assessments-using-the-cli"></a>SKU 评估使用 CLI 的示例

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**Azure SQL DB/MI SKU，建议使用价格刷新 （获取最新的价格） 的交互式身份验证** 

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

**Azure SQL DB/MI SKU，建议使用价格刷新 （获取最新的价格）-证书身份验证**

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

**价格刷新 （获取最新的价格）-azure SQL DB SKU/MI 建议令牌身份验证，并指定数据库来建议**
  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationDatabasesToRecommend=“TPCDS1G,EDW_3G,TPCDS10G”
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**Azure SQL DB/MI SKU 建议，而无需价格刷新 （使用静态价格）** 
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
