---
title: 为合并复制筛选已发布数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
helpviewer_keywords:
- merge replication [SQL Server replication], filtering published data
- replication [SQL Server], filtering published data
ms.assetid: 46c5023d-7a3b-4455-becc-e159fcb5d6c4
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88b23cba702b1c88da966bd01a949295c7e86f3f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="filter-published-data-for-merge-replication"></a>为合并复制筛选已发布数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  除了可使用其他类型的复制定义的静态行筛选器和列筛选器之外，合并复制还提供参数化行筛选器和联接筛选器。 有关静态行筛选器和列筛选器的详细信息，请参阅[筛选已发布数据](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
 合并复制用于多种支持移动用户的应用程序；这些应用程序通常有大量订阅，每个订阅接收唯一的数据集。 与联接筛选器结合的参数化筛选器允许管理员设置一个发布（或最多少量几个发布），并为用户提供不同的数据集，这就降低了因创建多个发布而造成的管理开销。  
  
-   通过参数化筛选器，可以将数据的不同分区发送给不同的订阅服务器，而不需要创建多个发布。 例如，可以对表进行筛选，以便仅将给定销售代表的数据复制给此销售代表。 参数化筛选器具有多种选项，允许定制筛选以优化性能并最大限度符合数据和应用程序的要求。 有关详细信息，请参阅 [参数化行筛选器](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
-   联接筛选器通常与参数化筛选器一起使用，以扩展对相关表的筛选（还可与静态筛选器一起使用）。 例如，销售代表通常在其他表（如 customer 和 order 表）中也有数据。 可以对这些数据进行筛选，从而使销售代表只收到其客户和客户订单的相关数据。 有关详细信息，请参阅 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)。  
  
 筛选器不能包含复制所用的 **rowguidcol** 来标识行。 默认情况下，这是您设置合并复制时添加的列，命名为 **rowguid**。  
  
## <a name="see-also"></a>另请参阅  
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
