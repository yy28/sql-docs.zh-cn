---
title: "快照选项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照复制 [SQL Server], 选项"
  - "快照 [SQL Server 复制], 选项"
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# 快照选项
  使用快照初始化订阅时，可以使用多个选项：  
  
-   指定一个备用快照文件夹位置来替代默认快照文件夹位置或作为默认快照文件夹位置的补充。 有关详细信息，请参阅 [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md)。  
  
-   压缩快照，以便在可移动介质上进行存储或者通过速度较低的网络进行传输。 有关详细信息，请参阅 [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md)。  
  
-   在应用快照前后执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。 有关详细信息，请参阅 [执行脚本之前和之后应用快照](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   使用文件传输协议 (FTP) 传输快照文件。 有关详细信息，请参阅 [通过 FTP 传输快照](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
## 另请参阅  
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  