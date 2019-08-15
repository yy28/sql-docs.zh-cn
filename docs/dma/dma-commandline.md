---
title: 从命令行运行数据迁移助手 (SQL Server) |Microsoft Docs
description: 了解如何从命令行运行数据迁移助手以评估要迁移的 SQL Server 数据库
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
ms.openlocfilehash: f98d96547a367dcf7853a5b0d7c14b2d79b7df63
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028707"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>从命令行运行数据迁移助手

在版本2.1 及更高版本中, 安装数据迁移助手时, 它还将在 *% ProgramFiles%\\\\Microsoft 数据迁移助手*中安装 dmacmd。 使用 dmacmd 在无人参与模式下评估数据库, 并将结果输出到 JSON 或 CSV 文件。 评估多个数据库或大型数据库时, 此方法特别有用。 

> [!NOTE]
> Dmacmd 仅支持运行评估。 此时不支持迁移。

## <a name="assessments-using-the-command-line-interface-cli"></a>使用命令行接口 (CLI) 进行评估

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|参数  |描述  | 必需 (是/否)
|---------|---------|---------------|
| `/help or /?`     | 如何使用 dmacmd 帮助文本        | N
|`/AssessmentName`     |   评估项目的名称   | Y
|`/AssessmentDatabases`     | 用空格分隔的连接字符串列表。 数据库名称 (初始目录) 区分大小写。 | Y
|`/AssessmentSourcePlatform`     | 评估的源平台: <br>支持的评估值:SqlOnPrem, RdsSqlServer (默认值) <br>目标准备情况评估支持的值:SqlOnPrem、RdsSqlServer (默认)、Cassandra (预览版)   | N
|`/AssessmentTargetPlatform`     | 评估的目标平台:  <br> 支持的评估值:AzureSqlDatabase、ManagedSqlServer、SqlServer2012、2014、Sqlserver2016-ssei-expr、SqlServerLinux2017 和 SqlServerWindows2017 (默认值)  <br> 目标准备情况评估支持的值:ManagedSqlServer (默认值), CosmosDB (预览)   | N
|`/AssessmentEvaluateFeatureParity`  | 运行功能奇偶校验规则。 如果源平台为 RdsSqlServer, 则目标平台 AzureSqlDatabase 不支持功能奇偶校验评估  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 运行兼容性规则  | Y <br> (需要 AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations。)
|`/AssessmentEvaluateRecommendations`     | 运行功能建议        | Y <br> (需要 AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations)
|`/AssessmentOverwriteResult`     | 覆盖结果文件    | N
|`/AssessmentResultJson`     | JSON 结果文件的完整路径     | Y <br> (需要 AssessmentResultJson 或 AssessmentResultCsv)
|`/AssessmentResultCsv`    | CSV 结果文件的完整路径   | Y <br> (需要 AssessmentResultJson 或 AssessmentResultCsv)
|`/Action`    | 使用 SkuRecommendation 获取 SKU 建议, 使用 AssessTargetReadiness 执行目标准备情况评估。   | N
|`/SourceConnections`    | 连接字符串的空格分隔列表。 数据库名称 (初始目录) 是可选的。 如果未提供任何数据库名称, 则对该源上的所有数据库进行评估。   | Y <br> (如果 Action 为 "AssessTargetReadiness", 则为必需)
|`/TargetReadinessConfiguration`    | 描述名称、源连接和结果文件的值的 XML 文件的完整路径。   | Y <br> (需要 TargetReadinessConfiguration 或 SourceConnections)
|`/FeatureDiscoveryReportJson`    | 功能发现 JSON 报表的路径。 如果生成此文件, 则可以使用它再次运行目标就绪评估, 而无需连接到源。 | N
|`/ImportFeatureDiscoveryReportJson`    | 先前创建的功能发现 JSON 报表的路径。 将使用此文件, 而不是源连接。   | N

## <a name="examples-of-assessments-using-the-cli"></a>使用 CLI 评估的示例

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

**使用 SQL Server 身份验证和运行功能建议的单一数据库评估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**目标平台的单一数据库评估 SQL Server 2012, 将结果保存到 json 和 .csv 文件**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**针对目标平台 SQL Azure 数据库的单一数据库评估, 将结果保存到 json 和 .csv 文件**

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

**多数据库评估**

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

**使用 Windows 身份验证的单数据库目标就绪状态评估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**使用 SQL Server 身份验证的单数据库目标就绪状态评估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**针对目标平台 SQL Azure 数据库的单一数据库评估, 将结果保存到 json 和 .csv 文件**

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

