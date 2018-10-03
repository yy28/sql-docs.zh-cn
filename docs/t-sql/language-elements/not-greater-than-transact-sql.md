---
title: '!&gt;（不大于）(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Not Greater
- Greater
- '!>_TSQL'
- '!>'
- Not Greater Than
dev_langs:
- TSQL
helpviewer_keywords:
- '!> (not greater than)'
- not greater than operator (!>)
ms.assetid: 71a413ed-64f1-4ab9-9c52-c5959a77d00f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 013c620609b5f8d3fc603df993eda1af377c1a26
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686777"
---
# <a name="gt-not-greater-than-transact-sql"></a>!&gt;（不大于）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  比较两个表达式（比较运算符）。 当比较非空表达式时，如果左侧操作数的值不大于右侧的操作数，则结果为 TRUE；否则结果为 FALSE。 与 =（等于）比较运算符不同，使用 !> 比较两个 NULL 值的结果不依赖于 ANSI_NULLS 设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
expression !> expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 为任意有效的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 两个表达式都必须包含可隐式转换的数据类型。 转换方式取决于[数据类型优先级](../../t-sql/data-types/data-type-precedence-transact-sql.md)的相关规则。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
