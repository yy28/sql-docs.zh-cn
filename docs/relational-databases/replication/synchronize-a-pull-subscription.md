---
title: "同步请求订阅 | Microsoft Docs"
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
  - "请求订阅 [SQL Server 复制], 同步"
  - "同步 [SQL Server 复制], 请求订阅"
  - "订阅 [SQL Server 复制], 请求"
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 同步请求订阅
  本主题描述如何同步请求订阅中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ，[复制代理程序](../../relational-databases/replication/agents/replication-agents-overview.md), ，或复制管理对象 (RMO)。  
  
 **本主题内容**  
  
-   **同步请求订阅，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [复制代理](#ReplProg)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 订阅由分发代理（对于快照复制和事务复制）或合并代理（对于合并复制）进行同步。 代理可以连续运行、按需运行或按计划运行。 有关指定同步计划的详细信息，请参阅 [指定同步计划](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
 在 **中的** “本地订阅” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]文件夹中，按需同步订阅。  
  
#### 在 Management Studio 中按需同步请求订阅  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击你想要同步，然后单击的订阅 **查看同步状态**。  
  
4.  在 **查看同步状态-\< 订阅服务器上>: \< 订阅数据库>** 对话框中，单击 **启动**。 完成同步后，将显示消息 **“同步完成”** 。  
  
5.  单击 **“关闭”**。  
  
##  <a name="ReplProg"></a> 复制代理  
 可通过在命令提示符下调用相应的复制代理可执行文件，以编程方式按需同步请求订阅。 被调用的复制代理可执行文件将取决于请求订阅所属的发布的类型。 有关详细信息，请参阅 [Replication Agents](../../relational-databases/replication/agents/replication-agents.md)。  
  
> [!NOTE]  
>  复制代理使用通过命令提示符启动该代理的用户的 Windows 身份验证凭据连接到本地服务器。 这些 Windows 凭据还在使用 Windows 集成身份验证连接到远程服务器时使用。  
  
#### 通过命令提示符或批处理文件启动分发代理  
  
1.  在命令提示符下或批处理文件中，启动 [复制分发代理](../../relational-databases/replication/agents/replication-distribution-agent.md) 通过运行 **distrib.exe**, ，指定下列命令行参数︰  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriptionType** = **1**  
  
     如果您使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则还必须指定下列参数：  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
#### 在命令提示符下或批处理文件中启动合并代理  
  
1.  在命令提示符下或批处理文件中，启动 [复制合并代理](../../relational-databases/replication/agents/replication-merge-agent.md) 通过运行 **replmerg.exe**, ，指定下列命令行参数︰  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-PublisherSecurityMode** = **1**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType** = **1**  
  
     如果您使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则还必须指定下列参数：  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> 示例（复制代理）  
 以下示例启动分发代理以同步请求订阅。 所有连接均使用 Windows 身份验证实现。  
  
```  
 -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks  
SET SubscriptionDB=AdventureWorksReplica   
SET Publication=AdvWorksProductsTran  
  
-- Start the Distribution Agent.  
-- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\100\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 1;  
```  
  
 以下示例启动合并代理以同步请求订阅。 所有连接均使用 Windows 身份验证实现。  
  
```  
-- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks  
SET SubscriptionDB=AdventureWorksReplica   
SET Publication=AdvWorksSalesOrdersMerge  
  
--Start the Merge Agent with concurrent upload and download processes.  
-- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\100\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
```  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 和托管代码对复制代理功能的访问权限，以编程方式同步请求订阅。 用于同步请求订阅的类取决于订阅所属的发布的类型。  
  
> [!NOTE]  
>  如果您要启动一个自主运行而不影响应用程序的订阅，请异步启动代理。 但是，如果您要监视同步的结果并在同步进程期间从代理处接收回调（例如，要显示进度栏），则应当同步启动代理。 对于 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 订阅服务器，必须同步启动代理。  
  
#### 将请求订阅与快照或事务发布进行同步  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 类，并设置以下属性︰  
  
    -   订阅数据库名称为 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>。  
  
    -   订阅所属的发布的名称 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>。  
  
    -   为发布数据库的名称 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>。  
  
    -   为发布服务器的名称 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>。  
  
    -   步骤 1 中创建的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取其他订阅属性。 如果该方法返回 **false**，则确保订阅存在。  
  
