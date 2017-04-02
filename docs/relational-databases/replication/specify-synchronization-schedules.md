---
title: "指定同步计划 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "订阅 [SQL Server 复制], 同步"
  - "计划同步 [SQL Server 复制]"
  - "同步 [SQL Server 复制], 计划"
  - "复制 [SQL Server 复制], 同步"
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 指定同步计划
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中指定同步计划。 在创建订阅时，可以定义同步计划以控制何时运行订阅的复制代理。 如果没有指定计划参数，则订阅将使用默认计划。  
  
 订阅由分发代理（对于快照复制和事务复制）或合并代理（对于合并复制）进行同步。 代理可以连续运行、按需运行或按计划运行。  
  
 **本主题内容**  
  
-   **指定同步计划，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 可在新建订阅向导的 **“同步计划”** 页上指定同步计划。 有关访问此向导的详细信息，请参阅 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md) 和 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
 在 **“作业计划属性”** 对话框中修改同步计划，该对话框位于 **的** “作业” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 文件夹和复制监视器的代理详细信息窗口中。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
 如果从 **“作业”** 文件夹指定计划，请使用下表确定代理作业的名称。  
  
|代理|作业名称|  
|-----------|--------------|  
|请求订阅的合并代理|**\< 发布服务器>-\< 发布数据库>-\< 发布>-\< 订阅服务器上>-\< 订阅数据库>-\< 整数>**|  
|推送订阅的合并代理|**\< 发布服务器>-\< 发布数据库>-\< 发布>-\< 订阅服务器上>-\< 整数>**|  
|推送订阅的分发代理|**\< 发布服务器>-\< 发布数据库>-\< 发布>-\< 订阅服务器上>-\< 整数>** <sup>1</sup>|  
|请求订阅的分发代理|**\< 发布服务器>-\< 发布数据库>-\< 发布>-\< 订阅服务器上>-\< 订阅数据库>-\< GUID>** <sup>2</sup>|  
|非 SQL Server 订阅服务器的推送订阅的分发代理|**\< 发布服务器>-\< 发布数据库>-\< 发布>-\< 订阅服务器上>-\< 整数>**|  
  
 <sup>1</sup> 对于对 Oracle 发布的推送订阅，它是 **\< 发布服务器>-\< 发布服务器**> 而不是 **\< 发布服务器>-\< 发布数据库>**  
  
 <sup>2</sup> 对于对 Oracle 发布的请求订阅，它是 **\< 发布服务器>-\< 分发数据库**> 而不是 **\< 发布服务器>-\< 发布数据库>**  
  
#### 指定同步计划  
  
1.  在 **SynchronizationSchedule** 新建订阅向导，选择下列其中一项值，从页面 **代理计划** 下拉列表框为您创建每个订阅︰  
  
    -   **连续运行**  
  
    -   **仅按需运行**  
  
    -   **\<定义计划...>**  
  
2.  如果您选择 **\< 定义计划 >**, ，指定在计划 **作业计划属性** 对话框中，然后单击 **确定**。  
  
3.  完成向导。  
  
#### 在复制监视器中修改推送订阅的同步计划  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，然后单击某个发布。  
  
2.  单击 **“所有订阅”** 选项卡。  
  
3.  右键单击订阅，然后单击 **查看详细信息**。  
  
4.  在 **订阅 \< 订阅名称 >** 窗口中，单击 **操作**, ，然后单击 **\< 代理名称> 作业属性**。  
  
5.  在 **计划** 页 **作业属性-\< JobName>** 对话框中，单击 **编辑。**  
  
6.  在 **作业计划属性** 对话框中，选择一个值从 **计划类型** 下拉列表︰  
  
    -   若要指定代理应连续运行，请选择 **“SQL Server 代理启动时自动启动”**。  
  
    -   若要指定代理应按计划运行，请选择 **“重复执行”**。  
  
    -   若要指定代理应按需运行，请选择 **“执行一次”**。  
  
7.  如果选择 **“重复执行”**，请为代理指定计划。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### 在 Management Studio 中修改推送订阅的同步计划  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到分发服务器，然后展开服务器节点。  
  
2.  展开 **“SQL Server 代理”** 文件夹，再展开 **“作业”** 文件夹。  
  
3.  右键单击该作业与该订阅，分发代理或合并代理程序关联，然后单击 **属性**。  
  
