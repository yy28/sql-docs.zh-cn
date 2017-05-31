---
title: "检测并解决合并复制冲突 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- conflict resolution [SQL Server replication]
- viewing merge replication conflicts
- resolving merge replication conflicts
- articles [SQL Server replication], conflict resolution
- merge replication conflict resolution [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 0d033c76-e8c9-4e35-ab95-4d335abb18c1
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea0d016f2fc6e73be6458ed44f34f42dfbd140bf
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-merge-replication---resolve-merge-replication-conflicts"></a>高级合并复制 - 解决合并复制冲突
  当发布服务器与订阅服务器连接并进行同步时，合并代理将检测是否存在任何冲突。 如果检测到冲突，合并代理将使用冲突解决程序来确定将接受哪些数据并将其传播到其他站点。  
  
> [!NOTE]  
>  虽然订阅服务器与发布服务器同步，但冲突通常发生于不同订阅服务器上进行的更新之间，而不是于订阅服务器和发布服务器上进行的更新之间。  
  
 合并复制提供了多种检测和解决冲突的方法。 此默认方法适用于大多数应用程序：  
  
-   如果发布服务器和订阅服务器发生冲突，则保留发布服务器更改，而放弃订阅服务器更改。  
  
-   如果使用客户端订阅（请求订阅的默认类型）的两台订阅服务器发生冲突，则保留第一台与发布服务器同步的订阅服务器的更改，而放弃第二台订阅服务器的更改。 有关指定客户端和服务器订阅的信息，请参阅[指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio)](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)。  
  
-   如果使用服务器订阅（推送订阅的默认类型）的两台订阅服务器发生冲突，则保留具有最高优先级值的订阅服务器的更改，而放弃另一台订阅服务器的更改。 如果优先级值相等，则保留第一台与发布服务器同步的订阅服务器的更改。  
  
 有关合并复制的冲突检测和解决的详细信息，请参阅 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
## <a name="see-also"></a>另请参阅  
 [合并复制的项目选项](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [订阅发布](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
