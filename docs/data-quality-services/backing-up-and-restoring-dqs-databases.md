---
title: "备份和还原 DQS 数据库 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f3091f62-2234-4a80-a615-cf14c2a1da85
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 93aa4c5421406067d6ff97bc148ca5970d40bb4a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="backing-up-and-restoring-dqs-databases"></a>备份和还原 DQS 数据库
  本主题说明如何备份和还原 DQS 数据库。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   您必须知道或记住您在 DQS 服务器安装过程中提供的数据库主密钥的密码。  
  
-   确保 DQS 中没有正在运行的活动或过程。 这可以使用 **“活动监视”** 屏幕进行验证。 有关使用该屏幕的详细信息，请参阅 [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md)。  
  
-   确保没有用户已登录 DQS 服务器。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
  
-   您的 Windows 用户帐户必须为 SQL Server 实例中 sysadmin 固定服务器角色的成员，才能执行备份和还原操作。  
  
-   您必须具有 DQS_MAIN 数据库的 dqs_administrator 角色，才能终止 DQS 中任何正在运行的活动或停止任何正在运行的过程。  
  
##  <a name="BackupRestore"></a> 备份和还原 DQS 数据库  
  
1.  启动 Microsoft SQL Server Management Studio 并连接到适当的 SQL Server 实例。  
  
2.  在“对象资源管理器”中，展开 **“数据库”** 节点。  
  
3.  备份 DQS_STAGING_DATA 数据库。 有关备份 SQL Server 数据库的分步说明，请参阅[创建完整数据库备份 (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。  
  
4.  备份 DQS_PROJECTS 数据库。  
  
5.  备份 DQS_MAIN 数据库。  
  
6.  断开与当前 SQL Server 实例的连接，然后连接到要还原这些数据库的 SQL Server 实例。  
  
7.  还原 DQS_MAIN 数据库。 有关还原 SQL Server 数据库的分步说明，请参阅[使用 SSMS 还原数据库备份](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)。  
  
8.  还原 DQS_PROJECTS 数据库。  
  
9. 还原 DQS_STAGING_DATA 数据库。  
  
10. 在“对象资源管理器”中，右键单击服务器，再单击 **“新建查询”**。  
  
11. 在“查询编辑器”窗口中，复制以下 SQL 语句，然后将 \<PASSWORD> 替换为在 DQS 安装过程中为数据库主密钥提供的密码：  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    EXECUTE [internal_core].[RestoreDQDatabases] '<PASSWORD>'  
    GO  
  
    ```  
  
12. 按 F5 执行这些语句。 检查 **“结果”** 窗格以验证是否已成功执行这些语句。  
  
## <a name="see-also"></a>另请参阅  
 [管理 DQS 数据库](../data-quality-services/manage-dqs-databases.md)  
  
  
