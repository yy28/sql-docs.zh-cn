---
title: "!&lt;（不小于）(Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '!<'
- Not Less
- '!<_TSQL'
- Not Less Than
- Less Than
dev_langs: TSQL
helpviewer_keywords:
- '!< (not less than)'
- not less than operator (!<)
ms.assetid: ecbb598e-58a2-4b6c-90b4-3ad5bdfcae39
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2bd79083902b27a5588587e246182fe061312805
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="lt-not-less-than-transact-sql"></a>!&lt;（不小于）(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  比较两个表达式（比较运算符）。 当比较非空表达式时，如果左边操作数的值不小于右边操作数的值，则结果为 TRUE；否则结果为 FALSE。 如果一个或两个操作数都是 NULL，请参阅主题[SET ANSI_NULLS &#40;Transact SQL &#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
expression !< expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 两个表达式都必须包含可隐式转换的数据类型。 转换取决于的规则[数据类型优先级](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
