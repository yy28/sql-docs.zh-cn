---
title: 删除视图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- dropping views
- deleting views
- views [SQL Server], deleting
- removing views
ms.assetid: 6823c7f8-06ca-4bda-8482-7092f03d52a0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7e727451fb0f9dc7a3d0726a2cb0fa2d6adf997
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "68196404"
---
# <a name="delete-views"></a>删除视图
  可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中删除视图 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   删除视图时，将从系统目录中删除视图的定义和有关视图的其他信息。 还将删除视图的所有权限。  
  
-   使用 `DROP TABLE` 删除的表上的任何视图都必须使用 `DROP VIEW`显式删除。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 需要对 SCHEMA 的 ALTER 权限或对 OBJECT 的 CONTROL 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-view-from-a-database"></a>从数据库中删除视图  
  
1.  在 **“对象资源管理器”** 中，展开包含要删除的视图的数据库，然后展开 **“视图”** 文件夹。  
  
2.  右键单击要删除的视图，然后单击“删除”****。  
  
3.  在 **“删除对象”** 对话框中，单击 **“确定”**。  
  
    > [!IMPORTANT]  
    >  单击“删除对象”**** 对话框中的“显示依赖关系”****，打开__“view_name 依赖关系”**** 对话框。 这将显示依赖于该视图的所有对象和该视图依赖的所有对象。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-view-from-a-database"></a>从数据库中删除视图  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。 仅在视图存在时，该示例才删除指定的视图。  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    IF OBJECT_ID ('HumanResources.EmployeeHireDate', 'V') IS NOT NULL  
    DROP VIEW HumanResources.EmployeeHireDate;  
    GO  
    ```  
  
 有关详细信息，请参阅 [DROP VIEW (Transact-SQL)](/sql/t-sql/statements/drop-view-transact-sql)。  
  
  
