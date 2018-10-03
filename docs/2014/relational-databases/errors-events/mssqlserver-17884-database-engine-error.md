---
title: MSSQLSERVER_17884 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e31c7a78b74a307bc4c57216ef6c87e989493519
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072333"
---
# <a name="mssqlserver17884"></a>MSSQLSERVER_17884
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17884|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SRV_SCHEDULER_DEADLOCK|  
|消息正文|在最后 %d 秒内，没有一个工作线程拾取了分配给节点 %d 上的进程的新查询。 查询被阻塞或长时间运行可能导致出现此情况，并且可能会延长客户端响应时间。 请使用 "最大工作线程数(max worker threads)" 配置选项增加允许的线程数，或者优化当前正运行的查询。  SQL 进程使用率: %d%%。 系统空闲率：%d%%。|  
  
## <a name="explanation"></a>解释  
 每个计划程序都没有向前运行的迹象，这可能是由死锁造成的：每个线程都无法向前运行和/或无法提取并处理新的工作。 如果进程使用率较低，计算机上的其他进程可能导致服务器进程 CPU 不足。  
  
## <a name="user-action"></a>用户操作  
 确定发生阻塞而无法向前运行的原因，并相应地解决这些问题。 如果进程使用率较低，请检查系统上其他进程产生的负载。  
  
  
