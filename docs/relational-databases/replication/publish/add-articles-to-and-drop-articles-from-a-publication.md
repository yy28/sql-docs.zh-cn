---
title: "将项目添加到发布中以及从发布中删除项目 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "项目 [SQL Server 复制], 删除"
  - "删除项目"
  - "删除项目"
  - "添加项目"
  - "项目 [SQL Server 复制], 添加"
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 将项目添加到发布中以及从发布中删除项目 (SQL Server Management Studio)
  在新建发布向导中创建项目时，首次将其添加到发布中。 有关使用此向导的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
 创建发布后，添加和删除文章在 **文章** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。 有关添加和删除项目时的注意事项的信息，请参阅 [添加项目和删除现有发布的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### 创建发布后添加项目  
  
1.  在 **文章** 页 **发布属性-\< 发布>** 对话框中，清除 **仅显示已选中的列表中的对象** 复选框。 这样可以查看发布数据库中未发布的对象。  
  
2.  选中要添加的每个项目旁边的复选框。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### 删除项目  
  
1.  在 **文章** 页 **发布属性-\< 发布>** 对话框中，清除该复选框你想要删除的每个项目旁边。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## 另请参阅  
 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)   
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  