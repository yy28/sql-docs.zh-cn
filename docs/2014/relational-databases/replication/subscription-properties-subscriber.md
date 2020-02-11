---
title: SQL Server 复制订阅属性-订阅服务器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.subproperties.subscriber.f1
- sql12.rep.newsubwizard.subproperties.publisher.f1
helpviewer_keywords:
- Subscription Properties dialog box
ms.assetid: bef66929-3234-4a45-8ec4-3b271519d07a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: af9cb7612837021b156fb8f467899f0e23ef1555
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250273"
---
# <a name="sql-server-replication-subscription-properties"></a>SQL Server 复制订阅属性 
本部分提供有关 "**订阅属性**" 对话框的信息。 

## <a name="publisher-properties"></a>发布服务器属性 
  使用发布服务器上的 **“订阅属性”** 对话框可以查看和设置推送订阅的属性。 您还可以查看请求订阅的某些属性，订阅服务器上的 **“订阅属性”** 对话框可以显示其他属性，并允许修改属性。  
  
 **“订阅属性”** 对话框中的每一个属性都包含相应的说明。 单击一个属性可以查看该属性的说明（显示于对话框的底部）。 本主题提供许多属性的其他相关信息，大多数属性只能在发布服务器上针对推送订阅显示。 属性分为以下类别：  
  
-   适用于所有订阅的属性。    
-   适用于事务订阅的属性。    
-   适用于合并订阅的属性。  
  
 如果某个选项显示为只读，则只能在创建订阅时对其进行设置。 若要设置在新建订阅向导中不可用的选项，请使用存储过程创建订阅。 有关详细信息，请参阅 [Create a Pull Subscription](create-a-pull-subscription.md) 和 [Create a Push Subscription](create-a-push-subscription.md)。  

  
### <a name="options-for-all-subscriptions"></a>用于所有订阅的选项  
 **安全性**  
 单击 **“代理进程帐户”** 行，再单击属性按钮 (**...**)，可以更改在分发服务器上运行分发代理或合并代理时所使用的帐户。 若要更改分发代理或合并代理在建立与订阅服务器的连接时所使用的帐户，请单击 **“订阅服务器连接”**，再单击属性按钮 (**...**)。  
  
 有关每个代理所需权限的详细信息，请参阅 [Replication Agent Security Model](security/replication-agent-security-model.md)。  
  
### <a name="publisher-options-for-transactional-subscriptions"></a>用于事务订阅的发布服务器选项  
 **防止事务循环**  
 确定分发代理是否将在订阅服务器上发起的事务发送回订阅服务器。 此选项用于双向事务复制。 有关详细信息，请参阅[双向事务复制](transactional/bidirectional-transactional-replication.md)。  
  
 **可更新订阅**  
 确定是否将订阅服务器更改复制回发布服务器。 使用排队更新或立即更新可以复制更改。 
  **“订阅服务器更新方法”** 选项用于确定要使用的方法。 有关详细信息，请参阅 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
### <a name="options-for-merge-subscriptions"></a>用于合并订阅的选项  
 **分区定义(HOST_NAME)**  
 对于使用参数化筛选器的发布，合并复制将在同步过程中对以下两个系统函数中的一个函数求值（如果筛选器同时引用了这两个函数，则对这两个函数求值），以确定订阅服务器应接收的数据： **SUSER_SNAME()** 或 **HOST_NAME()**。 默认情况下， **HOST_NAME()** 返回运行合并代理的计算机的名称，但可以在新建订阅向导中覆盖此值。 有关参数化筛选器和覆盖 **HOST_NAME()** 的详细信息，请参阅 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)。  
  
 **订阅类型**和**优先级**  
 显示订阅是客户端订阅还是服务器订阅（在创建订阅后不能更改）。 服务器订阅可以将数据重新发布到其他订阅服务器，并可以为服务器订阅分配冲突解决优先级。  
  
 如果在新建订阅向导中选择了服务器订阅类型，则会为该订阅服务器分配一个在冲突解决过程中使用的优先级。  
  
 **交互式解决冲突**  
 确定是否使用交互式冲突解决程序用户界面解决合并同步过程中的冲突。 这需要将 **“使用 Windows 同步管理器”** 的值设置为 **“启用”**。 有关详细信息，请参阅 [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md)。  


## <a name="subscriber-properties"></a>订阅服务器属性
  订阅服务器上的 "**订阅属性**" 对话框允许您查看和设置请求订阅的属性。  
  
 
  **“订阅属性”** 对话框中的每一个属性都包含相应的说明。 单击一个属性可以查看该属性的说明（显示于对话框的底部）。 本主题提供众多属性的其他信息。 属性分为以下类别：  
  
-   适用于所有订阅的属性。    
-   适用于事务订阅的属性。   
-   适用于合并订阅的属性。  
  
 如果某个选项显示为只读，则只能在创建订阅时对其进行设置。 若要设置在新建订阅向导中不可用的选项，请使用存储过程创建订阅。 有关详细信息，请参阅 [Create a Pull Subscription](create-a-pull-subscription.md) 和 [Create a Push Subscription](create-a-push-subscription.md)。  
  
