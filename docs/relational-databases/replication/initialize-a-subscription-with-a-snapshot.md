---
title: "使用快照初始化订阅 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85768c39b282ccfda1df1e68d42a1f6b3985bc46
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="initialize-a-subscription-with-a-snapshot"></a>使用快照初始化订阅
  在创建发布后，通常会创建一个初始快照，并将其复制到快照文件夹中（默认情况下，使用新建发布向导创建的合并发布将会执行此操作）。 此快照然后将在订阅的初始同步期间由分发代理（对于事务发布和快照发布）或合并代理（对于合并发布）应用于订阅服务器。 快照过程取决于发布的类型：  
  
-   如果快照用于快照发布、事务发布或不使用参数化筛选器的合并发布，那么快照将包含大容量复制程序 (bcp) 文件中的架构和数据，还包含进行复制所必需的约束、扩展属性、索引、触发器和系统表。 有关创建和应用快照的详细信息，请参阅[创建并应用快照](../../relational-databases/replication/create-and-apply-the-snapshot.md)。  
  
-   如果快照用于使用参数化筛选器的合并发布，则创建快照的过程包括两部分。 首先创建包含复制脚本和已发布对象的架构（但不包含数据）的架构快照。 然后，使用包括脚本、从架构快照复制的架构以及属于订阅分区的数据的快照初始化每个订阅。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
 根据复制的类型以及发布中包含的项目，快照可由不同的文件组成。 这些文件复制到配置分发服务器时指定的默认快照文件夹中，或创建发布时指定的备用快照文件夹中。  
  
|复制类型|常用快照文件|  
|-------------------------|---------------------------|  
|快照复制或事务复制|架构 (.sch)、数据 (.bcp)、约束和索引 (.dri)、约束 (.idx)、触发器 (.trg)（只用于更新订阅服务器）、压缩的快照文件 (.cab)。|  
|合并复制|架构 (.sch)、数据 (.bcp)、约束和索引 (.dri)、触发器 (.trg)、系统表数据 (.sys)、冲突表 (.cft)、压缩的快照文件 (.cab)。|  
  
 如果快照传输在任一点中断，它将自动恢复并且不再重新发送已经全部传输的任何文件。 对于每个发布项目，快照代理的传递单位是 bcp 文件，因此已部分传递的文件必须全部重新传递。 不过，恢复快照可以大幅度减少传输的数据量，即便在连接不可靠的情况下也可以确保及时进行快照传递。  
  
## <a name="snapshot-options"></a>快照选项  
 使用快照初始化订阅时有许多可用选项。 您可以：  
  
-   指定一个备用快照文件夹位置，以替代默认的快照文件夹位置或者与之并存。 有关详细信息，请参阅 [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md)。  
  
-   压缩快照，以便在可移动介质上进行存储或者通过速度较低的网络进行传输。 有关详细信息，请参阅 [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md)。  
  
-   在应用快照之前或之后执行 Transact-SQL 脚本。 有关详细信息，请参阅[在应用快照之前和之后执行脚本](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   使用文件传输协议 (FTP) 传输快照文件。 有关详细信息，请参阅[通过 FTP 传输快照](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
## <a name="see-also"></a>另请参阅  
 [初始化订阅](../../relational-databases/replication/initialize-a-subscription.md)   
 [保护快照文件夹](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
