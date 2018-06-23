---
title: MSSQLSERVER_9003 | Microsoft Docs
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
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 76b05ac7adb3577d45657ad2bc772507f79e7dde
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026777"
---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9003|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LOG_INVALID_LSN|  
|消息正文|传递给数据库 '%.*ls' 中的日志扫描操作的日志扫描号 %S_LSN 无效。 此错误可能指示数据损坏，或者日志文件(.ldf)与数据文件(.mdf)不匹配。 如果此错误是在复制期间出现的，请重新创建发布。 否则，如果该问题导致启动期间出错，请从备份还原。|  
  
## <a name="explanation"></a>解释  
 组件传递给数据库日志管理器的日志序列号无效。 这可能是由于复制、损坏或主数据文件与日志不一致造成的。  
  
## <a name="user-action"></a>用户操作  
 如果在复制期间出现这种错误，请重新创建发布。 否则，请从备份还原。  
  
  