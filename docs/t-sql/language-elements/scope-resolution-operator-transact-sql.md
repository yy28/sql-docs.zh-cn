---
title: ::（作用域解析）(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed1338f3cf8c5de3f532542b57e73533de035a1e
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36241669"
---
# <a name="-scope-resolution-transact-sql"></a>::（作用域解析）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  作用域解析运算符 :: 提供对复合数据类型的静态成员的访问。 复合数据类型包含多个简单数据类型和方法，例如内置 CLR 类型和自定义 SQL CLR 用户定义类型 (UDT)。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何使用作用域解析运算符访问 `GetRoot()` 类型的 `hierarchyid` 成员。  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>另请参阅  
 [运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
