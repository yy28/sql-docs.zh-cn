---
title: "创建数据库 （教程） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorial creating a database
ms.assetid: e1e2c83f-dfad-4bb8-aa7a-09d3f69517ae
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6628dcf0ab38db441de9bd9324e69993e5759c38
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-1---creating-a-database"></a>课程 1-1-创建数据库
与许多 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句一样，CREATE DATABASE 语句具有一个必需参数：数据库的名称。 CREATE DATABASE 还具有许多可选参数，如希望放置数据库文件的磁盘位置。 在您执行不带可选参数的 CREATE DATABASE 时， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用其中许多参数的默认值。 本教程使用的可选语法参数非常少。  
  
### <a name="to-create-a-database"></a>创建数据库  
  
1.  在查询编辑器窗口中，键入以下代码，但不要执行它：  
  
    ```  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  使用指针选择词语 `CREATE DATABASE`，再按 **F1**。 应该会打开 SQL Server 联机丛书中的 CREATE DATABASE 主题。 您可以使用此方法查找 CREATE DATABASE 以及在本教程中使用的其他语句的完整语法。  
  
3.  在查询编辑器中，按 **F5** 以执行语句并创建名为 `TestData`的数据库。  
  
创建数据库时， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 制作 **model** 数据库的副本，并将该副本重命名为数据库名称。 除非您将初始大小很大的数据库指定为可选参数，否则此操作应该只需要几秒钟。  
  
> [!NOTE]  
> 在单个批处理中提交多条语句时，可以用关键字 GO 分隔各语句。 当批处理只包含一条语句时，GO 是可选的。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[创建表（教程）](../t-sql/lesson-1-2-creating-a-table.md)  
  
## <a name="see-also"></a>另请参阅  
[CREATE DATABASE (SQL Server Transact-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
  

