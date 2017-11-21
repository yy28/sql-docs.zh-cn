---
title: MSSQLSERVER_9003 | Microsoft Docs
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
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 27d2fbf1bed8445eb8d3fd42000128741d2ee377
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9003|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LOG_INVALID_LSN|  
|消息正文|传递给数据库 '%.*ls' 中的日志扫描操作的日志扫描号 %S_LSN 无效。 此错误可能指示数据损坏，或者日志文件(.ldf)与数据文件(.mdf)不匹配。 如果此错误是在复制期间出现的，请重新创建发布。 否则，如果该问题导致启动期间出错，请从备份还原。|  
  
## <a name="explanation"></a>解释  
组件传递给数据库日志管理器的日志序列号无效。 这可能是由于复制、损坏或主数据文件与日志不一致造成的。  
  
## <a name="user-action"></a>用户操作  
如果在复制期间出现这种错误，请重新创建发布。 否则，请从备份还原。  
  

