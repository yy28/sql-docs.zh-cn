---
title: "用户定义函数 | Microsoft Docs"
ms.custom: ""
ms.date: "08/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-udf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "用户定义函数 [SQL Server], 组件"
  - "user-defined functions [SQL Server], about user-defined functions"
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 23
---
# 用户定义函数
  与编程语言中的函数类似，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户定义函数是接受参数、执行操作（例如复杂计算）并将操作结果以值的形式返回的例程。 返回值可以是单个标量值或结果集。  
   
##  <a name="Benefits"></a> 用户定义函数  
为什么要使用它们？ 
  
-   允许模块化程序设计。  
  
     只需创建一次函数并将其存储在数据库中，以后便可以在程序中调用任意次。 用户定义函数可以独立于程序源代码进行修改。  
  
-   执行速度更快。  
  
     与存储过程相似，[!INCLUDE[tsql](../../includes/tsql-md.md)] 用户定义函数通过缓存计划并在重复执行时重用它来降低 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码的编译开销。 这意味着每次使用用户定义函数时均无需重新解析和重新优化，从而缩短了执行时间。  
  
     和用于计算任务、字符串操作和业务逻辑的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数相比，CLR 函数具有显著的性能优势。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数更适用于数据访问密集型逻辑。  
  
-   减少网络流量。  
  
     基于某种无法用单一标量的表达式表示的复杂约束来过滤数据的操作，可以表示为函数。 然后，此函数便可以在 WHERE 子句中调用，以减少发送至客户端的数字或行数。  
  
> **注意：**查询中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 用户定义函数只能针对单个线程执行（串行执行计划）。  
  