**多数据库目标准备情况评估**

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

**使用 Windows 身份验证的服务器上所有数据库的目标准备情况评估**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**通过导入先前创建的功能发现报告来准备就绪评估**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**通过提供配置文件来定位准备情况评估**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

使用源连接时的配置文件内容:

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
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

导入功能发现报告时的配置文件内容:

```
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-databasemanaged-instance-sku-recommendations-using-the-cli"></a>使用 CLI 的 Azure SQL 数据库/托管实例 SKU 建议

这些命令支持 Azure SQL 数据库单一数据库和托管实例部署选项的建议。

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|参数  |描述  | 必需 (是/否)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | 使用 DMA 命令行执行 SKU 评估 | Y
|`/SkuRecommendationInputDataFilePath` | 从承载数据库的计算机收集到的性能计数器文件的完整路径 | Y
|`/SkuRecommendationTsvOutputResultsFilePath` | TSV 结果文件的完整路径 | Y <br> (需要 TSV 或 JSON 或 HTML 文件路径)
|`/SkuRecommendationJsonOutputResultsFilePath` | JSON 结果文件的完整路径 | Y <br> (需要 TSV 或 JSON 或 HTML 文件路径)
|`/SkuRecommendationHtmlResultsFilePath` | HTML 结果文件的完整路径 | Y <br> (需要 TSV 或 JSON 或 HTML 文件路径)
|`/SkuRecommendationPreventPriceRefresh` | 防止价格刷新发生。 如果在脱机模式下运行 (例如 true), 则使用。 | Y <br> (为静态价格选择此参数或需要选择以下所有参数以获取最新价格)
|`/SkuRecommendationCurrencyCode` | 显示价格的货币 (例如"USD") | Y <br> (适用于最新价格)
|`/SkuRecommendationOfferName` | 产品/服务名称 (例如"BC-OP-NT-AZR-MS-AZR-0003P")。 有关详细信息, 请参阅[Microsoft Azure 产品/服务详细](https://azure.microsoft.com/support/legal/offer-details/)信息页。 | Y <br> (适用于最新价格)
|`/SkuRecommendationRegionName` | 区域名称 (例如"WestUS") | Y <br> (适用于最新价格)
|`/SkuRecommendationSubscriptionId` | 订阅的 ID。 | Y <br> (适用于最新价格)
|`/SkuRecommendationDatabasesToRecommend` | 要为其建议的数据库的以空格分隔的列表 (例如"Database1" "Database2" "Database3")。 名称区分大小写, 必须用双引号括起来。 如果省略, 则提供所有数据库的建议。 | N
|`/AzureAuthenticationTenantId` | 身份验证租户。 | Y <br> (适用于最新价格)
|`/AzureAuthenticationClientId` | 用于身份验证的 AAD 应用的客户端 ID。 | Y <br> (适用于最新价格)
|`/AzureAuthenticationInteractiveAuthentication` | 设置为 true 可弹出窗口。 | Y <br> (适用于最新价格) <br>(选择3个身份验证选项中的一个选项-选项 1)
|`/AzureAuthenticationCertificateStoreLocation` | 设置为证书存储位置 (例如"CurrentUser")。 | Y <br>(适用于最新价格) <br> (选择3个身份验证选项之一-选项 2)
|`/AzureAuthenticationCertificateThumbprint` | 设置为证书指纹。 | Y <br> (适用于最新价格) <br>(选择3个身份验证选项之一-选项 2)
|`/AzureAuthenticationToken` | 设置为证书标记。 | Y <br> (适用于最新价格) <br>(选择3个身份验证选项之一-选项 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>使用 CLI 评估 SKU 的示例

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**带有价格刷新的 Azure SQL DB/MI SKU 建议 (获取最新价格)-交互式身份验证** 

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

**带有价格刷新的 Azure SQL DB/MI SKU 建议 (获取最新价格)-证书身份验证**

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

**Azure SQL DB SKU/MI 建议和价格刷新 (获取最新价格)-令牌身份验证并指定要建议的数据库**
  
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

**不使用价格刷新的 Azure SQL DB/MI SKU 建议 (使用静态价格)** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>请参阅
- [数据迁移助手](https://aka.ms/get-dma)下载。
- 本文介绍[适用于你的本地数据库的 AZURE SQL 数据库的正确 SKU](https://aka.ms/dma-sku-recommend-sqldb)。
