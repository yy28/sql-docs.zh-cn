---
title: "SQL 全文筛选器后台程序启动器 （SQL Server 配置管理器） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4bd16f589ae6561a128c76520bf3899c0a18604f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>SQL 全文筛选器后台程序启动器（SQL Server 配置管理器）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]从[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，SQL 全文筛选器后台程序启动器 (FDHOST Launcher) 服务由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]启动筛选器后台程序宿主进程，用于处理全文搜索筛选和断字的全文搜索。 必须运行此服务才能使用全文搜索。 FDHOST Launcher 服务是可识别实例的服务，它与特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例相关联。 FDHOST Launcher 服务将服务帐户信息传播到每个已启动的筛选器后台程序主机进程。 有关筛选器后台程序主机进程的信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“全文搜索体系结构”。  
  
  
