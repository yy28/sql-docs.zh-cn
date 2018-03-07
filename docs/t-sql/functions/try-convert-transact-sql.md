---
title: "TRY_CONVERT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRY_CONVERT_TSQL
- TRY_CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CONVERT function
ms.assetid: 3e6e7825-6482-4cb2-a8c2-9abc99e265a6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5fedc9777146d24cb04fb7652344f244babc8246
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="tryconvert-transact-sql"></a>TRY_CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回转换为指定数据类型的值（如果转换成功）；否则返回 Null。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
TRY_CONVERT ( data_type [ ( length ) ], expression [, style ] )  
```  
  
## <a name="arguments"></a>参数  
 *data_type （长度）*  
 要强制转换到其中的数据类型*表达式*。  
  
 *expression*  
 要转换的值。  
  
 *样式*  
 可选整数表达式，它指定如何**TRY_CONVERT**函数是转换*表达式*。  
  
 *样式*接受与相同的值*样式*参数**转换**函数。 有关详细信息，请参阅 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)。  
  
 可接受的值的范围由值*data_type*。 如果*样式*为 null，则**TRY_CONVERT** ，则返回 null。  
  
## <a name="return-types"></a>返回类型  
 返回转换为指定数据类型的值（如果转换成功）；否则返回 Null。  
  
## <a name="remarks"></a>Remarks  
 **TRY_CONVERT**采用传递给它的值，并尝试将其转换为指定*data_type*。 如果转换成功， **TRY_CONVERT**返回的值与指定*data_type*; 如果发生错误，则返回 null。 但是如果请求为显式不允许使用，然后转换**TRY_CONVERT**失败并出现错误。  
  
 **TRY_CONVERT** 110 和更高版本是兼容级别中的保留的关键字。  
  
 此功能可以在某个 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本以及更高版本的服务器上远程执行。 它将不到具有以下版本的服务器进行远程处理[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
## <a name="examples"></a>示例  
  
### <a name="a-tryconvert-returns-null"></a>A. TRY_CONVERT 返回 null  
 下面的示例演示转换失败时 TRY_CONVERT 返回 null。  
  
```sql  
SELECT   
    CASE WHEN TRY_CONVERT(float, 'test') IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 以下示例演示表达式必须采用所需的格式。  
  
```sql  
SET DATEFORMAT dmy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-tryconvert-fails-with-an-error"></a>B. TRY_CONVERT 将失败，并出现错误  
 下面的示例演示明确不允许转换时 TRY_CONVERT 返回错误。  
  
```sql  
SELECT TRY_CONVERT(xml, 4) AS Result;  
GO  
```  
  
 此语句的结果是一个错误，因为整数无法转换为 xml 数据类型。  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-tryconvert-succeeds"></a>C. TRY_CONVERT 成功  
 此示例演示表达式必须采用所需的格式。  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
