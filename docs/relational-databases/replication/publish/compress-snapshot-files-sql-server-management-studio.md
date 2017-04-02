---
title: "压缩快照文件 (SQL Server Management Studio) | Microsoft Docs"
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
  - "快照 [SQL Server 复制], 压缩"
  - "快照复制 [SQL Server], 压缩快照"
ms.assetid: 174ade3e-74a1-4e67-a6da-b874be3ff50f
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 压缩快照文件 (SQL Server Management Studio)
  指定应在压缩文件 **快照** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### 压缩快照文件  
  
1.  在 **快照** 页 **发布属性-\< 发布>** 对话框中︰  
  
    1.  选择 **“将文件放入下列文件夹”**，然后单击 **“浏览”** 定位到某个目录，或者输入用于存储快照文件的目录的路径。  
  
        > [!NOTE]  
        >  快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用请求订阅，您必须指定一个共享的目录作为通用命名约定 (UNC) 路径，如 \\\computername\snapshot。 有关详细信息，请参阅 [保护快照文件夹的安全](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
    2.  除非需要将快照文件同时写入两个位置，否则应清除 **“将文件放入默认文件夹”** 。  
  
        > [!NOTE]  
        >  如果选中了此复选框，则默认文件夹中存储的文件将不压缩。 压缩文件只能存储在上一步骤中指定的备用位置中。  
  
2.  选择 **“压缩此文件夹中的快照文件”**。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## 另请参阅  
 [配置快照属性和 #40;复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [压缩的快照](../../../relational-databases/replication/compressed-snapshots.md)   
 [使用快照初始化订阅](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  