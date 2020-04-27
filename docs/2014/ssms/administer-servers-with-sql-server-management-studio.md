---
title: 使用 SQL Server Management Studio 管理服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9d57657d47f28dc0502b83375f563fa9df737831
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63206811"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理服务器
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]是一个丰富的集成管理客户端，旨在满足[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]管理员的服务器管理要求。 在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]中，管理任务是使用对象资源管理器来完成的，使用对象资源管理器，您可以连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 系列中的任何服务器，并以图形方式浏览其内容。 服务器可以是[!INCLUDE[ssDE](../includes/ssde-md.md)]、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 或 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的实例。  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 的工具组件包括已注册的服务器、对象资源管理器、解决方案资源管理器、模板资源管理器、对象资源管理器详细信息页和文档窗口。 若要显示某个工具，请在“视图”  菜单上单击该工具的名称。 若要显示查询编辑器工具，请单击工具栏上的“新建查询”  按钮。  
  
> [!IMPORTANT]  
>  默认情况下，不对 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之间的网络通信进行加密。 除非建立了加密连接，否则不要在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中使用敏感数据（包括密码）。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 可以：  
  
-   注册服务器。  
  
-   连接到[!INCLUDE[ssDE](../includes/ssde-md.md)]、[!INCLUDE[ssAS](../includes/ssas-md.md)]、[!INCLUDE[ssRS](../includes/ssrs.md)] 或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 的一个实例。  
  
-   配置服务器属性。  
  
-   管理数据库和 [!INCLUDE[ssAS](../includes/ssas-md.md)] 对象（如多维数据集、维度和程序集等）。  
  
-   创建对象，如数据库、表、多维数据集、数据库用户和登录名等。  
  
-   管理文件和文件组。  
  
-   附加或分离数据库。  
  
-   启动脚本编写工具。  
  
-   管理安全性。  
  
-   查看系统日志。  
  
-   监视当前活动。  
  
-   配置复制。  
  
-   管理全文索引。  
  
 若要启动和停止 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理，请使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器。  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)   
 [查看或更改服务器属性 (SQL Server)](../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  
  
  
