---
title: "教程： 使用 SQL 操作 Studio （预览版） TRANSACT-SQL 编辑器创建数据库对象 |Microsoft 文档"
description: "本教程演示简化使用 T-SQL 的 SQL 操作 Studio （预览版） 中的关键功能。"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2754a998963be5a25d00aa58dcb9b4105bb8f37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>教程： 使用 TRANSACT-SQL 编辑器创建数据库对象的[!INCLUDE[name-sos](../includes/name-sos-short.md)]

创建和运行查询，存储的过程、 脚本等将是数据库专业人员的核心任务。 本教程演示如何在 T-SQL 编辑器中创建数据库对象的主要功能。

在本教程中，你将学习如何使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]到：
> [!div class="checklist"]
> * 搜索数据库对象
> * 编辑表数据 
> * 使用代码段快地编写 T-SQL
> * 查看数据库对象详细信息使用*查看定义*和*转到定义*


## <a name="prerequisites"></a>必备条件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [连接和查询 SQL Server 使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [连接和查询使用 Azure SQL 数据库[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>快速查找的数据库对象和执行一项常见任务

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]提供搜索小组件可以快速找到数据库对象。 结果列表中的常见任务与所选对象，提供了上下文菜单如*编辑数据*表。

1. 打开服务器边栏 (**Ctrl + G**)，展开**数据库**，然后选择**TutorialDB**。 

1. 打开*TutorialDB 仪表板*通过选择**管理**从上下文菜单。

   ![上下文菜单-管理](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 找到*客户*表通过键入*自定义*在搜索小组件中。
1. 右键单击**dbo。客户**和选择**编辑数据**。

   ![快速搜索小组件](./media/tutorial-sql-editor/quick-search-widget.png)

1. 编辑**电子邮件**第一行中，类型的列 *orlando0@adventure-works.com* ，按**Enter**以保存更改。

   ![编辑数据](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-a-stored-procedure"></a>使用 T-SQL 的代码段创建一个存储的过程

### <a name="use-snippets-in-includename-sos-shortincludesname-sos-shortmd"></a>使用中的代码段[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]

1. 打开一个新的查询编辑器按**Ctrl + N**。

2. 类型**sql**在编辑器中，向下箭头**sqlCreateStoredProcedure**，按*选项卡*键以加载新的存储的过程代码段。

   ![代码段列表](./media/tutorial-sql-editor/snippet-list.png)

3. 类型*getCustomer*和全部*StoredProcedureName*条目更改为*getCustomer*。 

   ![代码段](./media/tutorial-sql-editor/snippet.png)

4. 存储过程的其余部分替换为以下 T-SQL:

    ```sql
    -- Create a new stored procedure called 'getCustomer' in schema 'dbo'
    -- Drop the stored procedure if it already exists
    IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.ROUTINES
    WHERE SPECIFIC_SCHEMA = N'dbo'
    AND SPECIFIC_NAME = N'getCustomer'
    )
    DROP PROCEDURE dbo.getCustomer
    GO
    -- Create the stored procedure in the specified schema
    CREATE PROCEDURE dbo.getCustomer
    @ID int
    -- add more stored procedure parameters here
    AS
    -- body of the stored procedure
    SELECT  c.CustomerID, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerID = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. 若要创建存储的过程，并为其提供测试运行，请按**F5**。

## <a name="use-peek-definition-and-go-to-definition"></a>使用查看定义和转到定义 

1. 通过按下打开新的编辑器**Ctrl + N**。 

2. 键入，然后选择**sqlCreateStoredProcedure**从代码段建议列表。 键入**setCustomer**为**StoredProcedureName**和**dbo**为**SchemaName**

3. 替换@param替换以下参数定义的行：

   ```sql
       @json_val nvarchar(max)
   ```

4. 存储过程的正文替换为以下代码：
   ```sql
   -- body of the stored procedure
   INSERT INTO dbo.Customers
   ```

5. 右键单击**dbo。客户**和选择**查看定义**。

   ![查看定义](./media/tutorial-sql-editor/peek-definition.png)

6. 使用表定义来完成以下的 insert 语句：

   ```sql
   INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
   ```
7. 最后一条语句应为：

   ```sql
   -- Create a new stored procedure called 'setCustomer' in schema 'dbo'
   -- Drop the stored procedure if it already exists
   IF EXISTS (
   SELECT *
       FROM INFORMATION_SCHEMA.ROUTINES
       WHERE SPECIFIC_SCHEMA = N'dbo'
       AND SPECIFIC_NAME = N'setCustomer'
   )
   DROP PROCEDURE dbo.setCustomer
   GO
   -- Create the stored procedure in the specified schema
   CREATE PROCEDURE dbo.setCustomer
       @json_val nvarchar(max) 
   AS
       -- body of the stored procedure
       INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. 若要执行该脚本，请按**F5**。

## <a name="use-save-query-results-as-json-to-test-our-stored-procedure"></a>使用将查询结果保存为 JSON 以测试我们的存储的过程

1. **选择前 1000年行**从*dbo。客户*表。

2. 在该结果视图并单击选择的第一行**将另存为 JSON**。  
3. 单击**保存**，并且用为 JSON 格式打开突出显示的行。

   ![将另存为 JSON](./media/tutorial-sql-editor/save-as-json.png)

4. 选择的 JSON 数据并将其复制。

5. 打开一个查询，用于*TutorialDB*并完成以下的测试脚本为上一步中的模板中使用的 JSON 数据。 修改的值*CustomerID*，*名称*，*位置*，和*电子邮件*。

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerID": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. 通过按执行该脚本**F5**。 该脚本插入新客户，并以 JSON 格式返回新客户的信息。 单击要打开的格式化的视图的结果。

   ![测试结果](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>后续步骤
在本教程中，您学习了如何：
> [!div class="checklist"]
> * 快速搜索架构对象
> * 编辑表数据 
> * 编写使用代码段的 T-SQL 脚本
> * 了解有关使用查看定义的数据库对象详细信息，然后转到定义


若要了解如何启用**五个最慢的查询**示例见解，请完成下一步教程：

> [!div class="nextstepaction"]
> [启用速度慢的查询示例见解小组件](tutorial-qds-sql-server.md)
