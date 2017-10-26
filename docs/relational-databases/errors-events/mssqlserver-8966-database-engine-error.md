---
title: MSSQLSERVER_8966 | Microsoft Docs
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
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4c93290eaf142f7048458d9e4a18d12bc70e028b
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver8966"></a>MSSQLSERVER_8966
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8966|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|消息正文|无法使用闩锁类型 TYPE 读取并闩锁页 P_ID。 操作失败。|  
  
## <a name="explanation"></a>解释  
页读取失败或无法针对 PFS 或 GAM 页进行闩锁。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中可能会有闩锁超时或其他附带的消息。  
  
## <a name="user-action"></a>用户操作  
查阅 SQL 错误日志，检查附带的消息并解决其中的错误。  
  

