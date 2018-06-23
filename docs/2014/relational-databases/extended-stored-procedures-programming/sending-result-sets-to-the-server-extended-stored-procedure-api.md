---
title: 发送到服务器 （扩展存储的过程 API） 将结果集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 090f0030063abfc0246b816d4143468eb7e4e52f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029032"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>将结果集发送到服务器（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 发送将结果集时[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，扩展存储的过程应调用合适的 API，如下所示：  
  
-   **Srv_sendmsg**之前或之后使用发送的 （如果有） 的所有行均可按任意顺序调用函数**srv_sendrow**。 之前的完成状态不会发送所有消息必须都发送到客户端**srv_senddone**。  
  
-   对于发送到客户端的每行调用一次 srv_sendrow 函数。 必须将所有行都发送到任何消息，状态值之前客户端或完成状态会自动都发送带有**srv_sendmsg**、 **srv_status**参数**srv_pfield**，或**srv_senddone**。  
  
-   发送尚未与其使用定义的所有列的行**srv_describe**导致应用程序引发一条信息性错误消息，并返回到客户端失败。 在此情况下，将不发送该行。  
  
## <a name="see-also"></a>请参阅  
 [创建扩展存储过程](creating-extended-stored-procedures.md)  
  
  