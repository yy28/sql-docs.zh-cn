---
title: "监视错误日志 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server]
- database performance [SQL Server], errors
- Windows application logs [SQL Server]
- monitoring performance [SQL Server], errors
- server performance [SQL Server], errors
- comparing error and application log output
- errors [SQL Server], logs
- tuning databases [SQL Server], errors
- database monitoring [SQL Server], errors
- SQL Server error log
- logs [SQL Server], SQL Server error logs
- error logs [SQL Server]
- logs [SQL Server], Windows application logs
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9edd8e852a1e4272d7c9f94af442a7e9e5cd7016
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="monitoring-the-error-logs"></a>监视错误日志
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将某些系统事件和用户定义事件记录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 应用程序日志中。 这两种日志都会自动给所有记录事件加上时间戳。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中的信息可以解决 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相关问题。  
  
 Windows 应用程序日志完整地记录了 Windows 操作系统上发生的事件，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理中的事件。 使用 Windows 事件查看器可以查看 Windows 应用程序日志和筛选信息。 例如，可以筛选信息、警告、错误、审核成功和审核失败等事件。  
  
## <a name="comparing-error-and-application-log-output"></a>比较错误和应用程序日志输出  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志和 Windows 应用程序日志来标识产生问题的原因。 例如，监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志时，您可能会遇到不包含原因信息的错误消息。 通过比较两个日志中的事件日期和时间，可以缩小可能原因的范围。 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 日志文件查看器可以将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理和 Windows 日志集成到一个列表，这样可以轻松了解相关的服务器事件和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 有关详细信息，请参阅 SQL Server 联机丛书中的主题“日志文件查看器”。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[查看 SQL Server 错误日志](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以及如何查看该日志。|  
|[查看 Windows 应用程序日志](../../tools/configuration-manager/viewing-the-windows-application-log.md)|介绍了 Windows 应用程序日志以及如何查看该日志。|  
  
  

