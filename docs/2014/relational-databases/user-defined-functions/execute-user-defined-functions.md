---
title: 执行用户定义函数 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7e9c170a187fc3ccf28301a2ee1c9ee7b626169f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196441"
---
# <a name="execute-user-defined-functions"></a>执行用户定义函数
  您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 执行 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的用户定义函数。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要执行用户定义函数，请使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 在 Transact-SQL 中，可通过使用 *value* 或使用 @*parameter_name*=*value*来提供参数。 来提供参数。参数不是事务的一部分；因此，如果在以后回退的事务中更改了参数，则此参数的值不会恢复为以前的值。 返回给调用方的值总是模块返回时的值。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 运行 EXECUTE 语句无需权限。 但是，需要对 EXECUTE 字符串内引用的安全对象具有权限。 例如，如果字符串包含 INSERT 语句，则 EXECUTE 语句的调用方对目标表必须具有 INSERT 权限。 在遇到 EXECUTE 语句时，即使 EXECUTE 语句包含于模块内，也将检查权限。 有关详细信息，请参阅 [EXECUTE (Transact-SQL)](/sql/t-sql/language-elements/execute-transact-sql)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-execute-a-user-defined-function"></a>若要执行的用户定义函数  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Declares a variable and sets it to zero.  
    -- This variable is used to return the results of the function.  
    DECLARE @ret nvarchar(15)= NULL;   
  
    -- Executes the dbo.ufnGetSalesOrderStatusText function.  
    --The function requires a value for one parameter, @Status.   
    EXEC @ret = dbo.ufnGetSalesOrderStatusText @Status= 5;   
    --Returns the result in the message tab.  
    PRINT @ret;  
    ```  
  
 有关详细信息，请参阅 [EXECUTE (Transact-SQL)](/sql/t-sql/language-elements/execute-transact-sql)。  
  
  
