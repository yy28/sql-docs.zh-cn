---
title: 常规与上下文连接 |Microsoft Docs
description: 在 SQL Server 中，有时必须对 Transact-sql 语句使用常规连接，但上下文连接可提供性能和资源使用优势。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
ms.openlocfilehash: 881b7463400665d22baaa9b19f13cb5949df0830
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81485141"
---
# <a name="context-connections-vs-regular-connections"></a>上下文连接与常规连接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果要连接到远程服务器，请始终使用常规连接，而不使用上下文连接。 如果您需要连接到存储过程或函数正在其上运行的同一台服务器，则在大多数情况下请使用上下文连接。 这具有一些优势，例如，在同一个事务空间中运行以及不必重新验证。  
  
 此外，使用上下文连接通常会导致性能更佳和占用更少的资源。 上下文连接是一个仅进程内连接，因此它可以通过绕过网络协议和传输层来发送 Transact-sql 语句并接收结果，直接联系服务器。 同时跳过验证过程。 下图显示了**SqlClient**托管提供程序的主要组件，以及不同的组件在使用常规连接时以及使用上下文连接时如何彼此交互。  
  
 ![上下文代码路径和常规连接代码路径。](../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "上下文代码路径和常规连接代码路径。")  
  
 上下文连接所采用的代码路径较短，且所涉及的组件较少，因此，您可以预计请求到达服务器和从服务器获得结果的速度将高于采用常规连接时。 服务器上的查询执行时间对于上下文连接和常规连接是相同的。  
  
 在某些情况下，您可能需要与同一台服务器之间建立单独的常规连接。 例如，有关使用上下文连接的某些限制，请参阅对[常规连接和上下文连接的限制](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [上下文连接](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
