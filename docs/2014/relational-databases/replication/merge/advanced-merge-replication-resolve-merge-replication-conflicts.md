---
title: 检测并解决合并复制冲突 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 445314a89fabf4975c303a71ee1ae777b7f574ca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024800"
---
# <a name="detect-and-resolve-merge-replication-conflicts"></a>检测并解决合并复制冲突
  当发布服务器与订阅服务器连接并进行同步时，合并代理将检测是否存在任何冲突。 如果检测到冲突，合并代理将使用冲突解决程序来确定将接受哪些数据并将其传播到其他站点。  
  
> [!NOTE]  
>  虽然订阅服务器与发布服务器同步，但冲突通常发生于不同订阅服务器上进行的更新之间，而不是于订阅服务器和发布服务器上进行的更新之间。  
  
 合并复制提供了多种检测和解决冲突的方法。 此默认方法适用于大多数应用程序：  
  
-   如果发布服务器和订阅服务器发生冲突，则保留发布服务器更改，而放弃订阅服务器更改。  
  
-   如果使用客户端订阅（请求订阅的默认类型）的两台订阅服务器发生冲突，则保留第一台与发布服务器同步的订阅服务器的更改，而放弃第二台订阅服务器的更改。 有关指定客户端和服务器订阅的信息，请参阅[指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio)](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md)。  
  
-   如果使用服务器订阅（推送订阅的默认类型）的两台订阅服务器发生冲突，则保留具有最高优先级值的订阅服务器的更改，而放弃另一台订阅服务器的更改。 如果优先级值相等，则保留第一台与发布服务器同步的订阅服务器的更改。  
  
 有关合并复制的冲突检测和解决的详细信息，请参阅 [Advanced Merge Replication Conflict Detection and Resolution](advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
## <a name="see-also"></a>请参阅  
 [合并复制的项目选项](article-options-for-merge-replication.md)   
 [订阅发布](../subscribe-to-publications.md)  
  
  