##  <a name="FunctionTypes"></a> 函数类型  
**标量函数**  
 用户定义标量函数返回在 RETURNS 子句中定义的类型的单个数据值。 对于内联标量函数，没有函数体；标量值是单个语句的结果。 对于多语句标量函数，定义在 BEGIN...END 块中的函数体包含一系列返回单个值的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 返回类型可以是除 **text**、 **ntext**、 **image**、 **cursor**和 **timestamp**外的任何数据类型。 
 **[示例。](https://msdn.microsoft.com/library/bb386973(v=vs.110).aspx)**
  
**表值函数**  
 用户定义的表值函数返回 **table** 数据类型。 对于内联表值函数，没有函数主体；表是单个 SELECT 语句的结果集。 **[示例。](https://msdn.microsoft.com/library/bb386954(v=vs.110).aspx)**
  
**系统函数**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了许多系统函数，可用于执行各种操作。 这些函数不能修改。 有关详细信息，请参阅[内置函数 (Transact-SQL)](../Topic/Built-in%20Functions%20\(Transact-SQL\).md)、[系统存储函数 (Transact-SQL)](../Topic/System%20Stored%20Functions%20\(Transact-SQL\).md) 和[动态管理视图和函数 (Transact-SQL)](../Topic/Dynamic%20Management%20Views%20and%20Functions%20\(Transact-SQL\).md)。  
  
##  <a name="Guidelines"></a> 指导原则  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在函数中，将会区别处理导致语句被删除并继续执行模块（如触发器或存储过程）中的下一个语句的错误。 在函数中，上述错误会导致停止执行函数。 接下来该操作导致取消调用该函数的语句。  
  
 BEGIN...END 块中的语句不能有任何副作用。 函数副作用是指对具有函数外作用域（例如数据库表的修改）的资源状态的任何永久性更改。 函数中的语句唯一能做的更改是对函数上的局部对象（如局部游标或局部变量）的更改。 不能在函数中执行的操作包括：对数据库表的修改，对不在函数上的局部游标进行操作，发送电子邮件，尝试修改目录，以及生成返回至用户的结果集。  
  
> **注意：**如果 CREATE FUNCTION 语句对在发出 CREATE FUNCTION 语句时不存在的资源产生副作用，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将执行该语句。 但在调用函数时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不执行此函数。  
  
 在查询中指定的函数的实际执行次数在优化器生成的执行计划间可能不同。 示例为 WHERE 子句中的子查询调用的函数。 子查询及其函数执行的次数会因优化器选择的访问路径的不同而异。  
  
##  <a name="ValidStatements"></a> 函数中的有效语句  
 函数中的有效语句的类型包括：  
  
-   DECLARE 语句，该语句可用于定义函数局部的数据变量和游标。  
  
-   为函数局部对象的赋值，如使用 SET 为标量和表局部变量赋值。  
  
-   游标操作，该操作引用在函数中声明、打开、关闭和释放的局部游标。 不允许使用 FETCH 语句将数据返回到客户端。 仅允许使用 FETCH 语句通过 INTO 子句给局部变量赋值。  
  
-   TRY...CATCH 语句以外的流控制语句。  
  
-   SELECT 语句，该语句包含具有为函数的局部变量赋值的表达式的选择列表。  
  
-   INSERT、UPDATE 和 DELETE 语句，这些语句修改函数的局部表变量。  
  
-   EXECUTE 语句，该语句调用扩展存储过程。  
  
### 内置系统函数  
 下列具有不确定性的内置函数可以在 Transact-SQL 用户定义函数中使用。  
  
|||  
|-|-|  
|CURRENT_TIMESTAMP|@@MAX_CONNECTIONS|  
|GET_TRANSMISSION_STATUS|@@PACK_RECEIVED|  
|GETDATE|@@PACK_SENT|  
|GETUTCDATE|@@PACKET_ERRORS|  
|@@CONNECTIONS|@@TIMETICKS|  
|@@CPU_BUSY|@@TOTAL_ERRORS|  
|@@DBTS|@@TOTAL_READ|  
|@@IDLE|@@TOTAL_WRITE|  
|@@IO_BUSY||  
  
 下列不确定性内置函数**不能**在 Transact-SQL 用户定义函数中使用。  
  
|||  
|-|-|  
|NEWID|RAND|  
|NEWSEQUENTIALID|TEXTPTR|  
  
 有关确定性和不确定性的内置系统函数的列表，请参阅[确定性和不确定性的函数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
##  <a name="SchemaBound"></a> 绑定到架构的函数  
 CREATE FUNCTION 支持 SCHEMABINDING 子句，后者可将函数绑定到它引用的任何对象（如表、视图和其他用户定义函数）的架构。 尝试更改或删除绑定到架构的函数所引用的任何对象失败。  
  
 必须满足以下条件才能在 [CREATE FUNCTION](https://msdn.microsoft.com/library/ms186755.aspx) 中指定 SCHEMABINDING：  
  
-   该函数引用的所有视图和用户定义函数必须是绑定到架构的视图和函数。  
  
-   该函数引用的所有对象必须与该函数位于同一数据库中。 必须使用由一部分或两部分构成的名称来引用对象。  
  
-   必须具有该函数中引用的所有对象（表、视图和用户定义函数）的 REFERENCES 权限。  
  
 可使用 ALTER FUNCTION 删除架构绑定。 ALTER FUNCTION 语句会在不指定 WITH SCHEMABINDING 的情况下重新定义函数。  
  
##  <a name="Parameters"></a> 指定参数  
 用户定义函数采用零个或多个输入参数并返回标量值或表。 一个函数最多可以有 1024 个输入参数。 如果函数的参数有默认值，则调用该函数时必须指定 DEFAULT 关键字，才能获取默认值。 此行为与在用户定义存储过程中具有默认值的参数不同，在后一种情况下，忽略参数同样意味着使用默认值。 用户定义函数不支持输出参数。  
  
##  <a name="Tasks"></a> 更多示例！  
  
|||  
|-|-|  
|**任务说明**|**主题**|  
|介绍如何创建 Transact-SQL 用户定义函数。|[创建用户定义函数（数据库引擎）](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)|  
|介绍如何创建 CLR 函数。|[创建 CLR 函数](../../relational-databases/user-defined-functions/create-clr-functions.md)|  
|介绍如何创建用户定义聚合函数。|[创建用户定义聚合](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)|  
|介绍如何修改 Transact-SQL 用户定义函数。|[修改用户定义函数](../../relational-databases/user-defined-functions/modify-user-defined-functions.md)|  
|介绍如何删除用户定义函数。|[删除用户定义函数](../../relational-databases/user-defined-functions/delete-user-defined-functions.md)|  
|介绍如何执行用户定义函数。|[执行用户定义函数](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)|  
|介绍如何重命名用户定义函数。|[重命名用户定义函数](../../relational-databases/user-defined-functions/rename-user-defined-functions.md)|  
|介绍如何查看用户定义函数的定义。|[查看用户定义函数](../../relational-databases/user-defined-functions/view-user-defined-functions.md)|  
  
  