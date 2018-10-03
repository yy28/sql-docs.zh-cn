---
title: 指定合并项目的交互式冲突解决方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], interactive resolvers
- interactive conflict resolution [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c5153a9c3a21366ae83b1576b6d3c4e61725ff8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709055"
---
# <a name="specify-interactive-conflict-resolution-for-merge-articles"></a>指定合并项目的交互式冲突解决
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定合并项目的交互式冲突解决方法。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制提供交互式冲突解决程序，可用于在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 同步管理器中进行按需同步过程中手动解决冲突。 启用交互式冲突解决方法后，在同步过程中即可使用交互式冲突解决程序来交互式解决冲突。 交互式冲突解决程序可以通过 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 同步管理器获取。 有关详细信息，请参阅[使用 Windows 同步管理器同步订阅（Windows 同步管理器）](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
-   **指定合并项目的交互式冲突解决办法，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   如果在 Windows 同步管理器以外执行同步（如 SQL Server Management Studio 或复制监视器中的计划同步或按需同步），则会使用为项目指定的默认冲突解决方法自动解决冲突，而无需用户干预。 有关详细信息，请参阅 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-enable-interactive-conflict-resolution-for-an-article"></a>为项目启用交互式冲突解决方法  
  
1.  在新建发布向导或“发布属性 - \<发布>”对话框的“项目”页上，选择一个表。 有关如何使用该向导和如何访问该对话框的详细信息，请参阅[创建发布](../../../relational-databases/replication/publish/create-a-publication.md)和[查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
2.  单击 **“项目属性”**，然后单击 **“设置突出显示的表项目的属性”** 或 **“设置所有表项目的属性”**。  
  
3.  在“项目属性 - \<项目>”或“项目属性 - \<项目类型>”页上，单击“冲突解决程序”选项卡。  
  
4.  选择 **“允许订阅服务器在按需同步时交互式解决冲突”**。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  如果处于“发布属性 - \<发布>”对话框中，请单击“确定”以保存并关闭该对话框。  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>指定订阅应使用交互式冲突解决方法  
  
1.  在“订阅属性 - \<订阅服务器>: \<订阅数据库>”对话框中，为“交互式解决冲突”选项指定“True”值。 有关访问此对话框的详细信息，请参阅 [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 和 [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 创建合并发布的请求订阅时，您可以编程方式指定订阅服务器将使用此图形界面来解决项目冲突。 只有支持此选项的项目中的冲突才会显示在交互式冲突解决程序中。  
  
#### <a name="to-create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>创建使用交互式冲突解决程序的合并请求订阅  
  
1.  在发布服务器的发布数据库中，执行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)，同时指定 **@publication**中指定合并项目的交互式冲突解决方法。 注意结果集中其交互式冲突解决程序将被使用的每个项目的 **allow_interactive_resolver** 值。  
  
    -   如果该值为 **1**，将使用交互式冲突解决程序。  
  
    -   如果该值为 **0**，则您必须首先启用每个项目的交互式冲突解决程序。 为此，请执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)，同时指定 **@publication**和 **@article**，为 **allow_interactive_resolver** 指定 **@property**值，并将 **@value** 指定 **@value**中指定合并项目的交互式冲突解决方法。  
  
2.  在订阅服务器上，对订阅数据库执行 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 有关详细信息，请参阅 [创建请求订阅](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
3.  在订阅服务器的订阅数据库中，执行 [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)，同时指定下列参数：  
  
    -   **@publisher**和 **@publisher_db** （已发布的数据库）和 **@publication**中指定合并项目的交互式冲突解决方法。  
  
    -   将 **@value** 指定 **@enabled_for_syncmgr**中指定合并项目的交互式冲突解决方法。  
  
    -   将 **@value** 指定 **@use_interactive_resolver**中指定合并项目的交互式冲突解决方法。  
  
    -   合并代理所需的安全帐户信息。 有关详细信息，请参阅 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
4.  在发布服务器的发布数据库中，执行 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)。  
  
#### <a name="to-define-an-article-that-supports-the-interactive-resolver"></a>定义支持交互式冲突解决程序的项目  
  
1.  在发布服务器上，对发布数据库执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 为 **@publication**指定项目所属的发布的名称，为 **@article**指定项目的名称，为 **@source_object**值，并将 **@value** 指定 **@allow_interactive_resolver**中指定合并项目的交互式冲突解决方法。 有关详细信息，请参阅 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## <a name="see-also"></a>另请参阅  
 [查看和解决合并发布的数据冲突 (SQL Server Management Studio)](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
  
