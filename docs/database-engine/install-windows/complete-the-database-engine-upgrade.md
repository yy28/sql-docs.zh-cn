---
title: "完成数据库引擎升级 | Microsoft Docs"
ms.custom: ""
ms.date: "09/22/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: 10
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 10
---
# 完成数据库引擎升级
  升级到 SQL Server 2016 的过程完成后，还有一些可能需要完成的额外步骤。 其中包括：  
  
 升级 [!INCLUDE[ssDE](../../includes/ssde-md.md)]后，请完成以下任务：  
  
-   **备份你的数据库：** 为每个已升级的数据库执行完整备份。  
  
-   **启用新功能：**在 SQL Server 2016 中，一些更改仅在数据库的 DATABASE_COMPATIBILITY 级别更改为 130 后才可启用。  有关详细信息和建议工作流，请参阅 [更改数据库兼容性模式和使用 Query Store](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)。  
  
-   **Integration Services：**  
  
     将 Integration Services 包迁移到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 格式。 有关详细信息，请参阅 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
-   **Reporting Services：** 对于新安装升级，还原 Reporting Services 加密密匙。 有关详细信息，请参阅 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/back-up-and-restore-reporting-services-encryption-keys.md)。  
  
-   **Master Data Services：**  升级 MDS 数据库架构并创建 SQL Server 2016 Web 应用程序。 有关详细信息，请参阅 [Upgrade Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md)。  
  
-   **Data Quality Services：** 升级 DQS 数据库架构并验证 DQS 数据库架构升级。 有关详细信息，请参阅 [Upgrade Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)。  
  
-   **全文搜索：**重新填充全文目录以便确保查询结果中的语义一致性。 有关详细信息，请参阅[填充全文索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
## 本文是否对你有帮助？ 我们洗耳恭听  
 你正在查找哪些信息，是否已经找到？ 我们不断听取你的反馈来改进内容。 请将你的评论提交到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Complete%20the%20Database%20Engine%20Upgrade%20page)  
  
  