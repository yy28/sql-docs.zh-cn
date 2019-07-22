---
title: 双向事务复制 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3eefd48c594c0a13388bb932faf1c5cf9fd9adea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041527"
---
# <a name="bidirectional-transactional-replication"></a>双向事务复制
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  双向事务复制是一种特定的事务复制拓扑，它允许两台服务器相互交换更改：每台服务器均发布数据，然后从另一台服务器订阅包含相同数据的发布。 [sp_addsubscription (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 的 **@loopback_detection** 参数设置为 TRUE，可确保更改只发送到订阅服务器，而不会导致将更改发回到发布服务器。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中，对等事务复制也支持此拓扑，但采用双向复制可提高性能。  
  
## <a name="see-also"></a>另请参阅  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
