---
title: 使用命令行工具开发面向项目的数据库
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9a26def9-8fbd-43e4-9e57-414840b73ed8
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 04/26/2017
ms.openlocfilehash: 321c0988603f7c31460d1c95791d57e5945c2b07
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75243749"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>使用命令行工具开发面向项目的数据库

SQL Server Data Tools 经证明是支持多种面向项目的数据库开发方案的命令行工具。  
  
## <a name="in-this-section"></a>本节内容  
  
|||  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage.md)|本主题介绍了用于以下任务的 SQLPackage.exe 实用工具：<br /><br />-   从活动的 SQL Server 数据库中提取 .dacpac 文件。<br />-   将 .dacpac 文件发布到活动的 SQL Server 数据库，以便增量更新活动数据库架构以匹配 .dacpac。<br />-   将 .dacpac 文件与活动的 SQL Server 数据库进行比较，并且在不更新活动数据库的情况下生成增量升级 Transact\-SQL 脚本。<br />-   将两个 .dacpac 文件进行比较以便生成增量升级 Transact\-SQL 脚本。<br />-   生成一个 XML 报表，该报表汇总了在增量升级数据库时将发生的增量升级更改。|  
|[将 MSDeploy 用于 dbSqlPackage 提供程序](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|本主题介绍名为 dbSqlPackage 的 [Web 部署工具](https://go.microsoft.com/fwlink/?LinkId=231798)提供程序，它随 SSDT 一起提供，与 Microsoft Internet Information Services (IIS) Web 部署工具 (MSDeploy.exe) 结合使用可执行以下任务：<br /><br />-   从远程/本地 SQL Server 或 SQL Azure 数据库中提取 .dacpac 文件。<br />-   将 .dacpac 发布到远程/本地 SQL Server 或 SQL Azure 数据库以对其进行增量升级。<br />-   从本地 SQL Server 数据库发布到远程 SQL Server 或 SQL Azure 数据库，以便增量升级远程数据库。<br />-   将 .dacpac 与远程/本地 SQL Server 或 SQL Azure 数据库进行比较，以便在不更新活动数据库的情况下生成增量升级 Transact\-SQL 脚本。<br />-   生成一个 XML 报表，该报表汇总了在增量升级数据库时将发生的增量升级更改。|  
  
## <a name="related-sections"></a>相关章节  
[面向项目的脱机数据库开发](../ssdt/project-oriented-offline-database-development.md)  
  
