---
title: "教程：在连续连接的服务器之间复制数据 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6090a59e8f831d5d05def6f6ff65ee99a09aea84
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-replicating-data-between-continuously-connected-servers"></a>教程：在连续连接的服务器之间复制数据
复制是在连续连接的服务器之间实现数据移动的好方法。 使用复制向导可以轻松地配置和管理复制拓扑。 本教程演示如何为连续连接的服务器配置复制拓扑。  
  
## <a name="what-you-will-learn"></a>学习内容  
本教程将演示如何使用事务复制将数据从一个数据库发布到另一个数据库。 第一课介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建发布。 后面几课演示如何创建和验证订阅，以及如何测量滞后时间。  
  
## <a name="requirements"></a>要求  
本教程适用于熟悉数据库基本操作但复制经验不足的用户。 本教程要求你完成上一个教程， [准备用于复制的服务器](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)的学习。  
  
若要使用本教程，系统中必须安装有下列组件：  
  
-   发布服务器（源）：  
  
    -   任意版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但 Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) 或 [!INCLUDE[ssEW](../../includes/ssew-md.md)]除外。 这些版本不能充当复制发布服务器。  
  
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 示例数据库。 为了增强安全性，默认情况下不会安装示例数据库。  
  
-   订阅服务器（目标）：  
  
    -   任意版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但 [!INCLUDE[ssEW](../../includes/ssew-md.md)]除外。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 不能充当事务复制中的订阅服务器。  
  
    > [!NOTE]  
    > 默认情况下，不在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 上安装复制。  
  
> [!NOTE]  
> 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，必须使用属于 **sysadmin** 固定服务器角色成员的登录名连接到发布服务器和订阅服务器。  
  
**本教程的预计学时：30 分钟。**  
  
## <a name="lessons-in-this-tutorial"></a>本教程中的课程  
  
-   [第 1 课：使用事务复制发布数据](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md)  
  
-   [第 2 课：创建事务发布的订阅](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md)  
  
-   [第 3 课：验证订阅和测量滞后时间](../../relational-databases/replication/lesson-3-validating-the-subscription-and-measuring-latency.md)  
  
[开始教程](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md)  
  
## <a name="see-also"></a>另请参阅  
[复制编程概念](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
  

