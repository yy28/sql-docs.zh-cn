---
title: "通过运行 Stretch Database 顾问标识适用于 Stretch Database 的数据库以及表 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Stretch Database, 标识数据库"
  - "Stretch Database, 标识表"
  - "为 Stretch Database 标识数据库"
  - "为 Stretch Database 标识表"
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# 通过运行 Stretch Database 顾问标识适用于 Stretch Database 的数据库以及表
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  为标识 Stretch Database 的数据库和表的候选项，请下载 SQL Server 2016 升级顾问并运行 Stretch Database 顾问。 Stretch Database 顾问也能标识阻止问题。  
  
## 下载和安装升级顾问  
 下载和安装升级顾问请单击 [此处](http://go.microsoft.com/fwlink/?LinkID=613421)。 此工具不包含在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 安装介质中。  
  
## 运行 Stretch Database 顾问  
  
1.  运行升级顾问。  
  
2.  选择“方案” ，然后选择“运行 STRETCH DATABASE 顾问” 。  
  
3.  在“运行 Stretch Database 顾问”  边栏选项卡上，单击“选择要分析的数据库” 。  
  
4.  在“选择数据库”边栏选项卡，输入或选择服务器名称和身份验证信息。 单击 **“连接”**。

5.  将显示所选服务器上的数据库列表。 选择要分析的数据库。 然后单击“选择”。  
  
6.  在“运行 Stretch Database 顾问”  边栏选项卡上，单击“运行” 。  将运行分析。  
  
## 查看结果  
  
1.  分析完成后，在“已分析数据库”边栏选项卡上，选择一个已分析过的数据库以显示“分析结果”边栏选项卡。  
  
     “分析结果”  边栏选项卡在选定的数据库中列出了与默认推荐条件匹配的推荐表。 
  
2.  在“分析结果”边栏选项卡上的表列表中，选择一个推荐的表以显示“表结果”边栏选项卡。  
  
     “表结果”边栏选项卡将列出所选表的阻止问题（若有）。 有关 Stretch Database 顾问检测到的阻止问题的更多信息，请参阅 [Stretch Database 的限制](../../sql-server/stretch-database/limitations-for-stretch-database.md)。  
  
3.  在“表结果”边栏选项卡上的阻止问题列表中，选择其中一个问题并展示有关所选问题的详细信息以及提出缓解步骤。 如果你想将对 Stretch Database 配置所选的表，则执行建议的缓解步骤。  
  
## 下一步  
 启用 Stretch Database。  
  
-   要在 **数据库**上启用 Stretch Database，请参阅 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)。  
  
-   当 Stretch 已在数据库上启用时，要在另一个 **表**上启用 Stretch Database，请参阅 [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)。  
  
## 另请参阅  
 [Stretch Database 的限制](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [为数据库启用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [为表启用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  