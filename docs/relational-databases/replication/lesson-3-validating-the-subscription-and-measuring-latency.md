---
title: "第 3 课：验证订阅和测量滞后时间 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ad3fadb0017628fa54a102366f132bbc72b9cfb
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="lesson-3-validating-the-subscription-and-measuring-latency"></a>第 3 课：验证订阅和测量滞后时间
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在本课中，将使用跟踪令牌验证将更改复制到订阅服务器并确定滞后时间，即，发布服务器上所做的更改出现在订阅服务器中所需的时间。 本课程要求已完成上一课， [第 2 课：创建事务发布的订阅](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md)。  
  
### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>插入跟踪令牌并查看有关令牌的信息  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，展开服务器节点，右键单击 **“复制”** 文件夹，然后单击 **“启动复制监视器”**。  
  
    复制监视器启动。  
  
2.  在左窗格中展开发布服务器组，展开发布服务器实例，然后单击 **AdvWorksProductTrans** 发布。  
  
3.  单击 **“跟踪令牌”** 选项卡。  
  
4.  单击 **“插入跟踪器”**。  
  
5.  在以下列中查看跟踪令牌的运行时间： **“发布服务器到分发服务器”**、 **“分发服务器到订阅服务器”**、 **“总滞后时间”**。 值为 **“挂起”** 表示令牌尚未到达指定点。  
  
## <a name="next-steps"></a>Next Steps  
在本课中，您成功地使用跟踪令牌验证了正在将数据更改从发布服务器复制到订阅服务器。 您还可以在发布服务器的 **Product** 表中插入、更新或删除数据，并且可以在完成复制后，查询订阅服务器中的 **Product** 表以查看这些更改。  
  
现在将完成“在连续连接的服务器之间复制数据”教程。 有关使用合并复制的类似教程，请参阅 [Tutorial: Replicating Data with Mobile Clients](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)。  
  
## <a name="see-also"></a>另请参阅  
[为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
  
