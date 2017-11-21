---
title: MSSQLSERVER_3619 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f487685e727f9f5ccf3862ac62cf0f1e21fb78ea
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3619"></a>MSSQLSERVER_3619
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3619|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SYS_NOLOG|  
|消息正文|由于日志空间用尽，无法在数据库 ID %d 中写入检查点记录。 请与数据库管理员联系，截断日志或为数据库日志文件分配更多空间。|  
  
## <a name="explanation"></a>解释  
事务日志的磁盘空间不足。  
  
## <a name="user-action"></a>用户操作  
截断日志以释放一些空间，或者为日志分配更多的空间。 有关详细信息，请参阅 Server SQL 联机丛书中的“解决事务日志已满的问题（错误 9002）”。  
  

