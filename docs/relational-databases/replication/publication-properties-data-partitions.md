---
title: "发布属性，数据分区 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.datapartitions.f1"
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 发布属性，数据分区
  可以使用 **“发布属性”** 对话框的 **“数据分区”** 页，定义使用参数化筛选的合并发布的数据分区。 在定义分区后，您随后还可以生成这些分区的快照，为基于订阅服务器的连接属性（登录名和/或计算机名称）的不同订阅服务器提供不同的初始数据集。 如果订阅服务器在第一次同步时对其分区没有可用的快照，您还可以选择允许订阅服务器请求快照的传递和生成。 有关详细信息，请参阅 [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
## 选项  
 **添加**  
 单击 **添加** 可以定义分区。 在 **添加数据分区** 对话框框中，为指定值 **host_name （)** 和/或 **suser_sname （)**, ，并定义计划以刷新快照。  
  
 **编辑**  
 在网格中，选择现有分区，然后单击 **编辑** 来编辑相应的分区。  
  
 **删除**  
 在网格中，选择现有分区，然后单击 **删除** 以删除此分区。  
  
 **立即生成所选快照**  
 在网格中，选择一个或多个分区，然后单击 **立即生成所选的快照** 来生成这些分区的快照。  
  
 **清除现有快照**  
 在网格中，选择一个或多个分区，然后单击 **清除现有快照** 来清理这些分区的快照。  
  
 **在新订阅服务器尝试同步时，根据需要自动定义分区并生成快照**  
 如果希望允许订阅服务器请求快照的生成和应用程序，请选择此选项。 如果订阅服务器在第一次同步时对其分区没有可用的快照，则订阅服务器可能要求设置此选项。  
  
## 另请参阅  
 [创建发布](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [带有参数化筛选器的合并发布的快照](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  