---
title: 创建新的计划指南 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.designer.newplanguide.f1
helpviewer_keywords:
- creating plan guides
- plan guides [SQL Server]. creating
ms.assetid: e1ad78bb-4857-40ea-a0c6-dcf5c28aef2f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9fa024e9e744fd955e4ccc323919cb22a97b7dd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151189"
---
# <a name="create-a-new-plan-guide"></a>创建新的计划指南
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建计划指南。 计划指南通过将查询提示或现有查询计划附加到查询来影响查询优化。 在计划指南中，您需要指定要优化的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句以及包含要使用的查询提示的 OPTION 子句或要用于优化查询的特定查询计划。 当查询执行时，查询优化器会将相应 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句与计划指南进行匹配，然后在运行时将此 OPTION 子句附加到查询，或使用指定的查询计划。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要创建计划指南，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   sp_create_plan_guide 的参数必须以显示的顺序提供。 为 `sp_create_plan_guide` 的参数提供值时，所有参数名称都必须显式指定，或全部不指定。 例如，如果指定了 `@name =`，则也必须指定 `@stmt =`、`@type =` 等。 同样，如果省略了 `@name =` 并仅提供了参数值，则其余的参数名称也必须省略并仅提供它们的值。 参数名称仅用于说明，以帮助了解语法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会验证指定的参数名称是否与使用此名称的位置中的参数名称相匹配。  
  
-   您可以为相同的查询和批处理或模块创建多个 OBJECT 或 SQL 计划指南。 但是，在任何给定的时间只能启用一个计划指南。  
  
-   无法为引用存储过程、函数或 DML 触发器（指定了 WITH ENCRYPTION 子句或为临时触发器）的 @module_or_batch 值创建 OBJECT 类型的计划指南。  
  
-   如果尝试删除或修改的函数、存储过程或 DML 触发器由某个计划指南引用，则不管该指南为启用状态还是禁用状态，都会导致错误。 尝试删除计划指南被引用并已为其定义触发器的表也将导致错误。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 若要创建类型为 OBJECT 的计划指南，需要拥有对被引用对象的 ALTER 权限。 若要创建类型为 SQL 或 TEMPLATE 的计划指南，需要拥有对当前数据库的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-plan-guide"></a>创建计划指南  
  
1.  单击加号以便展开您要在其中创建计划指南的数据库，然后单击加号以便展开 **“可编程性”** 文件夹。  
  
2.  右键单击**计划指南**文件夹，然后选择**新建计划指南...** .  
  
3.  在 **“新建计划指南”** 对话框的 **“名称”** 框中，输入计划指南的名称。  
  
4.  在 **“语句”** 框中，输入要对其应用计划指南的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
5.  在 **“作用域类型”** 列表中，选择 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句在其中出现的实体的类型。 这便指定了用于将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句与计划指南匹配的上下文。 可能的值为 **OBJECT**、 **SQL**和 **TEMPLATE**。  
  
6.  在 **“作用域批处理”** 框中，请输入其中出现 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的批处理文本。 批处理文本不能包括 USE``*database* 语句。 只有在 **SQL** 选择为作用域类型时， **“作用域批处理”** 框才可用。 如果在 SQL 为作用域类型时在“作用域批处理”框中未输入任何内容，则将批处理文本的值设置为与 **“语句”** 框中相同的值。  
  
7.  在 **“作用域批处理”** 列表中，输入其中包含该对象的架构的名称。 只有在 **“对象”** 选择为作用域类型时， **“作用域架构名称”** 框才可用。  
  
8.  在“作用域对象名称”  框中，输入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程的名称、用户定义的标量函数的名称、多语句表值函数的名称或其中出现 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的 DML 触发器的名称。 只有在 **“对象”** 选择为作用域类型时， **“作用域对象名称”** 框才可用。  
  
9. 在 **“参数”** 框中，输入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中嵌入的所有参数的参数名称和数据类型。  
  
     只有当下列任意一个条件为真时才会应用参数：  
  
    -   作用域类型为 **SQL** 或 **TEMPLATE**。 如果为 **TEMPLATE**，则参数不能为 NULL。  
  
    -   [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句使用 sp_executesql 进行提交，并且指定了该参数的值，或者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在参数化某语句之后内部提交该语句。  
  
10. 在 **“提示”** 框中，输入要应用于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的查询提示或查询计划。 若要指定一个或多个查询提示，请输入一个有效的 OPTION 子句。  
  
11. 单击“确定”  。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-plan-guide"></a>创建计划指南  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
  
    ```  
  
 有关详细信息，请参阅 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)。  
  
  
