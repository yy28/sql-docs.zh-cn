---
title: 为合并项目指定不应跟踪删除 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d11badc932d1b759dca4ea9675d15a0b9cb7b773
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796417"
---
# <a name="specify-that-deletes-should-not-be-tracked-for-merge-articles"></a>为合并项目指定不应跟踪删除
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 默认情况下，合并复制同步发布服务器和订阅服务器之间的 DELETE 命令。 您可以使用合并复制来保留订阅数据库中的行，即使这些行已从发布中删除，反之亦然。 您可以通过编程方式指定在创建新项目时忽略 DELETE 命令，或者可以使用复制存储过程在以后启用此功能。  
  
> [!IMPORTANT]  
>  启用此功能将导致无法收敛，也就是说，位于订阅服务器上的数据将无法准确反映发布服务器上的数据。 您必须实现自己的用于手动删除已删除行的机制。  
  
### <a name="to-specify-that-deletes-be-ignored-for-a-new-merge-article"></a>指定对新合并项目忽略删除  
  
1.  在发布服务器上，对发布数据库执行 [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 将 **@delete_tracking** @delete_tracking **@delete_tracking**。 有关详细信息，请参阅 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  如果某个项目的源表已在另一个发布中发布，则两个项目的 **delete_tracking** 值必须相同。  
  
### <a name="to-specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>为现有的合并项目指定忽略删除  
  
1.  若要确定是否对项目启用了错误补偿，请执行 [sp_helpmergearticle (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) 并注意结果集中的 **delete_tracking** 值。 如果该值为 **0**，则删除已被忽略。  
  
2.  如果步骤 1 的值为 **1**，则在发布服务器上对发布数据库执行 [sp_changemergearticle (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 将 **delete_tracking** @delete_tracking **@property**，并将 **@delete_tracking** @delete_tracking **@value**。  
  
    > [!NOTE]  
    >  如果某个项目的源表已在另一个发布中发布，则两个项目的 **delete_tracking** 值必须相同。  
  
## <a name="see-also"></a>另请参阅  
 [使用条件性删除跟踪优化合并复制性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
