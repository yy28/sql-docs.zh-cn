---
title: "检查使用数据库邮件发送的电子邮件的状态 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "电子邮件 [SQL Server], 状态信息"
  - "邮件 [SQL Server], 状态信息"
  - "数据库邮件 [SQL Server], 消息状态"
  - "状态信息 [数据库邮件]"
ms.assetid: eb290f24-b52f-46bc-84eb-595afee6a5f3
caps.latest.revision: 30
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 30
---
# 检查使用数据库邮件发送的电子邮件的状态
  本主题说明在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 检查通过数据库邮件发送的电子邮件的状态。  
  
-   **开始之前：**  
  
-   **若要查看通过数据库邮件发送的电子邮件的状态，使用：** [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 数据库邮件保留发送的电子邮件的副本，并在 **msdb** 数据库的 **sysmail_allitems**、**sysmail_sentitems**、**sysmail_unsentitems**、**sysmail_faileditems** 视图中显示它们。 数据库邮件外部程序记录活动，并通过 Windows 应用程序事件日志以及 **msdb** 数据库的 **sysmail_event_log** 视图显示日志。 若要检查电子邮件的状态，请对此视图运行查询。 电子邮件可以处于下列四种可能的状态之一：**sent**、**unsent**、**retrying** 和 **failed**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **查看通过数据库邮件发送的电子邮件的状态**  
  
1.  从 **sysmail_allitems** 表中选择，按 **mailitem_id** 或 **sent_status** 指定要检查的邮件。  
  
2.  若要检查外部程序返回的电子邮件的状态，请将 **sysmail_allitems** 联接到 **sysmail_event_log** 视图中的 **mailitem_id** 列，如下所示。  
  
     默认情况下，外部程序不会记录有关发送成功的邮件的信息。 若要记录所有邮件，请使用 **“数据库邮件配置向导”** 的 **“配置系统参数”**页，将日志级别设置为“详细”。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 下面的示例列出了有关发送到 `danw` 的所有电子邮件（外部程序无法成功发送）的信息。 该语句列出了邮件的主题、外部程序发送邮件失败的日期和时间以及来自数据库邮件日志的错误消息。  
  
```  
USE msdb ;  
GO  
  
-- Show the subject, the time that the mail item row was last  
-- modified, and the log information.  
-- Join sysmail_faileditems to sysmail_event_log   
-- on the mailitem_id column.  
-- In the WHERE clause list items where danw was in the recipients,  
-- copy_recipients, or blind_copy_recipients.  
-- These are the items that would have been sent  
-- to danw.  
  
SELECT items.subject,  
    items.last_mod_date  
    ,l.description FROM dbo.sysmail_faileditems as items  
INNER JOIN dbo.sysmail_event_log AS l  
    ON items.mailitem_id = l.mailitem_id  
WHERE items.recipients LIKE '%danw%'    
    OR items.copy_recipients LIKE '%danw%'   
    OR items.blind_copy_recipients LIKE '%danw%'  
GO  
```  
  
## 另请参阅  
 [数据库邮件日志和审核](../../relational-databases/database-mail/database-mail-log-and-audits.md)  
  
  