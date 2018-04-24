---
title: 在应用快照之前和之后执行脚本 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
- scripts [SQL Server replication]
ms.assetid: 9a6872c2-9bed-477f-9d2f-332d640edcf2
caps.latest.revision: 35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cccd624e0ee21cf7ab3b38e1bb08a61e6e8935fd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="execute-scripts-before-and-after-the-snapshot-is-applied"></a>在应用快照之前和之后执行脚本
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  可以指定在应用快照之前或之后在订阅服务器上执行的脚本。 使用脚本的原因有多种，例如在每台订阅服务器上创建登录帐户和架构（对象所有者）。  
  
 可以为每个脚本指定一个文件位置，每次发生快照处理时，快照代理都会将脚本文件复制到当前快照文件夹中。 应用快照时，分发代理或合并代理会在执行任何复制的对象脚本之前执行快照前脚本。 分发代理或合并代理在所有其他复制的对象脚本和数据应用之后，才会执行快照后脚本。 在完成快照应用程序且成功执行脚本文件之后，这些脚本文件将从订阅服务器上的工作目录中删除。  
  
 通过启动 **sqlcmd** 实用工具来执行脚本。 部署脚本之前，请先用 **sqlcmd** 执行该脚本，以确保它可以按预期方式执行。 应用快照之前和之后执行的脚本的内容必须可重复。 例如，如果在脚本中创建了一个表，则应该首先检查该表是否存在，如果存在就执行相应的操作。 脚本必须可重复是因为，如果需要重新初始化已应用了脚本的订阅，则在重新初始化期间应用新的快照时，将再次应用该脚本。  
  
 如果压缩快照文件（采用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 文件格式压缩），则也会压缩脚本并将其置于此 CAB 文件中。 压缩的快照文件传输到订阅服务器并解压缩到订阅服务器上的工作目录后，将执行所有指示为快照前脚本的脚本。 同样，在应用快照的最后一个步骤中，所有快照后脚本在订阅服务器上解压缩并执行。  
  
 **在应用快照之前和之后执行脚本**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]：[如何在应用快照之前和之后执行脚本 \(SQL Server Management Studio\)](../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   复制 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编程：[配置快照属性&#40;复制 Transact-SQL 编程&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [快照选项](../../relational-databases/replication/snapshot-options.md)  
  
  
