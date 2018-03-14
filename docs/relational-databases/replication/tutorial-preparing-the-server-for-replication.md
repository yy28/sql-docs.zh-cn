---
title: "教程：准备用于复制的服务器 | Microsoft Docs"
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
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3f7055cc15673a5dfd4564f26c4d314ccc0f5180
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="tutorial-preparing-the-server-for-replication"></a>教程：准备用于复制的服务器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在配置复制拓扑之前，制定安全计划是非常重要的。 本教程向您介绍如何更好地保护复制拓扑以及如何配置分发，这是复制数据的第一步。 开始其他教程之前，必须先完成本教程。  
  
> [!NOTE]  
> 若要在服务器之间安全地复制数据，你应该实施 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)中提出的所有建议。  
  
## <a name="what-you-will-learn"></a>学习内容  
在本教程中，您将了解如何准备服务器以便用最少的特权安全地运行复制。 第一课介绍如何创建用于运行复制代理的 Windows 服务帐户。 第二课介绍如何配置用于生成和存储发布快照的文件夹。 第三课介绍如何配置分发以及如何设置权限。  
  
## <a name="requirements"></a>要求  
本教程适用于熟悉基本数据库操作，但对复制认识有限的用户。  
  
若要使用本教程，系统中必须安装下列组件：  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 数据库的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 。  
  
**本教程的预计学时：30 分钟。**  
  
## <a name="lessons-in-this-tutorial"></a>本教程中的课程  
  
-   [第 1 课：为复制创建 Windows 帐户](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [第 2 课：准备快照文件夹](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md)  
  
-   [第 3 课：配置分发](../../relational-databases/replication/lesson-3-configuring-distribution.md)  
  
[开始教程](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>另请参阅  
[配置分发](../../relational-databases/replication/configure-distribution.md)  
[安全性和保护（复制）](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
  
