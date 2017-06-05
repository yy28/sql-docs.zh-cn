---
title: "指定合并项目冲突解决程序 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
- merge replication conflict resolution [SQL Server replication], merge article resolvers
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2934cf0580b44b6a496f9dae4d5cd297cd8717d7
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="specify-a-merge-article-resolver"></a>指定合并项目冲突解决程序
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
  
    -   默认冲突解决程序。 默认冲突解决程序的行为取决于订阅是客户端订阅还是服务器订阅。 有关如何指定订阅类型的详细信息，请参阅[指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio)](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)。  
  
    -   您编写的自定义冲突解决程序，可以是业务逻辑处理程序（以托管代码编写）或基于 COM 的自定义冲突解决程序。 有关详细信息，请参阅 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)中指定合并项目冲突解决程序。 如果需要实现针对复制的每一行而非只是针对冲突行执行的自定义逻辑，请参阅 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)中指定合并项目冲突解决程序。  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]附带的基于 COM 的标准冲突解决程序。  
  
-   若要使用默认冲突解决程序以外的其他冲突解决程序，必须将该冲突解决程序复制到运行合并代理的计算机并对其进行注册（如果使用的是业务逻辑处理程序，还必须在发布服务器上注册）。 合并代理可以运行于：  
  
    -   分发服务器，对于推送订阅  
  
    -   订阅服务器，对于请求订阅  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) 服务器，对于使用 Web 同步的请求订阅  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 注册冲突解决程序之后，在“项目属性 - \<项目>”对话框（可在新建发布向导和“发布属性 - \<发布>”对话框中使用）的“冲突解决程序”选项卡上指定项目应使用该冲突解决程序。 有关如何使用该向导和如何访问该对话框的详细信息，请参阅[创建发布](../../../relational-databases/replication/publish/create-a-publication.md)和[查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-a-resolver"></a>指定冲突解决程序  
  
1.  在新建发布向导或“发布属性 - \<发布>”对话框的“项目”页上，选择一个表。  
  
2.  单击 **“项目属性”**，再单击 **“设置突出显示的表项目的属性”**。  
  
3.  在“项目属性 - \<项目>”页上，单击“冲突解决程序”选项卡。  
  
4.  选择 **“使用自定义冲突解决程序（已在分发服务器上注册）”**，然后在列表中单击冲突解决程序。  
  
5.  如果冲突解决程序需要输入信息（例如列名），请在 **“输入冲突解决程序所需的信息”** 文本框中指定。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  对需要冲突解决程序的每个项目重复此过程。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-register-a-custom-conflict-resolver"></a>注册自定义冲突解决程序  
  
1.  如果打算注册您自己的自定义冲突解决程序，请创建以下类型之一：  
  
    -   作为业务逻辑处理程序的基于托管代码的冲突解决程序。 有关详细信息，请参阅 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
    -   基于存储过程的冲突解决程序和基于 COM 的冲突解决程序。 有关详细信息，请参阅 [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)。  
  
2.  若要确定所需冲突解决程序是否已注册，请在发布服务器上对任意数据库执行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)。 这将显示自定义冲突解决程序的说明以及在分发服务器上注册的每个基于 COM 的冲突解决程序的类标识符 (CLSID)，或者显示在分发服务器上注册的每个业务逻辑处理程序的托管程序集相关信息。  
  
3.  如果尚未注册所需的自定义解决程序，请在分发服务器上执行 [sp_registercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)。 为 **@article_resolver**指定冲突解决程序的名称；对于业务逻辑处理程序，此为程序集的友好名称。 对于基于 COM 的冲突解决程序，请为 **@resolver_clsid** 指定 DLL 的 CLSID；对于业务逻辑处理程序，请为 **@is_dotnet_assembly** 指定值 **true**，为 **@dotnet_assembly_name** 指定程序集名称，并为 **@dotnet_class_name** 指定可覆盖 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 的类的完全限定名称。  
  
    > [!NOTE]  
    >  如果业务逻辑处理程序程序集与合并代理可执行文件不是部署在同一目录中，与同步启动合并代理的应用程序不是部署在同一目录中，或者不是部署在全局程序集缓存 (GAC) 中，则需要为 **@dotnet_assembly_name**中指定合并项目冲突解决程序。  
  
