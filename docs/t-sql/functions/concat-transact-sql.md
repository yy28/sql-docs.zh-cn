---
title: "CONCAT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONCAT
- CONCAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT function
ms.assetid: fce5a8d4-283b-4c47-95e5-4946402550d5
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 046278bb3016b39df8039a1450a58b177d2bc180
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="concat-transact-sql"></a>CONCAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

返回作为串联两个或更多字符串值的结果的字符串。 (若要在连接过程中添加一个分隔开来将的值，请参阅[CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md)。)
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>参数  
*string_value*  
要与其他值串联的字符串值。
  
## <a name="return-types"></a>返回类型
字符串，其长度和类型取决于输入。
  
## <a name="remarks"></a>注释  
**CONCAT**采用数量可变的字符串自变量并将它们连接到单个字符串。 它需要至少两个输入值；否则将引发错误。 所有参数都隐式转换为字符串类型，然后串联在一起。 Null 值被隐式转换为空字符串。 如果所有的自变量是 null，类型的空字符串**varchar**(1) 返回。 隐式转换为字符串的过程遵循现有的数据类型转换规则。 有关数据类型转换的详细信息，请参阅[CAST 和 CONVERT &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
返回类型取决于参数的类型。 下表将说明这一映射。
  
|输入类型|输出类型和长度|  
|---|---|
|如果任何参数为 SQL-CLR 系统类型、SQL-CLR UDT 或 `nvarchar(max)`|**nvarchar(max)**|  
|否则为如果任何参数为**varbinary （max)**或**varchar （max)**|**varchar （max)**除非其中一个参数是**nvarchar**任何长度。 如果这样，则结果是**nvarchar (max)**。|  
|否则为如果任何参数为**nvarchar**(< = 4000)|**nvarchar**(< = 4000)|  
|否则，在所有其他情况下|**varchar**(< = 8000) 除非其中一个参数是任意长度的 nvarchar。 如果这样，则结果是**nvarchar (max)**。|  
  
当自变量为 < = 为 4000 **nvarchar**，或 < = 8000 **varchar**，隐式转换可能会影响结果的长度。 当将其他数据类型隐式转换为字符串时，它们具有不同长度。 例如， **int** (14) 的字符串长度为 12，虽然**float**的长度为 32。 这样，串联两个整数后，结果的长度不小于 24。
  
如果没有任何输入参数属于支持的大型对象 (LOB) 类型，则返回类型的长度截断为 8000，而不考虑返回类型。 这种截断可节约空间并支持提高计划生成的效率。
  
CONCAT 函数可以在位于版本的链接服务器上远程执行[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更高版本。 对于较旧的链接服务器，CONCAT 操作将执行本地后从链接服务器返回的非串联的值。
  
## <a name="examples"></a>示例  
  
### <a name="a-using-concat"></a>A. 使用 CONCAT  
  
```sql
SELECT CONCAT ( 'Happy ', 'Birthday ', 11, '/', '25' ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------  
Happy Birthday 11/25  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-concat-with-null-values"></a>B. 使用 CONCAT 以及 NULL 值  
  
```sql
CREATE TABLE #temp (  
    emp_name nvarchar(200) NOT NULL,  
    emp_middlename nvarchar(200) NULL,  
    emp_lastname nvarchar(200) NOT NULL  
);  
INSERT INTO #temp VALUES( 'Name', NULL, 'Lastname' );  
SELECT CONCAT( emp_name, emp_middlename, emp_lastname ) AS Result  
FROM #temp;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
------------------  
NameLastname  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[字符串函数 (TRANSACT-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
[CONCAT_WS (Transact SQL)](../../t-sql/functions/concat-ws-transact-sql.md)   
  



