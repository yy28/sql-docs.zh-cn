---
title: MSSQLSERVER_7910 | Microsoft Docs
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
- 7910 (Database Engine error)
ms.assetid: 017a0113-2b17-40b3-a419-30bbc43d46b8
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01e0adf10277d3a584f1e485dada9eb99d071672
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver7910"></a>MSSQLSERVER_7910
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7910|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_REPAIR_PAGE_ALLOCATED|  
|消息正文|修复: 页 P_ID 已分配给对象 ID O_ID，索引 ID I_ID，分区 ID PN_ID，分配单元 ID A_ID（类型为 TYPE）。|  
  
## <a name="explanation"></a>解释  
这是来自 REPAIR 的信息性消息，指示页已分配给索引分配映射 (IAM) 页的单页槽数组。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  
