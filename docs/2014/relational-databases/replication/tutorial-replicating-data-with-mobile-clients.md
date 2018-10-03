---
title: 教程：使用移动客户端复制数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5a95b157761cc9a61d09271b5e081a65cd45998
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056237"
---
# <a name="tutorial-replicating-data-with-mobile-clients"></a>教程：使用移动客户端复制数据
  复制是解决中央服务器和偶尔连接的移动客户端之间的数据移动问题的好方法。 使用复制向导可以轻松地配置和管理复制拓扑。 本教程演示如何为移动客户端配置复制拓扑。  
  
## <a name="what-you-will-learn"></a>学习内容  
 在本教程中，您将使用合并复制将数据从中央数据库发布到一个或多个移动用户，以便每个用户都能获得唯一筛选的数据子集。 第一课介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建发布。 后面几课演示如何创建和同步订阅。  
  
## <a name="requirements"></a>要求  
 本教程适用于熟悉数据库基本操作但复制经验不足的用户。 在开始本教程的学习之前，必须已完成 [教程：准备用于复制的服务器](tutorial-preparing-the-server-for-replication.md)的学习。  
  
 若要使用本教程，系统中必须安装下列组件：  
  
-   发布服务器（源）：  
  
    -   任意版本的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，但 Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) 或 [!INCLUDE[ssEW](../../includes/ssew-md.md)]除外。 这些版本不能充当复制发布服务器。  
  
    -   [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库。 为了增强安全性，默认情况下不会安装示例数据库。  
  
-   订阅服务器（目标）：  
  
    -   任意版本的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，但 [!INCLUDE[ssEW](../../includes/ssew-md.md)]除外。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 本教程中创建的发布不支持。  
  
    > [!NOTE]  
    >  默认情况下，不在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]上安装复制。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，必须使用属于 sysadmin 固定服务器角色成员的登录名连接到发布服务器和订阅服务器。  
  
 **本教程的预计学时：30 分钟。**  
  
## <a name="lessons-in-this-tutorial"></a>本教程中的课程  
  
-   [第 1 课：使用合并复制发布数据](lesson-1-publishing-data-using-merge-replication.md)  
  
-   [第 2 课：创建合并发布订阅](lesson-2-creating-a-subscription-to-the-merge-publication.md)  
  
 [开始教程](merge/merge-replication.md)  
  
## <a name="see-also"></a>请参阅  
 [复制编程概念](concepts/replication-programming-concepts.md)  
  
  
