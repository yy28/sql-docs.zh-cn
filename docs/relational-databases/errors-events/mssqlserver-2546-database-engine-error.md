---
title: MSSQLSERVER_2546 | Microsoft Docs
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
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4eafa4dd883103c600864d15da704a8e6beb4cd4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2546"></a>MSSQLSERVER_2546
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2546|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_INDEX_MARKED_DISABLED|  
|消息正文|表 'OBJECT_NAME' 的索引 'INDEX_NAME' 已标记为禁用。 请重新生成该索引，以使之联机。|  
  
## <a name="explanation"></a>解释  
指定的索引已标记为离线或禁用。 因此，不能检查该索引。  
  
## <a name="user-action"></a>用户操作  
请使用 ALTER INDEX 重新生成索引。  
  
## <a name="see-also"></a>另请参阅  
[ALTER INDEX (Transact-SQL)](~/t-sql/statements/alter-index-transact-sql.md)  
[重新组织和重新生成索引](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
