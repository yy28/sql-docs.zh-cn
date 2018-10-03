---
title: 切换可更新事务订阅的更新模式 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, update modes
- subscriptions [SQL Server replication], updatable
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dbe5d710c29f8f63a1ee09eab322b23f74dbe2ec
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057897"
---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>切换可更新事务性订阅的更新模式
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中切换可更新事务订阅的更新模式。 可以使用新建订阅向导，为可更新的订阅指定模式。 有关使用此向导时设置模式的信息，请参阅[查看和修改请求订阅属性](../view-and-modify-pull-subscription-properties.md)。  
  
  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   可以随时从立即更新向排队更新进行故障转移。 但执行该操作后，只有在已连接订阅服务器和发布服务器且队列读取器代理已将队列中的所有挂起消息应用到发布服务器后，才能恢复立即更新。  
  
###  <a name="Recommendations"></a> 建议  
  
-   当对事务发布的更新订阅支持从一种更新模式故障转移到另一种更新模式时，可通过编程方式切换更新模式以应对连接发生短暂变化的情况。 可以使用复制存储过程，以编程方式并根据需要设置更新模式。 有关详细信息，请参阅 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)中切换可更新事务订阅的更新模式。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
> [!NOTE]  
>  若要在创建订阅后更改更新模式，必须在创建订阅时将 **update_mode** 属性设置为 **failover** （允许从立即更新切换到排队更新）或 **queued failover** （允许从排队更新切换到立即更新）。 在新建订阅向导中，这些属性是自动设置的。  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>设置推送订阅的更新模式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击要为其设置更新模式的订阅，然后单击 **“设置更新方法”**。  
  
4.  在“设置更新方法 - \<订阅服务器>: \<订阅数据库>”对话框中，选择“立即更新”或“排队更新”。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>设置请求订阅的更新模式  
  
1.  在“订阅属性 - \<发布服务器>: \<发布数据库>”对话框中，为“订阅服务器更新方法”选项选择“立即复制所做的更改”或“排队更改”的值。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 有关访问“订阅属性 - \<发布服务器>: \<发布数据库>”对话框的详细信息，请参阅[查看和修改请求订阅属性](../view-and-modify-pull-subscription-properties.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-switch-between-update-modes"></a>切换更新模式  
  
1.  通过对请求订阅执行 [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql) 或对推送订阅执行 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) ，验证订阅是否支持故障转移。 如果结果集中 **update mode** 的值为 **3** 或 **4**，则支持故障转移。  
  
2.  在订阅服务器上，对订阅数据库执行 [sp_setreplfailovermode](/sql/relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql)。 指定 **@publisher**、 **@publisher_db**、 **@publication**并为 **@failover_mode**指定以下值之一：  
  
    -   **queued** - 在短暂断开连接时将故障转移到排队更新。  
  
    -   **immediate** - 在恢复连接后将故障转移到立即更新。  
  
## <a name="see-also"></a>请参阅  
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
