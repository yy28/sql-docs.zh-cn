---
title: MSSQLSERVER_17803 | Microsoft Docs
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
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84dad82e56f418813c5a6ddfaf5425b3b9aec9f8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver17803"></a>MSSQLSERVER_17803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17803|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SRV_NOMEMORY|  
|消息正文|在建立连接过程中出现内存分配错误。 减少不必要的内存负载，或增加系统内存。 该连接已关闭。%.*ls|  
  
## <a name="explanation"></a>解释  
服务器内存不足。  
  
## <a name="user-action"></a>用户操作  
确定服务器内存不足的原因。 一般内存故障排除步骤可能会很有用  
  
