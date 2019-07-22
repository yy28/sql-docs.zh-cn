---
title: ::(Scope Resolution) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
author: rothja
ms.author: jroth
ms.openlocfilehash: ff16ec709e8ed3cf7e0d6a4b129641d1e553a11a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072287"
---
# <a name="-scope-resolution-transact-sql"></a>::(Scope Resolution) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  作用域解析运算符 :: 提供对复合数据类型的静态成员的访问。 复合数据类型是指包含多个简单数据类型和方法的数据类型。 复合数据类型包括内置的 CLR 类型和自定义 SQLCLR 用户定义类型 (UDT)。  
  
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
 