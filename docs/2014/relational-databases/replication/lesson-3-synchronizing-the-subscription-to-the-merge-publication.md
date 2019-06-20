---
title: 第 3 课：同步对合并发布的订阅 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 847b833d793d3b572b44bcb77903c534300109b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62720997"
---
# <a name="lesson-3-synchronizing-the-subscription-to-the-merge-publication"></a>第 3 课：同步对合并发布的订阅
  在本课中，您将使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]启动合并代理以初始化订阅。 您还将使用此过程与发布服务器同步。 本课程要求已完成上一课，[第 2 课：创建对合并发布的订阅](lesson-2-creating-a-subscription-to-the-merge-publication.md)。  
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>启动同步并初始化订阅  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到订阅服务器，展开服务器节点，然后展开 **“复制”** 文件夹。  
  
2.  在 **“本地订阅”** 文件夹中，右键单击 **SalesOrdersReplica** 数据库中的订阅，再单击 **“查看同步状态”** 。  
  
3.  单击 **“启动”** 以初始化订阅。  
  
## <a name="next-steps"></a>后续步骤  
 您已成功运行合并代理来启动同步并初始化订阅。 您还可以在发布服务器或订阅服务器的 **SalesOrderHeader** 或 **SalesOrderDetail** 表中插入、更新或删除数据，当网络连接可用时重复此过程以在发布服务器和订阅服务器之间同步数据，然后在其他服务器上查询 **SalesOrderHeader** 或 **SalesOrderDetail** 表以查看复制的更改。  
  
 这样就完成了“涉及移动客户端的数据复制”教程。 使用事务复制的类似教程，请参阅[教程：连续复制之间的数据连接的服务器](tutorial-replicating-data-between-continuously-connected-servers.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用快照初始化订阅](initialize-a-subscription-with-a-snapshot.md)   
 [同步数据](synchronize-data.md)   
 [同步请求订阅](synchronize-a-pull-subscription.md)  
  
  
