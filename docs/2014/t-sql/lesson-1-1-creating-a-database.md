---
title: 创建数据库（教程）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tutorial creating a database
ms.assetid: e1e2c83f-dfad-4bb8-aa7a-09d3f69517ae
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c4f5933c5e653ee4c219e289dc71a8032b056f34
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196583"
---
# <a name="creating-a-database-tutorial"></a>创建数据库（教程）
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
>  在单个批处理中提交多条语句时，可以用关键字 GO 分隔各语句。 当批处理只包含一条语句时，GO 是可选的。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建表&#40;教程&#41;](lesson-1-2-creating-a-table.md)  
  
## <a name="see-also"></a>请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
