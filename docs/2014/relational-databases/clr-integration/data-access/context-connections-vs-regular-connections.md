---
title: 常规与上下文连接 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
ms.openlocfilehash: ce531129099a8f4908bdc4b29920696d4ba3c505
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970630"
---
# <a name="regular-vs-context-connections"></a>常规连接与上下文连接
  如果要连接到远程服务器，请始终使用常规连接，而不使用上下文连接。 如果您需要连接到存储过程或函数正在其上运行的同一台服务器，则在大多数情况下请使用上下文连接。 这具有一些优势，例如，在同一个事务空间中运行以及不必重新验证。  
  
 此外，使用上下文连接通常会导致性能更佳和占用更少的资源。 上下文连接是一个仅进程内连接，因此它可以通过绕过网络协议和传输层来发送 Transact-sql 语句并接收结果，直接联系服务器。 同时跳过验证过程。 下图显示 `SqlClient` 托管提供程序的主要组件，并说明在使用常规连接和使用上下文连接时不同组件之间如何相互交互。  
  
 ![上下文代码路径和常规连接代码路径。](../../../database-engine/dev-guide/media/clrintdataaccess.gif "上下文代码路径和常规连接代码路径。")  
  
 上下文连接所采用的代码路径较短，且所涉及的组件较少，因此，您可以预计请求到达服务器和从服务器获得结果的速度将高于采用常规连接时。 服务器上的查询执行时间对于上下文连接和常规连接是相同的。  
  
 在某些情况下，您可能需要与同一台服务器之间建立单独的常规连接。 例如，有关使用上下文连接的某些限制，请参阅对[常规连接和上下文连接的限制](context-connections-and-regular-connections-restrictions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [上下文连接](context-connection.md)  
  
  
