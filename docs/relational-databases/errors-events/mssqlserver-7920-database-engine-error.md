---
title: MSSQLSERVER_7920 | Microsoft Docs
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
- 7920 (Database Engine error)
ms.assetid: d16290ea-3875-4148-8d53-057bfee00438
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2fab1d56794ae72d1e7122bfd2ca48d181181a6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver7920"></a>MSSQLSERVER_7920
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7920|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_SUMMARY_ENTRIES|  
|消息正文|已在系统目录中为数据库 ID D_ID 处理 ENTRY_COUNT 项。|  
  
## <a name="explanation"></a>解释  
这是由 DBCC CHECKALLOC 以外的所有 DBCC CHECK 命令返回的信息性消息。 返回值是所检查的总行集数。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  
