---
title: "验证已复制的数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "内联数据验证 [SQL Server 复制]"
  - "管理复制, 验证数据"
  - "复制 [SQL Server], 验证数据"
  - "事务复制, 验证数据"
  - "验证数据"
  - "合并复制数据验证 [SQL Server 复制]"
  - "合并复制数据验证 [SQL Server 复制], 关于数据验证"
  - "验证已复制的数据"
ms.assetid: f7500a2b-61cb-41b5-816d-27609a6c58e7
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 验证已复制的数据
  通过事务复制和合并复制，您可以验证订阅服务器中的数据与发布服务器中的数据是否匹配。 可以对特定订阅或某一发布的所有订阅执行验证。 指定下列验证类型之一，分发代理或合并代理便会在下次运行时验证数据：  
  
-   仅行计数。 此选项将验证订阅服务器上的表与发布服务器上的表的行数是否相同，但不验证行内容是否匹配。 行计数验证是一种简易验证方法，可帮助您了解数据是否存在问题。  
  
-   行计数和二进制校验和。 除了可在发布服务器和订阅服务器上对行进行计数之外，还可使用校验和算法来计算所有数据的校验和。 如果行计数失败，则不计算校验和。  
  
 除了验证订阅服务器和发布服务器上的数据是否匹配之外，合并复制还提供验证每个订阅服务器上的数据是否正确分区的功能。 有关详细信息，请参阅 [验证合并订阅服务器的分区信息](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md)。  
  
 **验证数据**  
  
 若要验证订阅中的所有项目，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、存储过程或复制管理对象 (RMO)。 有关详细信息，请参阅 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。 若要验证快照和事务发布中的各个项目，必须使用存储过程。  
  
## 数据验证结果  
 验证完成时，分发代理或合并代理将记录有关成功或失败的消息（复制不报告具体失败的行）。 可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、复制监视器和复制系统表中查看这些消息。 上面所列的操作指南主题说明如何运行验证和查看结果。  
  
 若要处理验证失败，请考虑以下事项：  
  
-   配置名为 **“复制: 订阅服务器未通过数据验证”** 的复制警报，以便您在验证失败时得到通知。 有关详细信息，请参阅 [配置预定义复制警报 （&) #40;SQL Server Management Studio & #41;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)。  
  
-   验证失败是否已对您的应用程序带来问题？ 如果验证失败带来了问题，请手动更新数据以进行同步，或者重新初始化订阅：  
  
    -   可以使用 [tablediff 实用工具](../../tools/tablediff-utility.md)来更新数据。 有关使用此实用程序的详细信息，请参阅 [比较复制的表之间的差异和 #40;复制编程 & #41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
    -   有关重新初始化的详细信息，请参阅 [重新初始化订阅](../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
## 数据验证的注意事项  
 请在验证数据时考虑下列问题：  
  
-   验证数据之前，必须停止订阅服务器上的一切更新活动（验证进行时不必停止发布服务器上的活动）。  
  
-   因为校验和与二进制校验和在验证大型数据集时可能需要大量处理器资源，所以应将验证安排在复制中所用服务器上的活动最少时进行。  
  
-   复制只验证表；它不验证只包含架构的项目（例如存储过程）是否在发布服务器和订阅服务器上相同。  
  
-   可以对任何发布的表使用二进制校验和。 校验和无法验证带有列筛选器的表或列偏移量不一致的逻辑表结构（由于存在用于删除或添加列的 ALTER TABLE 语句）。  
  
-   复制验证使用 **校验和** 和 **binary_checksum** 函数。 有关其行为的信息，请参阅  [校验和 & #40;Transact SQL & #41;](../../t-sql/functions/checksum-transact-sql.md) 和 [BINARY_CHECKSUM & #40;Transact SQL & #41;](../../t-sql/functions/binary-checksum-transact-sql.md)。  
  
-   如果订阅服务器与发布服务器上的数据类型不同，则使用二进制校验和或校验和进行的验证可能会错误地报告失败。 如果执行以下操作之一，则可能出现上述情况：  
  
    -   显式设置架构选项从而为早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]映射数据类型。  
  
    -   将合并发布的发布兼容级别设置为早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并且已发布表包含一个或多个必须为此版本映射的数据类型。  
  
    -   手动初始化订阅并且正在订阅服务器上使用不同的数据类型。  
  
-   事务复制的可转换订阅不支持二进制校验和和校验和验证。  
  
-   复制到非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器的数据不支持验证。  
  
## 数据验证的工作机制  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过计算发布服务器上的行计数或校验和，并将这些值与订阅服务器上计算所得的行计数或校验和值比较来验证数据。 为整个发布表和整个订阅表各计算一个值，但计算中不包括 **text**、 **ntext**或 **image** 列中的数据。  
  
 执行计算时，共享锁临时放置对其执行行计数或校验和的表上，不过计算很快完成，同时共享锁被删除，这一过程通常只需几秒钟。  
  
 使用二进制校验和时，32 位冗余校验 (CRC) 将逐列进行，而不是在数据页的物理行上进行。 这使得表中的列可以按任意顺序在数据页上进行物理排序，但对该行计算的 CRC 值不变。 发布上有行筛选器或列筛选器时，可使用二进制校验和进行验证。  
  
## 另请参阅  
 [复制管理最佳实践](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  