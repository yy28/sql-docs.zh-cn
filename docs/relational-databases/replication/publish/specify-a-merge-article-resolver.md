---
title: "指定合并项目冲突解决程序 | Microsoft Docs"
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
  - "项目 [SQL Server 复制], 冲突解决"
  - "冲突解决 [SQL Server 复制], 合并复制"
  - "合并复制冲突解决 [SQL Server 复制], 合并项目冲突解决程序"
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 指定合并项目冲突解决程序
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定合并项目冲突解决程序。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
-   **指定合并项目冲突解决程序，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   合并复制允许使用下列类型的项目冲突解决程序：  
  
    -   默认冲突解决程序。 默认冲突解决程序的行为取决于订阅是客户端订阅还是服务器订阅。 有关指定订阅类型的详细信息，请参阅 [指定合并订阅类型和冲突解决优先级 & #40;SQL Server Management Studio & #41;](../../../relational-databases/replication/specify a merge subscription type and conflict resolution priority.md)。  
  
    -   您编写的自定义冲突解决程序，可以是业务逻辑处理程序（以托管代码编写）或基于 COM 的自定义冲突解决程序。 有关详细信息，请参阅 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。 如果您需要实现为每个已复制的行，而不仅仅是针对冲突行，请参阅执行的自定义逻辑 [为合并项目实现业务逻辑处理程序](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
    -   标准的基于 COM 的冲突解决程序，它又包括在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   若要使用默认冲突解决程序以外的其他冲突解决程序，必须将该冲突解决程序复制到运行合并代理的计算机并对其进行注册（如果使用的是业务逻辑处理程序，还必须在发布服务器上注册）。 合并代理可以运行于：  
  
    -   分发服务器，对于推送订阅  
  
    -   订阅服务器，对于请求订阅  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) 服务器，对于使用 Web 同步的请求订阅  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 冲突解决程序注册后，指定项目应在使用冲突解决程序 **冲突解决程序** 的选项卡上 **项目属性-\< 项目>** 对话框中，可以在新建发布向导和 **发布属性-\< 发布>** 对话框。 有关使用向导和访问对话框中的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md) 和 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 指定冲突解决程序  
  
1.  在 **文章** 新建发布向导的页面或 **发布属性-\< 发布>** 对话框中，选择一个表。  
  
2.  单击 **“项目属性”**，再单击 **“设置突出显示的表项目的属性”**。  
  
3.  在 **项目属性-\< 项目>** 页上，单击 **冲突解决程序** 选项卡。  
  
4.  选择 **使用自定义冲突解决程序 （已在分发服务器上注册）**, ，然后在列表中，单击冲突解决程序。  
  
5.  如果冲突解决程序要求输入 （如列名），指定在 **输入所需的冲突解决程序信息** 文本框。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  对需要冲突解决程序的每个项目重复此过程。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 注册自定义冲突解决程序  
  
1.  如果打算注册您自己的自定义冲突解决程序，请创建以下类型之一：  
  
    -   作为业务逻辑处理程序的基于托管代码的冲突解决程序。 有关详细信息，请参阅 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
    -   基于存储过程的冲突解决程序和基于 COM 的冲突解决程序。 有关详细信息，请参阅 [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)。  
  
