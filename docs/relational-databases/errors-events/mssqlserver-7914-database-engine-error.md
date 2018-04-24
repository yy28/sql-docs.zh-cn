---
title: MSSQLSERVER_7914 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7914 (Database Engine error)
ms.assetid: d32a81ce-4ca7-4b33-b536-c7ea0ed6f226
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64a2f6c62dd7d07310521723ef78b3931d4c5750
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7914"></a>MSSQLSERVER_7914
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7914|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_REPAIR_ALLOCATION_PAGE_REBUILT|  
|消息正文|修复: 位于 P_ID 的 PAGE_TYPE 页已重新生成。|  
  
## <a name="explanation"></a>解释  
这是来自 REPAIR 的信息性消息，该消息声明 GAM 或 SGAM 页已通过使用 PFS 页数据重新生成。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  