4.  在 **计划** 页 **作业属性-\< JobName>** 对话框中，单击 **编辑。**  
  
5.  在 **作业计划属性** 对话框中，选择一个值从 **计划类型** 下拉列表︰  
  
    -   若要指定代理应连续运行，请选择 **“SQL Server 代理启动时自动启动”**。  
  
    -   若要指定代理应按计划运行，请选择 **“重复执行”**。  
  
    -   若要指定代理应按需运行，请选择 **“执行一次”**。  
  
6.  如果选择 **“重复执行”**，请为代理指定计划。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### 在 Management Studio 中修改请求订阅的同步计划  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“SQL Server 代理”** 文件夹，再展开 **“作业”** 文件夹。  
  
3.  右键单击该作业与该订阅，分发代理或合并代理程序关联，然后单击 **属性**。  
  
4.  在 **计划** 页 **作业属性-\< JobName>** 对话框中，单击 **编辑。**  
  
5.  在 **作业计划属性** 对话框中，选择一个值从 **计划类型** 下拉列表︰  
  
    -   若要指定代理应连续运行，请选择 **“SQL Server 代理启动时自动启动”**。  
  
    -   若要指定代理应按计划运行，请选择 **“重复执行”**。  
  
    -   若要指定代理应按需运行，请选择 **“执行一次”**。  
  
6.  如果选择 **“重复执行”**，请为代理指定计划。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用复制存储过程以编程的方式定义同步计划。 所使用的存储过程取决于复制类型和订阅类型（请求或推送）。  
  
 通过下列计划参数，这些行为继承自定义计划 [sp_add_schedule & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md):  
  
-   **@frequency_type** -计划代理时使用的频率的类型。  
  
-   **@frequency_interval** -星期几运行代理。  
  
-   **@frequency_relative_interval** -当代理计划每月运行的给定月份的星期。  
  
-   **@frequency_recurrence_factor** -同步之间发生的频率类型单位数。  
  
-   **@frequency_subday** -时通常少于一天一次运行代理的频率单位。  
  
-   **@frequency_subday_interval** -在通常少于一天一次运行代理时运行的之间的频率单位数值。  
  
-   **@active_start_time_of_day** -在给定日将要开始运行代理时的最早时间。  
  
-   **@active_end_time_of_day** -在给定日将要开始运行代理时的最晚时间。  
  
-   **@active_start_date** -代理计划将生效的第一天。  
  
-   **@active_end_date** -代理计划将生效的最后一天。  
  
#### 为事务发布的请求订阅定义同步计划  
  
