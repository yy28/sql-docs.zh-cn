---
title: "查看排序规则信息 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: collations
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 650a60efe0459981637c8930e9e126a4cdb08bf8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="view-collation-information"></a>查看排序规则信息
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
##  <a name="Top"></a> 您可以通过使用“对象资源管理器”菜单选项或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查看 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的服务器、数据库或列的排序规则。  
  
##  <a name="Procedures"></a> 如何查看排序规则设置  
 您可以使用以下项之一：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **使用对象资源管理器查看服务器（SQL Server 实例）的排序规则设置**  
  
1.  在“对象资源管理器”中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  右键单击该实例，然后选择“属性”。  
  
 **使用对象资源管理器查看数据库的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  展开“数据库”，右键单击数据库，然后选择“属性”。  
  
 **使用对象资源管理器查看列的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  依次展开 **“数据库”**、数据库和 **“表”**。  
  
3.  展开包含该列的表，然后展开 **“列”**。  
  
4.  右键单击该列并选择“属性”。 如果排序规则属性为空，则该列不是字符数据类型。  
  
###  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **查看服务器的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并在工具栏中单击 **“新建查询”**。  
  
2.  在查询窗口中，输入以下使用 SERVERPROPERTY 系统函数的语句。  
  
    ```  
    SELECT CONVERT (varchar, SERVERPROPERTY('collation'));  
    ```  
  
3.  或者，您可以使用 sp_helpsort 系统存储过程。  
  
    ```  
    EXECUTE sp_helpsort;  
    ```  
  
 **查看 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并在工具栏中单击 **“新建查询”**。  
  
2.  在查询窗口中，输入以下使用 SERVERPROPERTY 系统函数的语句。  
  
    ```  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **查看数据库的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并在工具栏中单击 **“新建查询”**。  
  
2.  在查询窗口中，输入以下使用 sys.databases 系统目录视图的语句。  
  
    ```  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  或者，您可以使用 DATABASEPROPERTYEX 的系统函数。  
  
    ```  
    SELECT CONVERT (varchar, DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **查看列的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并在工具栏中单击 **“新建查询”**。  
  
2.  在查询窗口中，输入以下使用 sys.columns 系统目录视图的语句。  
  
    ```  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [排序规则优先级 (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [sp_helpsort (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsort-transact-sql.md)  
  
  
