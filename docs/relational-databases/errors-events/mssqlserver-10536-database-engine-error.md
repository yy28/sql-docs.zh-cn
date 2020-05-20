---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 85901c0fc1a720849cb93f7392ade34ff1db35e0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71174277"
---
# <a name="mssqlserver_10536"></a>MSSQLSERVER_10536
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10536|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_TOO_MANY_STMTS|  
|消息正文|无法创建计划指南“%.\*ls”，因为与指定 \@plan_handle 对应的批或模块中包含的合格语句超过 1000 个。 通过为每个语句指定 **statement_start_offset** 值，为批处理或模块中的每个语句创建一个计划指南。|  
  
## <a name="explanation"></a>说明  
与指定的 \@plan_handle 对应的批或模块中包含的合格语句超过 1000 个。  
  
## <a name="user-action"></a>用户操作  
通过为每个语句指定 **statement_start_offset** 值，为批处理或模块中的每个语句创建一个计划指南。  
  
## <a name="see-also"></a>另请参阅  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
