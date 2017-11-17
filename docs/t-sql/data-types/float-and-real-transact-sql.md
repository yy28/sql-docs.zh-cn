---
title: "float 和 real (Transact SQL) |Microsoft 文档"
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 0ce2e3272c30057f533796e0822256c6235de0c1
ms.contentlocale: zh-cn
ms.lasthandoff: 10/04/2017

---
# <a name="float-and-real-transact-sql"></a>float 和 real (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

用于表示浮点数值数据的大致数值数据类型。 浮点数据为近似值；因此，并非数据类型范围内的所有值都能精确地表示。 ISO 同义词**实际**是**float(24)**。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
**float** [ **(***n***)** ] 其中 *n* 是用于存储的比特数尾数**float**数字科学记数法，因此，规定的精度和存储大小。 如果 *n* 指定，则它必须是介于**1**和**53**。 默认值 *n* 是**53**。
  
|*n*值|精度|存储大小|  
|---|---|---|
|**1-24**|7 位|4 个字节|  
|**25-53**|15 位数|8 字节|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将 *n* 作为两个可能值之一。 如果**1**<=n<=**24**，  *n* 将被视为**24**。 如果**25**<=n<=**53**，  *n* 将被视为**53**。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Float**[**(n)**] 数据类型符合 ISO 标准的所有值 *n* 从**1**通过**53**。 同义词**双精度**是**float(53)**。
  
## <a name="remarks"></a>注释  
  
|数据类型|范围|存储器|  
|---|---|---|
|**float**|-1.79E + 308 至 -2.23E - 308、0 以及 2.23E - 308 至 1.79E + 308|依赖于的值*n*|  
|**real**|-3.40E + 38 至 -1.18E - 38、0 以及 1.18E - 38 至 3.40E + 38|4 个字节|  
  
##  <a name="converting-float-and-real-data"></a>转换浮点型和真实数据  
值的**float**时它们会转换为任何整数类型将被截断。
  
如果想要从转换**float**或**实际**为字符数据时，使用 STR 字符串函数是通常比强制转换 （） 更有用。 这是因为 STR 能够对格式进行更严格的控制。 有关详细信息，请参阅[STR &#40;Transact SQL &#41;](../../t-sql/functions/str-transact-sql.md)和[函数 &#40;Transact SQL &#41;](../../t-sql/functions/functions.md).
  
转换**float**使用科学记数法到的值**十进制**或**数值**被限制为 17 位精度的值。 任何值 < 5E 18 将向舍入为 0。
  
## <a name="see-also"></a>另请参阅
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable (Transact-SQL)](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

