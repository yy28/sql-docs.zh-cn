---
title: ROWCOUNT_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ROWCOUNT_BIG
- ROWCOUNT_BIG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ROWCOUNT_BIG function
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 6e18a0eb-bb36-4348-90d9-8b1ecf095064
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: e1ccc5aa9619c96fd75400531041442138e0b4f3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828631"
---
# <a name="rowcount_big-transact-sql"></a>ROWCOUNT_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回已执行的上一语句影响的行数。 该函数的功能与 [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md) 类似，区别在于 ROWCOUNT_BIG 的返回类型为 bigint  。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ROWCOUNT_BIG ( )  
```  
  
## <a name="return-types"></a>返回类型  
 **bigint**  
  
## <a name="remarks"></a>备注  
 位于 SELECT 语句之后时，该函数返回由 SELECT 语句返回的行数。  
  
 位于 INSERT、UPDATE 或 DELETE 语句之后时，该函数返回受数据修改语句影响的行数。  
  
 位于 IF 这类不返回行的语句之后时，该函数返回 0。  
  
## <a name="see-also"></a>另请参阅  
 [COUNT_BIG (Transact-SQL)](../../t-sql/functions/count-big-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
