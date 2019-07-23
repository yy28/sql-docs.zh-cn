---
title: MSSQLSERVER_9003 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eb3fcdb8bc7921c8321cc25ec9380143e7f68a68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118352"
---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
