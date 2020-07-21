---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fde7bbf3e3db95f75606a7b735eef41b7b6abf2b
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552302"
---
# <a name="mssqlserver_1401"></a>MSSQLSERVER_1401
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1401|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBM_MASTERSTARTUP|  
|消息正文|数据库镜像主线程例程的启动因以下原因失败: %ls。 请纠正此错误的原因，然后重新启动 SQL Server 服务。|  
  
## <a name="explanation"></a>说明  
 镜像控制线程启动失败。  
  
## <a name="user-action"></a>用户操作  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中，查看此消息之前的相关错误。 请纠正此错误的原因，然后重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务 (MSSQLSERVER)。  
  
## <a name="see-also"></a>另请参阅  
 [启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
