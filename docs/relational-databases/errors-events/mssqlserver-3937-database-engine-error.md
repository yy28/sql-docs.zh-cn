---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 113385d8dd09b70f4d058fb24a113f7065866eeb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|MSSQLSERVER|  
|事件 ID|3937|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|XACT_FILESTREAM_ROLLBACK_ERROR|  
|消息正文|在试图通知 FILESTREAM 筛选器驱动程序某事务已回滚时出错。 错误代码：0x%0x。|  
  
## <a name="explanation"></a>解释  
发出有关某事务的回滚通知时，RsFx 驱动程序返回错误。 这可能是因资源不足而造成的。 这可能会导致 RsFx 筛选器驱动程序发生少量内存泄漏，但是，如果存在创建事务的 sqlservr.exe 进程，则可能不会发生这种情况。  
  
## <a name="user-action"></a>用户操作  