4.  使用下列方法之一在订阅服务器中启动分发代理：  
  
    -   调用 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> 方法的实例上 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 步骤 2 中。 该方法异步启动分发代理，并在代理作业运行时立即将控制权返回给您的应用程序。 不能调用此方法对于 [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 订阅服务器或订阅创建了值为 **false** 为 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> （默认值）。  
  
    -   获取其实例 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> 类 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> 属性，然后调用 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> 方法。 该方法可以同步启动代理，并且控制权仍属于运行代理作业。 在执行同步期间，您可以处理 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> 在代理运行的事件。  
  
        > [!NOTE]  
        >  如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> （默认值） 时创建请求订阅，还需要指定 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A>, ，<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>, ，和 （可选） <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A> 由于订阅中未提供与代理作业相关的元数据 [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)。  
  
#### 将请求订阅与合并发布进行同步  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 类，并设置以下属性︰  
  
    -   订阅数据库名称为 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>。  
  
    -   订阅所属的发布的名称 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>。  
  
    -   已发布的数据库的名称 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>。  
  
    -   为发布服务器的名称 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>。  
  
    -   步骤 1 中创建的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取其他订阅属性。 如果该方法返回 **false**，则确保订阅存在。  
  
4.  使用下列方法之一在订阅服务器中启动合并代理：  
  
    -   调用 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> 方法的实例上 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 步骤 2 中。 该方法异步启动合并代理，并在代理作业运行时立即将控制权返回给您的应用程序。 不能调用此方法对于 [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 订阅服务器或订阅创建了值为 **false** 为 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> （默认值）。  
  
    -   获取实例的 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> 类 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> 属性，然后调用 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> 方法。 该方法可以同步启动合并代理，并且控件仍属于运行代理作业。 在执行同步期间，您可以处理 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> 在代理运行的事件。  
  
        > [!NOTE]  
        >  如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> （默认值） 时创建请求订阅，还需要指定 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A>, ，和 （可选） <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A>, ，和 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A> 由于订阅中未提供与代理作业相关的元数据 [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 该示例将请求订阅与事务发布进行同步，其中，代理使用代理作业进行异步启动。  
  
```csharp  
// Define server, publication, and database names.  
String subscriberName = subscriberInstance;  
String publisherName = publisherInstance;  
String publicationName = "AdvWorksProductTran";  
String publicationDbName = "AdventureWorks";  
String subscriptionDbName = "AdventureWorksReplica";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
TransPullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define subscription properties.  
    subscription = new TransPullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription and the job exists, start the agent job.  
    if (subscription.LoadProperties() && subscription.AgentJobId != null)  
    {  
        subscription.SynchronizeWithJob();  
    }  
    else  
    {  
        // Do something here if the subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exists on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Do appropriate error handling here.  
    throw new ApplicationException("The subscription could not be synchronized.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksProductTran"  
Dim publicationDbName As String = "AdventureWorks"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As TransPullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define subscription properties.  
    subscription = New TransPullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription and the job exists, start the agent job.  
    If subscription.LoadProperties() And Not subscription.AgentJobId Is Nothing Then  
        subscription.SynchronizeWithJob()  
    Else  
        ' Do something here if the subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exists on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Do appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be synchronized.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 该示例将请求订阅与事务发布进行同步，其中，代理进行同步启动。  
  
```csharp  
// Define the server, publication, and database names.  
string subscriberName = subscriberInstance;  
string publisherName = publisherInstance;  
string publicationName = "AdvWorksProductTran";  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
TransPullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define the pull subscription.  
    subscription = new TransPullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription exists, then start the synchronization.  
    if (subscription.LoadProperties())  
    {  
        // Check that we have enough metadata to start the agent.  
        if (subscription.PublisherSecurity != null)  
        {  
            // Synchronously start the Distribution Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize();  
        }  
        else  
        {  
            throw new ApplicationException("There is insufficent metadata to " +  
                "synchronize the subscription. Recreate the subscription with " +  
                "the agent job or supply the required agent properties at run time.");  
        }  
    }  
    else  
    {  
        // Do something here if the pull subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exist on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement appropriate error handling here.  
    throw new ApplicationException("The subscription could not be " +  
        "synchronized. Verify that the subscription has " +  
        "been defined correctly.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define the server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksProductTran"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As TransPullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define the pull subscription.  
    subscription = New TransPullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription exists, then start the synchronization.  
    If subscription.LoadProperties() Then  
        ' Check that we have enough metadata to start the agent.  
        If Not subscription.PublisherSecurity Is Nothing Then  
  
            ' Write agent output to a log file.  
            subscription.SynchronizationAgent.Output = "distagent.log"  
            subscription.SynchronizationAgent.OutputVerboseLevel = 2  
  
            ' Synchronously start the Distribution Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize()  
        Else  
            Throw New ApplicationException("There is insufficent metadata to " + _  
             "synchronize the subscription. Recreate the subscription with " + _  
             "the agent job or supply the required agent properties at run time.")  
        End If  
    Else  
        ' Do something here if the pull subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exist on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Implement appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be " + _  
     "synchronized. Verify that the subscription has " + _  
     "been defined correctly.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 该示例将请求订阅与合并发布进行同步，其中，代理使用代理作业进行异步启动。  
  
```csharp  
// Define server, publication, and database names.  
String subscriberName = subscriberInstance;  
String publisherName = publisherInstance;  
String publicationName = "AdvWorksSalesOrdersMerge";  
String publicationDbName = "AdventureWorks";  
String subscriptionDbName = "AdventureWorksReplica";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define subscription properties.  
    subscription = new MergePullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription and the job exists, start the agent job.  
    if (subscription.LoadProperties() && subscription.AgentJobId != null)  
    {  
        subscription.SynchronizeWithJob();  
    }  
    else  
    {  
        // Do something here if the subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exists on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Do appropriate error handling here.  
    throw new ApplicationException("The subscription could not be synchronized.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publicationDbName As String = "AdventureWorks"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define subscription properties.  
    subscription = New MergePullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription and the job exists, start the agent job.  
    If subscription.LoadProperties() And Not subscription.AgentJobId Is Nothing Then  
        subscription.SynchronizeWithJob()  
    Else  
        ' Do something here if the subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exists on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Do appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be synchronized.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 该示例将请求订阅与合并发布进行同步，其中，代理进行同步启动。  
  
```csharp  
// Define the server, publication, and database names.  
string subscriberName = subscriberInstance;  
string publisherName = publisherInstance;  
string publicationName = "AdvWorksSalesOrdersMerge";  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define the pull subscription.  
    subscription = new MergePullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription exists, then start the synchronization.  
    if (subscription.LoadProperties())  
    {  
        // Check that we have enough metadata to start the agent.  
        if (subscription.PublisherSecurity != null || subscription.DistributorSecurity != null)  
        {  
            // Synchronously start the Merge Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize();  
        }  
        else  
        {  
            throw new ApplicationException("There is insufficent metadata to " +  
                "synchronize the subscription. Recreate the subscription with " +  
                "the agent job or supply the required agent properties at run time.");  
        }  
    }  
    else  
    {  
        // Do something here if the pull subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exist on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement appropriate error handling here.  
    throw new ApplicationException("The subscription could not be " +  
        "synchronized. Verify that the subscription has " +  
        "been defined correctly.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define the server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define the pull subscription.  
    subscription = New MergePullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription exists, then start the synchronization.  
    If subscription.LoadProperties() Then  
        ' Check that we have enough metadata to start the agent.  
        If Not subscription.PublisherSecurity Is Nothing Or subscription.DistributorSecurity Is Nothing Then  
  
            ' Output agent messages to the console.   
            subscription.SynchronizationAgent.OutputVerboseLevel = 1  
            subscription.SynchronizationAgent.Output = ""  
  
            ' Synchronously start the Merge Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize()  
        Else  
            Throw New ApplicationException("There is insufficent metadata to " + _  
             "synchronize the subscription. Recreate the subscription with " + _  
             "the agent job or supply the required agent properties at run time.")  
        End If  
    Else  
        ' Do something here if the pull subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exist on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Implement appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be " + _  
     "synchronized. Verify that the subscription has " + _  
     "been defined correctly.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 该示例使用 Web 同步将请求订阅与合并发布进行同步。 该订阅是在没有代理作业和相关订阅元数据的情况下创建的，因此，必须同步启动代理，并提供更多的订阅信息。  
  
```csharp  
// Define the server, publication, and database names.  
string subscriberName = subscriberInstance;  
string publisherName = publisherInstance;  
string distributorName = distributorInstance;  
string publicationName = "AdvWorksSalesOrdersMerge";  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
string hostname = @"adventure-works\garrett1";  
string webSyncUrl = "https://" + publisherInstance + "/SalesOrders/replisapi.dll";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
MergePullSubscription subscription;  
MergeSynchronizationAgent agent;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define the pull subscription.  
    subscription = new MergePullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription exists, then start the synchronization.  
    if (subscription.LoadProperties())  
    {  
        // Get the agent for the subscription.  
        agent = subscription.SynchronizationAgent;  
  
        // Check that we have enough metadata to start the agent.  
        if (agent.PublisherSecurityMode == null)  
        {  
            // Set the required properties that could not be returned  
            // from the MSsubscription_properties table.   
            agent.PublisherSecurityMode = SecurityMode.Integrated;  
            agent.DistributorSecurityMode = SecurityMode.Integrated;  
            agent.Distributor = publisherName;  
            agent.HostName = hostname;  
  
            // Set optional Web synchronization properties.  
            agent.UseWebSynchronization = true;  
            agent.InternetUrl = webSyncUrl;  
            agent.InternetSecurityMode = SecurityMode.Standard;  
            agent.InternetLogin = winLogin;  
            agent.InternetPassword = winPassword;  
        }  
        // Enable agent output to the console.  
        agent.OutputVerboseLevel = 1;  
        agent.Output = "";  
  
        // Synchronously start the Merge Agent for the subscription.  
        agent.Synchronize();  
    }  
    else  
    {  
        // Do something here if the pull subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exist on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement appropriate error handling here.  
    throw new ApplicationException("The subscription could not be " +  
        "synchronized. Verify that the subscription has " +  
        "been defined correctly.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define the server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
Dim hostname As String = "adventure-works\garrett1"  
Dim webSyncUrl As String = "https://" + publisherInstance + "/SalesOrders/replisapi.dll"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As MergePullSubscription  
Dim agent As MergeSynchronizationAgent  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define the pull subscription.  
    subscription = New MergePullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription exists, then start the synchronization.  
    If subscription.LoadProperties() Then  
        ' Get the agent for the subscription.  
        agent = subscription.SynchronizationAgent  
  
        ' Check that we have enough metadata to start the agent.  
        If agent.PublisherSecurityMode = Nothing Then  
            ' Set the required properties that could not be returned  
            ' from the MSsubscription_properties table.   
            agent.PublisherSecurityMode = SecurityMode.Integrated  
            agent.Distributor = publisherInstance  
            agent.DistributorSecurityMode = SecurityMode.Integrated  
            agent.HostName = hostname  
  
            ' Set optional Web synchronization properties.  
            agent.UseWebSynchronization = True  
            agent.InternetUrl = webSyncUrl  
            agent.InternetSecurityMode = SecurityMode.Standard  
            agent.InternetLogin = winLogin  
            agent.InternetPassword = winPassword  
        End If  
  
        ' Enable agent logging to the console.  
        agent.OutputVerboseLevel = 1  
        agent.Output = ""  
  
        ' Synchronously start the Merge Agent for the subscription.  
        agent.Synchronize()  
    Else  
        ' Do something here if the pull subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exist on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Implement appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be " + _  
     "synchronized. Verify that the subscription has " + _  
     "been defined correctly.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
## 另请参阅  
 [同步数据](../../relational-databases/replication/synchronize-data.md)   
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  