---
title: 授予访问数据库的权限 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 75d4f048573ce60b0be6704196b376c8136aa213
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424086"
---
# <a name="lesson-2-2---granting-access-to-a-database"></a>第 2-2 课 - 授予访问数据库的权限
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
现在 Mary 具有访问此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的权限，但是不具有访问数据库的权限。 在授权她作为数据库用户之前，她甚至无权访问其默认数据库 **TestData** 。  
  
若要授予 Mary 访问权限，请切换到 **TestData** 数据库，再使用 CREATE USER 语句将她的登录名映射到名为 Mary 的用户。  
  
### <a name="to-create-a-user-in-a-database"></a>在数据库中创建用户  
  
1.  键入并执行下列语句（将 `computer_name` 替换为您计算机的名称），以授予 `Mary` 访问 `TestData` 数据库的权限。  
  
    ```  
    USE [TestData];  
    GO  
  
    CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
    GO  
  
    ```  
  
    现在，对于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 `TestData` 数据库，Mary 都具有访问权限。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[创建视图和存储过程](../t-sql/lesson-2-3-creating-views-and-stored-procedures.md)  
  
  
  
