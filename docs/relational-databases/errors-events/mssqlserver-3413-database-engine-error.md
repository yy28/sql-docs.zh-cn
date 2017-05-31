---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 38900b11bc5e2892ea85f22db2a6c1490d6399fb
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
  
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
  

