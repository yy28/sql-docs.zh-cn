---
title: float 和 real (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- float
- real_TSQL
- real
- float_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- numeric data type, floating point
- float data type
- floating point data [SQL Server]
- real data type
ms.assetid: 08ea66b7-624e-4d8b-86bc-750ff76cdfc5
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7a9980c471f81b00f4011b449a1dfcaf9a1f5c98
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="float-and-real-transact-sql"></a>float 和 real (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

用于表示浮点数值数据的大致数值数据类型。 浮点数据为近似值；因此，并非数据类型范围内的所有值都能精确地表示。 real 的 ISO 同义词为 float(24)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
float [ (n) ] 其中 n 为用于存储 float 数值尾数的位数（以科学记数法表示），因此可以确定精度和存储大小****。 如果指定了 n，则它必须是介于 1 和 53 之间的某个值。 n 的默认值为 53。
  
|n 值|精度|存储大小|  
|---|---|---|
|**1-24**|7 位数|4 个字节|  
|**25-53**|15 位数|8 字节|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 n 视为下列两个可能值之一。 如果 1<=n<=24，将 n 视为 24。 如果 25<=n<=53，将 n 视为 53。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] float[(n)] 数据类型从 1 到 53 之间的所有 n 值均符合 ISO 标准。 double precision 的同义词是 float(53)。
  
## <a name="remarks"></a>Remarks  
  
|数据类型|范围|存储器|  
|---|---|---|
|**float**|-1.79E + 308 至 -2.23E - 308、0 以及 2.23E - 308 至 1.79E + 308|取决于 n 的值|  
|**real**|-3.40E + 38 至 -1.18E - 38、0 以及 1.18E - 38 至 3.40E + 38|4 个字节|  
  
##  <a name="converting-float-and-real-data"></a>转换 float 和 real 数据  
如果将 float 值转换为任一整数类型，这些值将被截断。
  
若要将 float 或 real 转换为字符数据，使用 STR 字符串函数通常比使用 CAST( ) 更有用。 这是因为 STR 能够对格式进行更严格的控制。 有关详细信息，请参阅 [STR (Transact-SQL)](../../t-sql/functions/str-transact-sql.md) 和[函数 (Transact-SQL)](../../t-sql/functions/functions.md)。
  
如果将使用科学记数法的 float 值转换为 decimal 或 numeric 时，转换会限制为只有 17 位精度的值。 任何 < 5E-18 的值舍入为 0。
  
## <a name="see-also"></a>另请参阅
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[数据类型转换（数据库引擎）](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
