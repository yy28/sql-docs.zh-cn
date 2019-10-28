---
title: 第 2 课：创建并应用命名标准策略 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87e51f4e-156c-4def-8572-76a15075d75e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4bd3b1b4d07b68ae693cd741e471dd5f53efae6e
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907062"
---
# <a name="lesson-2-create-and-apply-a-naming-standards-policy"></a>第 2 课：创建并应用命名标准策略
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
某些类型的基于策略的管理策略可以创建触发器，以强制要求以后符合策略。 在本课程中，您将创建一个策略以强制执行表命名标准。 然后，尝试创建一个违反该策略的表以对其进行测试。  


## <a name="prerequisites"></a>必备条件
若要完成本教程，需要 SQL Server Management Studio，以及针对运行 SQL Server 的服务器的访问权限。

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
  
## <a name="create-the-finance-database"></a>创建 Finance 数据库  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，打开查询窗口并执行以下语句：  
  
    ```sql  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  在对象资源管理器中，单击“数据库”  ，然后按 F5 键刷新数据库列表。  

## <a name="create-the-finance-tables-condition"></a>创建 Finance 表条件 

1.  在对象资源管理器中，依次展开“管理”  和“策略管理”  ，右键单击“条件”  ，然后单击“新建条件”  。 

   ![新建条件](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-condition.png)
  
2.  在“创建新条件”  对话框的“名称”  框中，键入 **Finance Tables**。  
    1. 在“Facet”  列表中，选择“多部分名称”  。 
    1. 在“表达式”  区域中，在“字段”  框中选择“\@Name”  ，在“运算符”  框中选择“Like”  ，然后在“值”  框中键入 ```'fintbl%'``` 以强制要求所有表名称以字母 fintbl  开头。
    1. 在“说明”  页中，键入 **Finance table names must begin with fintbl**，然后单击“确定”  以创建条件。  

    ![Finance 表条件](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-tables-condition.png)
 
## <a name="create-the-finance-name-policy"></a>创建 Finance Name 策略  
  
1.  在对象资源管理器中，右键单击“策略”  ，然后单击“新建策略”  。  

   ![新建策略](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-policy.png)
  
2.  在“新建新策略”  对话框的“名称”  框中，键入 **Finance Name**。
    1. 在“检查条件”  列表中，选择“Finance Tables”  。 它位于“多部分名称”  区域中。 
    1. 在“针对”  区域中，将会看到可能应用了此策略的数据库对象的列表。 选中“每个表”  复选框。
    1. 选择“已启用”  列表。 （“已启用”  框不适用于“按需”  策略。）
    1. 在“评估模式”  列表中，选择“更改时: 禁止”  。 这会对 Finance 数据库创建数据库触发器以强制实施策略。 
    1. 在“服务器限制”  列表中，选择“无”  。 
    1. 在“说明”  页上，添加“Finance 数据库中的表名必须包含 'fintbl%'”说明。 
    1. 返回到“常规”  页，在“每个数据库”  区域中，展开“每个”  ，然后单击“新建条件”  。

    ![创建新的 Finance Name 策略](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-policy-finance-name.png)
  
6.  在“创建新条件”  对话框的“名称”  框中，键入 **Finance Database**。
    1. 在“表达式”  框中，完成表达式以包含 @Name = 'Finance'，然后单击“确定”  关闭条件页。 
  
    ![创建新的“finance database”条件](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-condition.png)

    > [!NOTE]  
    > 可能需要按 Tab 键移出“值”  框才能启用“确定”  按钮。  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="create-the-finance-policy-category"></a>创建 Finance 策略类别  
  
1.  在对象资源管理器中，展开“管理”  ，右键单击“策略管理”  ，然后单击“管理类别”  。  

   ![管理类别](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-categories.png)
  
2.  在“管理策略类别”  对话框的“名称”  下的空白框中，键入 **Finance**，然后清除“托管数据库订阅”  。 “托管数据库订阅”  将强制实例中的每个数据库订阅属于该策略类别的策略。 在本课中，只有 Finance 数据库应订阅 Finance Name 策略。  

    ![管理策略类别](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-policy-categories.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="subscribe-to-the-finance-policy-category"></a>订阅 Finance 策略类别  
  
1.  在对象资源管理器中，展开“数据库”  ，右键单击“Finance”  ，指向“策略”  ，然后单击“类别”  。 

   ![Finance 策略类别](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-categories.png)
  
2.  选中“Finance”  类别的“已订阅”  复选框。  

   ![订阅 finance 策略](Media/lesson-2-create-and-apply-a-naming-standards-policy/subscribe-to-finance.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="test-the-enforcement-of-the-finance-name-policy"></a>测试 Finance Name 策略的实施情况  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，打开一个查询窗口。 执行下面的语句，以尝试创建一个违反 **Finance Name** 策略的表。 该表违反了此策略，因为表名没有以字母 **fintbl**开头。  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    请注意，此策略禁止创建该表，并返回一条提供策略名称的信息性消息。 

   ```
     Policy 'Finance Name' has been violated by 'SQLSERVER:\SQL\SQL\SQL2017\Databases\Finance\Tables\dbo.NewTable'.
     This transaction will be rolled back.
     Policy condition: '@Name LIKE 'fintbl%''
     Policy description: 'Tables names in the Finance database must contain 'fintbl%''.
     Additional help: '' : ''
     Statement: 'CREATE TABLE NewTable  
         (Col1 int)'.
     Msg 515, Level 16, State 2, Procedure msdb.sys.sp_syspolicy_execute_policy, Line 69 [Batch Start Line 2]
     Cannot insert the value NULL into column 'target_query_expression', table 'msdb.dbo.syspolicy_policy_execution_history_details_internal'; column does not allow nulls. INSERT fails.
     The statement has been terminated.
   ``` 
  
2.  若要提供有效的名称，请按如下方式修改代码并重新运行语句。  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    此时，将创建该表。  
  
## <a name="apply-the-policy-to-the-whole-server"></a>将策略应用于整个服务器  
  
1.  当前，仅 Finance 数据库订阅了 Finance 策略类别。 在很多情况下，将策略类别应用于整个服务器会更容易一些。 在对象资源管理器中，展开“管理”  ，右键单击“策略管理”  ，然后单击“管理类别”  。  
  
2.  在“管理策略类别”  对话框中，找到 Finance 类别，然后选中 Finance 类别的“托管数据库订阅”  复选框。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 现在，Finance 类别会应用于所有数据库，但创建的条件会将 Finance Name 策略限定为 Finance 数据库。 这说明了如何使用复杂的条件组合限定策略目标，以便按适当的方式在多个服务器上正确应用策略。  
  
## <a name="summary"></a>“摘要”  
本教程说明了如何创建基于策略的管理条件、策略和策略组，以及如何应用筛选器并检查基于策略的管理目标是否符合策略。  
  
## <a name="next"></a>Next  
现已学完了本教程。 若要返回到起始位置，请参阅[教程：使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md)。  
  
有关教程的列表，请参阅 [SQL Server 2016 教程](../../sql-server/tutorials-for-sql-server-2016.md)。  
  
## <a name="see-also"></a>另请参阅  
[使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
