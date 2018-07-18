---
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 40db649d00b0c543d6c4f1a332cb541029c0ffea
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34318778"
---
# <a name="mssqlserver3452"></a>MSSQLSERVER_3452
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
