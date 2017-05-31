---
title: "重命名表（数据库引擎）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table renaming [SQL Server]
- table names [SQL Server]
- tables [SQL Server], Visual Database Tools
- renaming tables
ms.assetid: 2f5c922d-4d71-4694-9fca-28dd99375799
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d65c475509d57577f691e656157c7754c7d8549f
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="rename-tables-database-engine"></a>重命名表（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 重命名 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的表。  
  
> [!CAUTION]  
>  在重命名表之前请仔细考虑。 如果现有的查询、视图、用户定义函数、存储过程或程序引用了该表，则对名称的修改将使这些对象无效。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用以下工具重命名表：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 重命名表将不会自动重命名对该表的引用。 您必须手动修改引用已重命名表的任何对象。 例如，如果您重命名某个表，并且触发器中引用了该表，则必须修改触发器以反映新的表名称。 请使用 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 在重命名表之前列出该表上的依赖关系。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 需要对表的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-a-table"></a>重命名表  
  
1.  在对象资源管理器中，右键单击要重命名的表，然后从快捷菜单中选择“设计”。  
  
2.  从 **“视图”** 菜单上选择 **“属性”**。  
  
3.  在 **“属性”** 窗口的 **“名称”** 值字段中，为该表键入新名称。  
  
4.  若要取消此操作，请在离开此字段前按 Esc 键。  
  
5.  从“文件”菜单中，选择“保存表名”。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-rename-a-table"></a>重命名表  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  下面的示例将 `SalesTerritory` 架构中的 `SalesTerr` 表重命名为 `Sales` 。 将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
    ```  
  
 有关其他示例，请参阅 [sp_rename (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)。  
  
  
