---
title: 教程：在两个完全连接的服务器之间配置复制（事务）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de374f4372f62741ff3c49a9433cf339cecf3d26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>教程：在两个完全连接的服务器之间配置复制（事务）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
事务复制是在持续连接的服务器之间实现数据移动的好方法。 使用复制向导可以轻松地配置和管理复制拓扑。 本教程演示如何为持续连接的服务器配置事务复制拓扑。 若要深入了解事务复制的工作机制，请参阅[事务复制概述](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication)。 
  
## <a name="what-you-will-learn"></a>学习内容  
本教程将演示如何使用事务复制将数据从一个数据库发布到另一个数据库。 

在本教程中，您将学习如何执行以下操作：
> [!div class="checklist"]
> * 通过事务复制创建发布服务器
> * 创建事务发布服务器的订阅服务器
> * 验证订阅和测量滞后时间
> * 错误故障排除方法
  
  
## <a name="prerequisites"></a>必备条件  
本教程适用于熟悉数据库基本操作但复制经验不足的用户。 本教程要求你完成上一个教程， [准备用于复制的服务器](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)的学习。  
  
要使用本教程，系统必须具有 SQL Server Management Studio (SSMS) 和以下组件：  
  
-   发布服务器（源）：  
  
    -   任意版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但 SQL Server Express 或 SQL Compact 除外。 这些版本不能充当复制发布服务器。   
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 示例数据库。 为了增强安全性，默认情况下不会安装示例数据库。  
  
-   订阅服务器（目标）：  
  
    -   任意版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但 [!INCLUDE[ssEW](../../includes/ssew-md.md)]除外。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 不能充当事务复制中的订阅服务器。  
  
