---
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 510233f2f843eafc3c8acca85e7e01872ab2dfcb
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411886"
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
  
  
