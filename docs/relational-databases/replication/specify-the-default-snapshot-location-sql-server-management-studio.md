---
title: "指定默认快照位置 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照 [SQL Server 复制]，默认位置"
  - "默认快照位置"
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 指定默认快照位置 (SQL Server Management Studio)
  可以在配置分发向导的 **“快照文件夹”** 页上指定默认快照位置。 有关使用此向导的详细信息，请参阅 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)。 如果在未配置为分发服务器的服务器上创建发布，请在新建发布向导的 **“快照文件夹”** 页上指定默认快照位置。 有关使用此向导的详细信息，请参阅 [创建发布](../../relational-databases/replication/publish/create-a-publication.md)。  
  
 上修改默认快照位置 **出版商** 页 **分发服务器属性-\< 分发服务器>** 对话框。 有关详细信息，请参阅 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。 设置在每个发布的快照文件夹 **发布属性-\< 发布>** 对话框。 有关详细信息，请参阅 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### 修改默认快照位置  
  
1.  在 **出版商** 页 **分发服务器属性-\< 分发服务器>** 对话框框中，单击属性按钮 (**...**) 发布者想要更改默认快照位置。  
  
2.  在 **发布服务器属性-\< 发布服务器>** 对话框框中，输入一个值 **默认快照文件夹** 属性。  
  
    > [!NOTE]  
    >  快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用请求订阅，您必须指定一个共享的目录作为通用命名约定 (UNC) 路径，如 \\\computername\snapshot。 有关详细信息，请参阅 [保护快照文件夹的安全](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另请参阅  
 [备用快照文件夹位置](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  