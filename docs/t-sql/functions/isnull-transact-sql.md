---
title: "ISNULL (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISNULL
- ISNULL_TSQL
- IFNULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- replacing null values
- null values [SQL Server], ISNULL
- null values [SQL Server], replacement values
- ISNULL function
ms.assetid: 6f3e5802-864b-4e77-9862-657bb5430b68
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8d364548d3303de493343365bd16677ffdfd5641
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="isnull-transact-sql"></a>ISNULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  使用指定的替换值替换 NULL。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ISNULL ( check_expression , replacement_value )  
```  
  
## <a name="arguments"></a>参数  
 *check_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)要检查是否为空。 *check_expression*可以是任何类型。  
  
 *replacement_value*  
 如果要返回的表达式*check_expression*为 NULL。 *replacement_value*隐式转换为的类型的类型必须是*check_expresssion*。  
  
## <a name="return-types"></a>返回类型  
 返回与相同的类型*check_expression*。 如果文本型 NULL 提供作为*check_expression*，返回的数据类型*replacement_value*。 如果文本型 NULL 提供作为*check_expression*并且不*replacement_value*提供，则返回**int**。  
  
## <a name="remarks"></a>注释  
 值*check_expression*如果它不 NULL; 否则为返回*replacement_value*后它将隐式转换为的类型，将返回*check_expression*，如果类型不同。 *replacement_value*如果可以截断*replacement_value*长于*check_expression*。  
  
> [!NOTE]  
>  使用[COALESCE &#40;Transact SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)返回第一个非 null 值。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-isnull-with-avg"></a>A. 将 ISNULL 与 AVG 一起使用  
 以下示例查找所有产品的重量平均值。 它用值 `50` 替换 `Weight` 表的 `Product` 列中的所有 NULL 项。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AVG(ISNULL(Weight, 50))  
FROM Production.Product;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------------- 
59.79  
  
 (1 row(s) affected)
 ```  
  
### <a name="b-using-isnull"></a>B. 使用 ISNULL  
 以下示例选择 `AdventureWorks2012` 中所有特价产品的说明、折扣百分比、最小量和最大量。 如果某个特殊特价产品的最大量为 NULL，则结果集中显示的 `MaxQty` 为 `0.00`。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Description, DiscountPct, MinQty, ISNULL(MaxQty, 0.00) AS 'Max Quantity'  
FROM Sales.SpecialOffer;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|  Description       |  DiscountPct    |   MinQty    |   最大数量       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0.00           |   0         |   0                  |
|  Volume Discount   |  0.02           |   11        |   14                 |
|  Volume Discount   |  0.05           |   15        |   4                  |
|  Volume Discount   |  0.10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0.20           |   61        |   0                  |
|  Mountain 100 Cl   |  0.35           |   0         |   0                  |
|  运动 Helmet Di   |  0.10           |   0         |   0                  |
|  道路 650 Overst   |  0.30           |   0         |   0                  |
|  Mountain 轮胎 S   |  0.50           |   0         |   0                  |
|  运动 Helmet Di   |  0.15           |   0         |   0                  |
|  LL 道路帧 S   |  0.35           |   0         |   0                  |
|  旅行车 3000 Pr   |  0.15           |   0         |   0                  |
|  Touring-1000 Pr   |  0.20           |   0         |   0                  |
|  半价格 Peda   |  0.50           |   0         |   0                  |
|  Mountain 500 Si   |  0.40           |   0         |   0                  |

 `(16 row(s) affected)`  
  
### <a name="c-testing-for-null-in-a-where-clause"></a>C. 测试 WHERE 子句中的 NULL  
 请勿使用 ISNULL 查找 NULL 值。 而应使用 IS NULL。 下面的示例查找 weight 列中存在 `NULL` 的所有产品。 请注意 `IS` 和 `NULL` 之间的空格。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight  
FROM Production.Product  
WHERE Weight IS NULL;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-isnull-with-avg"></a>D. 将 ISNULL 与 AVG 一起使用  
 下面的示例查找示例表中的所有产品的权重的平均值。 它用值 `50` 替换 `Weight` 表的 `Product` 列中的所有 NULL 项。  
  
```  
-- Uses AdventureWorks  
  
SELECT AVG(ISNULL(Weight, 50))  
FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------------   
52.88   
```  
  
### <a name="e-using-isnull"></a>E. 使用 ISNULL  
 下面的示例使用 ISNULL 测试是否在列中的 NULL 值`MinPaymentAmount`并显示值`0.00`对于这些行。  
  
```  
-- Uses AdventureWorks  
  
SELECT ResellerName,   
       ISNULL(MinPaymentAmount,0) AS MinimumPayment  
FROM dbo.DimReseller  
ORDER BY ResellerName;  
  
```  
  
 以下为部分结果集。  
  
|  ResellerName                |  MinimumPayment    |
|  -------------------------   |  --------------    |
|  自行车关联       |     0.0000         |
|  自行车存储                |     0.0000         |
|  周期式应用商店                |     0.0000         |
|  很好自行车公司     |     0.0000         |
|  典型的自行车式应用商店         |   200.0000         |
|  可接受的销售人员和服务  |     0.0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>F. 使用 IS NULL 测试为空的 WHERE 子句中  
 下面的示例查找所有产品`NULL`中`Weight`列。 请注意 `IS` 和 `NULL` 之间的空格。  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>另请参阅  
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [为 NULL &#40;Transact SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [System Functions (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [将合并 &#40;Transact SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  


