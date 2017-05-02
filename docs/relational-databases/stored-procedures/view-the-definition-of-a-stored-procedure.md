---
title: "查看存储过程的定义 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], viewing
- definition of stored procedure
- viewing stored procedures
- displaying stored procedures
ms.assetid: 93318587-a0c5-4788-946f-3b5dc8372ea9
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7c47576b90eb7b14738d8612b99f36ed8a5ccb12
ms.lasthandoff: 04/11/2017

---
# <a name="view-the-definition-of-a-stored-procedure"></a>查看存储过程的定义
    
##  <a name="Top"></a> 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用“对象资源管理器”菜单选项或在查询编辑器中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]来查看存储过程的定义。 本主题介绍如何在对象资源管理器中查看过程的定义，以及如何在查询编辑器中使用系统存储过程、系统函数和对象目录视图来查看过程的定义。  
  
-   **Before you begin:**  [Security](#Security)  
  
-   **To view the definition of a procedure, using:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 系统存储过程： **sp_helptext**  
 要求 **公共** 角色具有成员身份。 系统对象定义对所有用户可见。 用户对象的定义对于对象所有者或具有下列任一权限的被授权者可见：ALTER、CONTROL、TAKE OWNERSHIP 或 VIEW DEFINITION。  
  
 系统函数： **OBJECT_DEFINITION**  
 系统对象定义对所有用户可见。 用户对象的定义对于对象所有者或具有下列任一权限的被授权者可见：ALTER、CONTROL、TAKE OWNERSHIP 或 VIEW DEFINITION。 **db_owner**、 **db_ddladmin**和 **db_securityadmin** 固定数据库角色的成员隐式具有这些权限。  
  
 sys.sql_modules 目录视图： **sys.sql_modules**  
 目录视图中仅显示用户拥有的安全对象的元数据，或用户对其拥有某些权限的安全对象的元数据。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
##  <a name="Procedures"></a> 如何查看存储过程的定义  
 您可以使用以下项之一：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **在对象资源管理器中查看过程的定义**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  依次展开“数据库” ****、过程所属的数据库以及“可编程性” ****。  
  
3.  展开 **“存储过程”**，右键单击该过程，再单击 **“编写存储过程脚本为”**，然后单击下列选项之一： **“CREATE 到”**、 **“ALTER 到”**或 **“DROP 和 CREATE 到”**。  
  
4.  选择 **“新建查询编辑器窗口”**。 这将显示过程定义。  
  
###  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **在查询编辑器中查看过程的定义**  
  
 系统存储过程： **sp_helptext**  
 1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在工具栏上，单击 **“新建查询”**。  
  
3.  在查询窗口中，输入以下使用 **sp_helptext** 系统存储过程的语句。 更改数据库名称和存储过程名称以引用所需的数据库和存储过程。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_helptext N'AdventureWorks2012.dbo.uspLogError';  
    ```  
  
 系统函数： **OBJECT_DEFINITION**  
 1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在工具栏上，单击 **“新建查询”**。  
  
3.  在查询窗口中，输入以下使用 **OBJECT_DEFINITION** 系统函数的语句。 更改数据库名称和存储过程名称以引用所需的数据库和存储过程。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
 sys.sql_modules 目录视图： **sys.sql_modules**  
 1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在工具栏上，单击 **“新建查询”**。  
  
3.  在查询窗口中，输入以下使用 **sys.sql_modules** 目录视图的语句。 更改数据库名称和存储过程名称以引用所需的数据库和存储过程。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition  
    FROM sys.sql_modules  
    WHERE object_id = (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [创建存储过程](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [修改存储过程](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [删除存储过程](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [重命名存储过程](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [OBJECT_DEFINITION (Transact-SQL)](../../t-sql/functions/object-definition-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sp_helptext (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [OBJECT_ID (Transact-SQL)](../../t-sql/functions/object-id-transact-sql.md)  
  
  
