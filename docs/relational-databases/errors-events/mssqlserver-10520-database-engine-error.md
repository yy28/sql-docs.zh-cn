---
title: MSSQLSERVER_10520 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4b39522a5aa1e3208dfe1f7440abe20f4f0e00fc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68068162"
---
# <a name="mssqlserver_10520"></a>MSSQLSERVER_10520
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10520|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_PARAM_NOT_ALLOWED|  
|消息正文|无法创建计划指南 '%.*ls'，因为 @type 指定为 '%ls' ，并且为参数 '%ls' 指定了非 NULL 值。 此类型要求该参数的值为 NULL 值。 请为该参数指定 NULL 值，或将该类型更改为允许该参数为非 NULL 值的类型。|  
  
## <a name="explanation"></a>说明  
@type 中指定的类型要求指定参数的值为 NULL 值，但却提供了非 NULL 值。  
  
## <a name="user-action"></a>用户操作  
请为该参数指定 NULL 值，或将该类型更改为允许该参数为非 NULL 值的类型。  
  
## <a name="see-also"></a>另请参阅  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
  
