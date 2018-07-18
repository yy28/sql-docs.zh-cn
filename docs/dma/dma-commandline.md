---
title: 从命令行 (SQL Server) 中运行数据迁移助手 |Microsoft Docs
description: 了解如何从命令行来评估要迁移的 SQL Server 数据库运行数据迁移助手
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 6b364dc03d48cbc1c0487362712e10f7ab0b782e
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785458"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>从命令行运行数据迁移助手
版本 2.1 和更高版本，当你安装数据迁移助手，它还会安装在 dmacmd.exe *%programfiles%\\Microsoft Data Migration Assistant\\*。 Dmacmd.exe 用于评估在无人参与模式下，数据库，并输出到 JSON 或 CSV 文件的结果。 评估多个数据库或大型数据库时，此方法是特别有用。 

> [!NOTE]
> Dmacmd.exe 支持仅运行评估。 目前不支持迁移。


## <a name="command-line-arguments"></a>命令行参数

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
| `/help or /?`     | 如何使用 dmacmd.exe 帮助文本        | 否
|`/AssessmentName`     |   评估项目的名称   | 是
|`/AssessmentDatabases`     | 连接字符串的以空格分隔列表。 数据库名称 （初始目录） 是区分大小写。 | 是
|`/AssessmentTargetPlatform`     | 用于评估，支持的值的目标平台： SqlServer2012、 SqlServer2014、 SqlServer2016 和 AzureSqlDatabaseV12。 默认值是 SqlServer2016   | 否
|`/AssessmentEvaluateFeatureParity`  | 运行功能奇偶一致性规则  | 否
|`/AssessmentEvaluateCompatibilityIssues`     | 运行兼容性规则  | 是 <br> （AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations 是必需的。
|`/AssessmentEvaluateRecommendations`     | 运行功能推荐        | 是 <br> （AssessmentEvaluateCompatibilityIssues 或所需的 AssessmentEvaluateRecommendationsis）
|`/AssessmentOverwriteResult`     | 覆盖结果文件    | 否
|`/AssessmentResultJson`     | JSON 结果文件的完整路径     | 是 <br> （AssessmentResultJson 或 AssessmentResultCsv 是必需的）
|`/AssessmentResultCsv`    | CSV 结果文件的完整路径   | 是 <br>（AssessmentResultJson 或 AssessmentResultCsv 是必需的）




## <a name="examples"></a>示例

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



## <a name="see-also"></a>另请参阅

[数据迁移助手下载](https://www.microsoft.com/download/details.aspx?id=53595)
