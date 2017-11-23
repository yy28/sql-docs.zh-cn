---
title: "发送到服务器 （扩展存储的过程 API） 将结果集 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 37eb992a4ef260b1d8b94991e95fae6e9326bd6f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>将结果集发送到服务器（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 发送将结果集时[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，扩展存储的过程应调用合适的 API，如下所示：  
  
-   **Srv_sendmsg**之前或之后使用发送的 （如果有） 的所有行均可按任意顺序调用函数**srv_sendrow**。 之前的完成状态不会发送所有消息必须都发送到客户端**srv_senddone**。  
  
-   **Srv_sendrow**为发送到客户端每行一次调用函数。 必须将所有行都发送到任何消息，状态值之前客户端或完成状态会自动都发送带有**srv_sendmsg**、 **srv_status**参数**srv_pfield**，或**srv_senddone**。  
  
-   发送尚未与其使用定义的所有列的行**srv_describe**导致应用程序引发一条信息性错误消息，并返回到客户端失败。 在此情况下，将不发送该行。  
  
## <a name="see-also"></a>另请参阅  
 [创建扩展存储过程](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
