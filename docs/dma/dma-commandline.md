---
title: 从命令行 (SQL Server 数据 Migration Assistant) 运行 |Microsoft 文档
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
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
ms.openlocfilehash: 084ab21808c1dca1e5a0276ca78e421ea283acaf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>从命令行运行数据迁移助手
版本 2.1 和更高版本，当你安装数据迁移助手，它还将安装在 dmacmd.exe *%programfiles%\\Microsoft 数据迁移助手\\*。 Dmacmd.exe 用于评估在无人参与模式下，数据库和输出结果发送到 JSON 或 CSV 文件。 评估多个数据库或大型数据库时，这是特别有用。 

> [!NOTE]
> Dmacmd.exe 支持运行仅评估。 这次不支持迁移。


## <a name="command-line-arguments"></a>命令行自变量

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```


|参数  |Description  | 必需 (Y/N)
|---------|---------|---------------|
| `/help or /?`     | 如何使用 dmacmd.exe 帮助文本        | 否
|`/AssessmentName`     |   评估项目的名称   | 是
|`/AssessmentDatabases`     | 用空格分隔的连接字符串的列表。 数据库名称 （初始目录） 是区分大小写。 | 是
|`/AssessmentTargetPlatform`     | 目标平台，用于评估，支持的值： SqlServer2012、 SqlServer2014、 SqlServer2016 和 AzureSqlDatabaseV12。 默认值是 SqlServer2016   | 否
|`/AssessmentEvaluateFeatureParity`  | 运行功能奇偶校验规则  | 否
|`/AssessmentEvaluateCompatibilityIssues`     | 运行兼容性规则  | 是 <br> （AssessmentEvaluateCompatibilityIssues 或 AssessmentEvaluateRecommendations 是必需的。）
|`/AssessmentEvaluateRecommendations`     | 运行功能建议        | 是 <br> （AssessmentEvaluateCompatibilityIssues 或所需的 AssessmentEvaluateRecommendationsis）
|`/AssessmentOverwriteResult`     | 覆盖结果文件    | 否
|`/AssessmentResultJson`     | 为 JSON 结果文件的完整路径     | 是 <br> （AssessmentResultJson 或 AssessmentResultCsv 是必需的）
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



**使用 SQL Server 身份验证和运行功能建议的单一数据库评估**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```


**单一数据库评估为 SQL Server 2012 的目标平台并保存结果保存到.json 和.csv 文件**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
```


**针对目标平台 SQL Azure 数据库的单一数据库评估将结果保存到.json 和.csv 文件**

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
