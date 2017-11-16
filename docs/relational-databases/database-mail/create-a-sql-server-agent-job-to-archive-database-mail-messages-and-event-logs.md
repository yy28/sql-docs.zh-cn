---
title: "创建 SQL Server 代理作业以存档数据库邮件和事件日志 | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- archiving mail messages and attachments [SQL Server]
- removing mail messages and attachements
- Database Mail [SQL Server], archiving
- saving mail messages and attachments
ms.assetid: 8f8f0fba-f750-4533-9b76-a9cdbcdc3b14
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cace8601462fd2469d7cdbfb4cce168111d42d07
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs"></a>创建 SQL Server 代理作业以存档数据库邮件和事件日志
  数据库邮件及其附件的副本与数据库邮件事件日志一起保存在 **msdb** 表中。 您可能希望定期减小这些表的大小并对不再需要的邮件和事件进行存档。 下列过程将创建一个 SQL Server 代理作业，以自动完成上述过程。  
  
-   **开始之前：**[先决条件](#Prerequisites)、[建议](#Recommendations)、[权限](#Permissions)  
  
-   **To Archive Database Mail messages and logs using :**  [SQL Server Agent](#Process_Overview)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 用于存储存档数据的新表可以位于特殊的存档数据库中。 另外，还可将行导出到文本文件中。  
   
###  <a name="Recommendations"></a> 建议  
 在生产环境中，可能需要进一步添加错误检查，并在作业失败的情况下向操作员发送电子邮件。  
  
  
###  <a name="Permissions"></a> Permissions  
 只有 **sysadmin** 固定服务器角色的成员才能执行本主题中介绍的存储过程。  
  
  
###  <a name="Process_Overview"></a> 过程概述  
  
-   第一个过程创建一个名为“存档数据库邮件”的作业，其中包含下列步骤。  
  
    1.  将所有邮件从数据库邮件表中复制到一个格式为 **DBMailArchive_***<year_month>* 且用上一个月份命名的新表中。  
  
    2.  将与第一个步骤中复制的邮件相关的附件从数据库邮件表中复制到格式为 **DBMailArchive_Attachments_**<year_month> 且用上一个月份命名的新表中。  
  
    3.  将数据库邮件事件日志中与第一个步骤中复制的邮件相关的事件从数据库邮件表中复制到格式为 **DBMailArchive_Log_**<year_month> 且用上一个月份命名的新表中。  
  
    4.  从数据库邮件表中删除已传输邮件项的记录。  
  
    5.  从数据库邮件事件日志中删除与已传输邮件项相关的事件。  
  
-   安排定期运行作业。  
  
  
## <a name="to-create-a-sql-server-agent-job"></a>创建 SQL Server 代理作业  
  
1.  在对象资源管理器中，展开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理，右键单击“作业”，然后单击“新建作业”。  
  
2.  在 **“新建作业”** 对话框的 **“名称”** 框中，键入 **“存档数据库邮件”**。  
  
3.  在 **“所有者”** 框中，确定所有者是 **sysadmin** 固定服务器角色的成员。  
  
4.  在 **“类别”** 框中，单击 **“数据库维护”**。  
  
5.  在 **“说明”** 框中，键入 **“存档数据库邮件”**，然后单击 **“步骤”**。  
  
 [概述](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-messages"></a>创建步骤以存档数据库邮件  
  
1.  在 **“步骤”** 页上，单击 **“新建”**。  
  
2.  在 **“步骤名称”** 框中，键入 **“复制数据库邮件项”**。  
  
3.  在“类型”框中，选择“Transact-SQL 脚本 (T-SQL)”。  
  
4.  在 **“数据库”** 框中，选择 **msdb**。  
  
5.  在 **“命令”** 框中，键入以下语句以创建用上一个月份命名的表，在其中包含早于当前月份的开始日期的行：  
  
    ```tsql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_' + @LastMonth + '] FROM sysmail_allitems WHERE send_request_date < ''' + @CopyDate +'''';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  单击 **“确定”** 保存步骤。  
  
 [概述](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-attachments"></a>创建步骤以存档数据库邮件附件  
  
1.  在 **“步骤”** 页上，单击 **“新建”**。  
  
2.  在 **“步骤名称”** 框中，键入 **“复制数据库邮件附件”**。  
  
3.  在“类型”框中，选择“Transact-SQL 脚本 (T-SQL)”。  
  
4.  在 **“数据库”** 框中，选择 **msdb**。  
  
5.  在 **“命令”** 框中，键入以下语句以创建用上一个月份命名的附件表，在其中包含与上一步中转移的邮件相对应的附件：  
  
    ```tsql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Attachments_' + @LastMonth + '] FROM sysmail_attachments   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  单击 **“确定”** 保存步骤。  
  
 [概述](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-log"></a>创建步骤以存档数据库邮件日志  
  
1.  在 **“步骤”** 页上，单击 **“新建”**。  
  
2.  在 **“步骤名称”** 框中，键入 **“复制数据库邮件日志”**。  
  
3.  在“类型”框中，选择“Transact-SQL 脚本 (T-SQL)”。  
  
4.  在 **“数据库”** 框中，选择 **msdb**。  
  
5.  在 **“命令”** 框中，键入以下语句以创建用上一个月份命名的日志表，在其中包含与在前面的步骤中传输的邮件相对应的日志项：  
  
    ```tsql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Log_' + @LastMonth + '] FROM sysmail_Event_Log   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  单击 **“确定”** 保存步骤。  
  
 [概述](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-rows-from-database-mail"></a>创建步骤以从数据库邮件中删除已存档的行  
  
1.  在 **“步骤”** 页上，单击 **“新建”**。  
  
2.  在 **“步骤名称”** 框中，键入 **“从数据库邮件中删除行”**。  
  
3.  在“类型”框中，选择“Transact-SQL 脚本 (T-SQL)”。  
  
4.  在 **“数据库”** 框中，选择 **msdb**。  
  
5.  在 **“命令”** 框中，键入以下语句以从数据库邮件表中删除早于当前月份的行：  
  
    ```tsql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @CopyDate ;  
    ```  
  
6.  单击 **“确定”** 保存步骤。  
  
 [概述](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-items-from-database-mail-event-log"></a>创建步骤以从数据库邮件事件日志中删除已存档的项  
  
1.  在 **“步骤”** 页上，单击 **“新建”**。  
  
2.  在 **“步骤名称”** 框中，键入 **“从数据库邮件事件日志中删除行”**。  
  
3.  在“类型”框中，选择“Transact-SQL 脚本 (T-SQL)”。  
  
4.  在 **“命令”** 框中，键入以下语句以从数据库邮件事件日志中删除早于当前月份的行：  
  
    ```tsql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_log_sp @logged_before = @CopyDate ;  
    ```  
  
5.  单击 **“确定”** 保存步骤。  
  
 [概述](#Process_Overview)  
  
## <a name="to-schedule-the-job-to-run-periodically"></a>安排定期运行作业  
  
1.  在 **“新建作业”** 对话框中，单击 **“计划”**。  
  
2.  在 **“计划”** 页上，单击 **“新建”**。  
  
3.  在 **“名称”** 框中，键入 **“存档数据库邮件”**。  
  
4.  在 **“计划类型”** 框中，选择 **“重复执行”**。  
  
5.  在 **“频率”** 区域中，选择相应的选项以便定期运行该作业，比如每月一次。  
  
6.  在“每天频率”区域中，选择“在 \<时间> 执行一次”。  
  
7.  验证其他选项已按您希望的那样进行了配置，然后单击 **“确定”** 保存计划。  
  
8.  单击 **“确定”** 保存作业。  
  
 [概述](#Process_Overview)  
  
  