- 安装 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)。
- 下载 [AdventureWorks 示例数据库](https://github.com/Microsoft/sql-server-samples/releases)。 有关在 SSMS 中还原数据库的说明，请参阅[还原数据库](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 
 
>[!NOTE]
> - 在相差两个版本以上的 SQL Server 上不支持复制。 有关详细信息，请参阅[复制拓扑中受支持的 SQL 版本](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/)。
> - 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，必须使用属于 **sysadmin** 固定服务器角色成员的登录名连接到发布服务器和订阅服务器。 有关 sysadmin 角色的详细信息，请参阅[服务器级别角色](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles)。  
  
  
本教程的预计学时：60 分钟。  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>配置事务复制的发布服务器
在本节中，使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建一个事务发布，以便在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库中发布“Product”表的筛选子集。 您还要将分发代理使用的 SQL Server 登录名添加到发布访问列表 (PAL)。 开始本教程之前，应已完成上一个教程 [准备用于复制的服务器](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)。


### <a name="create-a-publication-and-define-articles"></a>创建发布并定义项目
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2. 右键单击“SQL Server 代理”，选择“启动”。 应在创建发布之前运行 SQL Server 代理。 如果该操作未启动代理，则需要从“SQL Server 配置管理器”手动启动。 
3. 展开“复制”文件夹，右键单击“本地发布”文件夹，然后选择“新建发布”。  此操作将启动发布配置向导：  

    ![新建发布](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. 在“发布数据库”页上，选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然后选择“下一步”。  
  
4. 在“发布类型”页上，选择“事务发布”，然后选择“下一步”：  

    ![事务复制](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. 在“项目”页上，展开“表”节点，选中“Product”复选框。 然后展开“Product”，并清除“ListPrice”和“StandardCost”旁边的复选框。 选择“下一步”：  

    ![要发布的项目](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. 在“筛选表行”页上，选择“添加”。   
  
7. 在“添加筛选器”对话框中，选择 SafetyStockLevel 列，然后选择向右键，将此列添加到筛选查询的 Filter 语句 WHERE 子句。 然后在 WHERE 子句修饰符中手动键入以下内容：  
  
    ```sql  
    WHERE [SafetyStockLevel] < 500  
    ```
  
    ![Filter 语句](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. 选择“确定”，然后选择“下一步”。  
  
9. 选中“立即创建快照并使快照保持可用状态，以初始化订阅”复选框，选择“下一步”：  

    ![快照代理](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. 在“代理安全性”页上，清除“使用快照代理的安全设置”复选框。   
  
    A. 选择快照代理的“安全设置”，在“进程帐户”框中输入 <Publisher_Machine_Name>\repl_snapshot，为此帐户提供密码，然后选择“确定”：  

    ![快照代理安全性](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. 重复上一步，将 <Publisher_Machine_Name>\repl_logreader 设置为日志读取器代理的进程帐户，然后选择“确定”：  

    ![日志读取器代理安全性](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. 在“完成向导”页的“发布名称”框中，键入 AdvWorksProductTrans，然后选择“完成”：  

    ![为发布命名](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. 创建发布后，选择“关闭”完成该向导。 

    尝试创建发布时，如果未运行 SQL Server 代理，则可能会遇到以下错误。 这说明已成功创建发布，但快照代理无法启动。 如果发生这种情况，需要启动 SQL Server 代理，然后手动启动快照代理。 在下一节中介绍与此相关的说明： 

    ![快照代理未能启动](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="to-view-the-status-of-snapshot-generation"></a>查看快照的生成状态  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。  
  
2.  在“本地发布”文件夹中，右键单击 AdvWorksProductTrans，然后选择“查看快照代理状态”：  

    ![快照代理状态](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3.  将显示该发布的快照代理作业的当前状态。 继续下一节之前，请确保快照作业已成功完成。
          
    如果首次创建发布时未运行 SQL Server 代理，检查发布的“快照代理状态”时，将看到快照代理处于“从未运行”状态。 如果是这种情况，则选择“启动”，启动快照代理： 

       ![启动快照代理](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
       如果看到此处的错误，请参阅[使用快照代理对错误进行故障排除](#troubleshoot-erros-with-snapshot-agent)。 

  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>将分发代理登录名添加到 PAL  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。  
  
2.  在“本地发布”文件夹中，右键单击 AdvWorksProductTrans，然后选择“属性”。  将显示“发布属性”对话框。    
  
    A. 选择“发布访问列表”页，选择“添加”。  
    B. 在“添加发布访问项”对话框中，选择“<Publisher_Machine_Name>\repl_distribution”，然后选择“确定”。 选择“确定”：

   
   ![将登录名添加到 PAL 列表](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

另请参阅：  
[复制编程概念](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>创建事务发布的订阅
在此节中，介绍如何将订阅服务器添加到先前创建的发布中。 本教程使用远程订阅服务器 (NODE2\SQL2016)，但订阅也可在本地添加到发布服务器。 

### <a name="to-create-the-subscription"></a>创建订阅  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。  
  
2.  在“本地发布”文件夹中，右键单击“AdvWorksProductTrans”发布，然后选择“新建订阅”。  新建订阅向导将启动。 
 
    ![“新建订阅”](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3.  在“发布”页上，选择“AdvWorksProductTrans”，然后选择“下一步”：  

    ![选择 Tran 发布服务器](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4.  在“分发代理位置”页上，选择“在分发服务器上运行所有代理”，然后选择“下一步”。  有关请求订阅和推送订阅的详细信息，请参阅[订阅发布](https://docs.microsoft.com/en-us/sql/relational-databases/replication/subscribe-to-publications)：

    ![在 Dist 运行代理](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5.  在“订阅服务器”页上，如果未显示订阅服务器实例的名称，选择“添加订阅服务器”，然后从下拉列表选择“添加 SQL Server 订阅服务器”。 这将启动“连接到服务器”对话框。 输入订阅服务器实例名称，然后选择“连接”。  
    
    A. 添加订阅服务器后，选中订阅服务器实例名称旁边的框。 然后在“订阅数据库”下选择“新建数据库”：   

  ![添加订阅服务器](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. 这将启动“新建数据库”对话框。 在“数据库名称”框中输入 ProductReplica，选择“确定”，然后选择“下一步”： 
  
    ![产品副本 DB](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8.  在“分发代理安全性”对话框中，选择省略号 (…) 按钮。 在“进程帐户”框中输入 <Publisher_Machine_Name>\repl_distribution，输入此帐户的密码，选择“确定”，然后选择“下一步”：

    ![添加分发帐户](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. 选择“完成”以接受其余页中的默认值并完成向导。  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>在订阅服务器上设置数据库权限  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到订阅服务器，展开“安全性”，右键单击“登录名”，然后选择“新建登录名”。     
  
    A. 在“常规”页的“登录名”下，选择“搜索”，并添加 <Subscriber_Machine_Name>\repl_distribution 的登录名。
    B. 在“用户映射”页上，将登录名 db_owner 授予 ProductReplica 数据库： 

    ![登录订阅服务器](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. 选择“确定”，即可关闭“新建登录名”对话框。 

  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>查看订阅的同步状态  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。  
  
2.  在“本地发布”文件夹中，展开“AdvWorksProductTrans”发布，右键单击“ProductReplica”数据库中的订阅，然后选择“查看同步状态”。 系统将显示订阅的当前同步状态：  
    ![查看同步状态](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3.  如果订阅未在“AdvWorksProductTrans”下出现，请按 F5 刷新列表。  
  
另请参阅：  
[使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md)  
[订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measuring-replication-latency"></a>测量复制滞后时间
在本节中，将用跟踪令牌来验证更改是否已复制到订阅服务器并确定滞后时间。 滞后时间是发布服务器处所做的更改显示到订阅服务器所需的时间。
  
1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，展开服务器节点，右键单击“复制”文件夹，然后选择“启动复制监视器”：

    ![启动复制监视器](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. 在左窗格中展开发布服务器组，展开发布服务器实例，然后选择“AdvWorksProductTrans”发布。  
  
    A. 选择“跟踪令牌”选项卡。  
    B. 选择“插入跟踪器”。    
    c. 在以下列中查看跟踪令牌的运行时间： **“发布服务器到分发服务器”**、 **“分发服务器到订阅服务器”**、 **“总滞后时间”**。 值为“挂起”表示令牌尚未到达指定点：


   ![跟踪令牌](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


另请参阅   
[为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

## <a name="error-troubleshooting-methodology"></a>错误故障排除方法
此节介绍如何排查基本复制同步故障。 请注意，本节旨在以故障排除为目的，带你了解复制组件。 但是，实际遇到的错误可能与此处谈论的不同，这种情况下可能需要不同的解决方法。 如果是这种情况，有必要进行进一步的故障排除，这超出了本教程的范围。 


### <a name="troubleshoot-errors-with-snapshot-agent"></a>使用快照代理对错误进行故障排除
“快照代理”这一代理用于生成快照，并将其写入指定的快照文件夹。 

1. 要查看快照代理的状态，请展开复制下的“本地发布”节点，右键选择发布 AdvWorksProductTrans  > “查看快照代理状态”。 
2. 如果在“快照代理状态”中报告了错误，可在“快照代理”作业历史记录中看到更多详细信息。 要访问历史记录，在“对象资源管理器”中展开“SQL Server 代理”，并打开“作业活动监视器”。 

    A. 按照“类别”排序，并根据类别“REPL-Snapshot”找到“快照代理”。 

    B. 右键单击“快照代理”，然后单击“查看历史记录”： 

   ![快照代理历史记录](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenthistory.png)
    
1. 在“快照代理历史记录”中，选择相关的日志项目。 通常为错误报告条目之前的一行或两行（错误由红色 X 指示）。  查看日志下方文本框中的消息文本： 

    ![快照代理访问遭拒绝](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotaccessdenied.png)

        The replication agent had encountered an exception.
        Exception Message: Access to path '\\node1\repldata.....' is denied.


  如果未正确配置快照文件夹的窗口权限，将看到“快照代理”出现“访问遭拒绝”的错误。 需要对 repldata 文件夹上 <Publisher_Machine_Name>\repl_snapshot 帐户验证权限。 有关详细信息，请参阅[为快照文件夹创建共享并分配权限](tutorial-preparing-the-server-for-replication.md#create-a-share-for-the-snapshot-folder-and-assign-permissions)。

### <a name="troubleshoot-errors-with-log-reader-agent"></a>使用日志读取器代理对错误进行故障排除
日志读取器代理会连接到发布服务器数据库，并扫描事务日志，查找标记为“用于复制”的任何事务。 然后，代理会将这些事务添加到“分发”数据库。 

1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，展开服务器节点，右键单击“复制”文件夹，然后选择“启动复制监视器”：  

    ![启动 Repl 监视器](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)
  
    复制监视器随即启动：![复制监视器](media/tutorial-replicating-data-between-continuously-connected-servers/replmonitor.png) 
   
2. 红色 X 指示发布不同步。 展开左侧的“我的发布服务器”，然后展开相关的发布服务器。  
  
3.  选择左侧的“AdvWorksProductTrans”发布，然后在其中一个选项卡上查找红色 X，确定问题的位置。 在本例中，红色 X 位于“代理选项卡”，表明其中一个代理出现了错误： 

    ![代理错误](media/tutorial-replicating-data-between-continuously-connected-servers/agenterror.png)

4. 选择“代理选项卡”，确定遇到错误的代理： 

    ![日志读取器发生故障](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentfailure.png)


5. 此视图显示两种代理：“快照代理”和“日志读取器代理”。 发生错误的代理具有红色 X。在本例中，“日志读取器代理”带有红色 X，表示该代理出现问题。 双击报告错误的行，本例中为“日志读取器代理”。 这将启动所选代理的“代理历史记录”，本例中为“日志读取器代理”历史记录。 历史记录提供有关该错误的详细信息： 
    
    ![日志读取器错误](media/tutorial-replicating-data-between-continuously-connected-servers/logreadererror.png)

       Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
       The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
       Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
       Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        

6. 上述错误通常是由于发布服务器数据库的所有者未正确设置而出现的。 此错误通常在还原数据库后出现。 要验证这一点，请展开“对象资源管理器”中的“数据库”，然后右键单击 AdventureWorks2012  > “属性”。 确认一名所有者存在于“文件”页下。 如果此字段为空，则这可能是产生该问题的原因所在： 

    ![DB 属性](media/tutorial-replicating-data-between-continuously-connected-servers/dbproperties.png)

7. 如果“文件”页上的所有者为空，请在 AdventureWorks2012 数据库的上下文中打开“新建查询”窗口。 运行以下 T-SQL 代码片段：

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXEC sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. 需要重启“日志读取器代理”。 要执行此操作，在“对象资源管理器”中展开“SQL Server 代理”节点，并打开“作业活动监视器”。 按照“类别”排序，并根据“REPL-LogReader”类别找到“日志读取器代理”。 右键单击“日志读取器代理”作业，然后单击“启动作业”： 

    ![重启日志读取器代理](media/tutorial-replicating-data-between-continuously-connected-servers/startjobatstep.png)

9. 通过再次打开“复制监视器”，确认发布现已同步。 如果尚未打开，通过右键单击“对象资源管理器”中的“复制”，可找到该监视器。 
10. 选择“AdvWorksProductTrans”发布，选择“代理”选项卡，然后双击选择“日志读取器代理”，打开代理历史记录。 现应看到“日志读取器代理”正在运行，并且正在复制命令，或具有“未复制事务”：

    ![日志读取器正在运行](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderrunning.png)

### <a name="troubleshoot-errors-with-distribution-agent"></a>使用分发代理对错误进行故障排除
“分发代理”采用在“分发”数据库中找到的数据，然后将其应用到订阅服务器。 

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，展开服务器节点，右键单击“复制”文件夹，然后选择“启动复制监视器”。  
2. 在“复制监视器”中，选择“AdvWorksProductTrans”发布，然后选择“所有订阅”选项卡。右键单击该订阅，然后单击“查看详细信息”：

    ![查看 Dist 详细信息](media/tutorial-replicating-data-between-continuously-connected-servers/viewdetails.png)

2. “分发服务器到订阅服务器”历史记录对话框随即打开，其中阐明了代理遇到的错误： 

     ![Dist 代理历史记录错误](media/tutorial-replicating-data-between-continuously-connected-servers/disthistoryerror.png)
    
        Error messages:
        Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.

3. 错误指示“分发代理”正在重试。 要了解详细信息，请在“对象资源管理器”中展开“SQL Server 代理” > “作业活动监视器”。 按照“类别”对作业进行排序。 

    A. 根据类别“REPL-Distribution”找到“分发代理”。 右键单击该代理，然后单击“查看历史记录”：

    ![查看Dist 代理历史记录](media/tutorial-replicating-data-between-continuously-connected-servers/viewdistagenthistory.png)

5. 选择其中一个错误条目，并在窗口底部查看错误文本：  

    ![Dist 代理的密码错误](media/tutorial-replicating-data-between-continuously-connected-servers/distpwwrong.png)
    
        Message:
        Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)

6. 此错误指示“分发代理”所使用的密码不正确。 要解决此问题，请在“对象资源管理器”中展开“复制”节点，右键单击该订阅，然后单击“属性”。 选择“代理进程帐户”旁边的省略号 (...)，并修改密码：

    ![修改 Dist 代理的 PW](media/tutorial-replicating-data-between-continuously-connected-servers/distagentpwchange.png)

7. 再次检查“复制监视器”，可通过右键单击“对象资源管理器”中的“复制”找到该监视器。 “所有订阅”下的红色 X 指示“分发代理”仍遇到错误。 通过右键单击“复制监视器”中的订阅  > “查看详细信息”，打开“分发到订阅服务器”历史记录。 此处的错误是不同的： 

    ![Dist 代理无法连接](media/tutorial-replicating-data-between-continuously-connected-servers/distagentcantconnect.png)
           
        Connecting to Subscriber 'NODE2\SQL2016'        
        Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
        Number:  18456
        Message: Login failed for user 'NODE2\repl_distribution'.

8. 此错误指示“分发代理”无法连接到订阅服务器，因为用户 NODE2\repl_distribution 登录失败。 若要进一步调查，请连接到订阅服务器，并在“对象资源管理器”的“管理”节点下，打开当前的“SQL 错误日志”： 

    ![订阅服务器登录失败](media/tutorial-replicating-data-between-continuously-connected-servers/loginfailed.png) 如果看到此错误，则意味着订阅服务器上丢失该登录名。 要解决此问题，请参阅[在订阅服务器上设置数据库权限](#setting-database-permissions-at-the-subscriber)。

9. 登录错误得到解决后，立即再次检查“复制监视器”。 如果所有问题均得以解决，在“所有订阅”下，应在“发布名称”旁边看到一个绿色箭头，以及“正在运行”的状态。 右键单击“订阅”，即可再次启动“分发服务器到订阅服务器”历史记录，从而验证是否成功。 如果是首次运行分发代理，将看到快照已批量复制到订阅服务器，如下图所示： 

     ![Dist 代理成功](media/tutorial-replicating-data-between-continuously-connected-servers/distagentsuccess.png)   

  ## <a name="next-steps"></a>后续步骤
已成功配置用于事务复制的发布服务器和订阅服务器。  现可插入、更新或删除发布服务器上“Product”表中的数据。 然后可以在订阅服务器上查询“Product”表，以查看已复制的更改。 下一篇文章介绍如何配置合并复制。  

转到下一篇文章，了解详细信息
> [!div class="nextstepaction"]
> [后续步骤](tutorial-replicating-data-with-mobile-clients.md)

  
