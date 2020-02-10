---
title: 数据库邮件配置对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlimail.manageexistingaccount.f1
- sql12.swb.sqlimail.addaccounttoprofile.f1
- sql12.swb.sqlmailconfiguration.f1
- sql12.swb.sqlimail.profileandaccountmanagement.f1
- sql12.swb.sqlimail.manageprofilesecurity.principalview.f1
- sql12.swb.sqlimail.newsqlimailaccount.f1
- sql12.swb.sqlimail.configuresystem.f1
- sql12.swb.sqlimail.selectconfiguration.f1
- sql12.swb.sqlimail.newprofile.f1
- sql12.swb.sqlimail.manageexistingprofile.f1
- sql12.swb.sqlimail.welcome.f1
- sql12.swb.sqlimail.manageprofilesecurity.profileview.f1
- sql12.swb.sqlimail.completewizard.f1
- sql12.swb.sqlimail.newaccount.f1
helpviewer_keywords:
- Database Mail [SQL Server], configuration objects
- Database Mail [SQL Server], accounts
- configuration objects [Database Mail]
- Database Mail [SQL Server], profiles
- profiles [SQL Server], Database Mail
- accounts [Database Mail]
ms.assetid: 03f6e4c0-04ff-490a-bd91-637806215bd1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71a2805eb935088f39c6b4a86714f263dc5ba643
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62872427"
---
# <a name="database-mail-configuration-objects"></a>数据库邮件配置对象
  数据库邮件具有两种配置对象：数据库配置对象提供了一种方法，您可以使用此方法配置从数据库应用程序或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理发送电子邮件时数据库邮件应使用的设置。  
  
-   数据库邮件帐户  
  
-   数据库邮件配置文件  
  
  
##  <a name="VisualElement"></a>数据库邮件配置对象关系  
 图中显示了两个配置文件、三个帐户和三个用户。 用户 1 可以访问配置文件 1，该配置文件使用帐户 1 和帐户 2。 用户 3 可以访问配置文件 2，该配置文件使用帐户 2 和帐户 3。 用户 2 既可以访问配置文件 1，也可以访问配置文件 2。  
  
 ![用户、配置文件和帐户的关系](../../database-engine/media/databasemailprofileaccount.gif "用户、配置文件和帐户的关系")  
  
  
##  <a name="DBAccount"></a>数据库邮件帐户  
 数据库邮件帐户包含由 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于向 SMTP 服务器发送电子邮件的信息。 每个帐户均包含一个电子邮件服务器的信息。  
  
 数据库邮件与 SMTP 服务器进行通信时支持三种身份验证方法：  
  
-   Windows 身份验证：数据库邮件使用 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] Windows 服务帐户的凭据在 SMTP 服务器中进行身份验证。  
  
-   基本身份验证：数据库邮件使用指定的用户名和密码在 SMTP 服务器上进行身份验证。  
  
-   匿名身份验证：SMTP 服务器不要求进行任何身份验证。  数据库邮件将不使用任何凭据在 SMTP 服务器上进行身份验证。  
  
 帐户信息存储在 **msdb** 数据库中。 每个帐户包含以下信息：  
  
-   帐户名称。  
  
-   帐户的说明。  
  
-   帐户的电子邮件地址。  
  
-   帐户的显示名称。  
  
-   用作帐户的答复信息的电子邮件地址。  
  
-   电子邮件服务器的名称。  
  
-   电子邮件服务器的类型。 对于[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，这始终为简单邮件传输协议（SMTP）。  
  
-   电子邮件服务器的端口号。  
  
-   用于指示是否使用安全套接字层 (SSL) 与 SMTP 邮件服务器建立连接的位列。  
  
-   用于指示是否使用为 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]配置的凭据与 SMTP 服务器建立连接的位列。  
  
-   用于电子邮件服务器身份验证的用户名（如果电子邮件服务器需要身份验证）。  
  
-   用于电子邮件服务器身份验证的密码（如果电子邮件服务器需要身份验证）。  
  
 使用数据库邮件配置向导可以方便地创建和管理帐户。 还可以使用 **msdb** 中的配置存储过程来创建和管理帐户。  
  
  
