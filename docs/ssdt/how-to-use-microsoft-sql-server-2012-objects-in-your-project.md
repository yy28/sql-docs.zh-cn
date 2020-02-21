---
title: 项目中的 SQL Server 2012 对象
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9baf122f-cf22-4860-98db-ef782cd972fc
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: c9ea326bc37d4843b6cb7e3bc4e21fa356af5435
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244245"
---
# <a name="how-to-use-microsoft-sql-server-2012-objects-in-your-project"></a>如何：在项目中使用 Microsoft SQL Server 2012 对象

在此示例中，你将向一个面向 Microsoft SQL Server 2012 的数据库项目中添加序列对象。  
  
Microsoft SQL Server 2012 中引入了序列。 序列是一种用户定义的架构绑定对象，它根据创建该序列时采用的规范生成一组数值。 这组数值以定义的间隔按升序或降序生成，并且可根据要求循环（重复）。  有关序列对象的详细信息，请参阅[序列号](htttp://msdn.microsoft.com/library/ff878058(SQL.110).aspx)。 有关 Microsoft SQL Server 2012 新增功能的信息，请参阅 [SQL Server 2012 中的新增功能](https://msdn.microsoft.com/library/bb500435(SQL.110).aspx)。  
  
> [!WARNING]  
> 以下过程利用在[连接的数据库开发](../ssdt/connected-database-development.md)和[面向项目的脱机数据库开发](../ssdt/project-oriented-offline-database-development.md)部分中的之前过程中创建的实体。  
  
### <a name="to-add-a-new-sequence-object-to-your-project"></a>向您的项目添加一个新的序列对象  
  
1.  在“解决方案资源管理器”中，右键单击“TradeDev”数据库项目，选择“添加”，然后选择“新项”。  
  
2.  在左窗格上单击“可编程性”，然后选择“序列”。 单击“添加”，将新对象添加到项目中。  
  
3.  将默认代码替换为以下代码。  
  
    ```  
    CREATE SEQUENCE [dbo].[Seq1]  
    AS INT  
    START WITH 1  
    INCREMENT BY 1  
    MAXVALUE 1000  
    NO CYCLE  
    CACHE 10  
    ```  
  
4.  如果项目的目标平台未设置为 Microsoft SQL Server 2012，则“错误列表”将显示 `CREATE SEQUENCE` 语句的语法错误。 若要更正此问题，请按照[如何：更改目标平台并发布数据库项目](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)主题所述相应地更改目标平台。  
  
5.  请按照[如何：更改目标平台并发布数据库项目](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)主题所述，将项目发布到已连接的 Microsoft SQL Server 2012 服务器中的数据库。  
  
### <a name="to-use-the-new-sequence-object"></a>使用新的序列对象  
  
1.  在 SQL Server 对象资源管理器中，右击你在上一个过程中发布到的数据库，然后选择“新建查询”。  
  
2.  将以下代码粘贴到查询窗口中。  
  
    ```  
    DECLARE @counter INT  
    SET @counter=0  
    WHILE @counter<10  
    BEGIN  
        SET @counter = @counter +1  
         INSERT dbo.Products (Id, Name, CustomerId) VALUES (NEXT VALUE FOR dbo.Seq1, 'ProductItem'+cast(@counter as varchar), 1)  
    END   
    GO  
    ```  
  
3.  按下“执行查询”按钮。  
  
4.  在 SQL Server 对象资源管理器中，导航到数据库中的 Products 表。 右键单击并选择“查看数据”，以便检查新添加的行。  
  
