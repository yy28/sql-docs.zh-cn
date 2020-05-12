---
title: 数学函数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- calculations [SQL Server]
- mathematical functions [SQL Server]
- functions [SQL Server], mathematical
ms.assetid: 46495a2e-81d0-4677-9d72-9db083cd1023
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 28cee5f6b7b1f3ea16ac490a24b10417d0d5f83d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822479"
---
# <a name="mathematical-functions-transact-sql"></a>数学函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  下列标量函数通常基于作为参数提供的输入值执行计算，并返回一个数值：  
  
||||  
|-|-|-|  
|[ABS](../../t-sql/functions/abs-transact-sql.md)|[DEGREES](../../t-sql/functions/degrees-transact-sql.md)|[RAND](../../t-sql/functions/rand-transact-sql.md)|  
|[ACOS](../../t-sql/functions/acos-transact-sql.md)|[EXP](../../t-sql/functions/exp-transact-sql.md)|[ROUND](../../t-sql/functions/round-transact-sql.md)|  
|[ASIN](../../t-sql/functions/asin-transact-sql.md)|[FLOOR](../../t-sql/functions/floor-transact-sql.md)|[SIGN](../../t-sql/functions/sign-transact-sql.md)|  
|[ATAN](../../t-sql/functions/atan-transact-sql.md)|[LOG](../../t-sql/functions/log-transact-sql.md)|[SIN](../../t-sql/functions/sin-transact-sql.md)|  
|[ATN2](../../t-sql/functions/atn2-transact-sql.md)|[LOG10](../../t-sql/functions/log10-transact-sql.md)|[SQRT](../../t-sql/functions/sqrt-transact-sql.md)|  
|[CEILING](../../t-sql/functions/ceiling-transact-sql.md)|[PI](../../t-sql/functions/pi-transact-sql.md)|[SQUARE](../../t-sql/functions/square-transact-sql.md)|  
|[COS](../../t-sql/functions/cos-transact-sql.md)|[POWER](../../t-sql/functions/power-transact-sql.md)|[TAN](../../t-sql/functions/tan-transact-sql.md)|  
|[COT](../../t-sql/functions/cot-transact-sql.md)|[RADIANS](../../t-sql/functions/radians-transact-sql.md)||  
  
> [!NOTE]  
>  算术函数（例如 ABS、CEILING、DEGREES、FLOOR、POWER、RADIANS 和 SIGN）返回与输入值具有相同数据类型的值。 三角函数和其他函数（包括 EXP、LOG、LOG10、SQUARE 和 SQRT）将输入值转换为 float 并返回 float 值   。  
  
 除 RAND 以外的所有数学函数都为确定性函数。 这意味着在每次使用特定的输入值集调用这些函数时，它们都将返回相同的结果。 仅当指定种子参数时 RAND 才是确定性函数。 有关函数确定性的详细信息，请参阅[确定性函数和不确定性函数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="see-also"></a>另请参阅  
  [算术运算符 (Transact-SQL)](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)  
  [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)  
  
  
