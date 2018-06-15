---
title: 指定合并项目的冲突跟踪和解决方法级别 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], levels
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: 35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f3fb598a48665aecf43ea2d3498020229c5767b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32962382"
---
# <a name="specify-the-conflict-tracking-and-resolution-level-for-merge-articles"></a>指定合并项目的冲突跟踪和解决方法级别
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定合并项目的冲突跟踪和解决方法级别。  
  
 在同步对合并发布的订阅时，复制检查是否存在因对发布服务器和订阅服务器上的相同数据进行更改而导致的冲突。 可以指定是在行级别检测冲突（即对行的任何更改都视为冲突），还是在列级别检测冲突（即只有更改了相同的行和列时才视作冲突）。 项目的冲突解决在行级别执行。 有关在使用逻辑记录时检测和解决冲突的详细信息，请参阅 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
-   **指定合并项目的冲突跟踪和解决方法级别，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   如果在初始化订阅后修改跟踪级别，必须重新初始化这些订阅。 有关属性更改的影响的详细信息，请参阅[更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
-   对于行级和列级跟踪，始终在行级执行冲突解决：入选行将覆盖落选行。 合并复制还允许您指定在逻辑记录级跟踪和解决冲突，但 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]没有提供这些选项。 有关在复制存储过程中设置这些选项的信息，请参阅 [定义合并表项目间的逻辑记录关系](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在“项目属性”对话框的“属性“选项卡上指定合并项目的行级或列级跟踪，该对话框可以在新发布向导和“发布属性 - \<发布>”对话框中找到。 有关如何使用该向导和如何访问该对话框的详细信息，请参阅[创建发布](../../../relational-databases/replication/publish/create-a-publication.md)和[查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-row--or-column-level-tracking"></a>指定行级或列级跟踪  
  
1.  在新建发布向导或“发布属性 - \<发布>”对话框的“项目”页上，选择一个表。  
  
2.  单击 **“项目属性”**，然后单击 **“设置突出显示的表项目的属性”** 或 **“设置所有表项目的属性”**。  
  
3.  在“项目属性 \<项目>”对话框的“属性”选项卡上，为“跟踪级别”属性选择以下值之一：“行级跟踪”或“列级跟踪”。  
  
4.  如果处于“发布属性 - \<发布>”对话框中，请单击“确定”以保存并关闭该对话框。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-specify-conflict-tracking-options-for-a-new-merge-article"></a>为新的合并项目指定冲突跟踪选项  
  
1.  在发布服务器上的发布数据库中，执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 并为 **@column_tracking**指定以下值之一：  
  
    -   **true** - 为项目使用列级别跟踪。  
  
    -   **false** - 使用行级别跟踪，这是默认值。  
  
#### <a name="to-change-conflict-tracking-options-for-a-merge-article"></a>更改合并项目的冲突跟踪选项  
  
1.  若要确定某个合并项目的冲突跟踪选项，请执行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 请注意项目的结果集中 **column_tracking** 选项的值。 值为 **1** 表明使用的是列级别的跟踪，值为 **0** 表明使用的是行级别的跟踪。  
  
2.  在发布服务器上，对发布数据库执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 将 **column_tracking** 的值指定为 **@property** ，并且将 **@value**指定以下值之一：  
  
    -   **true** - 为项目使用列级别跟踪。  
  
    -   **false** - 使用行级别跟踪，这是默认值。  
  
     将 **1** 和 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**中指定合并项目的冲突跟踪和解决方法级别。  
  
## <a name="see-also"></a>另请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [定义合并表项目间的逻辑记录关系](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [检测并解决合并复制冲突](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)  
  
  
