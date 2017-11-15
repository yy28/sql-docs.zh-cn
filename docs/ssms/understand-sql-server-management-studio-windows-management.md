---
title: "了解 SQL Server Management Studio Windows 管理 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- autohide [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], tool windows
- push pin [SQL Server Management Studio]
- tool windows [SQL Server Management Studio]
ms.assetid: bebf8383-dcaf-466e-84f5-63b81c9cfe52
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6517b160d9cf14fa89230e7ba8fa43d35ed66022
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="understand-sql-server-management-studio-windows-management"></a>了解 SQL Server Management Studio Windows 管理
[!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 中的工具窗口是功能强大、灵活和高效的系统，使用该窗口可以：  
  
-   最大化用于开发和管理的用户工作区。  
  
-   减少同时显示的不使用的窗口数。  
  
-   方便地自定义用户环境。  
  
操作窗口是 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 环境的中心。 用户可以很方便地访问频繁使用的工具和窗口。 用户可以控制其想要分配给不同信息的空间量，相应地，环境会使用于编辑查询的空间最大化。 可以将窗口移动到屏幕上的不同位置。 很多窗口都可以从 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 框架中取消停靠并拖出。 如果正在使用多个监视器，该功能会特别有用。  
  
为了在保持功能的同时增大编辑空间，所有窗口都提供了自动隐藏功能，该功能可使窗口显示为主 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 环境中边框栏上的选项卡。 在将指针放在其中一个选项卡之上时，将显示其对应的窗口。 通过单击“自动隐藏”按钮（以窗口右上角的图钉表示），可以切换窗口的自动隐藏。 “窗口”菜单上还提供了一个“自动全部隐藏”选项。  
  
可以在两种模式下配置某些组件：一种是选项卡式模式，在该模式下组件作为选项卡出现在相同的停靠位置；另一种是多文档界面 (MDI) 模式，在该模式下每个文档都有其自己的窗口。 若要配置该功能，请在“工具”菜单上，单击“选项”，单击“环境”，然后单击“常规”。  
  
> [!IMPORTANT]  
> 当一个登录名（或包含的数据库用户）进行连接并经过身份验证后，该连接存储有关该登录名的标识信息。 对于 Windows 身份验证登录，此标识信息包含有关 Windows 组中的成员身份的信息。 只要保持连接，该登录名的标识就保持已经过身份验证的状态。 若要在标识中强制进行更改（例如，重置密码或更改 Windows 组成员身份），则必须从身份验证机构（Windows 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]）注销，然后再次登录。 **sysadmin** 固定服务器角色的成员或任何使用 **ALTER ANY CONNECTION** 权限的登录名都可以使用 **KILL** 命令结束连接，并强制登录名重新连接。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 可以在打开与对象资源管理器和查询编辑器窗口之间的多个连接时重用连接信息。 关闭所有连接可强制重新连接。  
  
> [!IMPORTANT]  
> 当一个登录名（或包含的数据库用户）进行连接并经过身份验证后，该连接缓存有关该登录名的标识信息。 对于 Windows 身份验证登录，此标识信息包含有关 Windows 组中的成员身份的信息。 只要保持连接，该登录名的标识就保持已经过身份验证的状态。 若要在标识中强制进行更改（例如，重置密码或更改 Windows 组成员身份），则必须从身份验证机构（Windows 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]）注销，然后再次登录。 **sysadmin** 固定服务器角色的成员或任何使用 **ALTER ANY CONNECTION** 权限的登录名都可以使用 **KILL** 命令结束连接，并强制登录名重新连接。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 可以在打开与对象资源管理器和查询编辑器窗口之间的多个连接时重用连接信息。 关闭所有连接可强制重新连接。  
  
## <a name="see-also"></a>另请参阅  
[使用 SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[SQL Server Management Studio 环境](../ssms/the-sql-server-management-studio-environment.md)  
  
