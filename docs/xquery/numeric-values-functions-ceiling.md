---
title: ceiling 函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:ceiling function
- ceiling function [XQuery]
ms.assetid: 594f1dd0-3c27-41b3-b809-9ce6714c5a97
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ae81ae295664f4e1ef1a7ef60c01a4f866d2c496
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751225"
---
# <a name="numeric-values-functions---ceiling"></a>数值函数 - ceiling 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回不带小数部分并且不小于其参数值的最小数字。 如果参数是一个空序列，则返回空序列。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:ceiling ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将应用该函数的数字。  
  
## <a name="remarks"></a>备注  
 如果类型 *$arg*是三个基本数字类型之一**xs: float**， **xs: double**，或**xs: decimal**，返回类型是与相同 *$arg*类型。  
  
 如果类型 *$arg*是从其中一个数值类型派生的类型的返回类型为基的数值类型。  
  
 Fn: floor、 fn: ceiling 或 fn: round 函数的输入是否**xdt: untypedatomic**，隐式强制转换为**xs: double**。  
  
 任何其他类型都会生成静态错误。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-using-the-ceiling-xquery-function"></a>A. 使用 ceiling() XQuery 函数  
 对于产品型号 7，此查询返回产品型号生产过程中的生产车间的列表。 查询将返回每个生产车间的位置 ID、工时和批量大小（如果有记录）。 该查询使用**ceiling**函数返回类型的值作为工时**十进制**。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
     for $i in /AWMI:root/AWMI:Location  
     return   
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ ceiling($i/@LaborHours) }" >  
                    {   
                      $i/@LotSize  
                    }    
       </Location>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 请注意上述查询的以下方面：  
  
-   AWMI 命名空间前缀表示 Adventure Works 的生产说明。 此前缀引用被查询文档中使用的同一命名空间。  
  
-   **说明**是**xml**类型列。 因此， [query （） 方法 （XML 数据类型）](../t-sql/xml/query-method-xml-data-type.md)用于指定 XQuery。 XQuery 语句指定为该查询方法的参数。  
  
-   **有关...返回**是循环构造。 在查询中，**有关**循环标识一系列\<位置 > 元素。 对于每个车间**返回**中的语句**为**循环描述要生成的 XML:  
  
    -   一个\<位置 > 具有 LocationID 和 LaborHrs 属性的元素。 大括号 ({ }) 中对应的表达式从文档中检索所需的值。  
  
    -   {$i/@LotSize } 表达式从文档中，如果存在中检索 LotSize 属性。  
  
    -   结果如下：  
  
```  
ProductModelID Result    
-------------- ------------------------------------------------------  
7      <Location LocationID="10" LaborHrs="3" LotSize="100"/>  
       <Location LocationID="20" LaborHrs="2" LotSize="1"/>     
       <Location LocationID="30" LaborHrs="1" LotSize="1"/>     
       <Location LocationID="45" LaborHrs="1" LotSize="20"/>  
       <Location LocationID="60" LaborHrs="3" LotSize="1"/>     
       <Location LocationID="60" LaborHrs="4" LotSize="1"/>  
```  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Ceiling （)** 函数将所有整数值都映射到 xs: decimal。  
  
## <a name="see-also"></a>请参阅  
 [floor 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [round 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)  
  
  
