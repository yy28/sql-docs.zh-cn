---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b57f8a7985c9fb092209bc5a80b9d0c3294d98c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781490"
---
# <a name="mssqlserver_10519"></a>MSSQLSERVER_10519
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|10519|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|消息正文|无法创建计划指南“%.\*ls”，因为 \@hints 中指定的提示无法应用于 \@stmt 或 \@statement_start_offset 指定的语句  。 请确保提示可以应用于该语句。|  
  
## <a name="explanation"></a>说明  
\@hints 中指定的提示无法应用于 \@stmt 或 \@statement_start_offset 指定的语句  。  
  
## <a name="user-action"></a>用户操作  
请指定可以应用于该语句的提示。  
  
## <a name="see-also"></a>另请参阅  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
