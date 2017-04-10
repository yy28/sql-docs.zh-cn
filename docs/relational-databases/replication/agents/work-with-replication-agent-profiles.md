---
title: "处理复制代理配置文件 | Microsoft Docs"
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
  - "复制 [SQL Server], 代理和配置文件"
  - "复制代理配置文件 [SQL Server]"
  - "代理 [SQL Server 复制], 配置文件"
  - "配置文件 [SQL Server], 复制代理"
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
caps.latest.revision: 49
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 49
---
# 处理复制代理配置文件
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中处理复制代理配置文件。 每个复制代理的行为都受一组参数控制，这些参数是通过代理配置文件设置的。 每个代理都有一个默认配置文件，有些代理还有一些其他的预定义配置文件；每个代理每次只能使用一个配置文件。  
  
 **本主题内容**  
  
-   **处理复制代理配置文件，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
    -   访问“代理配置文件”对话框  
  
    -   指定代理的配置文件  
  
    -   创建配置文件  
  
    -   修改配置文件  
  
    -   删除配置文件  
  
     [Transact-SQL](#TsqlProcedure)  
  
    -   创建配置文件  
  
    -   修改配置文件  
  
    -   删除配置文件  
  
    -   在同步期间使用代理配置文件  
  
    -   Transact-SQL 示例  
  
     [复制管理对象](#RMOProcedure)  
  
    -   创建配置文件  
  
    -   修改配置文件  
  
    -   删除配置文件  
  
-   **跟进︰**  [在更改代理参数后](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
###  <a name="Access_SSMS"></a> 从 SQL Server Management Studio 访问“代理配置文件”对话框  
  
1.  在 **常规** 页 **分发服务器属性-\< 分发服务器>** 对话框中，单击 **配置文件默认**。  
  
#### 从复制监视器访问“代理配置文件”对话框  
  
-   要为所有代理打开对话框中，右键单击发布服务器，然后单击 **代理配置文件**。  
  
-   为单个代理打开此对话框：  
  
    1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，然后单击某个发布。  
  
    2.  对于分发代理和合并代理程序配置文件，右键单击订阅 **所有订阅** 选项卡上，然后单击 **代理配置文件**。 对于其他代理，右键单击代理 **代理** 选项卡上，然后单击 **代理配置文件**。  
  
###  <a name="Specify_SSMS"></a> 指定代理的配置文件  
  
1.  如果 **“代理配置文件”** 对话框中显示了多个代理的配置文件，请选择一个代理。  
  
2.  在 **“代理配置文件”** 网格的 **“作为新项的默认值”** 列中选择一个配置文件。 默认情况下，该配置文件只应用于新发布和订阅的代理。  
  
3.  若要指定用于现有发布或订阅且属于选定类型的所有代理都使用该配置文件，请单击 **“更改现有代理”**。  
  
###  <a name="Modify_SSMS"></a> 查看和编辑与配置文件关联的参数  
  
1.  如果 **“代理配置文件”** 对话框中显示了多个代理的配置文件，请选择一个代理。  
  
2.  单击属性按钮 (**...**) 配置文件旁边。  
  
3.  查看参数和中的值 **\< ProfileName> 配置文件属性** 对话框。  
  
    -   用户定义配置文件中的参数可以编辑，但预定义系统配置文件中的参数不可编辑。  
  
    -   若要查看代理的所有参数，请清除 **“仅显示此配置文件中使用的参数”** 复选框。 有关代理参数的信息，请参阅本主题末尾处的链接。  
  
4.  单击 **“关闭”**。  
  
###  <a name="Create_SSMS"></a> 创建用户定义的配置文件  
  
1.  如果 **“代理配置文件”** 对话框中显示了多个代理的配置文件，请选择一个代理。  
  
2.  单击 **“新建”**。  
  
3.  在 **“新建代理配置文件”** 初始化对话框中，选择一个作为新配置文件基础的现有配置文件。  
  
4.  在 **“新建代理配置文件”** 对话框的 **“名称”** 和 **“说明”** 文本框中输入相应值。  
  
5.  修改参数以调整配置文件。 若要查看代理的所有参数，请清除 **“仅显示此配置文件中使用的参数”** 复选框。 有关代理参数的信息，请参阅本主题末尾处的链接。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="Delete_SSMS"></a> 删除用户定义的配置文件  
  
1.  如果 **“代理配置文件”** 对话框中显示了多个代理的配置文件，请选择一个代理。  
  
2.  如果一个配置文件与一个或多个代理相关联，请更改这些代理的配置文件：  
  
    1.  在 **“代理配置文件”** 网格中选择其他配置文件。  
  
    2.  单击 **“更改现有代理”**。  
  
        > [!NOTE]  
        >  此操作将更改用于现有发布或订阅且属于选定类型的所有代理的配置文件，而不只更改那些使用要删除的配置文件的代理的配置文件。  
  
3.  选择要删除的配置文件，再单击 **“删除”**。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
###  <a name="Create_tsql"></a> 创建一个新的代理配置文件  
  
1.  在分发服务器上，执行 [sp_add_agent_profile & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)。 指定 **@name**, ，值为 **1** 为 **@profile_type**, ，以及下列其中一项值为 **@agent_type**:  
  
    -   **1** - [复制快照代理](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [复制日志读取器代理](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [复制分发代理](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [复制合并代理](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [复制队列读取器代理](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     如果此配置文件将成为此复制代理类型的新默认配置文件，请将 **@default** 的值指定为 **1**。 使用返回新的配置文件的标识符 **@profile_id** 输出参数。 这将会使用基于给定代理类型的默认配置文件的配置文件参数集创建新的配置文件。  
  
2.  在已创建新配置文件后，可添加、删除或修改默认参数以自定义该配置文件。  
  
###  <a name="Modify_tsql"></a> 修改现有代理配置文件  
  
1.  在分发服务器上，执行 [sp_help_agent_profile & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 指定以下值之一 **@agent_type**:  
  
    -   **1** - [复制快照代理](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [复制日志读取器代理](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [复制分发代理](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [复制合并代理](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [复制队列读取器代理](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     这将返回指定类型的代理的所有配置文件。 记下的值 **profile_id** 结果集中要更改的配置文件。  
  
2.  在分发服务器上，执行 [sp_help_agent_parameter & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)。 指定步骤 1 中的配置文件标识符 **@profile_id**。 这将返回该配置文件的所有参数。 请记下要从配置文件中修改或删除的任何参数的名称。  
  
3.  若要更改配置文件中参数的值，请执行 [sp_change_agent_profile & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)。 指定步骤 1 中的配置文件标识符 **@profile_id**, ，要更改的参数名称 **@property**, ，和一个新的参数的值 **@value**。  
  
    > [!NOTE]  
    >  您不能将现有的代理配置文件更改为代理的默认配置文件。 相反，您必须创建一个新的配置文件以作为默认配置文件，如前面的过程所示。  
  
4.  若要从配置文件中移除参数，请执行 [sp_drop_agent_parameter & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)。 指定步骤 1 中的配置文件标识符 **@profile_id** 和要删除的参数名称 **@parameter_name**。  
  
5.  若要向配置文件添加新的参数，必须执行下列操作：  
  
    -   查询 [MSagentparameterlist & #40;Transact SQL & #41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) 在分发服务器，以确定哪些配置文件参数可以设置为每个代理类型的表。  
  
    -   在分发服务器上，执行 [sp_add_agent_parameter & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)。 指定步骤 1 中的配置文件标识符 **@profile_id**, ，可以为添加的有效参数的名称 **@parameter_name**, ，并为参数的值 **@parameter_value**。  
  
###  <a name="Delete_tsql"></a> 删除代理配置文件  
  
1.  在分发服务器上，执行 [sp_help_agent_profile & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 指定以下值之一 **@agent_type**:  
  
    -   **1** - [复制快照代理](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [复制日志读取器代理](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [复制分发代理](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [复制合并代理](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [复制队列读取器代理](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     这将返回指定类型的代理的所有配置文件。 记下的值 **profile_id** 结果集中要删除的配置文件。  
  
2.  在分发服务器上，执行 [sp_drop_agent_profile & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)。 指定步骤 1 中的配置文件标识符 **@profile_id**。  
  
###  <a name="Synch_tsql"></a> 在同步期间使用代理配置文件  
  
1.  在分发服务器上，执行 [sp_help_agent_profile & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 指定以下值之一 **@agent_type**:  
  
    -   **1** - [复制快照代理](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [复制日志读取器代理](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [复制分发代理](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [复制合并代理](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [复制队列读取器代理](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     这将返回指定类型的代理的所有配置文件。 记下的值 **profile_name** 结果集中要使用的配置文件。  
  
2.  从代理作业启动代理时，如果编辑启动代理以指定的值的作业步骤 **profile_name** 在之后的第 1 步中获得 **-ProfileName** 命令行参数。 有关详细信息，请参阅 [查看和修改复制代理命令提示符参数 & #40;SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)。  
  
3.  当从命令提示符处启动代理，则指定的值 **profile_name** 在之后的第 1 步中获得 **-ProfileName** 命令行参数。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例创建名为的合并代理的自定义配置文件 **custom_merge**, ，更改的值 **-UploadReadChangesPerBatch** 参数，将添加一个新 **-ExchangeType** 参数，并返回创建的配置文件的信息。  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 RMO  
  
###  <a name="Create_RMO"></a> 创建一个新的代理配置文件  
  
1.  创建到分发服务器的连接使用的实例 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.AgentProfile> 类。  
  
3.  设置对象的下列属性：  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> -配置文件的名称。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> - <xref:Microsoft.SqlServer.Replication.AgentType> 值，该值指定复制代理程序正在为其创建配置文件的类型。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建。  
  
    -   （可选） <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> -配置文件的说明。  
  
    -   （可选） <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> -将此属性设置为 **true** 如果所有新的代理作业，此 <xref:Microsoft.SqlServer.Replication.AgentType> 将默认使用此配置文件。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> 方法，以在服务器上创建配置文件。  
  
5.  在服务器上存在此配置文件后，可以通过添加、删除或更改复制代理参数的值来对该配置文件进行自定义。  
  
6.  若要将该配置文件分配给现有的复制代理作业，请调用 <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> 方法。 为 *distributionDBName* 传递分发数据库的名称并为 *agentID*传递作业 ID。  
  
###  <a name="Modify_RMO"></a> 修改现有代理配置文件  
  
1.  创建到分发服务器的连接使用的实例 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 类。 传递 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建的对象。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法返回 **false**，请验证分发服务器是否存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> 方法。 传递 <xref:Microsoft.SqlServer.Replication.AgentType> 值来缩小到特定类型的复制代理返回的配置文件。  
  
5.  获取所需 <xref:Microsoft.SqlServer.Replication.AgentProfile> 从返回的对象 <xref:System.Collections.ArrayList>, ，其中 <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> 对象的属性与配置文件名称相匹配。  
  
6.  调用的以下方法之一 <xref:Microsoft.SqlServer.Replication.AgentProfile> 更改的配置文件︰  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> -将支持的参数添加到该配置文件，其中 *名称* 复制代理参数的名称和 *值* 是指定的值。 若要枚举给定的代理类型的所有支持的代理参数，请调用 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 方法。 此方法返回 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> 这些对象表示所有支持的参数。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> -从配置文件中，删除现有的参数位置 *名称* 复制代理参数的名称。 若要枚举为配置文件定义的所有当前代理参数，请调用 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 方法。 此方法返回 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> 代表为此配置文件的现有参数的对象。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> -现有参数的配置文件中设置更改为在其中 *名称* 是代理参数的名称和 *newValue* 是指更改参数的值。 若要枚举为配置文件定义的所有当前代理参数，请调用 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 方法。 此方法返回 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> 代表为此配置文件的现有参数的对象。 若要枚举所有支持的代理参数设置，请调用 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 方法。 此方法返回 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> 这些对象表示支持的所有参数值。  
  
###  <a name="Delete_RMO"></a> 删除代理配置文件  
  
1.  创建到分发服务器的连接使用的实例 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.AgentProfile> 类。 设置的配置文件的名称 <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法返回 **false**，则指定的名称不正确或服务器上不存在该配置文件。  
  
4.  验证 <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> 属性设置为 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>, ，这表示客户配置文件。 不应删除的配置文件，其值为 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> 为 <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> 方法中删除此对象表示从服务器的用户定义的配置文件。  
  
##  <a name="FollowUp"></a> 跟进：在更改代理参数后  
 对代理参数所做的更改在下次启动代理时生效。 如果代理连续运行，则必须停止该代理，然后重新启动。  
  
## 另请参阅  
 [复制代理配置文件](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [复制快照代理](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [复制日志读取器代理](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [复制分发代理](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [复制合并代理](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [复制队列读取器代理](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  