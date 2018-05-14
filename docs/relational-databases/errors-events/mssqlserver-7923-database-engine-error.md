---
title: MSSQLSERVER_7923 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7923 (Database Engine error)
ms.assetid: b09a95e2-0ffe-4847-aa77-51e6639259f6
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c97f09190c640e6af69ffdaf8fb58edf202e1188
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver7923"></a>MSSQLSERVER_7923
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7923|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_SUMMARY_TABLE_NAME|  
|消息正文|表 TABLE                对象 ID O_ID。|  
  
## <a name="explanation"></a>解释  
这是来自 DBCC CHECKALLOC 命令的信息性消息。 在该消息中，表中所有分配单元的分配信息列表顶部都包含表名和表 ID。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  
