---
title: '@@MAX_PRECISION (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@MAX_PRECISION_TSQL'
- '@@MAX_PRECISION'
dev_langs:
- TSQL
helpviewer_keywords:
- precision [SQL Server], @@MAX_PRECISION
- numeric data type, precision level
- decimal data type, precision level
- '@@MAX_PRECISION function'
- data types [SQL Server], precision
ms.assetid: 9e7158a1-e503-422a-b326-3c9b06e181b2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 696b0a010a8267e42cd55bc123081add60090840
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68130320"
---
# <a name="x40x40max_precision-transact-sql"></a>&#x40;&#x40;MAX_PRECISION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  按照服务器中的当前设置，返回 decimal 和 numeric 数据类型所用的精度级别   。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@MAX_PRECISION  
```  
  
## <a name="return-types"></a>返回类型  
 **tinyint**  
  
## <a name="remarks"></a>备注  
 默认情况下，最大精度返回 38。  
  
## <a name="examples"></a>示例  
  
```  
SELECT @@MAX_PRECISION AS 'Max Precision'  
```  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [decimal 和 numeric (Transact-SQL)](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [精度、小数位数和长度 (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)  
  
  
