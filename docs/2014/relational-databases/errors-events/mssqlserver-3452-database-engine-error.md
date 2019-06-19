---
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0e811d36160cf0a4477452acec336c61bf52e793
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868064"
---
# <a name="mssqlserver3452"></a>MSSQLSERVER_3452
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3452|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|REC_CHECKIDENTITY|  
|消息正文|数据库 '%.*ls' (%d)的恢复操作检测到表 ID %d 中的标识值可能不一致。 请运行 DBCC CHECKIDENT ('%.\*ls')。|  
  
## <a name="explanation"></a>解释  
 在升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 期间，用于恢复数据库中标识值的进程发现元数据中存在不一致的地方。  
  
## <a name="user-action"></a>用户操作  
 运行 DBCC CHECKIDENT。  
  
  
