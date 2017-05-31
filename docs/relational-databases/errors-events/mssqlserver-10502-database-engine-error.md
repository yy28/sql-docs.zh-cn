---
title: MSSQLSERVER_10502 | Microsoft Docs
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
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2f7e1cd208d731f1a8c0cde03a01e2feb0bacadc
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver10502"></a>MSSQLSERVER_10502
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10502|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_DUP_FOUND|  
|消息正文|无法创建计划指南 '%.*ls'，因为 @stmt 和 @module_or_batch 或 @plan_handle 和 @statement_start_offset 指定的语句与数据库中的现有计划指南 '%.\*ls' 相匹配。 请先删除现有计划指南，再创建新的计划指南。|  
  
## <a name="explanation"></a>解释  
指定语句的计划指南已经存在。  
  
## <a name="user-action"></a>用户操作  
请先删除现有计划指南，再创建新的计划指南。  
  
## <a name="see-also"></a>另请参阅  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

