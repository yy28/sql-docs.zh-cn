---
title: "sqlagent90 应用程序 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- starting SQL Server Agent
- sqlagent90 application
- SQL Server Agent, starting
- command prompt utilities [SQL Server], sqlagent90
ms.assetid: e8b80e8d-d0c9-4500-a868-0ce08233da08
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2bd890b534184789349962007e7c55e9f0238e05
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="sqlagent90-application"></a>sqlagent90 应用程序
  **sqlagent90** 应用程序从命令提示符处启动 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理。 通常，应从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或在应用程序中使用 SQL-SMO 方法来运行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 代理。 只有在诊断 **代理时或主要支持提供商指示你使用命令提示符时，才可以从命令提示符处运行** sqlagent90 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlagent90  
-c [-v] [-i instance_name]  
```  
  
## <a name="arguments"></a>参数  
 **-c**  
 指示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理从命令提示符运行，并且独立于 Microsoft Windows 服务控制管理器。 使用 **-c** 时，无法从“管理工具”的“服务”应用程序或从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器控制 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理。 此参数是必需的。  
  
 **-v**  
 指示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理以详细模式运行并向命令提示符窗口写入诊断信息。 该诊断信息与写入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理错误日志中的信息相同。  
  
 **-i** *instance_name*  
 指示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理连接到由 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instance_name *所指定的*命名实例。  
  
## <a name="remarks"></a>注释  
 在显示版权消息后，只有在指定了 **-v** 开关时， **sqlagent90** 才会在命令提示符窗口中显示输出。 若要停止 **sqlagent90**，请在命令提示符处按 CTRL+C。 在停止 **sqlagent90**之前，请不要关闭命令提示符窗口。  
  
## <a name="see-also"></a>另请参阅  
 [自动执行管理任务（SQL Server 代理）](http://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)  
  
  
