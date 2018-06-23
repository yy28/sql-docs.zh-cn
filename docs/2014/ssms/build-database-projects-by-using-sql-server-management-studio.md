---
title: 使用 SQL Server Management Studio 生成数据库项目 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scripts [SQL Server], database projects
- database projects [SQL Server]
- projects [SQL Server Management Studio], about projects
- projects [SQL Server Management Studio]
ms.assetid: c2e80045-894d-44cf-b65c-e547ed738947
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f27e236af3bb9cbf29ed88a952a8c5f0a3d0b3eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125515"
---
# <a name="build-database-projects-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 生成数据库项目
  数据库脚本项目是与数据库或数据库的某一部分关联的一组经过整理的脚本、连接信息和模板。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供了 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 用于在脚本项目上下文中管理和设计 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 包含设计器、编辑器、指南和向导，可帮助用户开发、部署和维护数据库。  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是一套管理工具，用于管理从属于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的组件。 此集成环境使用户可以在一个界面内执行各种任务，例如，备份数据、编辑查询和自动执行常见函数。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 包含以下工具：  
  
-   代码编辑器，用于编写和编辑脚本，是一种功能丰富的脚本编辑器。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 提供了四种版本的代码编辑器：针对 [!INCLUDE[ssDE](../includes/ssde-md.md)] 脚本的 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询编辑器、DMX 查询编辑器、MDX 查询编辑器和 XML/A 查询编辑器。  
  
-   对象资源管理器，用于查找、修改、编写脚本或运行从属于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的对象。  
  
-   模板资源管理器，用于查找模板以及为模板编写脚本。  
  
-   解决方案资源管理器，用于将相关脚本组织并存储为项目的一部分。  
  
-   属性窗口，用于显示当前选定对象的属性。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 通过提供下列项目支持有效的工作过程：  
  
-   断开连接的访问。 可以编写和编辑脚本，而不用与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例连接。  
  
-   在任意对话框中编写脚本。 可以在任意对话框中创建脚本，以便在创建脚本之后读取、修改、存储和重用脚本。  
  
-   无模式对话框。 在访问某个 UI 对话框时，可以浏览 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的其他资源而不用关闭该对话框。  
  
## <a name="solutions-and-script-projects"></a>解决方案和脚本项目  
 解决方案资源管理器是用来存储和重新打开数据库解决方案的实用工具。 解决方案将相关的脚本项目和文件组织在一起。 脚本项目用于存储 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 脚本文件、SQL 模板、连接信息和其他杂项文件。 将脚本保存到脚本项目中后，用户能够：  
  
-   维护脚本的版本控制。  
  
-   用脚本存储结果选项。  
  
-   在单个脚本项目中组织相关脚本。  
  
-   用脚本保存连接信息。  
  
 解决方案资源管理器是开发人员用来创建和重用与同一项目相关的脚本的一种工具。 如果以后需要类似的任务，就可以使用项目中存储的脚本组。 如果你曾经使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]创建过应用程序，就会发现解决方案资源管理器非常熟悉。  
  
 解决方案由一个或多个脚本项目组成。 项目则由一个或多个脚本或连接组成。 项目中可能还包括非脚本文件。  
  
## <a name="see-also"></a>请参阅  
 [使用 SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)   
 [查询和文本编辑器&#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [解决方案 (SQL Server Management Studio)](solution/solutions-sql-server-management-studio.md)  
  
  