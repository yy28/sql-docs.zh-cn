---
title: "压缩的快照 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
- compressed snapshots [SQL Server replication]
ms.assetid: 979ffa7c-3a88-4e70-8cf2-b8d452fd7a7f
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fceb41e32cbc4a2dbf779cb95827fef639341bea
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="compressed-snapshots"></a>压缩的快照
  如果要在慢速网络上传输快照，或者将快照存储到可移动介质上而未压缩的快照太大而不适于存储在介质上，则应该压缩快照文件。 在这些情况下，压缩快照文件很有用，但压缩增加了生成和应用快照的时间。  
  
 压缩快照文件采用了 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 文件格式，这种格式可以压缩不超过 2 GB 的文件（无法压缩超过 2 GB 的快照文件）。 若要压缩文件，必须将这些文件写入一个备用快照文件夹（无法压缩写入默认快照文件夹中的文件）。 有关备用快照文件夹的详细信息，请参阅[备用快照文件夹位置](../../relational-databases/replication/alternate-snapshot-folder-locations.md)。  
  
 文件在分发代理或合并代理运行的位置解压缩；请求通常将订阅与压缩快照一起使用，以便在订阅服务器上解压缩文件。 订阅服务器接收到压缩文件时，首先将文件写入一个临时位置。 压缩文件复制到订阅服务器后，压缩文件中的快照文件将由 CAB 实用工具按顺序逐个解压缩。 订阅服务器上所需的空间为压缩文件的大小与最大的未压缩文件的大小之和。  
  
> [!NOTE]  
>  在某些情况下，压缩的快照可以提高通过网络传输快照文件的性能。 但是，如果压缩快照，则在生成快照文件时需要通过快照代理进行额外处理，而在应用快照文件时需要通过分发代理或合并代理进行额外处理。 在某些情况下，这可能会降低生成快照的速度，并增加应用快照所需的时间。 此外，如果发生网络故障，压缩的快照将无法恢复，因此不适用于不可靠的网络。 在网络中使用压缩的快照时，应仔细权衡这些利弊。  
  
 **压缩和传输快照文件**  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]：[压缩快照文件 (SQL Server Management Studio)](../../relational-databases/replication/publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   复制 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编程：[配置快照属性（复制 Transact-SQL 编程）](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)  
  
  
