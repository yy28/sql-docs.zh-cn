---
title: Oracle 发布服务器的管理注意事项 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], administrative considerations
- administering replication, Oracle publishing
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 42791ed9e60ad633ee1331dfc8326d58c0546000
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756289"
---
# <a name="administrative-considerations-for-oracle-publishers"></a>Oracle 发布服务器的管理注意事项
  在配置 Oracle 发布服务器并实施复制更改跟踪机制后，Oracle 数据库系统管理员仍然可以使用标准 Oracle 数据库实用工具并执行典型的系统管理任务。 但是，应该了解执行某些管理任务对已发布数据的影响。  
  
 除了删除或修改为复制发布的列或者任意复制对象，这些注意事项不适用于快照发布。  
  
## <a name="importing-and-loading-data"></a>导入和加载数据  
 触发器用于 Oracle 中的事务发布的更改跟踪。 对已发布表的更改只有在发生更新、插入或删除时复制触发器激发的情况下才能复制到订阅服务器。 Oracle 导入和 SQL*Loader 这两个 Oracle 实用工具都有影响触发器的选项，用来决定当用这些实用工具将行插入到复制的表中时是否激发触发器。  
  
### <a name="oracle-import"></a>Oracle 导入  
 用 Oracle 导入，可以将 **ignore** 选项设置为“y”或“n”（默认值为“n”）。 如果将 **ignore** 设置为“n”，表会删除并在导入过程中重新创建。 这会删除复制触发器并禁用复制。 如果将 **ignore** 设置为“y”，导入将尝试将行加载到现有表中，这会激发复制触发器。 因此，用导入工具向复制的表导入时，确保将 **ignore** 设置为“y”。  
  
### <a name="sqlloader"></a>SQL*Loader  
 使用 SQL\*Loader，可以将选项 **direct** 设置为“true”或“false”（默认值为“false”）。 如果将 **direct** 设置为“false”，则用常规 INSERT 语句插入行，这些语句会激发复制触发器。 如果将 **direct** 设置为“true”，则优化加载而不激发触发器。 因此，使用 SQL*Loader 工具向复制的表导入时，请确保将 **direct** 设置为“false”。  
  
## <a name="making-changes-to-published-objects"></a>对已发布的对象进行更改  
 下列操作没有特别的注意事项：  
  
-   重新生成对已发布表的索引。  
  
-   将用户触发器添加到已发布表。  
  
 下列操作需要停止已发布表上的所有活动：  
  
-   移动已发布表。  
  
 下列操作要求删除发布、执行操作，然后重新创建发布：  
  
-   截断已发布表。  
  
-   重命名已发布表。  
  
-   向已发布表添加列。  
  
-   删除或修改为复制发布的列。  
  
-   执行日志未记录的操作。  
  
## <a name="dropping-or-modifying-replication-objects"></a>删除或修改复制对象  
 如果删除或修改了任何发布服务器级的跟踪表、触发器、序列或存储过程，必须删除并重新配置发布服务器。 有关这些对象的部分列表，请参阅[在 Oracle 发布服务器上创建的对象](objects-created-on-the-oracle-publisher.md)。  
  
 有关删除和重新配置发布服务器的信息，请参阅主题 [Troubleshooting Oracle Publishers](troubleshooting-oracle-publishers.md)中的“进行需要重新配置发布服务器的更改”部分。  
  
## <a name="see-also"></a>请参阅  
 [配置 Oracle 发布服务器](configure-an-oracle-publisher.md)   
 [Oracle 发布服务器的设计注意事项和限制](design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle 发布概述](oracle-publishing-overview.md)  
  
  
