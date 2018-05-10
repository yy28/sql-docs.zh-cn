---
title: 提示 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a404f015c177fe38985c07470645e9a16e2cb716
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
  
