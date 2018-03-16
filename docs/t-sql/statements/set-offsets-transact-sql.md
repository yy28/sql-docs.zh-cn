---
title: SET OFFSETS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_OFFSETS_TSQL
- OFFSETS_TSQL
- SET OFFSETS
- OFFSETS
dev_langs:
- TSQL
helpviewer_keywords:
- position relative to start of statement [SQL Server]
- OFFSETS option
- offsets [SQL Server]
- SET OFFSETS statement
ms.assetid: c7bcc697-0930-4630-acae-d8ccbfa4414c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 232550be5756505082b615a84ccbd35ef84b1477
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="set-offsets-transact-sql"></a>SET OFFSETS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中指定关键字的偏移量（相对于语句起始点的位置）返回给 DB-Library 应用程序。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SET OFFSETS keyword_list { ON | OFF }  
```  
  
## <a name="arguments"></a>参数  
 keyword_list  
 用逗号分隔的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 构造列表，包括 SELECT、FROM、ORDER、TABLE、PROCEDURE、STATEMENT、PARAM 和 EXECUTE。  
  
## <a name="remarks"></a>Remarks  
 SET OFFSETS 只用在 DB-Library 应用程序中。  
  
 SET OFFSETS 的设置是在分析时设置，而不是在执行或运行时设置。 在分析时进行设置意味着：SET 语句只要出现在批处理或存储过程中，该设置即生效，与代码执行实际上是否到达该点无关；并且 SET 语句在任何语句执行之前生效。 例如，假设 SET 语句在 IF...ELSE 语句块中，而在执行过程中从未到达过该语句块，但由于分析了 IF...ELSE 语句块，因此 SET 语句仍生效。  
  
 如果在存储过程中设置 SET OFFSETS，则从存储过程返回控制后将还原 SET OFFSETS 的值。 因此，动态 SQL 中指定的 SET OFFSETS 语句对动态 SQL 语句之后的任何语句无效。  
  
 如果 OFFSETS 选项为 ON 而且没有出现错误，则 SET PARSEONLY 返回偏移量。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET PARSEONLY (Transact-SQL)](../../t-sql/statements/set-parseonly-transact-sql.md)  
  
  
