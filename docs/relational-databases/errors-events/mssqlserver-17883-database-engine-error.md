---
title: MSSQLSERVER_17883 | Microsoft Docs
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
- 17883 (Database Engine error)
ms.assetid: adaf1c04-e397-4a69-90b8-9353a37277ea
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6228ef52269a304a5e72a3ff3bc50b915ab372f4
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17883"></a>MSSQLSERVER_17883
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17883|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SRV_SCHEDULER_NONYIELDING|  
|消息正文|计划程序 %ld 的进程 %ld:%ld:%ld (0x%lx)工作线程 0x%p 似乎无法完成。 线程创建时间: %I64d。 线程占用 CPU 的近似时间: 内核 %I64d 毫秒，用户 %I64d 毫秒。 进程使用率 %d%%。 系统空闲率 %d%%。 间隔: %I64d 毫秒。|  
  
## <a name="explanation"></a>解释  
指示计划程序上的某个线程可能出现问题，而无法完成。  这可能是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的错误或者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 没有足够的执行周期而引起的。  如果该线程最终完成，此错误可能会消失。  
  
## <a name="user-action"></a>用户操作  
如果系统上的负载过多，请减少负载，否则请与 Microsoft 客户支持服务部门联系。  
  

