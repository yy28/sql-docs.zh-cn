---
title: 项目 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c13af859-ca66-4e43-b76a-0650ac6566c0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 85bc34af971db386862528ac36ea04fef33f2daa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52759189"
---
# <a name="projects-sql-server-management-studio"></a>项目 (SQL Server Management Studio)
  一个 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 项目是一些在逻辑上相关并可保存在一起用于数据库管理和开发的脚本和文件的集合。  
  
## <a name="script-project-overview"></a>脚本项目概述  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本项目显示在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的解决方案资源管理器组件中。 脚本项目可以不包含项目文件，也可以包含多个项目文件。 可以将项目添加到解决方案中，或者将多个项目组合在一个解决方案中。  
  
 项目可以包括以下项：  
  
-   **连接**。 连接是项目中的持久项，它将包含登录信息、服务器名称、默认数据库、首选协议、身份验证类型和连接属性。 连接信息可能根据需要与脚本存储在一起（请参见下面内容）。  
  
-   **SQL 脚本**。 用户的常用 SQL 脚本。 双击项目中的 .sql 文件将会使 SQL 编辑器打开所选脚本。  
  
-   **MDX、DMX 和 XMLA 脚本**。 用户的常用 MDX 脚本。 双击项目中的 .mdx 文件将会使编辑器打开所选脚本。  
  
-   **杂项**。该文件夹可用于不完全适合于任何其他默认节点类型的文件，如包含项目目标的文本文件。  
  
 项目还可以集成到源代码管理系统中。  
  
## <a name="connecting-to-an-instance-of-sql-server-from-a-script-project"></a>从脚本项目连接到 SQL Server 实例  
 脚本项目可能包含与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 通过单击连接，可以连接到项目中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 这将打开一个 SQL 脚本窗口，该窗口将连接到在所选连接中定义的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 如果通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的连接打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 MDX 脚本，则在打开编辑器并且加载脚本之后，系统将使用“连接到 SQL Server”对话框提示你输入密码。  
  
 相应窗口关闭后，连接也将随之关闭。  
  
 若要修改有关连接的信息，请使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的属性窗口。  
  
## <a name="project-tasks"></a>项目任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|说明如何在解决方案中创建新项目。|[创建项目](create-a-project.md)|  
|说明如何向解决方案中添加现有项目。|[在解决方案中添加现有项目](add-an-existing-project-to-a-solution.md)|  
|说明如何更改保存项目文件的默认位置。|[更改项目的默认位置](change-the-default-location-for-projects.md)|  
|说明如何查看项目的当前属性。|[视图项目属性](view-project-properties.md)|  
|说明如何将新项（例如连接或脚本文件）添加到项目中。|[向项目添加新项](add-new-items-to-a-project.md)|  
|说明如何建立查询的连接信息。|[将查询与项目中的连接关联](associate-a-query-with-a-connection-in-a-project.md)|  
|说明如何更改查询的连接信息。|[更改与查询关联的连接](change-the-connection-associated-with-a-query.md)|  
|说明如何更改连接属性。|[查看或更改项目中的连接属性](view-or-change-the-properties-of-a-connection-in-a-project.md)|  
  
## <a name="see-also"></a>请参阅  
 [解决方案资源管理器](solution-explorer.md)   
 [解决方案&#40;SQL Server Management Studio&#41;](solutions-sql-server-management-studio.md)   
 [解决方案资源管理器源代码管理](../../database-engine/solution-explorer-source-control.md)  
  
  
