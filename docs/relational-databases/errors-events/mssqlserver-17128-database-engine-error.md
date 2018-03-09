---
title: MSSQLSERVER_17128 | Microsoft Docs
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
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10284d4192b05ff7fac278e5a02e33384982517f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver17128"></a>MSSQLSERVER_17128
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17128|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|INIT_NOBUFSPACE|  
|消息正文|initdata: 没有可用于核心缓冲区的内存。|  
  
## <a name="explanation"></a>解释  
缓冲池的初始内存分配或保留失败，并且 SQL Server 退出。  
  
## <a name="user-action"></a>用户操作  
通常是由在非常小的计算机（远小于最低系统要求）上启动 SQL Server 引起的。  
  
