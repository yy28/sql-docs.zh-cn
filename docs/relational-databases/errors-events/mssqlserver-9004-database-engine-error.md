---
title: MSSQLSERVER_9004 | Microsoft Docs
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
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6d2d5cefa8aa83b92f589d939f1c7c53b23b3f1f
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9004"></a>MSSQLSERVER_9004
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9004|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LOG_CORRUPT|  
|消息正文|处理数据库 '%.*ls' 的日志时出错。  如果可能，请从备份还原。 如果没有可用备份，可能需要重新生成日志。|  
  
## <a name="explanation"></a>解释  
在回滚、恢复或复制期间处理日志时出错。 这可能表明操作系统检测到错误，或者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 检测到内部一致性错误。  
  
## <a name="user-action"></a>用户操作  
执行以下操作之一将更正此错误：  
  
-   从备份还原。  
  
-   重新生成日志。  
  
此外，检查系统事件和错误日志以识别系统内可能导致该错误的问题。  
  

