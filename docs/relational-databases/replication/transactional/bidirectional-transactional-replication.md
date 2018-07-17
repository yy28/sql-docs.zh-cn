---
title: 双向事务复制 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7adb719f32533fe28a21bcd092e8c7b5bf593918
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351379"
---
# <a name="bidirectional-transactional-replication"></a>双向事务复制
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  双向事务复制是一种特定的事务复制拓扑，它允许两台服务器相互交换更改：每台服务器均发布数据，然后从另一台服务器订阅包含相同数据的发布。 [sp_addsubscription (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 的 **@loopback_detection** 参数设置为 TRUE，可确保更改只发送到订阅服务器，而不会导致将更改发回到发布服务器。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中，对等事务复制也支持此拓扑，但采用双向复制可提高性能。  
  
## <a name="see-also"></a>另请参阅  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
