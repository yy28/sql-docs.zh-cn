---
title: ":: （范围解析) (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
dev_langs: TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4fa0fa1cd5a86ab4dc736803f6d4926b98f4a30
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="-scope-resolution-transact-sql"></a>:: （范围解析) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  范围解析运算符**::**提供对复合数据类型的静态成员的访问。 复合数据类型是指包含多个简单数据类型和方法，如内置的 CLR 类型和自定义 SQLCLR User-Defined 类型 (Udt)。  
  
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
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
