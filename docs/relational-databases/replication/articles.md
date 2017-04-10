---
title: "项目 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.articles.f1"
ms.assetid: 7c743dc6-6c6d-4c92-b711-842e1b0b273e
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 项目
  在 **“项目”** 页中，可以指定要作为项目包含在发布中的数据库对象。 如果发布的数据库对象依赖于一个或多个其他数据库对象，则必须发布所有被引用对象。 例如，如果要发布的视图依赖于一个表，则也必须发布该表。  
  
 无法发布的对象旁边有一个红色图标，并在向导页底部的信息面板中附有说明。 无法发布下列对象：  
  
-   加密的对象。  
  
-   无法在事务发布中发布没有主键的表。  
  
-   在为排队更新订阅启用的合并发布和事务发布中，无法发布表。 有关在多个发布中发布项目的详细信息，请参阅中的"发布表中多个发布"一节 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
## Oracle 发布服务器  
 Oracle 发布服务器的其他注意事项：  
  
-   有关 Oracle 发布服务器可以发布的对象的列表，请参阅 [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)。 无法发布的对象不会显示。  
  
-   有关可以发布的数据类型的列表，请参阅 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)。 带有无法发布的数据类型的列不会显示。  
  
## 列筛选器  
 通过展开某个表中的筛选此页上的列 **要发布的对象** 窗格中，然后选择所需列 (可以在筛选行 **筛选表行** 此向导页)。 由于包括安全（防止复制敏感数据）和性能（例如，避免复制较大的二进制大型对象 (BLOB) 列）在内的很多原因，筛选列非常有用。 有关列筛选，包括无法筛选的列类型的列表的详细信息请参阅 [筛选已发布数据](../../relational-databases/replication/publish/filter-published-data.md)。  
  
## 选项  
 使用 **“要发布的对象”** 窗格，可以：  
  
-   查看所有可用于复制的对象。  
  
-   通过选中对象旁边的复选框可以将相应的对象添加到发布中。  
  
-   对象类型旁边的选中复选框发布中包括的一个特定类型 （例如表） 的所有对象 (如 **表**)。  
  
-   展开表节点可以查看表中的列。  
  
-   通过清除列旁边的复选框可以将表列从发布中筛除。  
  
-   右键单击窗格中的对象可以查看该对象的命令菜单。  
  
 **项目属性**  
 单击 **项目属性**, ，然后单击以下项之一︰  
  
-   单击 **设置属性的突出显示 \< ObjectType> 文章** 启动 **项目属性-\< 对象名>** 对话框; 属性在此对话框中所做的更改仅应用于突出显示在对象窗格中的对象 **文章** 页。  
  
-   单击 **设置属性的所有 \< 对象类型> 文章**, ，以启动 **所有属性 \< ObjectType> 文章** 对话框; 属性在此对话框中所做的更改应用于该类型的对象窗格中的所有对象 **文章** 页上，包括尚未选择发布。  
  
    > [!NOTE]  
    >  属性中所做的更改 **所有属性 \< ObjectType> 文章** 对话框重写中的以前所做的任何 **项目属性-\< 对象名>** 对话框。 例如，若要为某对象类型的所有项目设置一些默认值，但还希望为单个对象设置一些属性，请首先设置所有项目的默认值。 然后再设置单个对象的属性。  
  
 **已选中的表仅用于下载**  
 仅限合并复制。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本。 选择此项可以指定在使用客户端订阅后不允许在订阅服务器上进行更改。 因为仅供下载的项目不能在订阅服务器上更新，所以跟踪元数据不会发送到订阅服务器。 这可以减少订阅服务器上的存储量并提高性能，特别是当网络连接较慢时。 此选项对应于值为 **仅下载到订阅服务器，禁止订阅服务器更改** 选项 **同步方向** 中 **项目属性** 对话框。 有关详细信息，请参阅 [对 Download-Only 项目优化合并复制性能](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
 **仅显示列表中已选中的对象**  
 选中此复选框可以只显示对象窗格中选定的项目。  
  
## 另请参阅  
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [创建发布](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
  