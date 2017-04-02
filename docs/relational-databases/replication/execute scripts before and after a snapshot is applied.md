---
title: "在应用快照之前和之后执行脚本 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照 [SQL Server 复制], 脚本"
  - "脚本 [SQL Server 复制], 快照"
  - "快照复制 [SQL Server], 脚本"
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 在应用快照之前和之后执行脚本 (SQL Server Management Studio)
  指定在应用快照前后执行的可选脚本 **快照** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
> [!NOTE]  
>  这些选项将不可用如果 **快照格式** 选项设置为 **字符**。  
  
### 在应用快照前后执行脚本  
  
1.  在 **快照** 页 **发布属性-\< 发布>** 对话框中︰  
  
    -   若要指定在应用快照之前执行的脚本，请单击 **“浏览”** 导航到该脚本，或者在 **“应用快照之前执行此脚本”** 文本框中输入该脚本的路径。  
  
        > [!NOTE]  
        >  分发代理或合并代理必须对指定目录具有读取权限。 如果使用请求订阅，您必须指定一个共享的目录作为通用命名约定 (UNC) 路径，如 \\\computername\scripts\myscript.sql。  
  
    -   若要指定在应用快照之后执行的脚本，请单击 **“浏览”** 导航到该脚本，或者在 **“应用快照之后执行此脚本”** 文本框中输入该脚本的 UNC 路径。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另请参阅  
 [配置快照属性和 #40;复制 TRANSACT-SQL 编程 & #41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [更改发布和项目属性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [在应用快照之前和之后执行脚本](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  