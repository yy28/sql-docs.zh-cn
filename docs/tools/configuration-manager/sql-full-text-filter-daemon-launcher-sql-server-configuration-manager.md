---
title: "SQL 全文筛选器后台程序启动器 （SQL Server 配置管理器） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa2dd776499f0d0b5ea356c18cc9f23df3cbb39b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>SQL 全文筛选器后台程序启动器（SQL Server 配置管理器）
  从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]开始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文搜索将使用 SQL 全文筛选器后台程序启动器 (FDHOST Launcher) 服务来启动筛选器后台程序主机进程，此进程用于处理全文搜索筛选和断字。 必须运行此服务才能使用全文搜索。 FDHOST Launcher 服务是可识别实例的服务，它与特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例相关联。 FDHOST Launcher 服务将服务帐户信息传播到每个已启动的筛选器后台程序主机进程。 有关筛选器后台程序主机进程的信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“全文搜索体系结构”。  
  
  
