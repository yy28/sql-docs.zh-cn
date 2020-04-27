---
title: 重命名视图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], renaming
- renaming views
ms.assetid: 5eed0488-81d2-40e8-8fdf-b0a640a591d0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0dfa9a95697c4bb1fcb2e4e5d3798f18e305e42
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211654"
---
# <a name="rename-views"></a>重命名视图
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中重命名视图。  
  
> [!WARNING]  
>  如果重命名视图，则依赖于该视图的代码和应用程序可能会出错。 这些代码和应用程序包括其他视图、查询、存储过程、用户定义函数和客户端应用程序。 注意，这些错误会级联发生。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **重命名视图，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：** [在重命名视图之后](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
 获取视图的所有依赖关系的列表。 必须修改引用视图的任何对象、脚本或应用程序，以反映新的视图名称。 有关详细信息，请参阅 [Get Information About a View](get-information-about-a-view.md)。 我们建议您删除视图，然后使用新名称重新创建它，而不是重命名视图。 通过重新创建视图，您可以更新视图中引用的对象的依赖关系信息。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 需要对 SCHEMA 的 ALTER 权限或对 OBJECT 的 CONTROL 权限，以及数据库中的 CREATE VIEW 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-a-view"></a>重命名视图  
  
1.  在 **“对象资源管理器”** 中，展开包含要重命名的视图的数据库，然后展开 **“视图”** 文件夹。  
  
2.  右键单击要重命名的视图，然后选择 **“重命名”** 。  
  
3.  输入视图的新名称。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **重命名视图**  
  
 尽管可以使用 **sp_rename** 更改视图的名称，但是我们建议你删除现有视图，然后使用新名称重新创建它。  
  
 有关详细信息，请参阅 [CREATE VIEW (Transact-SQL)](/sql/t-sql/statements/create-view-transact-sql) 和 [DROP VIEW (Transact-SQL)](/sql/t-sql/statements/drop-view-transact-sql)。  
  
##  <a name="follow-up-after-renaming-a-view"></a><a name="FollowUp"></a> 跟进：在重命名视图之后  
 确保引用视图的旧名称的所有对象、脚本和应用程序现在都使用新名称。  
  
  
