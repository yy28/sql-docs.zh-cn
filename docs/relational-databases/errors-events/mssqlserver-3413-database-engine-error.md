---
title: MSSQLSERVER_3413 | Microsoft Docs
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
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9cfa7a7f5b40767776c0db4ac58918ccf45080f4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3413|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|MARKDB|  
|消息正文|数据库 ID 为 %d。 无法将数据库标记为可疑。 对 sys.databases.database_id 进行的 Getnext NC 扫描失败。 请参阅错误日志中以前的错误，以标识原因并更正任何相关的问题。|  
  
## <a name="explanation"></a>解释  
尝试将用户数据库标记为目录中的 SUSPECT 时意外失败。 SUSPECT 状态不会持久化。  
  
## <a name="user-action"></a>用户操作  
请参阅以前的错误并更正问题。  
  
