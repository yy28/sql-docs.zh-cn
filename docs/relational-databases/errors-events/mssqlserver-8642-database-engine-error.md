---
title: MSSQLSERVER_8642 | Microsoft Docs
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
- 8642 (Database Engine error)
ms.assetid: fc498059-202f-4d0b-8599-4e784b47c186
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7270f28654a90ab6245845b0ea606c3dfa8a070f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver8642"></a>MSSQLSERVER_8642
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8642|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|EXCHNGSTART_ERR|  
|消息正文|查询处理器未能为执行并行查询启动必要的线程资源。|  
  
## <a name="explanation"></a>解释  
服务器中的线程资源不足。  
  
## <a name="user-action"></a>用户操作  
减少服务器上的负载，然后重新运行查询。  
  
