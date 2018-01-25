---
title: "^ = （位异或赋值） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/10/2017
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
- ^=
- ^=_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ^= (bitwise exclusive OR equals)
- compound operators, ^=
- assignment operators, ^=
- augmented operators, ^=
ms.assetid: ce524b0f-a24d-44e7-bd5b-b6943793cd48
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4da8f3df7201794db31bfff09927c97c128f82b0
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="-bitwise-exclusive-or-assignment-transact-sql"></a>^ = （位异或赋值） (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在两个整数值之间执行“位异或”运算，并将一个值设置为运算的结果。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression ^= expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何数据类型之一除数值类别中**位**数据类型。  
  
## <a name="result-types"></a>结果类型  
 返回优先级较高的参数的数据类型。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>注释  
 有关详细信息，请参阅[^ &#40;按位异或 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md).  
  
## <a name="see-also"></a>另请参阅  
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [按位运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
