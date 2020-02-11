---
title: 事务复制的项目选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 992b479ea0867aef1ca75e42cc865db2cc5a735f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63268653"
---
# <a name="article-options-for-transactional-replication"></a>事务复制的项目选项
  事务发布中的项目具有多个选项。 使用事务复制，可以执行以下操作：  
  
-   指定更改如何从发布服务器传播到订阅服务器。 有关详细信息，请参阅[指定如何传播事务项目的更改](transactional-articles-specify-how-changes-are-propagated.md)。  
  
-   指定应复制存储过程的执行。 这对于复制面向维护的存储过程的结果很有用处，这种存储过程的结果会影响大量的数据。 有关详细信息，请参阅 [Publishing Stored Procedure Execution in Transactional Replication](publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
-   指定架构选项（例如，是否将约束和触发器复制到订阅服务器）。 有关详细信息，请参阅 [指定架构选项](../publish/specify-schema-options.md)。  
  
-   使用行筛选器和列筛选器。 通过筛选表项目，可以为要发布的数据创建分区。 有关详细信息，请参阅[筛选已发布数据](../publish/filter-published-data.md)。  
  
## <a name="see-also"></a>另请参阅  
 [发布数据和数据库对象](../publish/publish-data-and-database-objects.md)  
  
  