4.  如果冲突解决程序是基于 COM 的冲突解决程序，则：  
  
    -   将自定义冲突解决程序 DLL 复制到分发服务器（对于推送订阅）或订阅服务器（对于请求订阅）。  
  
        > [!NOTE]  
        >  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 自定义冲突解决程序位于 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM 目录中。  
  
    -   使用 regsvr32.exe 向操作系统注册自定义冲突解决程序 DLL。 例如，从命令提示符处执行以下命令可注册 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 累加性冲突解决程序：  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  如果冲突解决程序为业务逻辑处理程序，则将程序集与合并代理可执行文件 (replmerg.exe) 部署在同一文件夹中，与调用合并代理的应用程序部署在同一文件夹中，或者部署在步骤 3 中为 **@dotnet_assembly_name** 参数指定的文件夹中。  
  
    > [!NOTE]  
    >  合并代理可执行文件的默认安装位置为 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM。  
  
#### <a name="to-specify-a-custom-resolver-when-defining-a-merge-article"></a>定义合并项目时指定自定义冲突解决程序  
  
1.  如果您打算使用自定义冲突解决程序，请通过上述过程创建和注册冲突解决程序。  
  
2.  在发布服务器上执行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)，并记下所需自定义冲突解决程序在结果集的 **value** 字段中的名称。  
  
3.  在发布服务器上，对发布数据库执行 [sp_addmergearticle (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 为 **@article_resolver** 指定从步骤 2 获得的冲突解决程序的名称，并使用 **@resolver_info** 参数指定自定义冲突解决程序所需的任何输入内容。 对于基于存储过程的自定义冲突解决程序， **@resolver_info** 为存储过程的名称。 有关 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 提供的冲突解决程序所需输入内容的详细信息，请参阅 [Microsoft 基于 COM 的冲突解决程序](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
#### <a name="to-specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>为现有合并项目指定或更改自定义冲突解决程序  
  
1.  若要确定是否已为项目定义自定义冲突解决程序，或要获取冲突解决程序的名称，请执行 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 如果已为项目定义自定义冲突解决程序，则其名称将显示在 **article_resolver** 字段中。 为冲突解决程序提供的任何输入内容都将显示在结果集的 **resolver_info** 字段中。  
  
2.  在发布服务器上执行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)，并记下所需自定义冲突解决程序在结果集的 **value** 字段中的名称。  
  
3.  在发布服务器上，对发布数据库执行 [sp_changemergearticle (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 将 **article_resolver**的值指定为 **@property**（包括业务逻辑处理程序的完整路径），并为 **@value**中指定合并项目冲突解决程序。  
  
4.  若要更改自定义冲突解决程序所需的任何输入内容，请再次执行 [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 将 **resolver_info** @is_dotnet_assembly **@property** 并为 **@value**中指定合并项目冲突解决程序。 对于基于存储过程的自定义冲突解决程序， **@resolver_info** 为存储过程的名称。 有关所需输入内容的详细信息，请参阅 [Microsoft 基于 COM 的冲突解决程序](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
#### <a name="to-unregister-a-custom-conflict-resolver"></a>撤消注册自定义冲突解决程序  
  
1.  在发布服务器上执行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)，并记下要删除的自定义冲突解决程序在结果集的 **value** 字段中的名称。  
  
2.  在分发服务器上执行 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)。 为 **@article_resolver**中指定合并项目冲突解决程序。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 本示例创建了一个新项目，并指定当发生冲突时，将使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 平均化冲突解决程序计算 **UnitPrice** 列的平均值。  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 本示例更改了一个项目以指定当发生冲突时，将使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 累加性冲突解决程序计算 **UnitsOnOrder** 列的总和。  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## <a name="see-also"></a>另请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
