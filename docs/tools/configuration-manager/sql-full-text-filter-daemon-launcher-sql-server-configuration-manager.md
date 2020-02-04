---
title: SQL 全文筛选器后台程序启动器（SQL Server 配置管理器）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: bf40f8c38e7e674a3930e09819af973cb63fd5c3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75306716"
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>SQL 全文筛选器后台程序启动器（SQL Server 配置管理器）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]开始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文搜索将使用 SQL 全文筛选器后台程序启动器 (FDHOST Launcher) 服务来启动筛选器后台程序主机进程，此进程用于处理全文搜索筛选和断字。 必须运行此服务才能使用全文搜索。 FDHOST Launcher 服务是可识别实例的服务，它与特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例相关联。 FDHOST Launcher 服务将服务帐户信息传播到每个已启动的筛选器后台程序主机进程。 有关筛选器后台程序主机进程的信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“全文搜索体系结构”。  
  
  
