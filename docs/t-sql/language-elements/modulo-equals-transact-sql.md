---
title: "取模等于 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '%=_TSQL'
- '%='
dev_langs:
- TSQL
helpviewer_keywords:
- '%= (modulo equals)'
- compound operators, %=
ms.assetid: 45e35516-1f4c-406b-a580-70a14b087847
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5d425882e4d0e6b16334bcd0ec7dc5af0487a5c0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="modulo-equals-transact-sql"></a>取模等于 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  将一个数除以另一个数并将值设置为运算的结果。 例如，如果变量@x然后等于 38， @x %= 5 采用的原始值@x、 除以 5，并将设置@x到 (3) 该除法运算的余数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression %= expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何数据类型之一除数值类别中**位**数据类型。  
  
## <a name="result-types"></a>结果类型  
 返回优先级较高的参数的数据类型。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>注释  
 有关详细信息，请参阅[取模 &#40;Transact SQL &#41;](../../t-sql/language-elements/modulo-transact-sql.md).  
  
## <a name="see-also"></a>另请参阅  
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
