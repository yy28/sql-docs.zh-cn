---
title: 如何：显示 Transact-SQL 脚本的大纲和向 Transact-SQL 脚本添加代码片段 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 543e7ce7-8639-4281-8a91-85314755e5de
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b08337c4602e7eaad2da376b22caa8f806e5b18
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093716"
---
# <a name="how-to-outline-and-add-snippets-to-transact-sql-script"></a>如何显示 Transact-SQL 脚本的大纲和向 Transact-SQL 脚本添加代码段
SQL Server Data Tools 包括一个由代码段组成的代码库，可以直接将这些代码段插入到自己的应用程序中。 每个代码段都执行一项完整的脚本任务，如创建函数、表、触发器、索引、视图、用户定义数据类型等。你只需很少的鼠标单击操作即可将代码段插入源代码。 这些代码段可以通过减少您在键入上所用的时间，提高您的工作效率。  
  
需要浏览相应的代码段时，您可以使用代码段选择器，其中给出了可供选择的代码段的分类列表。 一旦您向代码添加了代码段后，就可能存在需要自定义的部分，例如使用更合适的名称替换变量名称，或者放置于存储过程的实际逻辑中。 您将注意到，插入的代码段代码在代码中有一个或多个针对此用途的突出显示的替换点。 如果将鼠标指针放置在替换点上，将出现一个工具提示，说明应该如何更改此代码。  
  
默认情况下，所有文本都会显示在 Transact\-SQL 编辑器中，但你可以选择在视图中隐藏某些代码。 Transact\-SQL 编辑器允许你选择代码的某个区域并且使其可折叠，以便它出现在加号 (+) 之下。然后，你可以通过单击该符号旁的加号 (+)，展开或隐藏该区域。 以大纲方式显示的代码并没有被删除，只是在视图中隐藏起来而已。  
  
> [!WARNING]  
> 以下过程利用在[连接的数据库开发](../ssdt/connected-database-development.md)和[面向项目的脱机数据库开发](../ssdt/project-oriented-offline-database-development.md)部分中的之前过程中创建的实体。  
  
### <a name="to-insert-snippets"></a>插入代码段  
  
1.  在“解决方案资源管理器”中，右键单击“TradeDev”项目，选择“添加”，然后选择“脚本”。 在“添加新项”对话框中，单击“添加”。  
  
2.  右键单击 Transact\-SQL 编辑器，然后选择“插入代码段”。 代码段选择器随即显示。  
  
3.  在代码段选择器中双击“表”，然后双击“创建表”。  
  
4.  请注意，替换点用黄色突出显示。 将鼠标指针悬停在 `Sample_Table` 上，信息提示将显示替换说明。 双击 `Sample_Table` 并将其更改为 `Shipper2`.  
  
5.  使用 Tab 键移到下一个替换点 `column_1`。 将其重命名为 `Id`。 按照相同的步骤将 `column_2` 重命名为 `name`，然后将其数据类型更改为 `nvarchar(128)` 并且允许 `NULL`。  
  
### <a name="to-outline-code"></a>显示代码大纲  
  
1.  请注意 CREATE TABLE 语句旁的 – 符号。 单击脚本中某一部分旁的 - 符号可以将其隐藏起来。  
  
2.  右键单击 Transact\-SQL 编辑器并且选择“大纲显示”，然后选择“停止大纲显示”以便在不影响编辑器中的基础代码的情况下删除大纲信息。  
  
3.  若要开始再次显示代码大纲，请右键单击 Transact\-SQL 编辑器并且选择“大纲显示”，然后选择“启动自动大纲显示”。 还可以选择“切换所有大纲显示”以便切换展开/隐藏部分。  
  
