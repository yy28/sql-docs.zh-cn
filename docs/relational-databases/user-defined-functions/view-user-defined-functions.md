---
title: 查看用户定义函数 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.udfproperties.general.f1
- sql13.swb.functionproperties.general.f1
helpviewer_keywords:
- displaying user-defined functions
- viewing user-defined functions
- user-defined functions [SQL Server], viewing
- status information [SQL Server], user-defined functions
ms.assetid: a45dfab5-6384-4311-b935-2e23a70c5c10
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1197244abd63560bf6fa9d76401c0836b833c6a5
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581420"
---
# <a name="view-user-defined-functions"></a>查看用户定义函数
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]可以获取有关用户定义函数的定义或属性的信息。 您可能需要查看函数的定义，以理解其数据从源表中派生的方式或查看函数所定义的数据。  
  
> [!IMPORTANT]  
>  如果您更改函数所引用的对象的名称，则必须修改函数，使其文本反映新名称。 因此，在重命名对象前，首先显示该对象的依赖关系，以确定所建议的更改是否影响任何函数。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要获取有关函数的信息，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 使用 **sys.sql_expression_dependencies** 查找函数的依赖关系要求对该数据库具有 VIEW DEFINITION 权限，以及对数据库具有 **sys.sql_expression_dependencies** 的 SELECT 权限。 系统对象定义（如 OBJECT_DEFINITION 中返回的对象定义）是公开可见的。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-show-a-user-defined-functions-properties"></a>显示用户定义函数的属性  
  
1.  在 **“对象资源管理器”** 中，单击包含要查看属性的函数的数据库旁边的加号，然后单击加号以展开 **“可编程性”** 文件夹。  
  
2.  单击加号以便展开 **“函数”** 文件夹。  
  
3.  单击加号以展开包含您要查看属性的函数的文件夹：  
  
    -   Table-valued Function  
  
    -   标量值函数  
  
    -   Aggregate 函数  
  
4.  右键单击要查看其属性的函数，然后选择“属性”  。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     The following properties appear in the **Function Properties -** _function_name_ dialog box.  
  
     **Database**  
     The name of the database containing this function.  
  
     **Server**  
     The name of the current server instance.  
  
     **User**  
     The name of the user of this connection.  
  
     **Created date**  
     Displays the date the function was created.  
  
     **Execute As**  
     Execution context for the function.  
  
     **Name**  
     The name of the current function.  
  
     **Schema**  
     Displays the schema that owns the function.  
  
     **System object**  
     Indicates whether the function is a system object. Values are True and False.  
  
     **ANSI NULLs**  
     Indicates if the object was created with the ANSI NULLs option.  
  
     **Encrypted**  
     Indicates whether the function is encrypted. Values are True and False.  
  
     **Function Type**  
     The type of user defined function.  
  
     **Quoted identifier**  
     Indicates if the object was created with the quoted identifier option.  
  
     **Schema bound**  
     Indicates whether the function is schema-bound. Values are True and False. For information about schema-bound functions, see the SCHEMABINDING section of [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-get-the-definition-and-properties-of-a-function"></a>获取函数的定义和属性  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例之一复制并粘贴到查询窗口中，然后单击 **“执行”** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the function name, definition, and relevant properties  
    SELECT sm.object_id,   
       OBJECT_NAME(sm.object_id) AS object_name,   
       o.type,   
       o.type_desc,   
       sm.definition,  
       sm.uses_ansi_nulls,  
       sm.uses_quoted_identifier,  
       sm.is_schema_bound,  
       sm.execute_as_principal_id  
    -- using the two system tables sys.sql_modules and sys.objects  
    FROM sys.sql_modules AS sm  
    JOIN sys.objects AS o ON sm.object_id = o.object_id  
    -- from the function 'dbo.ufnGetProductDealerPrice'  
    WHERE sm.object_id = OBJECT_ID('dbo.ufnGetProductDealerPrice')  
    ORDER BY o.type;  
    GO  
  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the definition of the function dbo.ufnGetProductDealerPrice  
    SELECT OBJECT_DEFINITION (OBJECT_ID('dbo.ufnGetProductDealerPrice')) AS ObjectDefinition;  
    GO  
    ```  
  
 有关详细信息，请参阅 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 和 [OBJECT_DEFINITION (Transact-SQL)](../../t-sql/functions/object-definition-transact-sql.md)。  
  
#### <a name="to-get-the-dependencies-of-a-function"></a>获取函数的依赖关系  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get all of the dependency information  
    SELECT OBJECT_NAME(sed.referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(sed.referencing_id, sed.referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        sed.referencing_class_desc, sed.referenced_class_desc,  
        sed.referenced_server_name, sed.referenced_database_name, sed.referenced_schema_name,  
        sed.referenced_entity_name,   
        COALESCE(COL_NAME(sed.referenced_id, sed.referenced_minor_id), '(n/a)') AS referenced_column_name,  
        sed.is_caller_dependent, sed.is_ambiguous  
    -- from the two system tables sys.sql_expression_dependencies and sys.object  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    -- on the function dbo.ufnGetProductDealerPrice  
    WHERE sed.referencing_id = OBJECT_ID('dbo.ufnGetProductDealerPrice');  
    GO  
    ```  
  
 有关详细信息，请参阅 [sys.sql_expression_dependencies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 和 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。  
  
  
