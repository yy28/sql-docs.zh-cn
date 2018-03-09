---
title: MSSQLSERVER_17142 | Microsoft Docs
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
- 17142 (Database Engine error)
ms.assetid: 83a53507-ac76-4cb9-b116-daf6f42aea1f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f335a03f49755e1671144a898cf59325538a3fe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver17142"></a>MSSQLSERVER_17142
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17142|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|INIT_SRVC_PAUSED|  
|消息正文|SQL Server 服务已经暂停。 不允许进行新的连接。 要恢复此服务，请使用 SQL 计算机管理器或控制面板中的服务应用程序。|  
  
## <a name="explanation"></a>解释  
服务控制管理器暂停了 SQL Server 的服务。  
  
## <a name="user-action"></a>用户操作  
使用 SQL Server 配置管理器恢复 SQL Server 的服务。  
  
