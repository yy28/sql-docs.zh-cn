---
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a9abebe50426f671e444514b29ccc2235e4a2109
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68120475"
---
# <a name="mssqlserver_8712"></a>MSSQLSERVER_8712
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8712|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|USEPLAN_ERR_NO_INDEX|  
|消息正文|USE PLAN 提示中指定的索引 '%.*ls' 不存在。 请指定一个现有索引，或者使用指定名称创建一个索引。|  
  
## <a name="explanation"></a>说明  
USE PLAN 提示中指定的索引不存在。  
  
## <a name="user-action"></a>用户操作  
请确保在 USE PLAN 提示中指定的所有索引均存在。  
  
## <a name="see-also"></a>另请参阅  
[查询提示 (Transact-SQL)](~/t-sql/queries/hints-transact-sql-query.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
  
