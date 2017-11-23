---
title: "money 和 smallmoney (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- money_TSQL
- money
- smallmoney
- smallmoney_TSQL
dev_langs: TSQL
helpviewer_keywords:
- money data type, about money data type
- money data type
- smallmoney data type
- values [SQL Server], monetary
- currency [SQL Server]
ms.assetid: 57861137-89ea-4b89-b361-390597d7bccc
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c9c66d9934618b1b8b21b0d4dcb0a234ff94731f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="money-and-smallmoney-transact-sql"></a>money 和 smallmoney (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

代表货币或货币值的数据类型。
  
## <a name="remarks"></a>注释  
  
|数据类型|范围|存储器|  
|---|---|---|
|**money**|-922,337,203,685,477.5808 到 922337203685，477.5807 (-922,337,203,685,477.58<br />to Informatica 的 922,337,203,685,477.58。  Informatica 仅支持两位小数，不四个。）|8 字节|  
|**smallmoney**|-214,748.3648 到 214,748.3647|4 个字节|  
  
**Money**和**smallmoney**数据类型是精确到它们表示的货币单位的万分之一。 有关 Informatica， **money**和**smallmoney**数据类型是精确到货币单位表示的百分之一。
  
用句点分隔局部货币单位（如美分）和总体货币单位。 例如，2.15 表示 2 美元 15 美分。
  
这些数据类型可以使用下列任意一种货币符号。
  
![表的十六进制值的货币符号](../../t-sql/data-types/media/money01.gif "的十六进制值的货币符号表")
  
货币数据不需要用单引号 (') 引起来。 请务必记住虽然您可以指定前面带有货币符号的货币值，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不存储任何与符号关联的货币信息，它只存储数值。
  
## <a name="converting-money-data"></a>将 money 数据转换
转换为**money**整数数据类型，从单元被假定为货币单位。 例如，4 的整数值转换为**money**等效的 4 个货币单位。
  
以下示例将转换**smallmoney**和**money**值复制到**varchar**和**十进制**分别数据类型。
  
```sql
DECLARE @mymoney_sm smallmoney = 3148.29,  
        @mymoney    money = 3148.29;  
SELECT  CAST(@mymoney_sm AS varchar) AS 'SM_MONEY varchar',  
        CAST(@mymoney AS decimal)    AS 'MONEY DECIMAL';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
SM_MONEY VARCHAR               MONEY DECIMAL  
------------------------------ ----------------------  
3148.29                        3148    
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[ALTER TABLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md) 
 [CAST 和 CONVERT &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md) 
[创建 TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md) 
[数据类型 &#40;Transact SQL &#41;](../../t-sql/data-types/data-types-transact-sql.md) 
 [DECLARE @local_variable &#40;Transact SQL &#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
[设置@local_variable&#40;Transact SQL &#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md) 
 [sys.types &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
