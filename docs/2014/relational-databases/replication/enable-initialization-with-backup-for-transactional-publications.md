---
title: 为事务发布启用使用备份进行初始化（SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f5e22614c8c4f5250db3966e747b686091512774
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010715"
---
# <a name="enable-initialization-with-a-backup-for-transactional-publications-sql-server-management-studio"></a>使用备份来初始化事务发布 (SQL Server Management Studio)
  若要使用备份初始化对事务发布的订阅，请启用发布以允许使用备份进行初始化，然后指定创建订阅时的备份信息：  
  
-   在 "**发布属性- \<Publication> ** " 对话框的 "**订阅选项**" 页上启用发布。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。  
  
-   使用存储过程 [sp_addsubscription (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) 指定备份信息。 有关 **sp_addsubscription** 所需的参数的详细信息，请参阅[使用备份初始化事务订阅（复制 Transact-SQL 编程）](initialize-a-transactional-subscription-from-a-backup.md)。  
  
### <a name="to-enable-initialization-with-a-backup"></a>启用使用备份来初始化  
  
1.  在 "**发布属性- \<Publication> ** " 对话框的 "**订阅选项**" 页上，为 "**允许从备份文件初始化**" 选项选择 " **True** " 值。  
  
## <a name="see-also"></a>另请参阅  
 [初始化事务订阅（不使用快照）](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
