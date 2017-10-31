---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 25109bc21ea0ec035aa30e7ba439dcd967c4ac55
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5245|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|消息正文|对象 ID O_ID (对象 'NAME'): 由于超过了锁请求超时期限，DBCC 无法获取该对象的锁。 已跳过此对象，不会处理它。|  
  
## <a name="explanation"></a>解释  
在 DBCC 等待指定对象的表锁时，出现锁超时。  
  
## <a name="user-action"></a>用户操作  
重新运行 DBCC 命令。  
  

