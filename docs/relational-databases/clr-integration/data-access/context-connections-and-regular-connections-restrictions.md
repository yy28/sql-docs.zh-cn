---
title: 常规连接和上下文连接的限制 |Microsoft Docs
description: 本文介绍与通过上下文和常规连接在 Microsoft SQL Server 进程中运行的代码相关的限制。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
ms.openlocfilehash: 5491e736bfa075c4cc9f001bc2515184de865ee2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717908"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>上下文连接和常规连接 - 限制
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  本主题讨论 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通过上下文和常规连接在进程中执行的代码的限制。  
  
## <a name="restrictions-on-context-connections"></a>对上下文连接的限制  
 开发应用程序时，请考虑应用于上下文连接的以下限制：  
  
-   对于给定的连接，在给定的时间，您只能打开一个上下文连接。 如果有多个语句并发运行在单独的连接中，则其中的每个语句都可以获得自己的上下文连接。 此限制不影响来自不同连接的并发请求；它只影响对给定连接的给定请求。  
  
-   上下文连接中不支持多个活动结果集 (MARS)。  
  
-   **SqlBulkCopy**类不在上下文连接中运行。  
  
-   不支持上下文连接中的更新批处理  
  
-   **SqlNotificationRequest**不能用于针对上下文连接执行的命令。  
  
-   不支持取消正在对上下文连接运行的命令。 **SqlCommand**方法会以静默方式忽略请求。  
  
-   使用“context connection=true”时，不能使用任何其他连接字符串关键字。  
  
-   如果**sqlconnection**的连接字符串为 "context connection = true"，而不是实例的名称，则**sqlconnection**属性返回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] null。  
  
-   对上下文连接执行命令时，设置**CommandTimeout**属性不起作用。  
  
## <a name="restrictions-on-regular-connections"></a>对常规连接的限制  
 开发应用程序时，请考虑应用于常规连接的以下限制：  
  
-   不支持对内部服务器异步执行命令。 如果在命令的连接字符串中包含 "async = true"，然后执行该命令，则会引发**NotSupportedException** 。 将出现此消息：“在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 进程内运行时，不支持异步处理。”  
  
-   不支持**SqlDependency**对象。  
  
## <a name="see-also"></a>另请参阅  
 [上下文连接](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
