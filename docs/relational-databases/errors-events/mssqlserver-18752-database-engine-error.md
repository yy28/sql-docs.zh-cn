---
title: MSSQLSERVER_18752 | Microsoft Docs
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
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ce144117d65f5e1c30f0f37ba7483c6d098db074
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver18752"></a>MSSQLSERVER_18752
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|18752|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|REPL_INUSE|  
|消息正文|一次只能有一个日志读取器代理或日志相关过程(sp_repldone、sp_replcmds 和 sp_replshowcmds)连接到某个数据库。 如果执行了一个日志相关过程，那么在启动日志读取器代理或者执行另一个日志相关过程之前，请删除执行第一个过程时所用的连接，或者在该连接上执行 sp_replflush。|  
  
## <a name="explanation"></a>解释  
一次只能有一个日志读取器代理或日志相关过程连接到某个数据库。  
  
## <a name="user-action"></a>用户操作  
确保没有为相同发布数据库运行其他日志读取器，并且以前其他活动连接在运行 sp_replcmds/sp_repltrans/sp_repldone 后均运行了 sp_replflush 或断开了连接。  
  
