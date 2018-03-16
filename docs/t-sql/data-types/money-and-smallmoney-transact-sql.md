---
title: "money 和 smallmoney (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- money_TSQL
- money
- smallmoney
- smallmoney_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- money data type, about money data type
- money data type
- smallmoney data type
- values [SQL Server], monetary
- currency [SQL Server]
ms.assetid: 57861137-89ea-4b89-b361-390597d7bccc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c9c66d9934618b1b8b21b0d4dcb0a234ff94731f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="money-and-smallmoney-transact-sql"></a>money 和 smallmoney (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

代表货币或货币值的数据类型。
  
## <a name="remarks"></a>Remarks  
  
|数据类型|范围|存储器|  
|---|---|---|
|**money**|-922,337,203,685,477.5808 到 922,337,203,685,477.5807（对于 Informatica，为 -922,337,203,685,477.58<br />到 922,337,203,685,477.58。  Informatica 仅支持两位小数，而不是四位。）|8 字节|  
|**smallmoney**|-214,748.3648 到 214,748.3647|4 个字节|  
  
money 和 smallmoney 数据类型精确到它们所代表的货币单位的万分之一。 对于 Informatica，money 和 smallmoney 数据类型精确到它们所代表的货币单位的百分之一。
  
用句点分隔局部货币单位（如美分）和总体货币单位。 例如，2.15 表示 2 美元 15 美分。
  
这些数据类型可以使用下列任意一种货币符号。
  
![货币符号表，十六进制值](../../t-sql/data-types/media/money01.gif "货币符号表，十六进制值")
  
货币数据不需要用单引号 (') 引起来。 请务必记住虽然您可以指定前面带有货币符号的货币值，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不存储任何与符号关联的货币信息，它只存储数值。
  
## <a name="converting-money-data"></a>转换 money 数据
如果将整型数据类型转换为 **money**，则假设采用货币单位。 例如，整数值 4 被转换为相当于 4 个货币单位的 **money** 值。
  
下面的示例分别将 smallmoney 和 money 值转换为 varchar 和 decimal 数据类型。
  
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
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)
[ (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)
[sys.types (Transact-SQL)](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
