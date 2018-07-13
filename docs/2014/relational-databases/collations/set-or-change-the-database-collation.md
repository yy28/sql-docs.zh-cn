---
title: 设置或更改数据库排序规则 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1284c5ea161942ab96d974549147f24cd72ae8ec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37158548"
---
# <a name="set-or-change-the-database-collation"></a>设置或更改数据库排序规则
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中设置和更改数据库排序规则。 如果未指定排序规则，则使用服务器排序规则。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要设置或更改数据库排序规则，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   仅限 Windows Unicode 的排序规则只能与 COLLATE 子句一起使用，以便将排序规则应用于列级别和表达式级别数据上的 `nchar`、`nvarchar` 和 `ntext` 数据类型。 它们不能与 COLLATE 子句一起使用以更改数据库或服务器实例的排序规则。  
  
-   如果指定的排序规则或者被引用的对象所使用的排序规则使用 Windows 不支持的代码页，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将显示错误。  
  
###  <a name="Recommendations"></a> 建议  
  
-   你可以在 [Windows 排序规则名称 (Transact-SQL)](/sql/t-sql/statements/windows-collation-name-transact-sql) 和 [SQL Server 排序规则名称 (Transact-SQL)](/sql/t-sql/statements/sql-server-collation-name-transact-sql)中找到支持的排序规则名称，或者可以使用 [sys.fn_helpcollations (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql) 系统函数。  
  
-   更改数据库排序规则时，需要更改下列内容：  
  
    -   将系统表中的任何 `char`、`varchar`、`text`、`nchar`、`nvarchar` 或 `ntext` 列更改为使用新的排序规则。  
  
    -   将存储过程和用户定义函数的所有现有 `char`、`varchar`、`text`、`nchar`、`nvarchar` 或 `ntext` 参数和标量返回值更改为使用新的排序规则。  
  
    -   `char`， `varchar`， `text`， `nchar`， `nvarchar`，或`ntext`系统数据类型，并基于这些系统数据类型的所有用户定义数据类型更改为新的默认排序规则。  
  
-   可以使用 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) 语句的 COLLATE 子句来更改在用户数据库中创建的任何新对象的排序规则。 使用此语句不能更改任何现有用户定义的表中列的排序规则。 使用 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)的 COLLATE 子句可以更改这些列的排序规则。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 CREATE DATABASE  
 需要对 **master** 数据库的 CREATE DATABASE 权限，或者需要 CREATE ANY DATABASE 或 ALTER ANY DATABASE 权限。  
  
 ALTER DATABASE  
 需要对数据库拥有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>设置或更改数据库排序规则  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，再依次展开该实例、 **“数据库”**。  
  
2.  如果您正在创建一个新数据库，则右键单击 **“数据库”** ，然后单击 **“新建数据库”**。 如果您不希望使用默认排序规则，则单击 **“选项”** 页，然后从 **“排序规则”** 下拉列表中选择某一排序规则。  
  
     或者，如果数据库已经存在，则右键单击所需数据库，然后单击 **“属性”**。 单击 **“选项”** 页，然后从 **“排序规则”** 下拉列表中选择某一排序规则。  
  
3.  在完成后，单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>设置数据库排序规则  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例演示如何使用 [COLLATE](/sql/t-sql/statements/collations) 子句来指定排序规则名称。 此示例创建使用 `MyOptionsTest` 排序规则的数据库 `Latin1_General_100_CS_AS_SC` 。 在创建数据库后，执行 `SELECT` 语句以验证设置。  
  
```tsql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
#### <a name="to-change-the-database-collation"></a>更改数据库排序规则  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例说明如何在 [ALTER DATABASE](/sql/t-sql/statements/collations) 语句中使用 [COLLATE](/sql/t-sql/statements/alter-database-transact-sql) 子句来更改排序规则名称。 执行 `SELECT` 语句以验证更改。  
  
```tsql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
## <a name="see-also"></a>请参阅  
 [排序规则和 Unicode 支持](collation-and-unicode-support.md)   
 [sys.fn_helpcollations (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [SQL Server 排序规则名称 (Transact-SQL)](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Windows 排序规则名称 (Transact-SQL)](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [COLLATE (Transact-SQL)](/sql/t-sql/statements/collations)   
 [排序规则优先级 (Transact-SQL)](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql)   
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER TABLE (Transact-SQL)](/sql/t-sql/statements/alter-table-transact-sql)   
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
