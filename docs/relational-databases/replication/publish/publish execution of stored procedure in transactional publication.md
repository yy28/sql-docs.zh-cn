---
title: "在事务发布中发布存储过程的执行 (SQL Server Management Studio) | Microsoft Docs"
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
  - "发布 [SQL Server 复制]，存储过程执行"
  - "存储过程 [SQL Server 复制]，发布"
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 在事务发布中发布存储过程的执行 (SQL Server Management Studio)
  指定应在中发布的存储的过程 （而不只是其定义） 执行 **项目属性-\< 项目>** 对话框。 此对话框可在新建发布向导和 **发布属性-\< 发布>** 对话框。 有关使用向导和访问对话框中的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md) 和 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
 初始化订阅时，过程定义（CREATE PROCEDURE 语句）将被复制到订阅服务器上；当在发布服务器上执行过程时，复制将在订阅服务器上执行相应的过程。  
  
### 发布存储过程的执行  
  
1.  在 **文章** 新建发布向导的页面或 **发布属性-\< 发布>** 对话框框中，选择一个存储的过程。  
  
2.  单击 **“项目属性”**，然后单击 **“设置突出显示的存储过程项目的属性”**。  
  
3.  在 **项目属性-\< 项目>** 对话框框中，指定以下值之一 **复制** 选项︰  
  
    -   **存储过程的执行**  
  
    -   **SP 的序列化事务中的执行**  
  
         建议选择此选项，因为此选项仅当过程在可序列化事务的上下文中执行时才复制过程的执行。 如果存储过程在可序列化事务的外部执行，则已发布表中的数据更改将复制为一系列数据操作语言 (DML) 语句。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您在 **发布属性-\< 发布>** 对话框中，单击 **确定** 以保存并关闭对话框。  
  
## 另请参阅  
 [在事务复制中发布存储过程执行](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  