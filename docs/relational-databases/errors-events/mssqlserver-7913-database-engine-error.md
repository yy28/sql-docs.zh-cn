---
title: MSSQLSERVER_7913 | Microsoft Docs
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
- 7913 (Database Engine error)
ms.assetid: 9d8ad456-b1a2-4f79-a252-657fbec9ad9b
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 91164043559461bb8bfd7d75b1792f11b8616972
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver7913"></a>MSSQLSERVER_7913
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7913|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_REPAIR_EXTENT_DEALLOCATED|  
|消息正文|修复：区 P_ID 已从对象 ID O_ID，索引 ID I_ID，分区 ID PN_ID，分配单元 ID A_ID (类型为 TYPE)释放。|  
  
## <a name="explanation"></a>解释  
这是来自 REPAIR 的信息性消息，该消息声明已将一个区从指定的对象释放。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  
