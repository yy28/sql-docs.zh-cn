---
title: 发送到服务器 （扩展存储的过程 API） 的结果集 |Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 590565f15ac9d53b7209fa6808c4c24baeee6344
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37182244"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>将结果集发送到服务器（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 发送结果集时[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，扩展存储的过程应调用合适的 API，如下所示：  
  
-   **Srv_sendmsg**之前或之后发送所有行 （如果有），可能会按任意顺序调用函数**srv_sendrow**。 与发送完成状态之前的所有消息必须都发送到客户端**srv_senddone**。  
  
-   对于发送到客户端的每行调用一次 srv_sendrow 函数。 必须将所有行都发送到客户端之前任何消息、 状态值或完成状态会自动都发送带有**srv_sendmsg**，则**srv_status**自变量**srv_pfield**，或**srv_senddone**。  
  
-   发送的某行未与定义其所有列**srv_describe**导致应用程序引发信息性错误消息并向客户端返回 FAIL。 在此情况下，将不发送该行。  
  
## <a name="see-also"></a>请参阅  
 [创建扩展存储过程](creating-extended-stored-procedures.md)  
  
  
