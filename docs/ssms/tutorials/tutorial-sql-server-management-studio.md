---
title: "教程：SQL Server Management Studio (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.tutorialstart.ssms.f1
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: d2bade70-07cf-4d94-b5d2-88aecb538ed1
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 5aa858aff03e93db9db36b8caa710cc3a3b874ca
ms.openlocfilehash: dde887f6e0999c5ebc107a300c33981a38ec7034
ms.contentlocale: zh-cn
ms.lasthandoff: 08/31/2017

---
# <a name="tutorial-sql-server-management-studio"></a>教程：SQL Server Management Studio
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

SQL Server Management Studio (SSMS) 将介绍用于管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基础结构的集成环境。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供用于配置、监视和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的图形界面。 此外，它还允许部署、监视和升级应用程序使用的数据层组件，如数据库。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 还提供用于编辑和调试脚本的 [!INCLUDE[tsql](../../includes/tsql-md.md)]、MDX、DMX 和 XML 语言编辑器。  
  
## <a name="what-you-will-learn"></a>学习内容  
本教程将帮助你理解 SSMS 中提供的信息以及如何利用其功能。
  
熟悉 SSMS 的最好方式是进行实践演练。 本教程将讲述如何管理 SSMS 组件以及如何查找常用的功能。  
  
本教程分为三课：  
  
[第 1 课：SQL Server Management Studio 中的基本导航](lesson-1-basic-navigation-in-sql-server-management-studio.md)  
在本课程中，您将学习如何使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]组件，如何重新配置环境布局以及如何还原默认布局。  
  
[第 2 课：编写 Transact-SQL](lesson-2-writing-transact-sql.md)  
在本课程中，你将学习如何打开查询编辑器、如何管理代码以及如何使用查询编辑器的其他功能。  
  
[第 3 课：使用模板、解决方案和脚本项目](lesson-3-working-with-templates-solutions-and-script-projects.md)  
在本课程中，您将学习如何使用模板，以及如何将脚本组织为解决方案和项目。  
  
## <a name="requirements"></a>要求  
本教程面向不熟悉 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，但熟悉数据库概念和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的经验丰富的数据库管理员和数据库开发人员。  
  
要使用此教程，必须安装以下组件：  

  
-   下载最新版的 [SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)。  
-   带 AdventureWorks 示例数据库的 SQL Server 2016 或更高版本。 要安装 AdventureWorks 示例数据库，请参阅 [AdventureWorks2014](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2014) 并安装 AdventureWorks2014 (OLTP) 数据库。  

  
## <a name="see-also"></a>另请参阅  
[数据库引擎教程](../../relational-databases/database-engine-tutorials.md)  
  
  
  


