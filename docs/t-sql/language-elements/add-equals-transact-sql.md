---
title: "+ = （加法赋值） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- +=
- +=_TSQL
dev_langs: TSQL
helpviewer_keywords:
- += (add equals)
- compound operators, +=
- assignment operators, +=
- augmented operators, +=
ms.assetid: 9ea52519-80d1-473f-b988-0572f0e2c92f
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 138f19c545c5d2ea8f8998e476e8af29d5919852
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="-addition-assignment-transact-sql"></a>+ = （加法赋值） (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  将两个数字相加并将值设置为该运算的结果。 例如，如果变量@x等于 35，则@x+ = 2 采用的原始值@x，将 2 和集添加@x为该新值 (37)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression += expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)除数值类别中的任何数据类型的**位**数据类型。  
  
## <a name="result-types"></a>结果类型  
 返回优先级较高的参数的数据类型。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>注释  
 有关详细信息，请参阅[+ &#40;添加 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/add-transact-sql.md).  
  
## <a name="see-also"></a>另请参阅  
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+ = &#40;字符串串联分配 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/string-concatenation-equal-transact-sql.md)  
  
  
