---
title: MSSQLSERVER_9001 | Microsoft Docs
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
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1eaae857105a13a133c2fc9cd216d701df9f51d5
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9001|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LOG_NOT_AVAIL|  
|消息正文|数据库 '%.*ls' 的日志不可用。 有关相应错误消息，请查看事件日志。 修复所有错误后重新启动数据库。|  
  
## <a name="explanation"></a>解释  
数据库日志处于脱机状态。 通常，这表示需要重新启动数据库的灾难性故障。  
  
## <a name="user-action"></a>用户操作  
诊断其他错误并重新启动 SQL Server 实例（如果尚未自行重新启动）。  
  

