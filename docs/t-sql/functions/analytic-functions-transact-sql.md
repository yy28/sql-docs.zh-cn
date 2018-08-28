---
title: 分析函数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 60fbff84-673b-48ea-9254-6ecdad20e7fe
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 82938a1b8953e36d83ff7da7de1ab0e5f1f85281
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43081979"
---
# <a name="analytic-functions-transact-sql"></a>分析函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

SQL Server 支持以下分析函数：
  
|||  
|-|-|  
|[CUME_DIST (Transact-SQL)](../../t-sql/functions/cume-dist-transact-sql.md)|[LEAD (Transact-SQL)](../../t-sql/functions/lead-transact-sql.md)|  
|[FIRST_VALUE (Transact-SQL)](../../t-sql/functions/first-value-transact-sql.md)|[PERCENTILE_CONT (Transact-SQL)](../../t-sql/functions/percentile-cont-transact-sql.md)|  
|[LAG (Transact-SQL)](../../t-sql/functions/lag-transact-sql.md)|[PERCENTILE_DISC (Transact-SQL)](../../t-sql/functions/percentile-disc-transact-sql.md)|  
|[LAST_VALUE (Transact-SQL)](../../t-sql/functions/last-value-transact-sql.md)|[PERCENT_RANK (Transact-SQL)](../../t-sql/functions/percent-rank-transact-sql.md)|  
  
分析函数基于一组行计算聚合值。 但是，与聚合函数不同，分析函数可能针对每个组返回多行。 可以使用分析函数来计算移动平均线、运行总计、百分比或一个组内的前 N 个结果。
 
## <a name="see-also"></a>另请参阅
[OVER 子句 (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
