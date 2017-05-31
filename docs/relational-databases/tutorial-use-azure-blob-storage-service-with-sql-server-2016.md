---
title: "教程：将 Azure Blob 存储服务用于 SQL Server 2016 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4ae1e9aef727303d55c79463d822c4f62d3cdae0
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="tutorial-use-azure-blob-storage-service-with-sql-server-2016"></a>教程：将 Azure Blob 存储服务用于 SQL Server 2016
欢迎使用“Microsoft Azure Blob 存储服务中使用 SQL Server 2016”教程。 本教程有助于学习如何将 Microsoft Azure Blob 存储服务用于 SQL Server 数据文件和 SQL Server 备份。  
  
Microsoft Azure Blob 存储服务的 SQL Server 集成支持最初是 SQL Server 2012 Service Pack 1 CU2 的一项增强功能，现在已随 SQL Server 2014 和 SQL Server 2016 进一步增强。 有关该功能的概述以及使用该功能的好处，请参阅 [Microsoft Azure 中的 SQL Server 数据文件](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)。 有关实时演示，请参阅 [时间点还原的演示](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)。  
  
  
**下载**<br /><br />**>>**  若要下载 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]，请转到  **[评估中心](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**。<br /><br />**>>**  是否拥有 Azure 帐户？  然后转到 **[此处](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** ，以加速已安装有 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的虚拟机。  
  
## <a name="what-you-will-learn"></a>学习内容  
此教程通过多个课程说明如何在 Microsoft Azure Blob 存储服务中处理 SQL Server 数据文件。 每个课程专注于某个特定任务，应按顺序完成课程学习。 首先，将学习如何使用存储访问策略和共享访问签名在 Blob 存储中新建容器。 然后，学习如何创建 SQL Server 凭据，将 SQL Server 与 Azure Blob 存储集成。 接下来，将数据库备份到 Blob 存储，并将其还原到 Azure 虚拟机。 然后，使用 SQL Server 2016 文件快照事务日志备份还原到某个时间点和新的数据库。 最后，本教程会演示元数据系统存储过程和函数的使用方法，帮助了解和使用文件快照备份。  
  
本文假设存在以下条件：  
  
-   具有 SQL Server 2016 本地实例，并安装有 AdventureWorks2014 副本。  
  
-   具有 Azure 存储帐户。  
  
-   至少有一个安装有 SQL Server 2016 的 Azure 虚拟机，并依照[在 Azure 上设置 SQL Server 虚拟机](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-provision-sql-server/)对该虚拟机进行设置。 还可以选择对[第 8 课.从日志备份还原为新数据库](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)) 中的方案使用第二个虚拟机。  
  
本教程分为 9 课，必须按顺序完成课程学习：  
  
**[第 1 课：在 Azure 容器上创建存储访问策略和共享访问签名](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
在本课中，将在新的 Blob 容器上创建策略并生成创建 SQL Server 凭据所用的共享访问签名。  
  
**[第 2 课：使用共享访问签名创建 SQL Server 凭据](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
在本课中，将使用 SAS 密钥创建凭据，存储用于访问 Microsoft Azure 存储帐户的安全信息。  
  
**[第 3 课：将数据库备份到 URL](../relational-databases/lesson-3-database-backup-to-url.md)**  
在本课程中，将本地数据库备份到 Microsoft Azure Blob 存储。  
  
**[第 4 课：将数据库从 URL 还原到虚拟机](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
在本课程中，将数据库从 Microsoft Azure Blob 存储还原到 Azure 虚拟机。  
  
**[第 5 课：使用文件快照备份来备份数据库](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)**  
在本课程中，使用文件快照备份来备份数据库，并查看文件快照元数据。  
  
**[第 6 课：使用文件快照备份生成活动和备份日志](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
在本课程中，使用文件快照备份在数据库中生成活动并执行多个日志备份，并查看文件快照元数据。  
  
**[第 7 课：将数据库还原到时间点](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
在本课程中，使用两个文件快照日志备份将数据库还原到某时间点。  
  
**[第 8 课：从日志备份还原为新数据库](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)**  
在本课程中，从文件快照日志备份还原到不同虚拟机上的新数据库。  
  
**[第 9 课：管理备份集和文件快照备份](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)**  
在本课程中，删除不需要的备份集并了解如何删除孤立的文件快照备份（如有必要）。  
  
## <a name="did-this-article-help-you-were-listening"></a>本文是否对你有帮助？ 我们洗耳恭听  
你正在查找哪些信息，是否已经找到？ 我们不断听取你的反馈来改进内容。 请将你的评论提交到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases%20page)  
  
## <a name="see-also"></a>另请参阅  
[Microsoft Azure 中的 SQL Server 数据文件](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)  
[Azure 中的数据库文件的文件快照备份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[SQL Server 备份到 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
  


