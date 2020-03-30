---
title: ^= 位异或赋值
description: 在两个整数值之间进行位异或运算，并将一个值设置为运算的结果。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ^=
- ^=_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ^= (bitwise exclusive OR equals)
- compound operators, ^=
- assignment operators, ^=
- augmented operators, ^=
ms.assetid: ce524b0f-a24d-44e7-bd5b-b6943793cd48
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 814d71913ad58463ad15908e189ae299f2ac7f48
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "75252175"
---
# <a name="-bitwise-exclusive-or-assignment-transact-sql"></a>^=（位异或赋值）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在两个整数值之间执行“位异或”运算，并将一个值设置为运算的结果。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression ^= expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 数值类别中任意数据类型（bit 数据类型除外）的任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)  。  
  
## <a name="result-types"></a>结果类型  
 返回优先级较高的参数的数据类型。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>备注  
 有关详细信息，请参阅[^（位异或）(Transact-SQL)](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [复合运算符 (Transact-SQL)](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)   
 [运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)   
 [位运算符 (Transact-SQL)](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
