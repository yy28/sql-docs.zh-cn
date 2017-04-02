---
title: "订阅属性 - 订阅服务器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subproperties.subscriber.f1"
helpviewer_keywords: 
  - "“订阅属性”对话框"
ms.assetid: bef66929-3234-4a45-8ec4-3b271519d07a
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# 订阅属性 - 订阅服务器
  使用订阅服务器上的 **“订阅属性”** 对话框可以查看和设置请求订阅的属性。  
  
 **“订阅属性”** 对话框中的每一个属性都包含相应的说明。 单击一个属性可以查看该属性的说明（显示于对话框的底部）。 本主题提供众多属性的其他信息。 属性分为以下类别：  
  
-   适用于所有订阅的属性。  
  
-   适用于事务订阅的属性。  
  
-   适用于合并订阅的属性。  
  
 如果某个选项显示为只读，则只能在创建订阅时对其进行设置。 若要设置在新建订阅向导中不可用的选项，请使用存储过程创建订阅。 有关详细信息，请参阅 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 和 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
> [!NOTE]  
>  如果还没有为订阅创建分发代理或合并代理作业，许多订阅属性将不会显示。 若要创建请求订阅的代理作业，请执行 [sp_addpullsubscription_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) （对于快照发布或事务发布的订阅） 或 [sp_addmergepullsubscription_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) （对于对合并发布的订阅）。  
  
## 用于所有订阅的选项  
 **用快照初始化已发布数据**  
 确定是通过快照（默认）还是通过其他方法初始化订阅。 有关初始化订阅的详细信息，请参阅 [初始化的订阅](../../relational-databases/replication/initialize-a-subscription.md)。  
  
 **快照位置**  
 确定在初始化或重新初始化过程中从中访问快照文件的位置。 该位置可以为下列值之一：  
  
-   **默认位置**：默认的位置，在配置分发服务器时定义。 有关详细信息，请参阅 [指定默认快照位置 & #40;SQL Server Management Studio & #41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)。  
  
-   **备用文件夹**：备用位置，可以在 **“发布属性”** 对话框中指定。 有关详细信息，请参阅 [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md)。  
  
-   **动态快照文件夹**：用于使用参数化行筛选器的合并发布的快照位置。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
-   **FTP 文件夹**︰ 文件传输协议 (FTP) 服务器可访问的文件夹。 有关详细信息，请参阅 [通过 FTP 传输快照](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
 **快照文件夹**  
 如果您选择的任何值之外 **默认位置** 为 **快照位置** 选项，必须指定快照文件夹的路径。  
  
 **使用 Windows 同步管理器**  
 确定是否可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同步管理器同步此订阅。  
  
 **安全性**  
 单击 **代理进程帐户** 行，然后单击属性按钮 (**...**) 若要更改运行的帐户在其下的分发代理或合并代理在订阅服务器。 与连接有关的安全选项取决于订阅类型：  
  
-   用于对事务发布的订阅︰ 若要更改在其下分发代理程序建立连接到分发服务器的帐户，请单击 **分发服务器连接**, ，然后单击属性按钮 (**...**)。  
  
-   对于对事务发布的立即更新订阅︰ 除了上面所述的分发服务器连接，您可以更改用来将更改从订阅服务器到发布服务器传播的方法︰ 单击 **发布服务器连接**, ，然后单击属性按钮 (**...**)。  
  
-   对于合并发布的订阅单击 **发布服务器连接**, ，然后单击属性按钮 (**...**)。  
  
 有关每个代理所需权限的详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## 用于事务订阅的选项  
 **可更新订阅**  
 确定是否将订阅服务器更改复制回发布服务器。 使用排队更新或立即更新可以复制更改。 **“订阅服务器更新方法”** 选项用于确定要使用的方法。 有关详细信息，请参阅 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
## 用于合并订阅的选项  
 **分区定义(HOST_NAME)**  
 以确定订阅服务器应接收的数据的同步期间合并复制的发布使用参数化筛选器，用于评估以下两个系统函数 （和 / 或如果筛选器引用了这两个函数） 之一︰ **suser_sname （)** 或 **host_name （)**。 默认情况下， **host_name （)** 返回在其合并代理正在运行，但您可以替代此值在新建订阅向导中的计算机的名称。 有关详细信息参数化筛选器和覆盖 **host_name （)**, ，请参阅 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 **订阅类型** 和 **优先级**  
 显示订阅是客户端订阅还是服务器订阅（在创建订阅后不能更改）。 服务器订阅可以将数据重新发布到其他订阅服务器，并可以为服务器订阅分配冲突解决优先级。  
  
 如果在新建订阅向导中选择了服务器订阅类型，则会为该订阅服务器分配一个在冲突解决过程中使用的优先级。  
  
 **交互式解决冲突**  
 确定是否使用交互式冲突解决程序用户界面解决合并同步过程中的冲突。 这需要将 **“使用 Windows 同步管理器”** 的值设置为 **“启用”**。 有关详细信息，请参阅 [Interactive Conflict Resolution](../../relational-databases/replication/merge/interactive-conflict-resolution.md)。  
  
 **Web 同步**  
 **使用 Web 同步** 确定是否要连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet 信息服务 (IIS) 服务器来同步订阅。 只有在为 Web 同步启用了发布时，此选项才可用。 有关详细信息，请参阅 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)。  
  
 对于 **“使用 Web 同步”** ，如果选择 **True**，则请执行以下操作：  
  
-   在 **“Web 服务器地址”**中输入 IIS 服务器的完整地址。  
  
-   单击 **Web 服务器连接** 行，然后单击属性按钮 (**...**) 来设置或更改订阅服务器连接到 IIS 服务器在其下的帐户。  
  
-   必要时更改 **“Web 服务器超时值”** 。 超时值是指表示 Web 同步请求在多长时间之后过期的时间长度（秒）。  
  
 有关配置的详细信息，请参阅 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  
  
## 另请参阅  
 [查看和修改请求订阅属性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [查看和修改推送订阅属性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  