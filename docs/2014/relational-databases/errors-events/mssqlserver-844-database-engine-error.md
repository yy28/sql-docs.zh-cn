---
title: MSSQLSERVER_844 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 844 (Database Engine error)
ms.assetid: 2060c886-1226-4066-bc0c-de90a1cfb82b
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1a3f477e809b154c89b9e141739fb49c26e9eb35
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129679"
---
# <a name="mssqlserver844"></a>MSSQLSERVER_844
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|844|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|BUFLATCH_TIMEOUT_CONTINUE|  
|消息正文|等待缓冲区闩锁时出现超时 - 类型 %d，bp %p，页 %d:%d，stat %#x，数据库 ID: %d，分配单元 ID: %I64d%ls，任务 0x%p : %d，等待时间 %d，标志 0x%I64x，所属任务 0x%p。  将继续等待。|  
  
## <a name="explanation"></a>解释  
 进程正在等待获取闩锁。 此问题可能是由所用时间太长而无法完成的 I/O 操作导致的。 通常，此类型的错误是其他任务阻塞系统进程的结果。 在一些实例中，此错误可能是硬件故障引起的。  
  
## <a name="user-action"></a>用户操作  
 尝试执行以下操作以防止出现此错误：  
  
-   减少工作负荷。  
  
-   在错误日志或事件日志中检查关联的 I/O 故障。 I/O 故障通常是指磁盘故障。  
  
-   检查错误日志以查找非生成任务和其他错误。  
  
-   如果频繁出现诸如断定之类的错误，请解决这些问题。  
  
 如果错误仍存在，请与 Microsoft 客户服务与支持部门联系。  
  
  