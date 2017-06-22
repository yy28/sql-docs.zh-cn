---
title: "设置排队更新冲突解决选项 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ee3af1a65573f04bce7f414638b052fdd38c4777
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>设置排队更新冲突解决选项 (SQL Server Management Studio)
  在“发布属性 - \<发布>”对话框的“订阅选项”页上，为支持排队更新订阅的发布设置冲突解决选项。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>设置排队更新冲突解决选项  
  
1.  在“发布属性 - \<发布>”对话框的“订阅选项”页上，为“冲突解决策略”选项选择以下值之一：  
  
    -   **保留发布服务器更改**  
  
    -   **保留订阅服务器更改**  
  
    -   **重新初始化订阅**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [允许更新事务发布的订阅](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
