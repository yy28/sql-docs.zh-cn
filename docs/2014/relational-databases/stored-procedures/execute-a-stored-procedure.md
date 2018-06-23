---
title: 执行存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-stored-procs
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.executeprocedure.f1
- sql12.swb.executeprocedure.general.f1
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- extended stored procedures [SQL Server], executing
- system stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- user-defined stored procedures [SQL Server]
ms.assetid: a0b1337d-2059-4872-8c62-3f967d8b170f
caps.latest.revision: 37
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7ee1299fa575af8e2d19798a2bd38bf0a7a0acf4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026508"
---
# <a name="execute-a-stored-procedure"></a>执行存储过程
  本主题介绍如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中执行存储过程。  
  
 有两种不同方法执行存储过程。 第一种方法和最常见的方法供应用程序或用户调用过程。 第二种方法是将过程设置为在启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时自动运行。 当应用程序或用户调用过程时，调用中显式声明了 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 或 EXEC 关键字。 或者，如果过程是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理中的第一条语句，那么不使用关键字也可以调用并执行此过程。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要执行存储过程，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   与系统过程名称匹配时使用调用数据库排序规则。 因此，在过程调用中始终使用系统过程名称的正确大小写形式。 例如，如果在具有区分大小写的排序规则的数据库上下文中执行，以下代码将失败：  
  
    ```tsql  
    EXEC SP_heLP; -- Will fail to resolve because SP_heLP does not equal sp_help  
    ```  
  
     若要显示确切的系统过程名称，请查询 [sys.system_objects](/sql/relational-databases/system-catalog-views/sys-system-objects-transact-sql) 和 [sys.system_parameters](/sql/relational-databases/system-catalog-views/sys-system-parameters-transact-sql) 目录视图。  
  
-   如果用户定义的过程与系统过程同名，则可能不会执行用户定义的过程。  
  
###  <a name="Recommendations"></a> 建议  
  
-   执行系统存储过程  
  
     系统过程以前缀 **sp_** 开头。 因为从逻辑意义上讲，这些过程出现在所有用户定义的数据库和系统定义的数据库中，所以可以从任何数据库执行这些过程，而不必完全限定过程名称。 但是，建议使用 **sys** 架构名称对所有系统过程名称进行架构限定，以防止名称冲突。 以下示例说明调用系统过程的推荐方法。  
  
    ```tsql  
    EXEC sys.sp_who;  
    ```  
  
-   执行用户定义存储过程  
  
     当执行用户定义的过程时，我们建议使用架构名称限定过程名称。 这种做法使性能得到小幅提升，因为 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 不必搜索多个架构。 如果某个数据库在多个架构中具有同名过程，则这还可以防止执行错误的过程。  
  
     以下示例说明执行用户定义过程的推荐方法。 请注意，此过程接受一个输入参数。 有关指定输入参数和输出参数的信息，请参阅 [指定参数](specify-parameters.md)。  
  
    ```tsql  
    USE AdventureWorks2012;  
    GO  
    EXEC dbo.uspGetEmployeeManagers @BusinessEntityID = 50;  
    ```  
  
     -或-  
  
    ```tsql  
    EXEC AdventureWorks2012.dbo.uspGetEmployeeManagers 50;  
    GO  
    ```  
  
     如果指定了非限定的用户定义过程，则 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 按以下顺序搜索此过程：  
  
    1.  当前数据库的 **sys** 架构。  
  
    2.  调用方的默认架构（如果它在批处理或动态 SQL 中执行）。 或者，如果非限定的过程名称出现在另一个过程定义的主体中，则接着搜索包含后一过程的架构。  
  
    3.  当前数据库中的 **dbo** 架构。  
  
-   自动执行存储过程  
  
     在每次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时将执行标记为自动执行的过程，并在启动过程期间中恢复 **master** 数据库。 将这些过程设置为自动执行对执行数据库维护操作或使这些过程作为后台进程连续运行很有用。 自动执行的另一个用途是使该过程执行 **tempdb**中的系统或维护任务，如创建一个全局临时表。 这将确保在 **启动过程中重新创建** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，始终存在这样一个临时表。  
  
     自动执行的过程使用与固定服务器角色 **sysadmin** 的成员相同的权限进行操作。 该过程生成的所有错误消息都将写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志。  
  
     虽然对启动过程的数目没有限制，但是请注意，在执行时每个启动过程将占用一个工作线程。 如果必须在启动时执行多个过程，但不需要并行执行，则可以指定一个过程作为启动过程，让该过程调用其他过程。 这样就只占用一个工作线程。  
  
    > [!TIP]  
    >  请勿从自动执行的过程中返回任何结果集。 因为该过程是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而不是由应用程序或用户执行的，所以结果集将无处可去。  
  
-   设置、清除和控制自动执行  
  
     只有系统管理员 (**sa**) 可以将过程标记为自动执行。 另外，该过程必须在 **master** 数据库中，由 **sa**所有，而且不能有输入或输出参数。  
  
     使用 [sp_procoption](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql) 可以：  
  
    1.  将现有过程指定为启动过程。  
  
    2.  阻止过程在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动时执行。  
  
###  <a name="Security"></a> 安全性  
 有关详细信息，请参阅 [EXECUTE AS (Transact-SQL)](/sql/t-sql/statements/execute-as-transact-sql) 和 [EXECUTE AS 子句 (Transact-SQL)](/sql/t-sql/statements/execute-as-clause-transact-sql)。  
  
####  <a name="Permissions"></a> Permissions  
 有关详细信息，请参阅 [EXECUTE (Transact-SQL)](/sql/t-sql/language-elements/execute-transact-sql)中执行存储过程。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-execute-a-stored-procedure"></a>执行存储过程  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，再依次展开该实例、 **“数据库”**。  
  
2.  展开所需的数据库，然后依次展开 **“可编程性”** 和 **“存储过程”**。  
  
3.  右键单击所需的用户定义存储过程，然后单击“执行存储过程”。  
  
4.  在 **“执行过程”** 对话框中，为每个参数指定一个值以及它是否应传递 Null 值。  
  
     **参数**  
     指示参数的名称。  
  
     **数据类型**  
     指示参数的数据类型。  
  
     **输出参数**  
     指示是否为输出参数。  
  
     **传递空值**  
     将 NULL 作为参数值传递。  
  
     **ReplTest1**  
     在调用过程时键入参数的值。  
  
5.  若要执行存储过程，请单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-execute-a-stored-procedure"></a>执行存储过程  
  
1.  连接到[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例演示如何执行应有一个参数的存储过程。 该示例执行 `uspGetEmployeeManagers` 存储过程，并将值  `6` 指定为 `@EmployeeID` 参数。  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
#### <a name="to-set-or-clear-a-procedure-for-executing-automatically"></a>设置或清除过程自动执行  
  
1.  连接到[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例演示如何使用 [sp_procoption](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql) 设置过程自动执行。  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';  
```  
  
#### <a name="to-stop-a-procedure-from-executing-automatically"></a>阻止过程自动执行  
  
1.  连接到[!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例说明如何使用 [sp_procoption](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql) 阻止过程自动执行。  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';  
```  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
  
## <a name="see-also"></a>请参阅  
 [指定参数](specify-parameters.md)   
 [配置 scan for startup procs 服务器配置选项](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)   
 [EXECUTE (Transact-SQL)](/sql/t-sql/language-elements/execute-transact-sql)   
 [CREATE PROCEDURE (Transact-SQL)](/sql/t-sql/statements/create-procedure-transact-sql)   
 [存储过程（数据库引擎）](stored-procedures-database-engine.md)  
  
  
