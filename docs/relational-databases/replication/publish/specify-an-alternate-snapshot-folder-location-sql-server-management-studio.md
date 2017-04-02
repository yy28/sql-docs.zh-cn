---
title: "指定备用快照文件夹位置 (SQL Server Management Studio) | Microsoft Docs"
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
  - "快照 [SQL Server 复制], 备用文件夹位置"
  - "快照复制 [SQL Server], 备用文件夹位置"
  - "备用快照文件夹 [SQL Server 复制]"
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# 指定备用快照文件夹位置 (SQL Server Management Studio)
  在指定备用快照位置 **快照** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### 指定备用快照位置  
  
1.  在 **快照** 页 **发布属性-\< 发布>** 对话框中︰  
  
    1.  选择 **“将文件放入下列文件夹”**，然后单击 **“浏览”** 定位到某个目录，或者输入用于存储快照文件的目录的路径。  
  
        > [!NOTE]  
        >  快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用请求订阅，您必须指定一个共享的目录作为通用命名约定 (UNC) 路径，如 \\\computername\snapshot。 有关详细信息，请参阅 [保护快照文件夹的安全](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
    2.  除非需要将快照文件同时写入两个位置，否则应清除 **“将文件放入默认文件夹”** 。  
  
     若要压缩快照文件，请选择 **“压缩此文件夹中的快照文件”**。 压缩通常用于低带宽连接和可移动介质（如 CD-ROM）上的备用快照位置。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## 另请参阅  
 [备用快照文件夹位置](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [配置快照属性和 #40;复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [指定默认快照位置 & #40;SQL Server Management Studio & #41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [使用快照初始化订阅](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  