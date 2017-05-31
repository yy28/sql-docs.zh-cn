---
title: "交互式冲突解决方法 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interactive conflict resolution [SQL Server replication]
- interactive resolver [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 410b9b720455a699ced2b276df7e76d442cf380e
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-merge-replication-conflict---interactive-resolution"></a>高级合并复制冲突 - 交互式解决方法
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] replication provides an Interactive Resolver, which allows you to resolve conflicts manually during on-demand synchronization in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager. 该交互式冲突解决程序为图形界面，在运行时激活后，显示每个冲突行的数据，并提供用于查看和编辑冲突数据以及逐个解决冲突的选项。  
  
 交互式冲突解决程序与冲突查看器类似。 不同的是，冲突查看器显示合并同步后已解决的冲突的结果，而交互式冲突解决程序显示解决前的每个冲突，使用户可以在合并同步过程中确定每个冲突的结果。 冲突发生时，应该有人监视交互式冲突解决程序。  
  
> [!NOTE]  
>  交互式解决方法需要 Windows 同步管理器。 如果在 Windows 同步管理器的外部执行同步（作为 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或复制监视器中的计划同步或按需同步），系统会根据为项目指定的冲突解决程序自动解决冲突，无需用户干预。 包含逻辑记录的冲突不会显示在交互式冲突解决程序中。 若要查看有关这些冲突的信息，请使用复制存储过程。 有关详细信息，请参阅[查看合并发布的冲突信息（复制 Transact-SQL 编程）](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)。  
  
## <a name="article-resolvers-and-the-interactive-resolver"></a>项目冲突解决程序和交互式冲突解决程序  
 冲突解决程序（默认冲突解决程序、业务逻辑处理程序或自定义冲突解决程序）将在创建发布时分配给特定项目，并使用一组规则确定输入冲突行数据时应使用哪组数据。 交互式冲突解决程序不是具有确定冲突入选方与落选方规则的独立冲突解决程序，而是与默认和自定义冲突解决程序一起使用的工具。 项目冲突解决程序仍确定入选行和落选行，而交互式冲突解决程序则允许用户干预接受、拒绝或修改结果。  
  
 若要使用交互式冲突解决程序，必须为每个要求使用该程序的项目和订阅启用交互式解决方法。 为一个或多个项目和订阅启用交互式解决方法后，在合并同步过程中检测到冲突时，将使用交互式冲突解决程序。  
  
 若要使用交互式冲突解决程序，请参阅[指定合并项目的交互式冲突解决方法](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)和[使用 Windows 同步管理器同步订阅（Windows 同步管理器）](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
