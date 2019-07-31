---
title: 指定合并复制属性 |Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], about merge replication
- merge replication [SQL Server replication]
ms.assetid: ff87c368-4c00-4e48-809d-ea752839551e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 033999701141387ee63712a8a9ce055ad3f55cb1
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661307"
---
# <a name="specify-merge-replication-properties"></a>指定合并复制属性
本主题说明如何为合并复制指定各种属性。 


## <a name="download-only"></a>仅限下载
  本部分介绍如何使用[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[tsql](../../../includes/tsql-md.md)]在中指定合并表项目仅用于下载。 仅用于下载的项目是为具有不在订阅服务器上更新的数据的应用程序设计的。 有关详细信息，请参阅[使用仅下载项目优化合并复制性能](../merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
 
  
###  <a name="limitations-and-restrictions"></a>限制和局限  
  
-   如果在初始化订阅后指定项目仅用于下载，则所有收到该项目的客户端订阅必须重新初始化。 服务器订阅不必重新初始化。 有关属性更改的影响的详细信息，请参阅[更改发布和项目属性](change-publication-and-article-properties.md)。  
  
### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
 在新建发布向导的“项目”  页或“项目属性 - \<项目>”  对话框的“属性”  选项卡上指定项目仅用于下载。 新建发布向导和“发布属性 - \<发布>”  对话框中提供了该对话框。 有关如何使用该向导和如何访问该对话框的详细信息，请参阅[创建发布](../publish/create-a-publication.md)和[查看和修改发布属性](../publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>在“项目”页上指定项目仅用于下载  
  
-   在新建发布向导的 **“项目”** 页上，选择一个表，然后选中复选框 **“已选中的表仅用于下载”** 。 
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>在“项目属性 - \<项目>”对话框的“属性”选项卡上指定项目仅用于下载  
  
1.  在新建发布向导或“发布属性 - \<发布>”  对话框的“项目”  页上，选择一个表，然后单击“项目属性”  。    
2.  单击 **“设置突出显示的表项目的属性”** 或 **“设置所有表项目的属性”** 。    
3.  在“项目属性 - \<项目>”  对话框的“属性”  选项卡的“目标对象”  部分中，为“同步方向”  指定以下值之一：    
    -   **下载到订阅服务器，禁止订阅服务器更改**    
    -   **下载到订阅服务器，允许订阅服务器更改**  
  
4.  如果处于“发布属性 - \<发布>”对话框中，请单击“确定”以保存并关闭该对话框。      

###  <a name="using-transact-sql"></a>使用 Transact-SQL  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>指定新合并表项目仅用于下载    
1.  执行[sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql), 为参数 **\@subscriber_upload_options**指定值**1**或**2** 。 这些数字分别与以下行为相对应：  
  
    -   **0** - 无限制（默认值）。 将订阅服务器上所做的更改上载到发布服务器。    
    -   **1** - 允许在订阅服务器上进行更改，但不会将它们上载到发布服务器。    
    -   **2** - 不允许在订阅服务器上进行更改。  
  
        > [!NOTE]  
        >  如果某个项目的源表已经在另一个发布中发布, 则这两个项目的 **\@subscriber_upload_options**值必须相同。  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>修改现有合并表项目以使其仅用于下载  
  
1.  若要确定项目是否仅用于下载，请执行 [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)。 记下结果集中该项目的 **upload_options** 值。    
2.  如果步骤1中返回的值为**0**, 则执行[sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), 将**subscriber_upload_options**的值指定为 **\@属性**, 将值**1**指定为 **\@force_invalidate_snapshot**  **\@** **和\@force_reinit_subscription**, 值为**1**或**2** , 对应于以下行为:  
  
    -   **1** - 允许在订阅服务器上进行更改，但不会将它们上载到发布服务器。    
    -   **2** - 不允许在订阅服务器上进行更改。  
  
        > [!NOTE]  
        >  如果某个项目的源表已经在另一个发布中发布，则两个项目的仅用于下载行为必须相同。  
 
## <a name="interactive-conflict-resolution">交互式冲突解决</a>
[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制提供交互式冲突解决程序，可用于在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 同步管理器中进行按需同步过程中手动解决冲突。 启用交互式冲突解决方法后，在同步过程中即可使用交互式冲突解决程序来交互式解决冲突。 交互式冲突解决程序可以通过 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 同步管理器获取。 有关详细信息，请参阅[使用 Windows 同步管理器同步订阅（Windows 同步管理器）](../synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
    
###  <a name="Recommendations"></a> 建议  
  
-   如果在 Windows 同步管理器以外执行同步（如 SQL Server Management Studio 或复制监视器中的计划同步或按需同步），则会使用为项目指定的默认冲突解决方法自动解决冲突，而无需用户干预。 有关详细信息，请参阅 [Interactive Conflict Resolution](../merge/advanced-merge-replication-conflict-interactive-resolution.md)。  
  
###  <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
  
#### <a name="enable-interactive-conflict-resolution-for-an-article"></a>为项目启用交互式冲突解决方法  
  
1.  在新建发布向导或“发布属性 - \<发布>”  对话框的“项目”  页上，选择一个表。 有关如何使用该向导和如何访问该对话框的详细信息，请参阅[创建发布](create-a-publication.md)和[查看和修改发布属性](view-and-modify-publication-properties.md)。    
2.  单击 **“项目属性”** ，然后单击 **“设置突出显示的表项目的属性”** 或 **“设置所有表项目的属性”** 。    
3.  在“项目属性 - \<项目>”  或“项目属性 - \<项目类型>”  页上，单击“冲突解决程序”  选项卡。    
4.  选择 **“允许订阅服务器在按需同步时交互式解决冲突”** 。    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
6.  如果处于“发布属性 - \<发布>”  对话框中，请单击“确定”  以保存并关闭该对话框。  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>指定订阅应使用交互式冲突解决方法  
  
1.  在“订阅属性 - \<Subscriber>:\<SubscriptionDatabase>”对话框中，为“以交互方式解决冲突”选项指定“True”值**   。 有关访问此对话框的详细信息，请参阅 [View and Modify Push Subscription Properties](../view-and-modify-push-subscription-properties.md) 和 [View and Modify Pull Subscription Properties](../view-and-modify-pull-subscription-properties.md)。 
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="using-transact-sql"></a>使用 Transact-SQL  
 创建合并发布的请求订阅时，您可以编程方式指定订阅服务器将使用此图形界面来解决项目冲突。 只有支持此选项的项目中的冲突才会显示在交互式冲突解决程序中。  
  
#### <a name="create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>创建使用交互式冲突解决程序的合并请求订阅  
  
1.  在发布服务器上, 对发布数据库执行[sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), 并指定 **\@发布**。 注意结果集中其交互式冲突解决程序将被使用的每个项目的 **allow_interactive_resolver** 值。    
    -   如果该值为 **1**，将使用交互式冲突解决程序。    
    -   如果该值为 **0**，则您必须首先启用每个项目的交互式冲突解决程序。 为此, 请执行[sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), 并指定 **\@发布**、  **\@项目**、  **\@属性**的值**allow_interactive_resolver**和值**true** **作为\@值**。    
2.  在订阅服务器上，对订阅数据库执行 [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)。 有关详细信息，请参阅 [创建请求订阅](../create-a-pull-subscription.md)。    
3.  在订阅服务器的订阅数据库中，执行 [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)，同时指定下列参数：  
  
    -   **\@发布服务器**、  **publisher_db\@** (已发布的数据库) 和发布。  **\@**    
    -   Enabled_for_syncmgr 的值为**true** 。  **\@**    
    -   Use_interactive_resolver 的值为**true** 。  **\@**    
    -   合并代理所需的安全帐户信息。 有关详细信息，请参阅 [Create a Pull Subscription](../create-a-pull-subscription.md)。    
4.  在发布服务器的发布数据库中，执行 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)。  
  
#### <a name="define-an-article-that-supports-the-interactive-resolver"></a>定义支持交互式冲突解决程序的项目  
  
在发布服务器上，对发布数据库执行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 指定项目所属的 **\@**  **\@** 发布的名称、项目的 **\@名称、要**为 source_object 发布的数据库对象, 以及值对于 **\@allow_interactive_resolver**为**true** 。 有关详细信息，请参阅 [定义项目](define-an-article.md)。  

## <a name="specify-the-conflict-tracking-and-resolution-level"></a>指定冲突跟踪和解决方法级别 
在同步对合并发布的订阅时，复制检查是否存在因对发布服务器和订阅服务器上的相同数据进行更改而导致的冲突。 可以指定是在行级别检测冲突（即对行的任何更改都视为冲突），还是在列级别检测冲突（即只有更改了相同的行和列时才视作冲突）。 项目的冲突解决在行级别执行。 有关在使用逻辑记录时检测和解决冲突的详细信息，请参阅 [Detecting and Resolving Conflicts in Logical Records](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)。  
  

  
###  <a name="Restrictions"></a> 限制和局限  
  
-   如果在初始化订阅后修改跟踪级别，必须重新初始化这些订阅。 有关属性更改的影响的详细信息，请参阅[更改发布和项目属性](../publish/change-publication-and-article-properties.md)。    
-   对于行级和列级跟踪，始终在行级执行冲突解决：入选行将覆盖落选行。 合并复制还允许您指定在逻辑记录级跟踪和解决冲突，但 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]没有提供这些选项。 有关在复制存储过程中设置这些选项的信息，请参阅 [定义合并表项目间的逻辑记录关系](../publish/define-a-logical-record-relationship-between-merge-table-articles.md)。  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在“项目属性”  对话框的“属性“  选项卡上指定合并项目的行级或列级跟踪，该对话框可以在新发布向导和“发布属性 - \<发布>”  对话框中找到。 有关如何使用该向导和如何访问该对话框的详细信息，请参阅[创建发布](create-a-publication.md)和[查看和修改发布属性](../publish/view-and-modify-publication-properties.md)。  
  
#### <a name="specify-row--or-column-level-tracking"></a>指定行级别或列级别跟踪  
  
1.  在新建发布向导或“发布属性 - \<发布>”  对话框的“项目”  页上，选择一个表。    
2.  单击 **“项目属性”** ，然后单击 **“设置突出显示的表项目的属性”** 或 **“设置所有表项目的属性”** 。   
3.  在“项目属性 \<项目>”对话框的“属性”选项卡上，为“跟踪级别”属性选择以下值之一：    “行级别跟踪”或“列级别跟踪”   。    
4.  如果处于“发布属性 - \<发布>”对话框中，请单击“确定”以保存并关闭该对话框。    
  
###  <a name="using-transact-sql"></a>使用 Transact-SQL  
  
#### <a name="specify-conflict-tracking-options-for-a-new-merge-article"></a>为新的合并项目指定冲突跟踪选项  
  
1.  在发布服务器上, 对发布数据库执行[sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) , 并为 **\@column_tracking**指定以下值之一:  
  
    -   **true** - 为项目使用列级别跟踪。    
    -   **false** - 使用行级别跟踪，这是默认值。  
  
#### <a name="change-conflict-tracking-options-for-a-merge-article"></a>更改合并项目的冲突跟踪选项  
  
1.  若要确定某个合并项目的冲突跟踪选项，请执行 [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)。 请注意项目的结果集中 **column_tracking** 选项的值。 值为 **1** 表明使用的是列级别的跟踪，值为 **0** 表明使用的是行级别的跟踪。    
2.  在发布服务器上，对发布数据库执行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 为 "  **\@属性**" 指定**column_tracking**值, 并为 **\@"值**" 指定以下值之一:
    -   **true** - 为项目使用列级别跟踪。
    -   **false** - 使用行级别跟踪，这是默认值。  
  
     将 **\@force_invalidate_snapshot**和**force_reinit_subscription的值都指定为1。\@**  

## <a name="tracking-deletes"></a>跟踪删除

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 默认情况下，合并复制同步发布服务器和订阅服务器之间的 DELETE 命令。 您可以使用合并复制来保留订阅数据库中的行，即使这些行已从发布中删除，反之亦然。 您可以通过编程方式指定在创建新项目时忽略 DELETE 命令，或者可以使用复制存储过程在以后启用此功能。  
  
> [!IMPORTANT]  
>  启用此功能将导致无法收敛，也就是说，位于订阅服务器上的数据将无法准确反映发布服务器上的数据。 您必须实现自己的用于手动删除已删除行的机制。  
  
### <a name="specify-that-deletes-be-ignored-for-a-new-merge-article"></a>指定对新合并项目忽略删除  
  
1.  在发布服务器上，对发布数据库执行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 将的值`false`指定为 **\@delete_tracking**。 有关详细信息，请参阅 [定义项目](../publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  如果某个项目的源表已在另一个发布中发布，则两个项目的 **delete_tracking** 值必须相同。  
  
### <a name="specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>指定对现有合并项目忽略删除  
  
1.  若要确定是否对项目启用了错误补偿，请执行 [sp_helpmergearticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) 并注意结果集中的 **delete_tracking** 值。 如果该值为 **0**，则删除已被忽略。    
2.  如果步骤 1 的值为 **1**，则在发布服务器上对发布数据库执行 [sp_changemergearticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 **为\@属性**指定**delete_tracking**值, 并将`false`值指定 **\@为。**  
  
    > [!NOTE]  
    >  如果某个项目的源表已在另一个发布中发布，则两个项目的 **delete_tracking** 值必须相同。  
  
## <a name="processing-order"></a>处理顺序
  通过使用合并复制，您可以指定在同步过程中合并代理处理项目的顺序。 您可以在使用复制存储过程创建项目时以编程方式为每个项目指定顺序。 项目按值的由低到高顺序进行处理。 如果两个项目具有相同值，将对其进行并发处理。 有关详细信息，请参阅[指定合并复制属性](../publish/specify-merge-replication-properties.md)。  

  从 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]开始，可以覆盖合并发布的项目默认处理顺序。 例如，如果通过触发器定义引用完整性而这些触发器又必须按某顺序激发，以上操作就会很有用。 

### <a name="how-processing-order-is-determined"></a>如何确定处理顺序  
 合并同步过程中，项目在默认情况下按照对象间相关性要求的顺序处理，包括基表中定义的声明性引用完整性 (DRI) 约束。 处理涉及将更改枚举到表，然后应用这些更改。 若不存在 DRI，但在表项目之间存在联接筛选器或逻辑记录，则就以筛选器和逻辑记录要求的顺序处理项目。 未通过 DRI、联接筛选器、逻辑记录或其他依赖关系与任何其他项目相关的项目，根据 [sysmergearticles (Transact-SQL)](/sql/relational-databases/system-tables/sysmergearticles-transact-sql) 系统表中的项目别名进行处理。  
  
 考虑一个包含 **SalesOrderHeader** 表和 **SalesOrderDetail** 表的发布，并且 **SalesOrderHeader** 表中具有主键列 **SalesOrderID** 而 **SalesOrderDetail** 表中具有对应的外键列 **SalesOrderID** 。 同步过程中，合并复制通过在 **SalesOrderDetail** 中插入相关行之前先在 **SalesOrderHeader**中插入某些新行的方式来防止违反外键。 同样，要先从 **SalesOrderDetail** 中删除行，然后才从 **SalesOrderHeader**中删除相关行。  
  
 但是，在某些应用程序中，通过数据库触发器（或者在应用程序级，而不是通过 DRI）强制引用完整性。 考虑上述具有引用完整性的发布（而不是 DRI）， **SalesOrderDetail** 表可能会有一个插入触发器以确保在允许插入之前 **SalesOrderHeader** 表中存在相关行。 **SalesOrderHeader** 可能有一个删除触发器以确保在允许删除之前 **SalesOrderDetail** 中没有相关行。 由于合并复制无法在激发触发器之前确定触发器的结果，所以在确定项目的处理顺序时，合并复制不会考虑触发器。 同样，复制也不会考虑在应用程序级定义的约束。  
  
 通过触发器或在应用程序级维护引用完整性时，您应该指定项目应处理的顺序。 在有关触发器的示例中，需要指定在处理 **SalesOrderDetail** 之前先处理 **SalesOrderHeader**表，因为项目排序是根据插入顺序进行的。 合并复制会自动反转删除顺序。 不进行项目排序也不会导致合并复制失败，因为即使违反约束，合并代理也会继续处理项目；然后它会在处理完其他项目后重试所有过去失败的操作。 指定项目顺序仅避免重试以及其他与其相关联的处理。 如果指定了错误顺序（比如，导致详细记录在标题记录前处理的顺序），合并复制会重试处理直到成功。  

### <a name="new-article"></a>新文章
  
1.  在发布服务器上，对发布数据库执行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 指定一个整数值, 该值表示针对 **\@processing_order**的项目的处理顺序。 有关详细信息，请参阅 [定义项目](define-an-article.md)。  
  
    > [!NOTE]  
    >  创建指定了顺序的项目时，应在项目顺序值之间留有间隔。 这样便于以后设置新值。 例如, 如果有三个项目需要指定固定处理顺序, 请将 **\@processing_order**的值分别设置为10、20和 30, 而不是分别设置为1、2和3。  
  
### <a name="existing-article"></a>现有项目
  
1.  若要确定项目的处理顺序，请执行 [sp_helpmergearticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)，并记下结果集中的 **processing_order** 值。  
  
2.  在发布服务器上，对发布数据库执行 [sp_changemergearticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 为 **\@** **属性\@** 指定值 processing_order, 并将一个整数值指定为值的处理顺序。  



## <a name="see-also"></a>请参阅  
 [使用条件性删除跟踪优化合并复制性能](../merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
 [Detecting and Resolving Conflicts in Logical Records](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [定义合并表项目间的逻辑记录关系](define-a-logical-record-relationship-between-merge-table-articles.md)   
 [检测并解决合并复制冲突](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [使用仅下载项目优化合并复制性能](../merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](define-an-article.md)   
 [查看和修改项目属性](view-and-modify-article-properties.md)  