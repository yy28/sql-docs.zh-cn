---
title: 第 3 课：验证订阅和测量滞后时间 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
author: rothja
ms.author: jroth
ms.openlocfilehash: eba65b6b19054414a13a46ebd2ccb92a28305dde
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065878"
---
# <a name="lesson-3-validating-the-subscription-and-measuring-latency"></a>第 3 课：验证订阅和测量滞后时间
  在本课中，将使用跟踪令牌验证将更改复制到订阅服务器并确定滞后时间，即，发布服务器上所做的更改出现在订阅服务器中所需的时间。 本课程要求已完成上一课， [第 2 课：创建事务发布的订阅](lesson-2-creating-a-subscription-to-the-transactional-publication.md)。  
  
### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>插入跟踪令牌并查看有关令牌的信息  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，展开服务器节点，右键单击 **“复制”** 文件夹，然后单击 **“启动复制监视器”**。  
  
     复制监视器启动。  
  
2.  在左窗格中展开发布服务器组，展开发布服务器实例，然后单击 **AdvWorksProductTrans** 发布。  
  
3.  单击 **“跟踪令牌”** 选项卡。  
  
4.  单击 **“插入跟踪器”**。  
  
5.  在以下列中查看跟踪令牌的运行时间： **“发布服务器到分发服务器”**、 **“分发服务器到订阅服务器”**、 **“总滞后时间”**。 值为 "**挂起**" 表示令牌尚未到达给定点。  
  
## <a name="next-steps"></a>后续步骤  
 在本课中，您成功地使用跟踪令牌验证了正在将数据更改从发布服务器复制到订阅服务器。 您还可以在发布服务器的 **Product** 表中插入、更新或删除数据，并且可以在完成复制后，查询订阅服务器中的 **Product** 表以查看这些更改。  
  
 现在将完成“在连续连接的服务器之间复制数据”教程。 有关使用合并复制的类似教程，请参阅 [Tutorial: Replicating Data with Mobile Clients](tutorial-replicating-data-with-mobile-clients.md)。  
  
## <a name="see-also"></a>另请参阅  
 [为事务复制测量滞后时间和验证连接](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
