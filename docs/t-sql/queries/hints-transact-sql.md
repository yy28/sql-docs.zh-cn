---
title: 提示 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query optimizer [SQL Server], hints
- hints [SQL Server], about hints
- SELECT statement [SQL Server], hints
- hints [SQL Server]
- INSERT statement [SQL Server], hints
- UPDATE statement [SQL Server], hints
- DELETE statement [SQL Server], hints
ms.assetid: 99412475-b0df-4264-9938-33a0b302b41a
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8bd2692d428012e0af4ea4f41059228178810abb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62935492"
---
# <a name="hints-transact-sql"></a>提示 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  提示是指定的强制选项或策略，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询处理器针对 SELECT、INSERT、UPDATE 或 DELETE 语句执行。 提示将覆盖查询优化器可能为查询选择的任何执行计划。  
  
> [!CAUTION]  
>  因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询优化器通常会为查询选择最优执行计划，因此我们建议，只有在万般无奈的情况下才由经验丰富的开发人员和数据库管理员使用 \<join_hint>、\<query_hint> 和 \<table_hint>。
  
 本节将介绍下列提示：  
  
-   [联接提示 ](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [查询提示](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [表提示](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
