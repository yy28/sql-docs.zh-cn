---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cfc717c63cb85207315d00ae8dc06fdd881a503c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48053597"
---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9001|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LOG_NOT_AVAIL|  
|消息正文|数据库 '%.*ls' 的日志不可用。 有关相应错误消息，请查看事件日志。 修复所有错误后重新启动数据库。|  
  
## <a name="explanation"></a>解释  
 数据库日志处于脱机状态。 通常，这表示需要重新启动数据库的灾难性故障。  
  
## <a name="user-action"></a>用户操作  
 诊断其他错误并重新启动 SQL Server 实例（如果尚未自行重新启动）。  
  
  