> [!NOTE]  
>  如果还没有为订阅创建分发代理或合并代理作业，许多订阅属性将不会显示。 若要为请求订阅创建代理作业，请执行 [sp_addpullsubscription_agent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)（适用于快照发布或事务发布的订阅）或 [sp_addmergepullsubscription_agent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)（适用于合并发布的订阅）。  
  
### <a name="options-for-all-subscriptions"></a>用于所有订阅的选项  
 **用快照初始化已发布数据**  
 确定是通过快照（默认）还是通过其他方法初始化订阅。 有关初始化订阅的详细信息，请参阅[初始化订阅](initialize-a-subscription.md)。  
  
 **快照位置**  
 确定在初始化或重新初始化过程中从中访问快照文件的位置。 该位置可以为下列值之一：  
  
-   **默认位置**：配置分发服务器时定义的默认位置。 有关详细信息，请参阅[指定默认快照位置](snapshot-options.md#snapshot-folder-locations)。    
-   **备用文件夹**：备用位置，可在 "**发布属性**" 对话框中指定。 有关详细信息，请参阅 [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md)。    
-   **动态快照文件夹**：用于使用参数化行筛选器的合并发布的快照位置。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)。  
-   **FTP 文件夹**：文件传输协议（FTP）服务器可以访问的文件夹。 有关详细信息，请参阅[通过 FTP 传输快照](transfer-snapshots-through-ftp.md)。  
  
 **快照文件夹**  
 如果为 **“快照位置”** 选项选择了 **“默认位置”** 之外的任何其他值，则必须指定快照文件夹的路径。  
  
 **使用 Windows 同步管理器**  
 确定是否可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同步管理器同步此订阅。  
  
 **安全性**  
 单击 **“代理进程帐户”** 行，再单击属性按钮 (**...**)，可以更改在订阅服务器上运行分发代理或合并代理时所使用的帐户。 与连接有关的安全选项取决于订阅类型：  
  
-   对于对事务发布的订阅：若要更改分发代理在连接到分发服务器时所使用的帐户，请单击 **“分发服务器连接”**，再单击属性按钮 (**...**)。    
-   对于对事务发布的立即更新订阅：除了上面所述的分发服务器连接，通过单击 **“发布服务器连接”**，再单击属性按钮 (**...**)，还可以更改用于从订阅服务器向发布服务器传播更改的方法。  
-   对于对合并发布的订阅：请单击 **“发布服务器连接”**，再单击属性按钮 (**...**)。  
  
 有关每个代理所需权限的详细信息，请参阅 [Replication Agent Security Model](security/replication-agent-security-model.md)。  
  
### <a name="options-for-transactional-subscriptions"></a>用于事务订阅的选项  
 **可更新订阅**  
 确定是否将订阅服务器更改复制回发布服务器。 使用排队更新或立即更新可以复制更改。 
  **“订阅服务器更新方法”** 选项用于确定要使用的方法。 有关详细信息，请参阅 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
### <a name="options-for-merge-subscriptions"></a>用于合并订阅的选项  
 **分区定义(HOST_NAME)**  
 对于使用参数化筛选器的发布，合并复制将在同步过程中对以下两个系统函数中的一个函数求值（如果筛选器同时引用了这两个函数，则对这两个函数求值），以确定订阅服务器应接收的数据： **SUSER_SNAME()** 或 **HOST_NAME()**。 默认情况下， **HOST_NAME()** 返回运行合并代理的计算机的名称，但可以在新建订阅向导中覆盖此值。 有关参数化筛选器和覆盖 **HOST_NAME()** 的详细信息，请参阅 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)。  
  
 **订阅类型**和**优先级**  
 显示订阅是客户端订阅还是服务器订阅（在创建订阅后不能更改）。 服务器订阅可以将数据重新发布到其他订阅服务器，并可以为服务器订阅分配冲突解决优先级。  
  
 如果在新建订阅向导中选择了服务器订阅类型，则会为该订阅服务器分配一个在冲突解决过程中使用的优先级。  
  
 **交互式解决冲突**  
 确定是否使用交互式冲突解决程序用户界面解决合并同步过程中的冲突。 这需要将 **“使用 Windows 同步管理器”** 的值设置为 **“启用”**。 有关详细信息，请参阅 [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md)。  
  
 **Web 同步**  
 "**使用 Web 同步**" 确定是否连接到[!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services （IIS）服务器以同步订阅。 只有在为 Web 同步启用了发布时，此选项才可用。 有关详细信息，请参阅 [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md)。  
  
 对于 **“使用 Web 同步”** ，如果选择 **True**，则请执行以下操作：  
  
-   在 **“Web 服务器地址”** 中输入 IIS 服务器的完整地址。   
-   单击 **“Web 服务器连接”** 行，再单击属性按钮 (**...**)，以设置或更改订阅服务器连接到 IIS 服务器时所使用的帐户。   
-   必要时更改 **“Web 服务器超时值”** 。 超时值是指表示 Web 同步请求在多长时间之后过期的时间长度（秒）。  
  
 有关配置的详细信息，请参阅 [Configure Web Synchronization](configure-web-synchronization.md)。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改请求订阅属性](view-and-modify-pull-subscription-properties.md)   
 [查看和修改推送订阅属性](view-and-modify-push-subscription-properties.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  
