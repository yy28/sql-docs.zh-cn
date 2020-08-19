---
description: 游标函数 (Transact-SQL)
title: 游标函数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cursors
- cursor functions
ms.assetid: 7d9daa10-4c50-4212-9400-42120222b2b8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: feed3d608cf3031d03467b19494dabc7844460fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468066"
---
# <a name="cursor-functions-transact-sql"></a>游标函数 (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

以下标量函数可返回有关游标的信息：
  
- [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)
- [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)
- [CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)
  
所有游标函数都是非确定性的。 换言之，即使是同一组输入值，也不一定在每次调用这些函数时都返回相同的结果。 有关函数确定性的详细信息，请参阅[确定性函数和不确定性函数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
## <a name="see-also"></a>另请参阅

[内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)
