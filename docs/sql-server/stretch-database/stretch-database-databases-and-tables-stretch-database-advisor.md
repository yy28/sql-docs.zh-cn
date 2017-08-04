---
title: "Stretch Database 的数据库和表 - Stretch Database 顾问 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, identifying databases
- Stretch Database, identifying tables
- identifying databases for Stretch Database
- identifying tables for Stretch Database
ms.assetid: 81bd93d8-eef8-4572-88d7-5c37ab5ac2bf
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 59608301d353d99eb710a956389fd9f8d8948dfe
ms.contentlocale: zh-cn
ms.lasthandoff: 07/29/2017

---
# <a name="stretch-database-databases-and-tables---stretch-database-advisor"></a>Stretch Database 的数据库和表 - Stretch Database 顾问
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  为标识 Stretch Database 的数据库和表的候选项，请下载 SQL Server 2016 升级顾问并运行 Stretch Database 顾问。 Stretch Database 顾问也能标识阻止问题。  
  
## <a name="download-and-install-upgrade-advisor"></a>下载和安装升级顾问  
 下载和安装升级顾问请单击 [此处](https://www.microsoft.com/en-us/download/details.aspx?id=53595)。 此工具不包含在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 安装介质中。  
  
## <a name="run-the-stretch-database-advisor"></a>运行 Stretch Database 顾问  
  
1.  运行升级顾问。  
  
2.  选择“方案” ，然后选择“运行 STRETCH DATABASE 顾问” 。  
  
3.  在“运行 Stretch Database 顾问”  边栏选项卡上，单击“选择要分析的数据库” 。  
  
4.  在“选择数据库”边栏选项卡，输入或选择服务器名称和身份验证信息。 单击 **“连接”**。

5.  将显示所选服务器上的数据库列表。 选择要分析的数据库。 然后单击“选择”。  
  
6.  在“运行 Stretch Database 顾问”  边栏选项卡上，单击“运行” 。  将运行分析。  
  
## <a name="review-the-results"></a>查看结果  
  
1.  分析完成后，在“已分析数据库”边栏选项卡上，选择一个已分析过的数据库以显示“分析结果”边栏选项卡。  
  
     “分析结果”  边栏选项卡在选定的数据库中列出了与默认推荐条件匹配的推荐表。 
  
2.  在“分析结果”边栏选项卡上的表列表中，选择一个推荐的表以显示“表结果”边栏选项卡。  
  
     “表结果”边栏选项卡将列出所选表的阻止问题（若有）。 有关 Stretch Database 顾问检测到的阻止问题的更多信息，请参阅 [Stretch Database 的限制](../../sql-server/stretch-database/limitations-for-stretch-database.md)。  
  
3.  在“表结果”边栏选项卡上的阻止问题列表中，选择其中一个问题并展示有关所选问题的详细信息以及提出缓解步骤。 如果你想将对 Stretch Database 配置所选的表，则执行建议的缓解步骤。  
  
## <a name="next-step"></a>下一步  
 启用 Stretch Database。  
  
-   要在 **数据库**上启用 Stretch Database，请参阅 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)。  
  
-   当 Stretch 已在数据库上启用时，要在另一个 **表**上启用 Stretch Database，请参阅 [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)。 
  
## <a name="see-also"></a>另请参阅  
 [Stretch Database 的限制](../../sql-server/stretch-database/limitations-for-stretch-database.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [为表启用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  

