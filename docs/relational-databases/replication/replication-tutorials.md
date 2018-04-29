---
title: 复制教程 | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- walkthroughs [SQL Server replication]
- replication [SQL Server], tutorials
ms.assetid: 19fbd10e-5b59-4cd0-a988-52d5d9206242
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3900aae4e96b5490b0b65cbbee004fc66337ff63
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="replication-tutorials"></a>复制教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
复制是一种功能强大的解决方案，可用于在服务器之间移动数据或数据子集。 可以使用事务复制在完全连接的服务器之间复制数据。 此外，还可以使用合并复制在间歇连接的服务器和客户端之间复制数据。 接下来，你将发现可帮助准备复制的服务器的教程，以及介绍如何配置事务复制和合并复制的教程。 
  
在复制教程中，“发布服务器”是指包含将要复制的源数据的服务器，“订阅服务器”是指目标服务器。 发布服务器和订阅服务器可以共享同一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，但这不是必须的。 有关详细信息，请参阅 [复制发布模型概述](../../relational-databases/replication/publish/replication-publishing-model-overview.md)。  

上述教程使用 NODE1\SQL2016 作为发布服务器和分发服务器，使用 NODE2\SQL2016 作为订阅服务器。 
  
> [!NOTE]  
> 这些教程中列举的大多数任务都能够以编程方式执行。 有关详细信息，请参阅 [复制开发人员文档](../../relational-databases/replication/concepts/replication-developer-documentation.md)。  
  
## <a name="replication-tutorials"></a>复制教程  
[教程：为复制准备 SQL Server - 发布服务器、分发服务器、订阅服务器](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) 
 
学习如何准备服务器以便以最少的权限运行复制。 开始其他复制教程之前，必须先完成本教程。  
  
[教程：在两个完全连接的服务器之间配置复制（事务）](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)

了解如何配置事务复制，以在完全连接的服务器之间复制数据。 本教程还包括一些基本的错误故障排除方法。 

  
[教程：配置服务器和移动客户端之间的复制（合并）](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)

了解如何配置合并复制，以在服务器与仅偶尔连接的一个或多个客户端之间交换数据。  
  
## <a name="see-also"></a>另请参阅  
[复制的安全性和保护](../../relational-databases/replication/security/security-and-protection-replication.md) 

[事务复制概述](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication) 

[合并复制概述](https://docs.microsoft.com/en-us/sql/relational-databases/replication/merge/merge-replication)

  