1.  对事务发布创建一个新的请求订阅。 有关详细信息，请参阅 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
2.  在订阅服务器上，执行 [sp_addpullsubscription_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分发代理在订阅服务器上运行的 Windows 凭据 **@job_name** 和 **@password**。 指定上面详细说明的同步参数，为同步订阅的分发代理作业定义计划。  
  
#### 为事务发布的推送订阅定义同步计划  
  
1.  对事务发布创建一个新的推送订阅。 有关详细信息，请参阅 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
2.  在订阅服务器上，执行 [sp_addpushsubscription_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)。 指定 **@subscriber**, ，**@subscriber_db**, ，**@publication**, ，并在其下订阅服务器上的分发代理运行的 Windows 凭据 **@job_name** 和 **@password**。 指定上面详细说明的同步参数，为同步订阅的分发代理作业定义计划。  
  
#### 为合并发布的请求订阅定义同步计划  
  
1.  对合并发布创建一个新的请求订阅。 有关详细信息，请参阅 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
2.  在订阅服务器上，执行 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，并在其下运行的合并代理在订阅服务器上的 Windows 凭据 **@job_name** 和 **@password**。 指定上面详细说明的同步参数，为同步订阅的合并代理作业定义计划。  
  
#### 为合并发布的推送订阅定义同步计划  
  
1.  对合并发布创建一个新的推送订阅。 有关详细信息，请参阅 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
2.  在订阅服务器上，执行 [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)。 指定 **@subscriber**, ，**@subscriber_db**, ，**@publication**, ，并在其下运行的合并代理在订阅服务器上的 Windows 凭据 **@job_name** 和 **@password**。 指定上面详细说明的同步参数，为同步订阅的合并代理作业定义计划。  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 复制使用 SQL Server 代理为定期发生的活动计划作业（如快照生成和订阅同步）。 可以编程的方式使用复制管理对象 (RMO) 为复制代理作业指定计划。  
  
> [!NOTE]  
>  当创建订阅并指定一个值 **false** 为 **CreateSyncAgentByDefault** （对于请求订阅的默认行为） 则不创建代理作业并忽略计划属性。 在这种情况下，必须由应用程序确定同步计划。 有关详细信息，请参阅 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 和 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
#### 在创建事务发布的推送订阅时定义一个复制代理计划  
  
1.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransSubscription> 您创建的订阅中的类。 有关详细信息，请参阅 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
2.  在调用之前 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, ，设置一个或多个以下字段的 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> 属性︰  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -计划代理时使用类型的频率 （如每天或每周）。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> -星期几运行代理。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> -当代理计划每月运行的给定月份的星期。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -同步之间发生的频率类型单位数。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -时通常少于一天一次运行代理的频率单位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -在通常少于一天一次运行代理时运行的之间的频率单位数值。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> -在给定日期内代理运行开始的最早时间。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> -在给定日期内代理运行开始的最晚时间。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> -代理计划是有效的第一天。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> -代理计划是有效的最后一天。  
  
    > [!NOTE]  
    >  如果未指定上述某个属性，将设置为默认值。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法来创建订阅。  
  
#### 在创建事务发布的请求订阅时定义一个复制代理计划  
  
1.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 您创建的订阅中的类。 有关详细信息，请参阅 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
2.  在调用之前 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, ，设置一个或多个以下字段的 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> 属性︰  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -计划代理时使用 （如每天或每周） 的频率的类型。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> -星期几运行代理。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> -计划每月运行代理的给定月份的星期。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -同步之间发生的频率类型单位数。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -时通常少于一天一次运行代理的频率单位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -在通常少于一天一次运行代理时运行的之间的频率单位数值。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> -在给定日期内代理运行开始的最早时间。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> -在给定日期内代理运行开始的最晚时间。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> -代理计划是有效的第一天。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> -代理计划是有效的最后一天。  
  
    > [!NOTE]  
    >  如果未指定上述某个属性，将设置为默认值。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 方法来创建订阅。  
  
#### 在创建合并发布的请求订阅时定义一个复制代理计划  
  
1.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 您创建的订阅中的类。 有关详细信息，请参阅 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
2.  在调用之前 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, ，设置一个或多个以下字段的 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> 属性︰  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -计划代理时使用 （如每天或每周） 的频率的类型。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> -星期几运行代理。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> -计划每月运行代理的给定月份的星期。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -同步之间发生的频率类型单位数。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -时通常少于一天一次运行代理的频率单位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -在通常少于一天一次运行代理时运行的之间的频率单位数值。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> -在给定日期内代理运行开始的最早时间。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> -在给定日期内代理运行开始的最晚时间。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> -代理计划是有效的第一天。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> -代理计划是有效的最后一天。  
  
    > [!NOTE]  
    >  如果未指定上述某个属性，将设置为默认值。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> 方法来创建订阅。  
  
#### 在创建合并发布的推送订阅时定义一个复制代理计划  
  
1.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 您创建的订阅中的类。 有关详细信息，请参阅 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
2.  在调用之前 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, ，设置一个或多个以下字段的 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> 属性︰  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -计划代理时使用 （如每天或每周） 的频率的类型。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> -星期几运行代理。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> -计划每月运行代理的给定月份的星期。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -同步之间发生的频率类型单位数。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -时通常少于一天一次运行代理的频率单位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -在通常少于一天一次运行代理时运行的之间的频率单位数值。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> -在给定日期内代理运行开始的最早时间。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> -在给定日期内代理运行开始的最晚时间。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> -代理计划是有效的第一天。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> -代理计划是有效的最后一天。  
  
    > [!NOTE]  
    >  如果未指定上述某个属性，将设置为默认值。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法来创建订阅。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 此示例创建一个合并发布的推送订阅并指定同步订阅计划。  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## 另请参阅  
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [同步推送订阅](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [同步请求订阅](../../relational-databases/replication/synchronize-a-pull-subscription.md)   
 [同步数据](../../relational-databases/replication/synchronize-data.md)  
  
  