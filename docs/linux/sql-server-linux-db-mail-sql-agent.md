---
title: "数据库邮件和电子邮件警报使用 Linux 上的 SQL 代理 |Microsoft 文档"
description: "本文介绍如何在 Linux 上的 SQL 服务器上使用数据库邮件和电子邮件警报"
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: tbd
ms.workload: Inactive
ms.openlocfilehash: d5d9dd84a7c3489c96e4e1aeaeb6d0928140a83f
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="db-mail-and-email-alerts-with-sql-agent-on-linux"></a>数据库邮件和 Linux 上的 SQL 代理的电子邮件警报

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

以下步骤演示如何设置数据库邮件并将其用于 SQL Server 代理 (**mssql server 代理**) 在 Linux 上。 

> [!NOTE]
> 若要在 Linux 上的 SQL 服务器上使用数据库邮件，你需要使用 SQL Server 自 2017 年 1 RC1 或更高版本。

## <a name="prerequisites"></a>必要條件

- SQL Server 自 2017 年 1 RC1 和更高版本
- SQL Server 代理 v14.0.800.90 2 及更高版本 （如果你打算使用警报的电子邮件）

## <a name="1-enable-db-mail"></a>1.启用数据库邮件

```sql
USE master 
GO 
sp_configure 'show advanced options',1 
GO 
RECONFIGURE WITH OVERRIDE 
GO 
sp_configure 'Database Mail XPs', 1 
GO 
RECONFIGURE  
GO  
```

## <a name="2-create-a-new-account"></a>2.创建新帐户
```sql
EXECUTE msdb.dbo.sysmail_add_account_sp 
@account_name = 'SQLAlerts', 
@description = 'Account for Automated DBA Notifications', 
@email_address = 'sqlagenttest@gmail.com', 
@replyto_address = 'sqlagenttest@gmail.com', 
@display_name = 'SQL Agent', 
@mailserver_name = 'smtp.gmail.com', 
@port = 587, 
@enable_ssl = 1, 
@username = 'sqlagenttest@gmail.com', 
@password = '<password>' 
GO
```

## <a name="3-create-a-default-profile"></a>3.创建默认配置文件

```sql
EXECUTE msdb.dbo.sysmail_add_profile_sp 
@profile_name = 'default', 
@description = 'Profile for sending Automated DBA Notifications' 
GO
```

## <a name="4-add-the-database-mail-account-to-a-database-mail-profile"></a>4.将数据库邮件帐户添加到数据库邮件配置文件
```sql
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp 
@profile_name = 'default', 
@principal_name = 'public', 
@is_default = 1 ; 
 ```
 
## <a name="5-add-account-to-profile"></a>5.将帐户添加到配置文件 
```sql
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp   
@profile_name = 'default',   
@account_name = 'SQLAlerts',   
@sequence_number = 1;  
 ```
 
## <a name="6-send-test-email"></a>6.发送测试电子邮件
> [!NOTE]
> 你可能需要转到你的电子邮件客户端并启用"允许安全级别较低客户端发送邮件。" 并非所有客户端将数据库邮件识别为电子邮件守护程序。

```
EXECUTE msdb.dbo.sp_send_dbmail 
@profile_name = 'default', 
@recipients = 'recipient-email@gmail.com', 
@Subject = 'Testing DBMail', 
@Body = 'This message is a test for DBMail' 
GO
```

## <a name="7-set-db-mail-profile-using-mssql-conf-or-environment-variable"></a>7.设置数据库邮件配置文件使用 mssql conf 或环境变量
你可以使用 mssql conf 实用程序或环境变量注册你的数据库邮件配置文件。 在这种情况下，让我们调用我们的配置文件默认。

```bash
# via mssql-conf
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile default
# via environment variable
MSSQL_AGENT_EMAIL_PROFILE=default
```

## <a name="8-set-up-an-operator-for-sqlagent-job-notifications"></a>8.设置 SQLAgent 作业通知的运算符 

```sql
EXEC msdb.dbo.sp_add_operator 
@name=N'JobAdmins',  
@enabled=1, 
@email_address=N'recipient-email@gmail.com',  
@category_name=N'[Uncategorized]' 
GO 
```

## <a name="9-send-email-when-agent-test-job-succeeds"></a>9.代理测试作业成功时发送电子邮件 

```
EXEC msdb.dbo.sp_update_job 
@job_name='Agent Test Job', 
@notify_level_email=1, 
@notify_email_operator_name=N'JobAdmins' 
GO
```

## <a name="next-steps"></a>后续步骤
有关如何使用 SQL Server 代理来创建、 计划和运行作业的详细信息，请参阅[在 Linux 上运行的 SQL Server 代理作业](sql-server-linux-run-sql-server-agent-job.md)。
