---
title: 向日志传送配置添加辅助数据库 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- adding secondary databases
- secondary databases [SQL Server], in log shipping
- secondary data files [SQL Server], adding
- log shipping [SQL Server], secondary databases
ms.assetid: b02eba13-f8e6-4684-b7e4-75ea038ea473
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 22f1fbc9470eb4002bb40f0e4e513f35134c442e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62774331"
---
# <a name="add-a-secondary-database-to-a-log-shipping-configuration-sql-server"></a>向日志传送配置添加辅助数据库 (SQL Server)
  此主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中向现有的日志传送配置添加辅助数据库。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要添加日志传送辅助数据库，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 日志传送存储过程要求 **sysadmin** 固定服务器角色中的成员身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-add-a-log-shipping-secondary-database"></a>添加日志传送辅助数据库  
  
1.  右键单击要在日志传送配置中用作主数据库的数据库，然后单击“属性”。  
  
2.  在 **“选择页”** 下，单击 **“事务日志传送”**。  
  
3.  在 **“辅助服务器实例和数据库”** 下，单击 **“添加”**。  
  
4.  单击 **“连接”** ，连接到要用作辅助服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
5.  在 **“辅助数据库”** 框中，从列表中选择一个数据库或键入要创建的数据库的名称。  
  
6.  在 **“初始化辅助数据库”** 选项卡上，选择要用于初始化辅助数据库的选项。  
  
7.  在 **“复制文件”** 选项卡的 **“复制文件的目标文件夹”** 框中，键入应将事务日志备份复制到的文件夹的路径。 该文件夹通常位于辅助服务器上。  
  
8.  请注意 **“复制作业”** 下的 **“计划”** 框中列出的复制计划。 如果要自定义安装计划，请单击 **“计划”** ，然后根据需要调整 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理计划。 此计划应为大致的备份计划。  
  
9. 在 **“还原”** 选项卡上的 **“还原备份时的数据库状态”** 下，选择 **“无恢复模式”** 或 **“备用模式”** 选项。  
  
10. 如果选择了 **“备用模式”** 选项，请选择是否要在进行还原操作时从辅助数据库断开用户连接。  
  
11. 如果希望延迟辅助服务器上的还原进程，请在 **“延迟还原备份操作至少”** 下选择延迟时间。  
  
12. 在 **“在以下时间内没有执行还原时报警”** 下选择警报阈值。  
  
13. 请注意 **“还原作业”** 下 **“计划”** 框中列出的还原计划。 如果要自定义安装计划，请单击 **“计划”** ，然后根据需要调整 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理计划。 此计划应为大致的备份计划。  
  
14. 单击 **“确定”** 中向现有的日志传送配置添加辅助数据库。  
  
15. 在“数据库属性”对话框上单击 **“确定”** ，以开始配置过程。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-add-a-log-shipping-secondary-database"></a>添加日志传送辅助数据库  
  
1.  在辅助服务器上，执行 [sp_add_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql) ，提供主服务器和数据库的详细信息。 此存储过程返回辅助 ID 以及复制和还原作业 ID。  
  
2.  在辅助服务器上，执行 [sp_add_jobschedule](/sql/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql) 以设置复制和还原作业的计划。  
  
3.  在辅助服务器上，执行 [sp_add_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql) 以添加辅助数据库。  
  
4.  在主服务器上，执行 [sp_add_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql) 向主服务器添加有关新辅助数据库的必需信息。  
  
5.  在辅助服务器上，启用复制和还原作业。 有关详细信息，请参阅 [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [日志传送升级到 SQL Server 2014 &#40;Transact SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [配置日志传送 (SQL Server)](configure-log-shipping-sql-server.md)  
  
-   [从日志传送配置中删除辅助数据库 (SQL Server)](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [删除日志传送 (SQL Server)](remove-log-shipping-sql-server.md)  
  
-   [查看日志传送报告 (SQL Server Management Studio)](view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [监视日志传送 (Transact-SQL)](monitor-log-shipping-transact-sql.md)  
  
-   [故障转移到日志传送辅助服务器 (SQL Server)](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [关于日志传送 (SQL Server)](about-log-shipping-sql-server.md)   
 [日志传送表和存储过程](log-shipping-tables-and-stored-procedures.md)  
  
  
