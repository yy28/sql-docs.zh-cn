---
title: '*=（乘法赋值）(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '*=_TSQL'
- '*='
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, *=
- assignment operators, *=
- augmented operators, *=
- '*= (multiply equals)'
- '*= (multiplication assignment)'
ms.assetid: 816ff5dc-9a40-4c07-8351-39c194dbc079
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a72aef774c866b8ad3d8569768c8d8730d58e681
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65981967"
---
# <a name="-multiplication-assignment-transact-sql"></a>*=（乘法赋值）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

将两个数字相乘并将值设置为该运算的结果。 例如，如果变量 @x 等于 35，则 @x *= 2 会将 @x 的原始值乘以 2 并将 @x 设置为该新值 (70)。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression *= expression  
```  
  
## <a name="arguments"></a>参数  
_expression_  
数值类别中的任意有效数据类型[表达式](../../t-sql/language-elements/expressions-transact-sql.md)（bit 类型除外）。  
  
## <a name="result-types"></a>结果类型  
返回优先级较高的参数的数据类型。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
有关详细信息，请参阅[（乘法）(Transact-SQL)](../../t-sql/language-elements/multiply-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
[复合运算符 (Transact-SQL)](../../t-sql/language-elements/compound-operators-transact-sql.md)   
[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)   
[运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
