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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 5d8f9be6d414580994a68c4ee56a26deee583d38
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "76286956"
---
# <a name="bidirectional-transactional-replication"></a>双向事务复制
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  双向事务复制是一种特定的事务复制拓扑，它允许两台服务器相互交换更改：每台服务器均发布数据，然后从另一台服务器订阅包含相同数据的发布。 `@loopback_detection`sp_addsubscription &#40;Transact-SQL&#41;[ 的 ](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 参数设置为 TRUE，可确保更改只发送到订阅服务器，而不会导致将更改发回到发布服务器。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中，对等事务复制也支持此拓扑，但采用双向复制可提高性能。  
  
## <a name="see-also"></a>另请参阅  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
