---
title: "通过 FTP 传递快照 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照 [SQL Server 复制], FTP 快照"
  - "FTP 快照 [SQL Server 复制]"
  - "快照复制 [SQL Server], FTP"
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# 通过 FTP 传递快照
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中通过 FTP 传递快照。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **通过 FTP 传递快照，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用请求订阅，您必须指定一个共享的目录作为通用命名约定 (UNC) 路径，如 \\\ftpserver\home\snapshots。 有关详细信息，请参阅 [保护快照文件夹的安全](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   若要通过文件传输协议 (FTP) 传输快照文件，必须先配置一个 FTP 服务器。 有关详细信息，请参阅 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) 文档。  
  
###  <a name="Security"></a> 安全性  
 为了帮助改进安全性，建议您在通过 Internet 使用 FTP 快照传递时实现虚拟专用网络 (VPN)。 有关详细信息，请参阅 [发布数据通过 Internet 使用 VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md)。  
  
 出于安全考虑，最好不允许匿名登录 FTP 服务器。 快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用请求订阅，您必须指定一个共享的目录作为通用命名约定 (UNC) 路径，如 \\\ftpserver\home\snapshots。 有关详细信息，请参阅 [保护快照文件夹的安全](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
 如果可能，请在运行时提示用户输入其凭据。 如果将凭据存储在脚本文件中，则必须确保此文件的安全。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 配置 FTP 服务器后，指定在该服务器的目录和安全信息 **发布属性 \< 出版物>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 指定 FTP 信息  
  
1.  在 **发布属性-\< 发布>** 对话框中，选择 **允许订阅服务器下载快照文件使用 FTP** 从以下页面之一︰  
  
    -    **“FTP 快照”** 页，用于快照发布和事务发布以及运行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]之前版本的发布服务器的合并发布。  
  
    -   **“FTP 快照和 Internet”** 页，用于运行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本的发布服务器的合并发布。  
  
2.  为 **“FTP 服务器名称”**、 **“端口号”**、 **“从 FTP 根文件夹开始的路径”**、 **“登录名”**和 **“密码”**指定值。  
  
     例如，如果 FTP 服务器根目录是 \\\ftpserver\home，而您希望将快照存储在 \\\ftpserver\home\snapshots，指定属性的 \snapshots\ftp **从 FTP 根文件夹的路径** （复制 ' 将 ftp 追加到快照文件夹路径时创建快照文件）。  
  
