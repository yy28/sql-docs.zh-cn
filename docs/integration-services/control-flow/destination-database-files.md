---
title: "目标数据库文件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transferdatabasetask.destdbfiles.f1"
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# 目标数据库文件
  可以使用 **“目标数据库文件”** 对话框查看或更改目标服务器上的数据库文件的名称和位置，或为传输数据库任务指定网络文件位置。 有关此任务的详细信息，请参阅[传输数据库任务](../../integration-services/control-flow/transfer-database-task.md)。  
  
 若要使用源服务器上数据库文件的名称和位置自动填充此对话框，请首先在 **“传输数据库任务编辑器”**对话框的 **“数据库”**页中指定 **SourceConnection** 、 **SourceDatabaseName** 和 **SourceDatabaseFiles** 。  
  
## 选项  
 **目标文件**  
 目标服务器上作为传输目标的数据库文件的名称。  
  
 请输入文件名，或单击文件名以编辑该名称。  
  
 **目标文件夹**  
 数据库文件要传输到的目标服务器上的文件夹。  
  
 请输入文件夹路径，单击文件夹路径以编辑该路径，或单击“浏览”以找到数据库文件要传输到的目标服务器上的文件夹。  
  
 **网络文件共享**  
 数据库文件要传输到的目标服务器上的网络共享文件夹。 通过在 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页中为 **“方法”** 指定 **DatabaseOffline** 以脱机模式传输数据库时，可以使用 **“网络文件共享”** 。  
  
 请输入网络文件共享位置，或单击“浏览”以找到网络文件共享位置。  
  
 以脱机模式传输数据库时，数据库文件先复制到 **“网络文件共享”** 位置，然后才会传输到 **“目标文件夹”** 位置。  
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [传输数据库任务编辑器（“常规”页）](../../integration-services/control-flow/transfer-database-task-editor-general-page.md)   
 [传输数据库任务编辑器（“数据库”页）](../../integration-services/control-flow/transfer-database-task-editor-databases-page.md)  
  
  