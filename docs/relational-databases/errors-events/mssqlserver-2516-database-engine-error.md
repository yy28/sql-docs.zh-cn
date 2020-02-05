---
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4a9c6719946842be6d5b3e8484186d57e4b98042
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68138522"
---
# <a name="mssqlserver_2516"></a>MSSQLSERVER_2516
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2516|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|消息正文|修复操作已经使数据库 NAME 的差异位图无效。 差异备份链断开。 必须首先执行完全数据库备份，才能执行差异备份。|  
  
## <a name="explanation"></a>说明  
在修复错误 MSSQLEngine_2515 时返回了此信息性消息。  
  
## <a name="user-action"></a>用户操作  
执行一次完整数据库备份。  
  
## <a name="see-also"></a>另请参阅  
[创建完整数据库备份 (SQL Server)](~/relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
