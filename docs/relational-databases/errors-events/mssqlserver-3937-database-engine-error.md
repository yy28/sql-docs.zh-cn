---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6f02486a0a113f2e589a5f17d40344c374c1d853
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