3.  指定快照代理应将快照文件写入在步骤 2 中指定的目录。 例如，若要有快照代理编写将快照文件传递到 \\\ftpserver\home\snapshots\ftp，必须指定的路径 \\\ftpserver\home\snapshots 在两个位置之一︰  
  
    -   与发布关联的分发服务器的默认快照位置。  
  
         有关指定默认快照位置的详细信息，请参阅 [指定默认快照位置 & #40;SQL Server Management Studio & #41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)。  
  
    -   发布的备用快照文件夹位置。 如果压缩快照，则需要指定备用位置。  
  
         输入中的路径 **将文件放入下列文件夹** 的快照页上的文本框中 **发布属性-\< 发布>** 对话框。 有关备用快照文件夹位置的详细信息，请参阅 [Alternate Snapshot Folder Locations](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 通过使用复制存储过程，可以按编程方式设置在 FTP 服务器上提供快照文件的选项以及修改这些 FTP 设置。 所用的过程由发布的类型决定。 FTP 快照传递仅可同请求订阅一起使用。  
  
#### 为快照发布或事务发布启用 FTP 快照传递  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 指定 **@publication**, ，值为 **true** 为 **@enabled_for_internet**, ，并将相应的以下参数的值︰  
  
    -   **@ftp_address** -用于传递快照的 FTP 服务器的地址。  
  
    -   （可选） **@ftp_port** -FTP 服务器所使用的端口。  
  
    -   （可选） **@ftp_subdirectory** -分配给 FTP 登录名的默认 FTP 目录的子目录。 例如，如果 FTP 服务器根目录是 \\\ftpserver\home，而您希望将快照存储在 \\\ftpserver\home\snapshots，指定 **\snapshots\ftp** 为 **@ftp_subdirectory** （复制 ' 将 ftp 追加到快照文件夹路径时创建快照文件）。  
  
    -   （可选） **@ftp_login** -连接到 FTP 服务器时使用的登录帐户。  
  
    -   （可选） **@ftp_password** -FTP 登录名的密码。  
  
     此操作将创建一个使用 FTP 的发布。 有关详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 为合并发布启用 FTP 快照传递  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定 **@publication**, ，值为 **true** 为 **@enabled_for_internet** 并将相应的以下参数的值︰  
  
    -   **@ftp_address** -用于传递快照的 FTP 服务器的地址。  
  
    -   （可选） **@ftp_port** -FTP 服务器所使用的端口。  
  
    -   （可选） **@ftp_subdirectory** -分配给 FTP 登录名的默认 FTP 目录的子目录。 例如，如果 FTP 服务器根目录是 \\\ftpserver\home，而您希望将快照存储在 \\\ftpserver\home\snapshots，指定 **\snapshots\ftp** 为 **@ftp_subdirectory** （复制 ' 将 ftp 追加到快照文件夹路径时创建快照文件）。  
  
    -   （可选） **@ftp_login** -连接到 FTP 服务器时使用的登录帐户。  
  
    -   （可选） **@ftp_password** -FTP 登录名的密码。  
  
     此操作将创建一个使用 FTP 的发布。 有关详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 创建对使用 FTP 快照传递的快照发布或事务发布的请求订阅  
  
1.  在订阅服务器上的订阅数据库上，执行 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)。 指定 **@publisher** 和 **@publication**。  
  
    -   在订阅服务器上的订阅数据库上，执行 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, 、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 分发代理在订阅服务器上运行的 Windows 凭据 **@job_login** 和 **@job_password**, ，且值为 **true** 为 **@use_ftp**。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 以注册请求订阅。 有关详细信息，请参阅 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
#### 创建对使用 FTP 快照传递的合并发布的请求订阅  
  
1.  在订阅服务器上的订阅数据库上，执行 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 指定 **@publisher** 和 **@publication**。  
  
2.  在订阅服务器上的订阅数据库上，执行 [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，分发代理在订阅服务器上运行的 Windows 凭据 **@job_login** 和 **@job_password**, ，且值为 **true** 为 **@use_ftp**。  
  
3.  在发布服务器上对发布数据库中，执行 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) 以注册请求订阅。 有关详细信息，请参阅 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
#### 为快照发布或事务发布更改一个或多个 FTP 快照传递设置  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 将下列值之一指定给 **@property** ，将该设置的新值指定给 **@value**：  
  
    -   **ftp_address** -用于传递快照的 FTP 服务器的地址。  
  
    -   **ftp_port** -FTP 服务器所使用的端口。  
  
    -   **ftp_subdirectory** -用于 FTP 快照的默认 FTP 目录的子目录。  
  
    -   **ftp_login** -用于连接到 FTP 服务器的登录名。  
  
    -   **ftp_password** -FTP 登录名的密码。  
  
2.  （可选）对更改的每个 FTP 设置重复步骤 1。  
  
3.  （可选）若要禁用 FTP 快照传递，请执行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 发布服务器上对发布数据库。 将值指定为 **enabled_for_internet** 为 **@property** ，值为 **false** 为 **@value**。  
  
#### 为合并发布更改 FTP 快照传递的设置  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 将下列值之一指定给 **@property** ，将该设置的新值指定给 **@value**：  
  
    -   **ftp_address** -用于传递快照的 FTP 服务器的地址。  
  
    -   **ftp_port** -FTP 服务器所使用的端口。  
  
    -   **ftp_subdirectory** -用于 FTP 快照的默认 FTP 目录的子目录。  
  
    -   **ftp_login** -用于连接到 FTP 服务器的登录名。  
  
    -   **ftp_password** -FTP 登录名的密码。  
  
2.  （可选）对更改的每个 FTP 设置重复步骤 1。  
  
3.  （可选）若要禁用 FTP 快照传递，请执行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 发布服务器上对发布数据库。 将值指定为 **enabled_for_internet** 为 **@property** ，值为 **false** 为 **@value**。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 下面的示例创建一个合并发布，该发布允许订阅服务器通过使用 FTP 访问快照数据。 访问 FTP 共享区时，订阅服务器应使用安全的 VPN 连接。 **sqlcmd** 脚本变量用于提供登录名和密码值。 有关详细信息，请参阅 [将 sqlcmd 与脚本变量](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_1.sql)]  
  
 下面的示例创建一个对合并发布的订阅，在该订阅中订阅服务器通过使用 FTP 来获取快照。 访问 FTP 共享区时，订阅服务器应使用安全的 VPN 连接。 **sqlcmd** 脚本变量用于提供登录名和密码值。 有关详细信息，请参阅 [将 sqlcmd 与脚本变量](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_2.sql)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_3.sql)]  
  
## 另请参阅  
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [通过 FTP 传输快照](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [使用快照初始化订阅](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  