##  <a name="DBProfile"></a>数据库邮件配置文件  
 数据库邮件配置文件是相关数据库邮件帐户的有序集合。 配置文件将由使用数据库邮件（而不是直接使用帐户）来发送电子邮件的应用程序指定。 将单个电子邮件服务器的信息与应用程序使用的对象分隔可以提高灵活性和可靠性：配置文件提供自动故障转移，因此如果一个电子邮件服务器停止响应，数据库邮件可以自动将邮件发送到另一个电子邮件服务器。 数据库管理员可以添加、删除或重新配置帐户，而不需要更改应用程序代码或作业步骤。  
  
 配置文件还有助于数据库管理员控制对电子邮件的访问。 若要发送数据库邮件，必须具有 **DatabaseMailUserRole** 中的成员身份。 配置文件使管理员可以更加灵活地控制谁来发送邮件以及使用哪些帐户。  
  
 配置文件可以是公共的，也可以是专用的。  
  
 **公共配置文件**可用于**Msdb**数据库中**DatabaseMailUserRole**数据库角色的所有成员。 它们允许 **DatabaseMailUserRole** 角色的所有成员使用该配置文件发送电子邮件。  
  
 **专用配置文件**为**msdb**数据库中的安全主体而定义。 它们仅允许指定的数据库用户、角色和 **sysadmin** 固定服务器角色的成员来使用该配置文件发送电子邮件。 默认情况下，配置文件是专用的，而且仅允许 **sysadmin** 固定服务器角色的成员访问。 若要使用专用配置文件， **sysadmin** 必须授予用户使用该配置文件的权限。 此外， **sp_send_dbmail** 存储过程的 EXECUTE 权限只授予 **DatabaseMailUserRole**成员。 系统管理员必须将用户添加到 **DatabaseMailUserRole** 数据库角色，该用户才能发送电子邮件。  
  
 在电子邮件服务器无法访问或无法处理邮件的情况下，配置文件可提高可靠性。 配置文件中的每个帐户都有一个序列号。 序列号可以确定数据库邮件使用配置文件中帐户的顺序。 对于新的电子邮件，数据库邮件将使用最后一个成功发送邮件的帐户；如果尚未发送邮件，则使用序列号最小的帐户。 如果该帐户失败，数据库邮件就使用具有下一个序列号较大的帐户，依此类推，直到数据库邮件成功发送邮件，或者序列号最大的帐户也失败为止。 如果序列号最大的帐户失败，数据库邮件将暂停尝试发送邮件，暂停时间在 **sysmail_configure_sp** 的 **AccountRetryDelay**参数中配置，然后从最小序列号再次开始尝试发送邮件的过程。 使用 **sysmail_configure_sp** 的 **AccountRetryAttempts**参数可以配置外部邮件进程尝试使用指定配置文件中的每个帐户发送电子邮件的次数。  
  
 如果存在具有相同序列号的多个帐户，则数据库邮件将仅使用其中一个帐户发送给定的电子邮件。 在此情况下，数据库邮件不能保证使用具有该序列号的特定帐户，也不能保证使用同一个帐户发送各个邮件。  
  
  
##  <a name="RelatedTasks"></a>数据库邮件配置任务  
 下表介绍了数据库邮件配置任务。  
  
|配置任务|主题链接|  
|------------------------|----------------|  
|介绍如何创建数据库邮件帐户|[创建数据库邮件帐户](create-a-database-mail-account.md)|  
|介绍如何创建数据库邮件配置文件|[创建数据库邮件配置文件](create-a-database-mail-profile.md)|  
|介绍如何配置数据库邮件|[配置数据库邮件](configure-database-mail.md)|  
|介绍如何使用模板创建数据库邮件配置脚本||  
  
  
##  <a name="Add_Tasks"></a>其他数据库配置任务（系统存储过程）  
 数据库邮件配置存储过程位于 **msdb** 数据库中。  
  
 以下几个表列出了用于配置和管理数据库邮件的存储过程。  
  
### <a name="database-mail-settings"></a>数据库邮件设置  
  
|名称|说明|  
|----------|-----------------|  
|[sysmail_configure_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql)|更改数据库邮件的配置设置。|  
|[sysmail_help_configure_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql)|显示数据库邮件的配置设置。|  
  
### <a name="accounts-and-profiles"></a>帐户和配置文件  
  
|名称|说明|  
|----------|-----------------|  
|[sysmail_add_profileaccount_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql)|将邮件帐户添加到数据库邮件配置文件中。|  
|[sysmail_delete_account_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-delete-account-sp-transact-sql)|删除数据库邮件帐户。|  
|[sysmail_delete_profile_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-delete-profile-sp-transact-sql)|删除数据库邮件配置文件。|  
|[sysmail_delete_profileaccount_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-delete-profileaccount-sp-transact-sql)|从数据库邮件配置文件中删除帐户。|  
|[sysmail_help_account_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-help-account-sp-transact-sql)|列出有关数据库邮件帐户的信息。|  
|[sysmail_help_profile_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-help-profile-sp-transact-sql)|列出有关一个或多个数据库邮件配置文件的信息。|  
|[sysmail_help_profileaccount_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-help-profileaccount-sp-transact-sql)|列出与一个或多个数据库邮件配置文件相关联的帐户。|  
|[sysmail_update_account_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-update-account-sp-transact-sql)|更新现有数据库邮件帐户中的信息。|  
|[sysmail_update_profile_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-update-profile-sp-transact-sql)|更改数据库邮件配置文件的说明或名称。|  
|[sysmail_update_profileaccount_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql)|更新数据库邮件配置文件中帐户的序列号。|  
  
### <a name="security"></a>安全性  
  
|名称|说明|  
|----------|-----------------|  
|[sysmail_add_principalprofile_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql)|授予数据库主体使用数据库邮件配置文件的权限。|  
|[sysmail_delete_principalprofile_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-delete-principalprofile-sp-transact-sql)|删除数据库用户使用公共或专用数据库邮件配置文件的权限。|  
|[sysmail_help_principalprofile_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql)|列出所给数据库用户的数据库邮件配置文件信息。|  
|[sysmail_update_principalprofile_sp （Transact-sql）](/sql/relational-databases/system-stored-procedures/sysmail-update-principalprofile-sp-transact-sql)|更新所给数据库用户的权限信息。|  
  
### <a name="system-state"></a>系统状态  
  
|名称|说明|  
|----------|-----------------|  
|[sysmail_start_sp &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql)|启动数据库邮件外部程序和关联的 SQL Service Broker 队列。|  
|[sysmail_stop_sp &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql)|停止数据库邮件外部程序和关联的 SQL Service Broker 队列。|  
|[sysmail_help_status_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql)|指示数据库邮件是否已启动。|  
  
##  <a name="RelatedContent"></a>其他参考  
  
-   [数据库邮件日志和审核](database-mail-log-and-audits.md)  
  
  
  