2.  若要确定是否已经注册所需冲突解决程序，请执行 [sp_enumcustomresolvers & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 在任何数据库上的发布服务器。 这将显示自定义冲突解决程序的说明以及在分发服务器上注册的每个基于 COM 的冲突解决程序的类标识符 (CLSID)，或者显示在分发服务器上注册的每个业务逻辑处理程序的托管程序集相关信息。  
  
3.  如果尚未注册所需的自定义冲突解决程序，执行 [sp_registercustomresolver & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) 在分发服务器上。 指定的冲突解决程序的名称 **@article_resolver**; 对于业务逻辑处理程序，这是该程序集的友好名称。 对于基于 COM 的冲突解决程序，指定的 dll 的 CLSID **@resolver_clsid**, ，对于业务逻辑处理程序中，指定的值 **true** 为 **@is_dotnet_assembly**, ，为程序集的名称 **@dotnet_assembly_name**, ，和类，并重写的完全限定名称 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 为 **@dotnet_class_name**。  
  
    > [!NOTE]  
    >  如果业务逻辑处理程序程序集未部署与合并代理可执行文件的相同目录中，与应用程序的相同目录中，同步启动合并代理程序，或者在全局程序集缓存 (GAC) 中，您需要指定的完整路径的程序集名称和 **@dotnet_assembly_name**。  
  
4.  如果冲突解决程序是基于 COM 的冲突解决程序，则：  
  
    -   将自定义冲突解决程序 DLL 复制到分发服务器（对于推送订阅）或订阅服务器（对于请求订阅）。  
  
        > [!NOTE]  
        >  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 在找不到自定义冲突解决程序 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM 目录。  
  
    -   使用 regsvr32.exe 向操作系统注册自定义冲突解决程序 DLL。 例如，从命令提示符处执行以下命令可注册 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 累加性冲突解决程序：  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  如果冲突解决程序为业务逻辑处理程序，部署与合并代理可执行文件 (replmerg.exe) 位于同一文件夹中的程序集或指定的文件夹中的应用程序时，将调用合并代理所在的文件夹 **@dotnet_assembly_name** 在步骤 3 中的参数。  
  
    > [!NOTE]  
    >  合并代理可执行文件的默认安装位置为 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM。  
  
#### 定义合并项目时指定自定义冲突解决程序  
  
1.  如果您打算使用自定义冲突解决程序，请通过上述过程创建和注册冲突解决程序。  
  
2.  在发布服务器上，执行 [sp_enumcustomresolvers & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 记下在所需的自定义解析程序的名称 **值** 结果集的字段。  
  
3.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定从步骤 2 获得的冲突解决程序的名称 **@article_resolver** 和任何所需的自定义冲突解决程序使用的输入 **@resolver_info** 参数。 有关存储的基于过程的自定义冲突解决程序， **@resolver_info** 是存储过程的名称。 有关所需的输入的解析程序提供的详细信息 [!INCLUDE[msCoName](../../../includes/msconame-md.md)], ，请参阅 [Microsoft 基于 COM 的冲突解决程序](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md)。  
  
#### 为现有合并项目指定或更改自定义冲突解决程序  
  
1.  若要确定是否已定义的自定义冲突解决程序一篇文章，或获取冲突解决程序的名称，执行 [sp_helpmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 如果没有为项目定义的自定义冲突解决程序，其名称将显示在 **article_resolver** 字段。 冲突解决程序提供的任何输入将显示在 **resolver_info** 结果集的字段。  
  
2.  在发布服务器上，执行 [sp_enumcustomresolvers & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 记下在所需的自定义解析程序的名称 **值** 结果集的字段。  
  
3.  在发布服务器上对发布数据库中，执行 [sp_changemergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 将值指定为 **article_resolver**, ，包括业务逻辑处理程序的完整路径为 **@property**, ，以及从步骤 2 获得所需的自定义解析程序的名称 **@value**。  
  
4.  若要更改任何所需的输入的自定义冲突解决程序，请执行 [sp_changemergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 电子邮件了。 将值指定为 **resolver_info** 为 **@property** 和任何所需的输入的自定义冲突解决程序 **@value**。 有关存储的基于过程的自定义冲突解决程序， **@resolver_info** 是存储过程的名称。 有关所需的输入的详细信息，请参阅 [Microsoft 基于 COM 的冲突解决程序](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md)。  
  
#### 撤消注册自定义冲突解决程序  
  
1.  在发布服务器上，执行 [sp_enumcustomresolvers & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 记下要删除在自定义冲突解决程序的名称 **值** 结果集的字段。  
  
2.  执行 [sp_unregistercustomresolver & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) 在分发服务器上。 指定步骤 1 中的自定义冲突解决程序的完整名称 **@article_resolver**。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 本示例创建了一个新项目，并指定当发生冲突时，将使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 平均化冲突解决程序计算 **UnitPrice** 列的平均值。  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 本示例更改了一个项目以指定当发生冲突时，将使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 累加性冲突解决程序计算 **UnitsOnOrder** 列的总和。  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## 另请参阅  
 [高级合并复制冲突的检测和解决](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [实现合并项目的业务逻辑处理程序](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  