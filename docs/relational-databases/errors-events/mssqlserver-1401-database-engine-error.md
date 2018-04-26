---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d30bfa0a55fcf15c5027f4fd7dcdceaf9c22d55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1401|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBM_MASTERSTARTUP|  
|消息正文|数据库镜像主线程例程的启动因以下原因失败: %ls。 请纠正此错误的原因，然后重新启动 SQL Server 服务。|  
  
## <a name="explanation"></a>解释  
镜像控制线程启动失败。  
  
## <a name="user-action"></a>用户操作  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中，查看此消息之前的相关错误。 请纠正此错误的原因，然后重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务 (MSSQLSERVER)。  
  
## <a name="see-also"></a>另请参阅  
[启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
