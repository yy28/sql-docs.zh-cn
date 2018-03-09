---
title: "行集函数 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], rowsets
- rowsets [SQL Server], functions
- rowsets [SQL Server]
ms.assetid: ac24d700-3144-4ab5-9fa8-8c014001cc71
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 665dec7b2e143267fe5964fe3f8d987ddb087d2f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="rowset-functions-transact-sql"></a>行集函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  下列行集函数将返回一个可用于代替 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中表引用的对象。  
  
|||  
|-|-|  
|[OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md)|[OPENJSON](../../t-sql/functions/openjson-transact-sql.md)|  
|[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)|[OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)|  
|[OPENXML](../../t-sql/functions/openxml-transact-sql.md)||  
  
 所有行集函数都具有不确定性。 这意味着即使同一组输入值，也不一定在每次调用这些函数时都返回相同的结果。 有关函数的确定性的详细信息，请参阅[Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)  
  
  
